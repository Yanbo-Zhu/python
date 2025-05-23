
https://peps.python.org/pep-0008/#comments


# 1 [Block Comments](https://peps.python.org/pep-0008/#block-comments)

Block comments generally apply to some (or all) code that follows them, and are indented to the same level as that code. Each line of a block comment starts with a `#` and a single space (unless it is indented text inside the comment).

Paragraphs inside a block comment are separated by a line containing a single `#`.

# 2 [Inline Comments](https://peps.python.org/pep-0008/#inline-comments)

Use inline comments sparingly.

An inline comment is a comment on the same line as a statement. Inline comments should be separated by at least two spaces from the statement. They should start with a # and a single space.

Inline comments are unnecessary and in fact distracting if they state the obvious. Don’t do this:

x = x + 1                 # Increment x

But sometimes, this is useful:

x = x + 1                 # Compensate for border

# 3 [Documentation Strings](https://peps.python.org/pep-0008/#documentation-strings)

Conventions for writing good documentation strings (a.k.a. “docstrings”) are immortalized in [PEP 257](https://peps.python.org/pep-0257/ "PEP 257 – Docstring Conventions").

- Write docstrings for all public modules, functions, classes, and methods. Docstrings are not necessary for non-public methods, but you should have a comment that describes what the method does. This comment should appear after the `def` line.
- [PEP 257](https://peps.python.org/pep-0257/ "PEP 257 – Docstring Conventions") describes good docstring conventions. Note that most importantly, the `"""` that ends a multiline docstring should be on a line by itself:
    
    """Return a foobang
    
    Optional plotz says to frobnicate the bizbaz first.
    """
    
- For one liner docstrings, please keep the closing `"""` on the same line:
    
    """Return an ex-parrot."""
    


# 4 Docstring 用法

https://peps.python.org/pep-0257/

Docstrings sollten Sie auf jedem Fall für Module, Klassen und Funktionen verwenden. Sie sollten Informationen über den Zweck der Funktion, die Parameter und die Rückgabewerte enthalten. Wenn Sie eine klare Beschreibung der Funktionsweise und Zwecke Ihrer Funktionen und Klassen in Docstrings hinterlegen, ist das oft ausreichend für jemanden, der Ihren Code verwendet oder darauf aufbauen möchte.

Inline-Kommentare sollten Sie hinzufügen, um komplexe Logik oder spezifische Entscheidungen im Code zu erklären, die nicht sofort offensichtlich sind, wenn ein Stück Code besondere Bedingungen hat oder eine nicht intuitive Lösung verwende Übermäßige Kommentierung jeder Codezeile insbesondere für selbsterklärenden Code senkt m. E. sogar die Lesbarkeit von Python-Code.
## 4.1 [What is a Docstring?](https://peps.python.org/pep-0257/#what-is-a-docstring)

A docstring is a string literal that occurs as the first statement in a module, function, class, or method definition. Such a docstring becomes the `__doc__` special attribute of that object.

All modules should normally have docstrings, and all functions and classes exported by a module should also have docstrings. Public methods (including the `__init__` constructor) should also have docstrings. A package may be documented in the module docstring of the `__init__.py` file in the package directory.

String literals occurring elsewhere in Python code may also act as documentation. They are not recognized by the Python bytecode compiler and are not accessible as runtime object attributes (i.e. not assigned to `__doc__`), but two types of extra docstrings may be extracted by software tools:

1. String literals occurring immediately after a simple assignment at the top level of a module, class, or `__init__` method are called “attribute docstrings”.
2. String literals occurring immediately after another docstring are called “additional docstrings”.

Please see [PEP 258](https://peps.python.org/pep-0258/ "PEP 258 – Docutils Design Specification"), “Docutils Design Specification”, for a detailed description of attribute and additional docstrings.

For consistency, always use `"""triple double quotes"""` around docstrings. Use `r"""raw triple double quotes"""` if you use any backslashes in your docstrings.

There are two forms of docstrings: one-liners and multi-line docstrings.

# 5 [One-line Docstrings](https://peps.python.org/pep-0257/#one-line-docstrings)

One-liners are for really obvious cases. They should really fit on one line. For example:

```python
def kos_root():
    """Return the pathname of the KOS root directory."""
    global _kos_root
    if _kos_root: return _kos_root
    ...
```


Notes:

- Triple quotes are used even though the string fits on one line. This makes it easy to later expand it.
- The closing quotes are on the same line as the opening quotes. This looks better for one-liners.
- There’s no blank line either before or after the docstring.
- The docstring is a phrase ending in a period. It prescribes the function or method’s effect as a command (“Do this”, “Return that”), not as a description; e.g. don’t write “Returns the pathname …”.
- The one-line docstring should NOT be a “signature” reiterating the function/method parameters (which can be obtained by introspection). Don’t do:
    
    def function(a, b):
        """function(a, b) -> list"""
    
    This type of docstring is only appropriate for C functions (such as built-ins), where introspection is not possible. However, the nature of the _return value_ cannot be determined by introspection, so it should be mentioned. The preferred form for such a docstring would be something like:
    
    def function(a, b):
        """Do X and return a list."""
    
    (Of course “Do X” should be replaced by a useful description!)
    

## 5.1 [Multi-line Docstrings](https://peps.python.org/pep-0257/#multi-line-docstrings)

Multi-line docstrings consist of a summary line just like a one-line docstring, followed by a blank line, followed by a more elaborate description. The summary line may be used by automatic indexing tools; it is important that it fits on one line and is separated from the rest of the docstring by a blank line. The summary line may be on the same line as the opening quotes or on the next line. The entire docstring is indented the same as the quotes at its first line (see example below).

Insert a blank line after all docstrings (one-line or multi-line) that document a class – generally speaking, the class’s methods are separated from each other by a single blank line, and the docstring needs to be offset from the first method by a blank line.

The docstring of a script (a stand-alone program) should be usable as its “usage” message, printed when the script is invoked with incorrect or missing arguments (or perhaps with a “-h” option, for “help”). Such a docstring should document the script’s function and command line syntax, environment variables, and files. Usage messages can be fairly elaborate (several screens full) and should be sufficient for a new user to use the command properly, as well as a complete quick reference to all options and arguments for the sophisticated user.

The docstring for a module should generally list the classes, exceptions and functions (and any other objects) that are exported by the module, with a one-line summary of each. (These summaries generally give less detail than the summary line in the object’s docstring.) The docstring for a package (i.e., the docstring of the package’s `__init__.py` module) should also list the modules and subpackages exported by the package.

The docstring for a function or method should summarize its behavior and document its arguments, return value(s), side effects, exceptions raised, and restrictions on when it can be called (all if applicable). Optional arguments should be indicated. It should be documented whether keyword arguments are part of the interface.

The docstring for a class should summarize its behavior and list the public methods and instance variables. If the class is intended to be subclassed, and has an additional interface for subclasses, this interface should be listed separately (in the docstring). The class constructor should be documented in the docstring for its `__init__` method. Individual methods should be documented by their own docstring.

If a class subclasses another class and its behavior is mostly inherited from that class, its docstring should mention this and summarize the differences. Use the verb “override” to indicate that a subclass method replaces a superclass method and does not call the superclass method; use the verb “extend” to indicate that a subclass method calls the superclass method (in addition to its own behavior).

_Do not_ use the Emacs convention of mentioning the arguments of functions or methods in upper case in running text. Python is case sensitive and the argument names can be used for keyword arguments, so the docstring should document the correct argument names. It is best to list each argument on a separate line. For example:

```python

def complex(real=0.0, imag=0.0):
    """Form a complex number.

    Keyword arguments:
    real -- the real part (default 0.0)
    imag -- the imaginary part (default 0.0)
    """
    if imag == 0.0 and real == 0.0:
        return complex_zero
    ...

```



```python
def greet(name):  
    """ This function greets the user with the provided name.  
  
    Parameters:    name (str): The name of the person to greet.  
    Returns:    str: A greeting message.    
    """    
    return f"Hello, {name}! Welcome to our PyML class!"
```

Unless the entire docstring fits on a line, place the closing quotes on a line by themselves. This way, Emacs’ `fill-paragraph` command can be used on it.

## 5.2 [Handling Docstring Indentation](https://peps.python.org/pep-0257/#handling-docstring-indentation)

Docstring processing tools will strip a uniform amount of indentation from the second and further lines of the docstring, equal to the minimum indentation of all non-blank lines after the first line. Any indentation in the first line of the docstring (i.e., up to the first newline) is insignificant and removed. Relative indentation of later lines in the docstring is retained. Blank lines should be removed from the beginning and end of the docstring.

Since code is much more precise than words, here is an implementation of the algorithm:

```

def trim(docstring):
    if not docstring:
        return ''
    # Convert tabs to spaces (following the normal Python rules)
    # and split into a list of lines:
    lines = docstring.expandtabs().splitlines()
    # Determine minimum indentation (first line doesn't count):
    indent = sys.maxsize
    for line in lines[1:]:
        stripped = line.lstrip()
        if stripped:
            indent = min(indent, len(line) - len(stripped))
    # Remove indentation (first line is special):
    trimmed = [lines[0].strip()]
    if indent < sys.maxsize:
        for line in lines[1:]:
            trimmed.append(line[indent:].rstrip())
    # Strip off trailing and leading blank lines:
    while trimmed and not trimmed[-1]:
        trimmed.pop()
    while trimmed and not trimmed[0]:
        trimmed.pop(0)
    # Return a single string:
    return '\n'.join(trimmed)
```

The docstring in this example contains two newline characters and is therefore 3 lines long. The first and last lines are blank:

```
def foo():
    """
    This is the second line of the docstring.
    """
```

To illustrate:
```python
>>> print repr(foo.__doc__)
'\n    This is the second line of the docstring.\n    '
>>> foo.__doc__.splitlines()
['', '    This is the second line of the docstring.', '    ']
>>> trim(foo.__doc__)
'This is the second line of the docstring.'
```


Once trimmed, these docstrings are equivalent:

```
def foo():
    """A multi-line
    docstring.
    """

def bar():
    """
    A multi-line
    docstring.
    """

```

# 6 Different types of docstring styles


- There are different styles of docstrings which one could use.   
- The most prominent are:  
  1. Google Style Docstrings  
  2. Numpydoc  
  3. reStructuredText (reST) Style Docstrings

```python
# 1. Google Style Docstrings  
def function_name(param1, param2):  
    """  
    This is a one-line summary of what the function does.  
    Args:        param1 (int): Description of param1.        param2 (str): Description of param2.  
    Returns:        bool: Description of return value.    """    # Function implementation



# 2. Numpydoc
def function_name(param1, param2):
    """
    This is a one-line summary of what the function does.

    Parameters
    ----------
    param1 : int
        Description of param1.
    param2 : str
        Description of param2.

    Returns
    -------
    bool
        Description of return value.
    """
    # Function implementation

# 3. reStructuredText (reST) Style Docstrings
def function_name(param1, param2):
    """
    This is a one-line summary of what the function does.

    :param param1: Description of param1.
    :type param1: int
    :param param2: Description of param2.
    :type param2: str
    :return: Description of return value.
    :rtype: bool
    """
    # Function implementation



```


# 7 pydoc or help()

- Pydoc is a documentation tool that extracts docstrings to generate user-friendly *documentation for Python code*.  
- Pydoc is accessible from the command line using `pydoc` followed by the object name, or within Python using the `help()` function.

```
help(greet)
```



# 8 Pros and cons of different docstring styles

| Docstring Style                              | Pros                                                                                                                                             | Cons                                                                                                                            |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| **Google Style Docstrings**                  | **Structured**: Follows a clear structure with sections like Parameters, Returns, Raises, Examples, etc., making it easy to read and understand. | **Verbose**: Can become lengthy, especially for complex functions or methods.                                                   |
|                                              | **Popular**: Widely used, especially in the Python community, making it familiar to many developers.                                             | **Non-standard**: While widely used, it's not an official standard, so there might be variations in how it's applied.           |
|                                              | **Integrates with Tools**: Many tools and libraries support parsing and generating documentation from Google Style Docstrings.                   | **Formatting**: Requires strict adherence to formatting conventions for consistency.                                            |
| **Numpydoc**                                 | **Scientific Community**: Popular in the scientific Python community, particularly for documenting NumPy and SciPy functions.                    | **Lengthy**: Like Google Style, it can become verbose for complex functions.                                                    |
|                                              | **Structured**: Similar to Google Style, it provides a clear structure for documenting parameters, return values, etc.                           | **Non-standard**: While widely used, it's not an official standard, so there might be variations in how it's applied.           |
|                                              | **Sphinx Integration**: Compatible with Sphinx, making it suitable for projects using Sphinx for documentation generation.                       | **Learning Curve**: Requires familiarity with reStructuredText markup, which might be a learning curve for some developers.     |
| **reStructuredText (reST) Style Docstrings** | **Integration with Sphinx**: Fully compatible with Sphinx and other reStructuredText-based documentation tools.                                  | **Markup Complexity**: Requires knowledge of reStructuredText markup, which can be more complex than plain text.                |
|                                              | **Clear Structure**: Follows a clear structure with parameters, types, and return values specified inline, making it easy to read.               | **Non-Pythonic**: Some developers may find the syntax less intuitive, especially if they're not familiar with reStructuredText. |
|                                              | **Sphinx Directives**: Supports Sphinx directives for cross-referencing and linking to other documentation.                                      |                                                                                                                                 |



# 9 How to create (publishable) documentation of Python Code?

- **Sphinx** is a documentation generation tool widely used in the Python community.  
  - It automates the process of generating documentation from source code, making it easier to maintain and update. [Official website](https://www.sphinx-doc.org/en/master/).

- Example: [numpy official documentation](https://numpy.org/doc/stable/index.html) created with Sphinx  
  - [ndarray documentation](https://numpy.org/doc/stable/reference/generated/numpy.ndarray.html#numpy.ndarray)  
   
- Example: [Quantus explainability package](https://quantus.readthedocs.io/en/latest/index.html) created with Sphinx  
  - [Floating point discretisation](https://quantus.readthedocs.io/en/latest/docs_api/quantus.functions.discretise_func.html#quantus.functions.discretise_func.floating_points)  
  - Directly specified in [source](https://github.com/understandable-machine-intelligence-lab/Quantus/blob/8ad10763f2ed670ae28059baa90bb4f2e7b9f3ab/quantus/functions/discretise_func.py#L15)!

- Key Features:  
    - **reStructuredText (reST) Support**: Sphinx uses reStructuredText, a lightweight markup language, for documentation source files.  
    - **Automatic Generation**: It can automatically generate documentation from source code, including module hierarchies, function signatures, and docstrings.  
    - **Customizable Output**: Sphinx supports multiple output formats such as HTML, PDF, and ePub, allowing documentation to be published in various formats.  
    - **Cross-Referencing**: Sphinx generates cross-references within the documentation, making it easier for users to navigate and understand the codebase.

- **Note**: `reStructuredText` is a markup language for creating structured text documents, while `reStructuredText Style docstring` refers to using `reStructuredText` syntax within Python docstrings for code documentation.

