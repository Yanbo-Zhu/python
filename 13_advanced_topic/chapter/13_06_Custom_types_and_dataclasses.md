

# 1 Recap: Type Annotations

- Python supports optional type hints
- helps with code documentation and tooling
- does not affect runtime behavior
- uses the `typing` module for complex types

```python
from typing import Callable  
  
def process_numbers(  
    numbers: list[float],  
    operation: Callable[[float], float],  
    threshold: float | None = None  
) -> list[float]:  
    result = [operation(x) for x in numbers]  
    if threshold is not None:  
        result = [x for x in result if x > threshold]  
    return result  
  
# Example usage  
nums = [1.0, 2.0, 3.0, 4.0]  
result = process_numbers(  
    numbers=nums,  
    operation=lambda x: x * 2,  
    threshold=5.0  
)  
print(f"Processed numbers: {result}")
```



# 2 Custom Types

- create custom type definitions for complex data structures  
- Note: TypedDict is still just a dict - it will not perform type checking

```python
from typing import Literal, Callable, TypedDict  
  
# Custom types for our pipeline  
StringProcessingStep = Callable[[str], str]  
TextType = str | list[str]  
ModelType = Literal["bert", "gpt2", "roberta"]  
  
class ProcessingConfig(TypedDict):  
    model: ModelType  
    mask_prob: float  
    batch_size: int  
    max_length: int | None  
  
# Example usage  
config: ProcessingConfig = {  
    "model": "bert",  
    "mask_prob": 0.15,  
    "batch_size": 4,  
    "max_length": None  
}  
  
print(config)
{'model': 'bert', 'mask_prob': 0.15, 'batch_size': 4, 'max_length': None}
```

# 3 Classes as Custom Types  

- classes allow bundling data and behavior together  
- create custom data structures with methods  
- support attributes and inheritance  
- define initialization and other special behaviors

```python
# To initialize the class, we need to define the __init__ method  
class ProcessingConfig:  
    def __init__(self, model: ModelType, mask_prob: float, batch_size: int, max_length: int | None):  
        self.model = model  
        self.mask_prob = mask_prob  
        self.batch_size = batch_size  
        self.max_length = max_length  
  
config = ProcessingConfig(model="bert", mask_prob=0.15, batch_size=32, max_length=None)  
print(config.model)    
print(config)
```



To make the class printable, we need to define the `__repr__` method
```python
class PrintableProcessingConfig(ProcessingConfig):  
    # The `__repr__` method in Python is a special method used to define a string representation of an object. This method is particularly useful for debugging, as it provides a detailed, unambiguous string that ideally gives insight into the object’s contents or state.
    
    def __repr__(self):  
        return f"ProcessingConfig(model={self.model}, mask_prob={self.mask_prob}, batch_size={self.batch_size}, max_length={self.max_length})"  


printable_config = PrintableProcessingConfig(model="bert", mask_prob=0.15, batch_size=32, max_length=None)  
print(printable_config)
```


To make the class comparable, we need to define the `__eq__` method

```python
class ComparableProcessingConfig(ProcessingConfig):  
    def __eq__(self, other):  
        if not isinstance(other, ProcessingConfig):  
            return False  
        return self.model == other.model and self.mask_prob == other.mask_prob and self.batch_size == other.batch_size and self.max_length == other.max_length  

comparable_config = ComparableProcessingConfig(model="bert", mask_prob=0.15, batch_size=32, max_length=None)  

print(comparable_config == printable_config)
```



# 4 From Classes to Dataclasses

- regular classes often require lots of boilerplate code   
- dataclasses implement` \__init__, \__eq__, and \__repr__ `automatically  
- we can define a` \__post_init__ `function instead of an` \__init__` function  
- intended purely as data containers  
- can be made immutable (with frozen=True) - we cannot mutate the attributes of an instance after creation (raises an error)
    - Careful: Frozen only applies to top-level attributes. We can still mutate mutatable attributes:

```python
from dataclasses import dataclass  
  
@dataclass(frozen=True)  
class TextBatch:  
    texts: list[list[str]]  
    labels: list[str]  
      
    def __post_init__(self):  
        if len(self.texts) != len(self.labels):  
            raise ValueError("Number of texts and labels must match")  
      
    def __len__(self) -> int:  
        return len(self.texts)  
      
    def __getitem__(self, index: int) -> tuple[str, str]:  
        return self.texts[index], self.labels[index]  
          
          
print("Repr Example:", TextBatch([["text1"], ["text2"]], ["pos", "neg"]))  
print("Eq Example:", TextBatch(["text1"], ["pos"]) == TextBatch(["text1"], ["pos"]))

#打印出来
#Repr Example: TextBatch(texts=[['text1'], ['text2']], labels=['pos', 'neg'])
#Eq Example: True
```


Careful: Frozen only applies to top-level attributes. We can still mutate mutatable attributes:
```python
batch = TextBatch(texts=[["text1"], ["text2"]], labels=["pos", "neg"])  
batch.texts.append(["text3"])  
print(batch)  
try:  
    batch.texts = (["text3"], ["text4"])  
except Exception as e:  
    print(f"Error: {e}")

# 打印出来: 
TextBatch(texts=[['text1'], ['text2'], ['text3']], labels=['pos', 'neg'])
Error: cannot assign to field 'texts'

```

Let's apply dataclasses to our data pipeline example from above:
```python
from pathlib import Path  
from typing import Callable  
from dataclasses import dataclass  
  
@dataclass(frozen=True)  
class ProcessingConfig:  
    data_path: str = "data/imdb_snippet.csv"  
    mask_token: str = "[MASK]"  
    mask_prob: float = 0.15  
    batch_size: int = 4  
  
    def __post_init__(self):  
        if self.batch_size <= 0:  
            raise ValueError("Batch size must be positive")  
        if not 0 <= self.mask_prob <= 1:  
            raise ValueError("Mask probability must be between 0 and 1")  
        if not Path(self.data_path).exists():  
            raise FileNotFoundError(f"Data file does not exist: {self.data_path}")  
  
@dataclass(frozen=True)  
class DataBatch:  
    texts: list[list[str]]  
    labels: list[str]  
  
    def __len__(self) -> int:  
        return len(self.texts)  
      
    def __str__(self) -> str:  
        shortened_texts = [text[:10] + ["..."] for text in self.texts]  
        return f"\nTexts: {shortened_texts}, \nLabels: {self.labels}"  
  
## Process steps as functions  
def clean_text(text: str) -> str:  
    """Convert to lowercase and normalize spaces"""  
    return " ".join(text.lower().split())  
  
def remove_special_chars(text: str) -> str:  
    """Keep only letters and spaces"""  
    return re.sub(r"[^a-z ]", "", text)  
  
def split_words(text: str) -> list[str]:  
    """Split text into words"""  
    return text.split()  
  
def mask_words(words: list[str], mask_token: str, mask_prob: float) -> list[str]:  
    """Randomly mask words with given probability and token"""  
    return [mask_token if random.random() < mask_prob else word   
            for word in words]  
  
def create_batches(texts: list[list[str]], labels: list[str],   
                  batch_size: int = 2) -> list[DataBatch]:  
    """Create batches from texts and labels"""  
    return [  
        DataBatch(texts=texts[i:i+batch_size], labels=labels[i:i+batch_size])  
        for i in range(0, len(texts), batch_size)  
    ]  
  
def debug(func: Callable) -> Callable:  
    """Simple decorator to show intermediate results"""  
    def wrapper(*args, **kwargs):  
        result = func(*args, **kwargs)  
        preview = result[:50] if isinstance(result, str) else result[:5]  
        print(f"{func.__name__}: {preview}...")  
        return result  
    return wrapper  
  
def compose(*functions: Callable) -> Callable:  
    """Compose multiple functions from left to right"""  
    def composed_function(x):  
        result = x  
        for func in functions:  
            result = func(result)  
        return result  
    return composed_function  
  
def load_data(filepath: str) -> tuple[list, list]:  
    """Load data from CSV file"""  
    with open(filepath) as f:  
        next(csv.reader(f))  # skip headers  
        data = [row for row in csv.reader(f)]  
    texts, labels = zip(*data)  
    return list(texts), list(labels)  
  
def process_batch(config: ProcessingConfig) -> list[DataBatch]:  
    """Pure function that processes a batch"""  
    texts, labels = load_data(config.data_path)  
  
    masker = partial(mask_words, mask_token=config.mask_token, mask_prob=config.mask_prob)  
      
    # Create pipeline function  
    pipeline = compose(  
        clean_text,  
        remove_special_chars,  
        split_words,  
        masker  
    )  
      
    # Use list comprehension instead of map  
    processed_texts = [pipeline(text) for text in texts]  
      
    return create_batches(processed_texts, labels, config.batch_size)  
  
# Usage in pipeline  
config = ProcessingConfig()  
processed = process_batch(config)  
print(f"First batch: {processed[0]}")  
print(f"Batch size: {len(processed[0])}")  
print(f"Config: {config}")
```






