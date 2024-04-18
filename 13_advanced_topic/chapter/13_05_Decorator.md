
# 1 Python Decorators

In Python, a decorator is a design pattern that allows you to modify the functionality of a [function](https://www.programiz.com/python-programming/function) by wrapping it in another function.
The outer function is called the decorator, which takes the original function as an argument and returns a modified version of it.

## 1.1 

![](images/Pasted%20image%2020240418163316.png)

![](images/Pasted%20image%2020240418163324.png)

Decorated_function 就是 say_hello()

![](images/Pasted%20image%2020240418163332.png)

![](images/Pasted%20image%2020240418163342.png)

Decorator 的例子 
![](images/Pasted%20image%2020240418163347.png)

## 1.2 Prerequisites for learning decorators

Before we learn about decorators, we need to understand a few important concepts related to Python functions. Also, remember that everything in Python is an [object](https://www.programiz.com/python-programming/class#objects), even functions are objects.

### 1.2.1 Nested Function

We can include one function inside another, known as a nested function. For example,

```
def outer(x):
    def inner(y):
        return x + y
    return inner

add_five = outer(5)
result = add_five(6)
print(result)  # prints 11

# Output: 11
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

Here, we have created the `inner()` function inside the `outer()` function.

### 1.2.2 Pass Function as Argument

We can pass a function as an argument to another function in Python. For Example,

```
def add(x, y):
    return x + y

def calculate(func, x, y):
    return func(x, y)

result = calculate(add, 4, 6)
print(result)  # prints 10
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

**Output**

10

In the above example, the `calculate()` function takes a function as its argument. While calling `calculate()`, we are passing the `add()` function as the argument.

In the `calculate()` function, arguments: `func`, `x`, `y` become `add`, `4`, and `6` respectively.

And hence, `func(x, y)` becomes `add(4, 6)` which returns **10**.

### 1.2.3 Return a Function as a Value

In Python, we can also return a function as a return value. For example,

```
def greeting(name):
    def hello():
        return "Hello, " + name + "!"
    return hello

greet = greeting("Atlantis")
print(greet())  # prints "Hello, Atlantis!"

# Output: Hello, Atlantis!
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

In the above example, the `return hello` statement returns the inner `hello()` function. This function is now assigned to the greet variable.

That's why, when we call `greet()` as a function, we get the output.

---

## 1.3 Python Decorators

As mentioned earlier, A Python decorator is a function that takes in a function and returns it by adding some functionality.

In fact, any object which implements the special `__call__()` method is termed callable. So, in the most basic sense, a decorator is a callable that returns a callable.

Basically, a decorator takes in a function, adds some functionality and returns it.

```
def make_pretty(func):
    def inner():
        print("I got decorated")
        func()
    return inner


def ordinary():
    print("I am ordinary")

# Output: I am ordinary
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

Here, we have created two functions:

- `ordinary()` that prints `"I am ordinary"`
- `make_pretty()` that takes a function as its argument and has a nested function named `inner()`, and returns the inner function.

We are calling the `ordinary()` function normally, so we get the output `"I am ordinary"`. Now, let's call it using the decorator function.

```
def make_pretty(func):
    # define the inner function 
    def inner():
        # add some additional behavior to decorated function
        print("I got decorated")

        # call original function
        func()
    # return the inner function
    return inner

# define ordinary function
def ordinary():
    print("I am ordinary")
    
# decorate the ordinary function
decorated_func = make_pretty(ordinary)

# call the decorated function
decorated_func()
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

**Output**

I got decorated
I am ordinary

In the example shown above, `make_pretty()` is a decorator. Notice the code,

```
decorated_func = make_pretty(ordinary)
```

- We are now passing the `ordinary()` function as the argument to the `make_pretty()`.
- The `make_pretty()` function returns the inner function, and it is now assigned to the decorated_func variable.

```
decorated_func()
```

Here, we are actually calling the `inner()` function, where we are printing

### 1.3.1 @ Symbol With Decorator

Instead of assigning the function call to a [variable](https://www.programiz.com/python-programming/variables-constants-literals), Python provides a much more elegant way to achieve this functionality using the `@` symbol. For example,

```
def make_pretty(func):

    def inner():
        print("I got decorated")
        func()
    return inner

@make_pretty
def ordinary():
    print("I am ordinary")

ordinary()  
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

**Output**

I got decorated
I am ordinary

Here, the `ordinary()` function is decorated with the `make_pretty()` decorator using the `@make_pretty` syntax, which is equivalent to calling `ordinary = make_pretty(ordinary)`.

---

## 1.4 Decorating Functions with Parameters

The above decorator was simple and it only worked with functions that did not have any parameters. What if we had functions that took in parameters like:

```
def divide(a, b):
    return a/b
```

This function has two parameters, `a` and `b`. We know it will give an error if we pass in b as **0**.

Now let's make a decorator to check for this case that will cause the error.

```
def smart_divide(func):
    def inner(a, b):
        print("I am going to divide", a, "and", b)
        if b == 0:
            print("Whoops! cannot divide")
            return

        return func(a, b)
    return inner

@smart_divide
def divide(a, b):
    print(a/b)

divide(2,5)

divide(2,0)
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

**Output**

I am going to divide 2 and 5
0.4
I am going to divide 2 and 0
Whoops! cannot divide

Here, when we call the `divide()` function with the arguments **(2,5)**, the `inner()` function defined in the `smart_divide()` decorator is called instead.

This `inner()` function calls the original `divide()` function with the arguments **2** and **5** and returns the result, which is **0.4**.

Similarly, When we call the `divide()` function with the arguments (**2,0)**, the `inner()` function checks that `b` is equal to **0** and prints an error message before returning `None`.

---

## 1.5 Chaining Decorators in Python

Multiple decorators can be chained in Python.

To chain decorators in Python, we can apply multiple decorators to a single function by placing them one after the other, with the most inner decorator being applied first.

```
def star(func):
    def inner(*args, **kwargs):
        print("*" * 15)
        func(*args, **kwargs)
        print("*" * 15)
    return inner


def percent(func):
    def inner(*args, **kwargs):
        print("%" * 15)
        func(*args, **kwargs)
        print("%" * 15)
    return inner


@star
@percent
def printer(msg):
    print(msg)

printer("Hello")
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

**Output**

***************
%%%%%%%%%%%%%%%
Hello
%%%%%%%%%%%%%%%
***************

The above syntax of,

```
@star
@percent
def printer(msg):
    print(msg)
```

is equivalent to

```
def printer(msg):
    print(msg)
printer = star(percent(printer))
```

The order in which we chain decorators matter. If we had reversed the order as,

```
@percent
@star
def printer(msg):
    print(msg)
```

The output would be:

%%%%%%%%%%%%%%%
***************
Hello
***************
%%%%%%%%%%%%%%%

---

# 2 Python @property decorator

Python programming provides us with a built-in `@property` decorator which makes usage of getter and setters much easier in [Object-Oriented Programming](https://www.programiz.com/python-programming/object-oriented-programming).

Before going into details on what `@property` decorator is, let us first build an intuition on why it would be needed in the first place.

---

## 2.1 Class Without Getters and Setters

Let us assume that we decide to make a [class](https://www.programiz.com/python-programming/class) that stores the temperature in degrees Celsius. And, it would also implement a method to convert the temperature into degrees Fahrenheit.

One way of doing this is as follows:

```
class Celsius:
    def __init__(self, temperature = 0):
        self.temperature = temperature

    def to_fahrenheit(self):
        return (self.temperature * 1.8) + 32
```

We can make objects out of this class and manipulate the `temperature` attribute as we wish:

```
# Basic method of setting and getting attributes in Python
class Celsius:
    def __init__(self, temperature=0):
        self.temperature = temperature

    def to_fahrenheit(self):
        return (self.temperature * 1.8) + 32


# Create a new object
human = Celsius()

# Set the temperature
human.temperature = 37

# Get the temperature attribute
print(human.temperature)

# Get the to_fahrenheit method
print(human.to_fahrenheit())
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

**Output**

37
98.60000000000001

Here, the extra decimal places when converting into Fahrenheit is due to the [Floating Point Arithmetic Error](https://www.programiz.com/python-programming/numbers#dec).

So, whenever we assign or retrieve any object attribute like `temperature` as shown above, Python searches it in the object's built-in `__dict__` dictionary attribute as

```
print(human.__dict__) 
# Output: {'temperature': 37}
```

Therefore, `human.temperature` internally becomes `human.__dict__['temperature']`.

---

## 2.2 Using Getters and Setters

Suppose we want to extend the usability of the Celsius class defined above. We know that the temperature of any object cannot reach below **-273.15** degrees Celsius.

Let's update our code to implement this value constraint.

An obvious solution to the above restriction will be to hide the attribute `temperature` (make it private) and define new getter and setter methods to manipulate it.

This can be done as follows:

```
# Making Getters and Setter methods
class Celsius:
    def __init__(self, temperature=0):
        self.set_temperature(temperature)

    def to_fahrenheit(self):
        return (self.get_temperature() * 1.8) + 32

    # getter method
    def get_temperature(self):
        return self._temperature

    # setter method
    def set_temperature(self, value):
        if value < -273.15:
            raise ValueError("Temperature below -273.15 is not possible.")
        self._temperature = value
```

As we can see, the above method introduces two new `get_temperature()` and `set_temperature()` methods.

Furthermore, `temperature` was replaced with `_temperature`. An underscore `_` at the beginning is used to denote private [variables](https://www.programiz.com/python-programming/variables-constants-literals) in Python.

Now, let's use this implementation:

```
# Making Getters and Setter methods
class Celsius:
    def __init__(self, temperature=0):
        self.set_temperature(temperature)

    def to_fahrenheit(self):
        return (self.get_temperature() * 1.8) + 32

    # getter method
    def get_temperature(self):
        return self._temperature

    # setter method
    def set_temperature(self, value):
        if value < -273.15:
            raise ValueError("Temperature below -273.15 is not possible.")
        self._temperature = value


# Create a new object, set_temperature() internally called by __init__
human = Celsius(37)

# Get the temperature attribute via a getter
print(human.get_temperature())

# Get the to_fahrenheit method, get_temperature() called by the method itself
print(human.to_fahrenheit())

# new constraint implementation
human.set_temperature(-300)

# Get the to_fahreheit method
print(human.to_fahrenheit())
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

**Output**

37
98.60000000000001
Traceback (most recent call last):
  File "<string>", line 30, in <module>
  File "<string>", line 16, in set_temperature
ValueError: Temperature below -273.15 is not possible.

This update successfully implemented the new restriction. We are no longer allowed to set the temperature below **-273.15** degrees Celsius.

**Note**: The private variables don't actually exist in Python. There are simply norms to be followed. The language itself doesn't apply any restrictions.

However, the bigger problem with the above update is that all the programs that implemented our previous class have to modify their code from `obj.temperature` to `obj.get_temperature()` and all expressions like `obj.temperature = val` to `obj.set_temperature(val)`.

This refactoring can cause problems while dealing with hundreds of thousands of lines of codes.

All in all, our new update was not backwards compatible. This is where `@property` comes to rescue.

---

## 2.3 The property Class

A pythonic way to deal with the above problem is to use the `property` class. Here is how we can update our code:

```
# using property class
class Celsius:
    def __init__(self, temperature=0):
        self.temperature = temperature

    def to_fahrenheit(self):
        return (self.temperature * 1.8) + 32

    # getter
    def get_temperature(self):
        print("Getting value...")
        return self._temperature

    # setter
    def set_temperature(self, value):
        print("Setting value...")
        if value < -273.15:
            raise ValueError("Temperature below -273.15 is not possible")
        self._temperature = value

    # creating a property object
    temperature = property(get_temperature, set_temperature)
```

We added the [print()](https://www.programiz.com/python-programming/methods/built-in/print) function inside `get_temperature()` and `set_temperature()` to clearly observe that they are being executed.

The last line of the code makes a property object `temperature`. Simply put, property attaches some code (`get_temperature` and `set_temperature`) to the member attribute accesses (`temperature`).

Let's use this update code:

```
# using property class
class Celsius:
    def __init__(self, temperature=0):
        self.temperature = temperature

    def to_fahrenheit(self):
        return (self.temperature * 1.8) + 32

    # getter
    def get_temperature(self):
        print("Getting value...")
        return self._temperature

    # setter
    def set_temperature(self, value):
        print("Setting value...")
        if value < -273.15:
            raise ValueError("Temperature below -273.15 is not possible")
        self._temperature = value

    # creating a property object
    temperature = property(get_temperature, set_temperature)


human = Celsius(37)

print(human.temperature)

print(human.to_fahrenheit())

human.temperature = -300
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

**Output**

Setting value...
Getting value...
37
Getting value...
98.60000000000001
Setting value...
Traceback (most recent call last):
  File "<string>", line 31, in <module>
  File "<string>", line 18, in set_temperature
ValueError: Temperature below -273 is not possible

As we can see, any code that retrieves the value of `temperature` will automatically call `get_temperature()` instead of a [dictionary](https://www.programiz.com/python-programming/dictionary "Python Dictionary") (__dict__) look-up.

Similarly, any code that assigns a value to `temperature` will automatically call `set_temperature()`.

We can even see above that `set_temperature()` was called even when we created an object.

```
human = Celsius(37) # prints Setting value...
```

**Can you guess why?**

The reason is that when an object is created, the `__init__()` method gets called. This method has the line `self.temperature = temperature`. This expression automatically calls `set_temperature()`.

Similarly, any access like `c.temperature` automatically calls `get_temperature()`. This is what property does.

By using `property`, we can see that no modification is required in the implementation of the value constraint. Thus, our implementation is backward compatible.

**Note**: The actual temperature value is stored in the private `_temperature` variable. The `temperature` attribute is a property object which provides an interface to this private variable.

---

## 2.4 The @property Decorator

In Python, [property()](https://www.programiz.com/python-programming/methods/built-in/property) is a built-in function that creates and returns a `property` object. The syntax of this [function](https://www.programiz.com/python-programming/function) is:

```
property(fget=None, fset=None, fdel=None, doc=None)
```

Here,

- `fget` is function to get value of the attribute
- `fset` is function to set value of the attribute
- `fdel` is function to delete the attribute
- `doc` is a string (like a comment)

As seen from the implementation, these function arguments are optional.

A property object has three methods, `getter()`, `setter()`, and `deleter()` to specify `fget`, `fset` and `fdel` at a later point. This means, the line:

```
temperature = property(get_temperature,set_temperature)
```

can be broken down as:

```
# make empty property
temperature = property()

# assign fget
temperature = temperature.getter(get_temperature)

# assign fset
temperature = temperature.setter(set_temperature)
```

These two pieces of code are equivalent.

Programmers familiar with [Python Decorators](https://www.programiz.com/python-programming/decorator) can recognize that the above construct can be implemented as decorators.

We can even not define the names `get_temperature` and `set_temperature` as they are unnecessary and pollute the class [namespace](https://www.programiz.com/python-programming/namespace).

For this, we reuse the `temperature` name while defining our getter and setter functions. Let's look at how to implement this as a decorator:

```
# Using @property decorator
class Celsius:
    def __init__(self, temperature=0):
        self.temperature = temperature

    def to_fahrenheit(self):
        return (self.temperature * 1.8) + 32

    @property
    def temperature(self):
        print("Getting value...")
        return self._temperature

    @temperature.setter
    def temperature(self, value):
        print("Setting value...")
        if value < -273.15:
            raise ValueError("Temperature below -273 is not possible")
        self._temperature = value


# create an object
human = Celsius(37)

print(human.temperature)

print(human.to_fahrenheit())

coldest_thing = Celsius(-300)
```

[Run Code](https://www.programiz.com/python-programming/online-compiler)

**Output**

Setting value...
Getting value...
37
Getting value...
98.60000000000001
Setting value...
Traceback (most recent call last):
  File "", line 29, in 
  File "", line 4, in __init__
  File "", line 18, in temperature
ValueError: Temperature below -273 is not possible

The above implementation is simple and efficient. It is the recommended way to use `property`.