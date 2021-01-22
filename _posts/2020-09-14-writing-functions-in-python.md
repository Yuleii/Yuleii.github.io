---
layout: article
title: Writing Functions in Python
key: 20200914
tags: Python
pageview: false
modify_date: 2020-09-14
aside:
  toc: true
---

The original jupyter notebook is on my [programming_notebook](https://github.com/Yuleii/programming_notebook) repository.

<!--more-->


# Best Practices

## Docstrings

### Anatomy of a docstring


```python
def function_name(arguments):
    """  
    Description of what the function does.
    
    Description of the arguments, if any. 
    
    Description of the return value(s), if any.  
    
    Description of errors raised, if any.  
    
    Optional extra notes or examples of usage.  
    """
```

### Docstring formats

- Google Style

- Numpydoc

- reStructuredText

- EpyText

#### Google style 


```python
def function(arg_1, arg_2=42):
    """Description of what the function does. 
    
    Args:   arg_1 (str): Description of arg_1 that can break onto the next line     
        if needed.   
    arg_2 (int, optional): Write optional when an argument has a default     
        value. 
        
    Returns:   
        bool: Optional description of the return value   
        Extra lines are not indented. 
        
    Raises:   
        ValueError: Include any error types that the function intentionally
            raises. 
            
    Notes:   
        See https://www.datacamp.com/community/tutorials/docstrings-python   
        for more info.   
    """

```

#### [Numpydoc](https://numpydoc.readthedocs.io/en/latest/format.html)


```python
def function(arg_1, arg_2=42):
    """ Description of what the function does.
    
    Parameters 
    ---------- 
    arg_1 : expected type of arg_1   
        Description of arg_1. 
    arg_2 : int, optional   
        Write optional when an argument has a default value.
        Default=42.
      
    Returns 
    ------- 
    The type of the return value
        Can include a description of the return value.
        Replace "Returns" with "Yields" if this function is a generator. 
    """
```

### Retrieving docstrings


```python
def the_answer():
    """Return the answer to life, the universe, and everything.
    
    Returns:    
        int
    """
    return 42
print(the_answer.__doc__)
```

    Return the answer to life, the universe, and everything.
        
        Returns:    
            int
        



```python
import inspect 
print(inspect.getdoc(the_answer))
```

    Return the answer to life, the universe, and everything.
    
    Returns:    
        int


### Exercise 1


```python
def count_letter(content, letter):
    """Count the number of times `letter` appears in `content`.

    Args:
        content (str): The string to search.
        letter (str): The letter to search for.

    Returns:
        int

    # Add a section detailing what errors might be raised
    Raises:
        ValueError: If `letter` is not a one-character string.
    """
    if (not isinstance(letter, str)) or len(letter) != 1:
        raise ValueError('`letter` must be a single character string.')
    return len([char for char in content if char == letter])
```

### Exercise 2


```python
# Get the docstring with an attribute of count_letter()
docstring = count_letter.__doc__

border = '#' * 28
print('{}\n{}\n{}'.format(border, docstring, border))
```

    ############################
    Count the number of times `letter` appears in `content`.
    
        Args:
            content (str): The string to search.
            letter (str): The letter to search for.
    
        Returns:
            int
    
        # Add a section detailing what errors might be raised
        Raises:
            ValueError: If `letter` is not a one-character string.
        
    ############################



```python
import inspect

# Get the docstring with a function from the inspect module
docstring = inspect.getdoc(count_letter)

border = '#' * 28
print('{}\n{}\n{}'.format(border, docstring, border))
```

    ############################
    Count the number of times `letter` appears in `content`.
    
    Args:
        content (str): The string to search.
        letter (str): The letter to search for.
    
    Returns:
        int
    
    # Add a section detailing what errors might be raised
    Raises:
        ValueError: If `letter` is not a one-character string.
    ############################



```python
# Use the inspect module again to get the docstring for any function being passed to the build_tooltip() function.

def build_tooltip(function):
    """Create a tooltip for any function that shows the 
    function's docstring.

    Args:
        function (callable): The function we want a tooltip for.

    Returns:
        str
    """
    # Use 'inspect' to get the docstring
    docstring = inspect.getdoc(function)
    border = '#' * 28
    return '{}\n{}\n{}'.format(border, docstring, border)

print(build_tooltip(count_letter))
print(build_tooltip(range))
print(build_tooltip(print))
```

    ############################
    Count the number of times `letter` appears in `content`.
    
    Args:
        content (str): The string to search.
        letter (str): The letter to search for.
    
    Returns:
        int
    
    # Add a section detailing what errors might be raised
    Raises:
        ValueError: If `letter` is not a one-character string.
    ############################
    ############################
    range(stop) -> range object
    range(start, stop[, step]) -> range object
    
    Return an object that produces a sequence of integers from start (inclusive)
    to stop (exclusive) by step.  range(i, j) produces i, i+1, i+2, ..., j-1.
    start defaults to 0, and stop is omitted!  range(4) produces 0, 1, 2, 3.
    These are exactly the valid indices for a list of 4 elements.
    When step is given, it specifies the increment (or decrement).
    ############################
    ############################
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.
    ############################


## DRY and "Do One Thing"

### Don't repeat yourself (DRY)


```python
def load_and_plot(path):
    """Load a data set and plot the first two principal components. 
    
    Args:   
        path (str): The location of a CSV file. 
        
    Returns:   
        tuple of ndarray: (features, labels) 
    """
    # load the data
    data = pd.read_csv(path) 
    y = data['label'].values 
    X = data[col for col in train.columns if col != 'label'].values 
    
    # plot the first two principal components
    pca = PCA(n_components=2).fit_transform(X) 
    plt.scatter(pca[:,0], pca[:,1])
    
    # return loaded dat
    return X, y


train_X, train_y = load_and_plot('train.csv')
val_X, val_y = load_and_plot('validation.csv')
test_X, test_y = load_and_plot('test.csv')
```

### Do One Thing


```python
def load_data(path):
    """Load a data set. 
    Args:   
        path (str): The location of a CSV file. 
    
    Returns:   
        tuple of ndarray: (features, labels) 
    """ 
    data = pd.read_csv(path) 
    y = data['labels'].values 
    X = data[col for col in data.columns if col != 'labels'].values
    
    return X, y


def plot_data(X):
    """Plot the first two principal components of a matrix.
    
        Args:   
            X (numpy.ndarray): The data to plot. 
    """ 
    pca = PCA(n_components=2).fit_transform(X) 
    plt.scatter(pca[:,0], pca[:,1])
```

## Pass by assignment

### surprising example

Immutable
- int
- float
- bool
- string
- bytes
- tuple
- frozenset
- None

Mutable
- list
- dict
- set
- bytearray
- objects
- functions
- almost everything else!


```python
def foo(x):  
    x[0] = 99
    
my_list = [1, 2, 3]
foo(my_list)
print(my_list)
```

    [99, 2, 3]



```python
# intergers are Immutable
def bar(x):
    x = x + 90
    
my_var = 3
bar(my_var)
print(my_var)
```

    3


### Mutable default arguments are dangerous


```python
def foo(var=[]):
    var.append(1)
    return var

foo()
```




    [1]




```python
foo()
```




    [1, 1]




```python
def foo(var=None):
    if var is None:
        var = []
    var.append(1)
    return var

foo()
```




    [1]




```python
foo()
```




    [1]



### Best practice for default arguments

Bad way to assign mutable default arguments


```python
def add_column(values, df=pandas.DataFrame()):
    """Add a column of `values` to a DataFrame `df`.
    The column will be named "col_<n>" where "n" is
    the numerical index of the column.

    Args:
        values (iterable): The values of the new column
        df (DataFrame, optional): The DataFrame to update.
          If no DataFrame is passed, one is created by default.

    Returns:
        DataFrame
    """
    df['col_{}'.format(len(df.columns))] = values
    return df
```

Good way to assign mutable default arguments


```python
# Use an immutable variable for the default argument 
def better_add_column(values, df=None):
    """Add a column of `values` to a DataFrame `df`.
    The column will be named "col_<n>" where "n" is
    the numerical index of the column.

    Args:
        values (iterable): The values of the new column
        df (DataFrame, optional): The DataFrame to update.
        If no DataFrame is passed, one is created by default.

    Returns:
        DataFrame
    """
    # Update the function to create a default DataFrame
    if df is None:
        df = pandas.DataFrame()
    df['col_{}'.format(len(df.columns))] = values
    return df
```

# Context Managers

## Using context managers

A context manager:
- Sets up a context
- Runs your code 
- Removes the context


```python
with <context-manager>(<args>) as <variable-name>:
    # Run your code here
    # This code is running "inside the context"
    
# This code runs after the context is removed
```

### A real-world example

`open()` does three things: 
- Sets up a context by opening a file
- Lets you run any code you want on that file
- Removes the context by closing thele


```python
with open('my_file.txt') as my_file:
    text = my_file.read()
    length = len(text)
    
print('The file is {} characters long'.format(length))
```

### Exercise: The speed of cats


```python
image = get_image_from_instagram()

# Time how long process_with_numpy(image) takes to run
with timer():
    print('Numpy version')
    process_with_numpy(image)

# Time how long process_with_pytorch(image) takes to run
with timer():
    print('Pytorch version')
    process_with_pytorch(image)
    
Numpy version
Processing..........done!
Elapsed: 1.52 seconds
Pytorch version
Processing..........done!
Elapsed: 0.33 seconds
```

## Writing context managers

Two ways to define a context manager
- Class-based
- **Function-based**

### How to create a context manager

1. Define a function.
2. (optional) Add any set up code your context needs.
3. Use the "yield" keyword.
4. (optional) Add any teardown code your context needs.
5. Add the @contextlib.contextmanager decorator.


```python
import contextlib
from contextlib import contextmanager

@contextlib.contextmanager
def my_context():
    # Add any set up code you need
    yield
    # Add any teardown code you need
```

### The "yield" keyword


```python
@contextlib.contextmanager
def my_context():  
    print('hello')
    yield 42  # The value that your contex manager yields can be assigned to a variable in the "with" statement by adding"as" variable name.
    print('goodbye')
    
with my_context() as foo:  
    print('foo is {}'.format(foo))
```

    hello
    foo is 42
    goodbye


### Setup and teardown


```python
@contextlib.contextmanager
def database(url):
    # set up database connection  
    db = postgres.connect(url)
    yield db  # yields the database connection
    
    # tear down database connection  
    db.disconnect()
    

url = 'http://datacamp.com/data'
with database(url) as my_db:  
    course_list = my_db.execute('SELECT * FROM courses')
```

### Yielding a value or None


```python
# context manager that changes the current working directory to a specific path and the change it back after the context block is done.
# It does not need to return anything with "yield" statement
@contextlib.contextmanager
def in_dir(path): 
    # save current working directory 
    old_dir = os.getcwd()
    
    # switch to new working directory 
    os.chdir(path)
    
    yield  # not yield explicit value
    
    # change back to previous
    # working directory 
    os.chdir(old_dir)
    
    
with in_dir('/data/project_1/'):  # not yield a value
    project_files = os.listdir()
```

### Exercise: The timer() context manager


```python
# Add a decorator that will make timer() a context manager
@contextlib.contextmanager
def timer():
    """Time the execution of a context block.

    Yields:
      None
    """
    start = time.time()
    # Send control back to the context block
    yield
    end = time.time()
    print('Elapsed: {:.2f}s'.format(end - start))

with timer():
    print('This should take approximately 0.25 seconds')
    time.sleep(0.25)
    
This should take approximately 0.25 seconds
Elapsed: 0.25s
```

### Exercise: A read-only open() context manager

The regular `open()` context manager:

- takes a filename and a mode (`'r'` for read, `'w'` for write, or `'a'` for append)
- opens the file for reading, writing, or appending
- sends control back to the context, along with a reference to the file
- waits for the context to finish
- and then closes the file before exiting


```python
@contextlib.contextmanager
def open_read_only(filename):
    """Open a file in read-only mode.

    Args:
        filename (str): The location of the file to read

    Yields:
        file object
    """
    read_only_file = open(filename, mode='r')
    # Yield read_only_file so it can be assigned to my_file
    yield read_only_file
    # Close read_only_file
    read_only_file.close()

with open_read_only('my_file.txt') as my_file:
    print(my_file.read())
```

## Advanced topics

### Nested contexts

This approach works fine until you try to copy a file that is too large to fit in memory


```python
def copy(src, dst):
    """Copy the contents of one file to another. 
    
    Args:   
        src (str): File name of the file to be copied.   
        dst (str): Where to write the new file. 
    """
    
    # Open the source file and read in the contents
    with open(src) as f_src:
        contents = f_src.read()
        
    # Open the destination file and write out the contents
    with open(dst, 'w') as f_dst:   
        f_dst.write(contents)
```

Ideal: open both files at once and copy over oneline at a time.


```python
with open('my_file.txt') as my_file:
    for line in my_file:
        # do something
```


```python
def copy(src, dst):
    """Copy the contents of one file to another. 
    
    Args:   
        src (str): File name of the file to be copied.   
        dst (str): Where to write the new file. 
    """
    # Open both files
    with open(src) as f_src:
        with open(dst, 'w') as f_dst:
            # Read and write each line, one at a time
            for line in f_src:       
                f_dst.write(line)
```

### Handling errors

No handling errors


```python
def get_printer(ip): 
    p = connect_to_printer(ip)
    
    yield
    
    # This MUST be called or no one else will
    # be able to connect to the printer 
    p.disconnect() 
    print('disconnected from printer')
    
doc = {'text': 'This is my text.'}

with get_printer('10.0.34.111') as printer: 
    printer.print_page(doc['txt'])
    

Traceback (most recent call last):  
    File "<stdin>", line 1, in <module>    
        printer.print_page(doc['txt'])
KeyError: 'txt'
```

with handling errors


```python
try:
    # code that might raise an error
except:
    # do something about the error
finally:
    # this code runs no matter what
```


```python
def get_printer(ip):  
    p = connect_to_printer(ip)
    
    try:
        yield
    finally:    
        p.disconnect()    
        print('disconnected from printer')
        
        
doc = {'text': 'This is my text.'}

with get_printer('10.0.34.111') as printer:  
    printer.print_page(doc['txt'])
    
    
disconnected from printer
Traceback (most recent call last):  
    File "<stdin>", line 1, in <module>    
        printer.print_page(doc['txt'])
KeyError: 'txt'
```

### Context manager patterns

|         |            |
|---------|------------|
| Open    | Close      |
| Lock    | Release    |
| Change  | Reset      |
| Enter   | Exit       |
| Start   | Stop       |
| Setup   | Teardown   |
| Connect | Disconnect |




### Exercise: Scraping the NASDAQ

The context manager `stock('NVDA')` will connect to the NASDAQ and return an object that you can use to get the latest price by calling its `.price()` method.

You want to connect to `stock('NVDA')` and record 10 timesteps of price data by writing it to the file `NVDA.txt`.


```python
# Use the "stock('NVDA')" context manager
# and assign the result to the variable "nvda"
with stock('NVDA') as nvda:
    # Open "NVDA.txt" for writing as f_out
    with open('NVDA.txt', 'w') as f_out:
        for price in range(10):
            value = nvda.price()
            print('Logging ${:.2f} for NVDA'.format(value))
            f_out.write('{:.2f}\n'.format(value))
```

### Exercise: Changing the working directory


```python
def in_dir(directory):
    """Change current working directory to `directory`,
    allow the user to run some code, and change back.

    Args:
        directory (str): The path to a directory to work in.
    """
    current_dir = os.getcwd()
    os.chdir(directory)

    # Add code that lets you handle errors
    try:
        yield
        # Ensure the directory is reset,
        # whether there was an error or not
    finally:
        os.chdir(current_dir)
```

# Decorators
[Python 函数装饰器](https://www.runoob.com/w3cnote/python-func-decorators.html)

## Functions are objects

### Functions are just another type of object

Python objects:


```python
def x():
    pass
x = [1, 2, 3]
x = {'foo': 42}
x = pandas.DataFrame()
x = 'This is a sentence.'
x = 3
x = 71.2
import x
```

### Functions as variables


```python
def my_function():  
    print('Hello')
x = my_function
type(x)
```




    function




```python
x
```




    <function __main__.my_function()>




```python
x()
```

    Hello



```python
PrintyMcPrintface = print
PrintyMcPrintface('Python is awesome!')
```

    Python is awesome!


### Lists and dictionaries of functions


```python
list_of_functions = [my_function, open, print]
list_of_functions[2]('I am printing with an element of a list!')
```

    I am printing with an element of a list!



```python
dict_of_functions = {
    'func1': my_function,
    'func2': open,
    'func3': print
}
dict_of_functions['func3']('I am printing with a value of a dict!')
```

    I am printing with a value of a dict!


### Referencing a function


```python
def my_function():
    return 42

x = my_function
my_function()
```




    42




```python
my_function
```




    <function __main__.my_function()>



### Functions as arguments


```python
def has_docstring(func):
    """Check to see if the function  `func` has a docstring. 
    
    Args:   
        func (callable): A function. 
        
    Returns:   
        bool 
    """
    return func.__doc__ is not None
```


```python
def no():
    return 42

def yes():
    """Return the value 42 """
    return 42

has_docstring(no)
```




    False




```python
has_docstring(yes)
```




    True



### Defining a function inside another function


```python
def foo():
    x = [3, 6, 9]
    
    def bar(y):    
        print(y)
        
    for value in x:
        bar(x)
```


```python
def foo(x, y):
    if x > 4 and x < 10 and y > 4 and y < 10:    
        print(x * y)
        
        
        
def foo(x, y):
    def in_range(v):
        return v > 4 and v < 10 
    
    if in_range(x) and in_range(y):    
        print(x * y)
```


```python
def get_function():
    def print_me(s):   
        print(s)
    
    return print_me

new_func = get_function()
new_func('This is a sentence.')
```

    This is a sentence.


## Scope


```python
x = 7
y = 200
print(x)
```

    7



```python
def foo():    
    x = 42    
    print(x)    
    print(y)
    
foo()
```

    42
    200



```python
print(x)
```

    7


### The global keyword


```python
x = 7

def foo():  
    x = 42  
    print(x)
    
foo()
```

    42



```python
print(x)
```

    7



```python
x = 7

def foo():
    global x  
    x = 42  
    print(x)
    
foo()
```

    42



```python
print(x)
```

    42


### The nonlocal keyword
You should try to avoid using `global` variables if possible, because it can make testing and debugging harder.
The `nonlocal` keyword works exactly the same as the `global` key word, but it is used whenyou are inside a nested function, and you want to update a variable that is defined inside your parent function.


```python
def foo():  
    x = 10
    
    def bar():    
        x = 200    
        print(x)  
        
    bar()  
    print(x)
    
foo()
```

    200
    10



```python
def foo():  
    x = 10
    
    def bar():
        nonlocal x
        x = 200    
        print(x)  
        
    bar()  
    print(x)
    
foo()
```

    200
    200



```python
x = 50

def one():
    x = 10

def two():
    global x
    x = 30

def three():
    x = 100
    print(x)

for func in [one, two, three]:
    func()
    print(x)
```

    50
    30
    100
    30


## Closures

A closure in Python is a tuple of variables that are no longer in scope, but that a function needs in order to run.

### Attaching nonlocal variables to nested functions


```python
def foo(): 
    a = 5
    def bar():
        print(a)
    return bar

func = foo()

func()
```

    5



```python
type(func.__closure__)
```




    tuple




```python
len(func.__closure__)
```




    1




```python
func.__closure__[0].cell_contents
```




    5



### Closures and deletion


```python
x = 25 # x is defined in the gloabl scope

def foo(value):
    def bar():   
        print(value)
    return bar

my_func = foo(x)
my_func() # print the value x
```

    25



```python
# delete x and call my_func again, it would still print 25. 
# Because foo()'s value argument gets added to the closure attached to the new my_func function.
# So even though x doesn't exist anymore, thevalue persists in its closure
del(x)
my_func() 
```

    25



```python
len(my_func.__closure__)
```




    1




```python
my_func.__closure__[0].cell_contents
```




    25



### Closures and overwriting


```python
# pass x into foo() and then assigned the new function to the variable x. 
# The old value of x 25 is still stored in the new function's closure. 
# even though the new function is now stores in the x variable
x = 25

def foo(value):
    def bar():   
        print(value)
    return bar

x = foo(x)
x() 
```

    25



```python
len(x.__closure__)
```




    1




```python
x.__closure__[0].cell_contents
```




    25



## Why does all of this matter?

Decorators use:
- Functions as objects
- Nested functions
- Nonlocal scope
- Closures

Nested function: A function dened inside another function


```python
# outer function
def parent():
    # nested function
    def child():
        pass
    return child
```

Nonlocal variables: Variables dened in the parent function that are used by the child function


```python
def parent(arg_1, arg_2):
    # From child()'s point of view,
    # `value` and `my_dict` are nonlocal variables,
    # as are `arg_1` and `arg_2`.  
    value = 22  
    my_dict = {'chocolate': 'yummy'}
    
    def child():    
        print(2 * value)    
        print(my_dict['chocolate'])    
        print(arg_1 + arg_2)
        
    return child
```

Closure: Nonlocal variables attached to a returned function


```python
def parent(arg_1, arg_2):  
    value = 22 
    my_dict = {'chocolate': 'yummy'}
    def child():    
        print(2 * value)    
        print(my_dict['chocolate'])    
        print(arg_1 + arg_2)
        
    return child

new_function = parent(3, 4)

print([cell.cell_contents for cell in new_function.__closure__])
```

    [3, 4, {'chocolate': 'yummy'}, 22]


## Decorators

### The double_args decorator


```python
def multiply(a, b):
    return a * b
def double_args(func):
    def wrapper(a, b):
        # Call the passed in function, but double each argument
        return func(a * 2, b * 2)
    return wrapper

# assign the new function to "new_multiply"
new_multiply = double_args(multiply)
new_multiply(1, 5)
```




    20




```python
multiply(1, 5)
```




    5




```python
def multiply(a, b):
    return a * b
def double_args(func):
    def wrapper(a, b):
        # Call the passed in function, but double each argument
        return func(a * 2, b * 2)
    return wrapper

# instead of assign the new function to "new_multiply", we're going to overwrite the "multiply" varable
# we can do this because Python stores the orignial multipy function in the new function's closure
multiply = double_args(multiply)
multiply(1, 5)
```




    20



### Decorator syntax


```python
def double_args(func):
    def wrapper(a, b):
        return func(a * 2, b * 2)
    return wrapper

@double_args
def multiply(a, b):
    return a * b

multiply(1, 5)
```




    20



### Exercise: Defining a decorator


```python
def print_before_and_after(func):
    def wrapper(*args):
        print('Before {}'.format(func.__name__))
        # Call the function being decorated with *args
        func(*args)
        print('After {}'.format(func.__name__))
      # Return the nested function
    return wrapper

@print_before_and_after
def multiply(a, b):
    print(a * b)

multiply(5, 10)
```

    Before multiply
    50
    After multiply


## Real-world examples

### Time a function


```python
import time

def timer(func):
    """A decorator that prints how long a function took to run.  
    
    Args:    
        func (callable): The function being decorated.  
        
    Returns:    
        callable: The decorated function.  
    """
    # Define the wrapper function to return.
    def wrapper(*args, **kwargs):
        # When wrapper() is called, get the current time.   
        t_start = time.time()
        # Call the decorated function and store the result.   
        result = func(*args, **kwargs)
        # Get the total time it took to run, and print it.   
        t_total = time.time() - t_start   
        print('{} took {}s'.format(func.__name__, t_total))
        return result
    return wrapper
```

### Using timer()


```python
@timer
def sleep_n_seconds(n):  
    time.sleep(n)
```


```python
sleep_n_seconds(5)
```

    sleep_n_seconds took 5.001962184906006s



```python
sleep_n_seconds(10)
```

    sleep_n_seconds took 10.00467300415039s


### When to use decorators

Add common behavior to multiple functions


```python
@timer
def foo():
    # do some computation
    
@timer
def bar():
    # do some other computation
    
@timer
def baz():
    # do something else
```

### Exercise: Print the return type


```python
def print_return_type(func):
  # Define wrapper(), the decorated function
    def wrapper(*args, **kwargs):
    # Call the function being decorated
        result = func(*args, **kwargs)
        print('{}() returned type {}'.format(
          func.__name__, type(result)
        ))
        return result
    # Return the decorated function
    return wrapper
  
@print_return_type
def foo(value):
    return value
  
print(foo(42))
print(foo([1, 2, 3]))
print(foo({'a': 42}))
```

    foo() returned type <class 'int'>
    42
    foo() returned type <class 'list'>
    [1, 2, 3]
    foo() returned type <class 'dict'>
    {'a': 42}


### Exercise: Counter


```python
def counter(func):
    def wrapper(*args, **kwargs):
        wrapper.count += 1
        # Call the function being decorated and return the result
        return wrapper
    wrapper.count = 0
    # Return the new decorated function
    return wrapper

# Decorate foo() with the counter() decorator
@counter
def foo():
    print('calling foo()')

    
foo()
foo()
foo()

print('foo() was called {} times.'.format(foo.count))
```

    foo() was called 3 times.


## Decorators and metadata


```python
def sleep_n_seconds(n=10):
    """Pause processing for n seconds.  
    
    Args:    
    n (int): The number of seconds to pause for.  
    """  
    time.sleep(n)
    
print(sleep_n_seconds.__doc__)
```

    Pause processing for n seconds.  
        
        Args:    
        n (int): The number of seconds to pause for.  
        



```python
print(sleep_n_seconds.__name__)
```

    sleep_n_seconds



```python
print(sleep_n_seconds.__defaults__)
```

    (10,)


problem: Ouput输出应该是"a_function_requiring_decoration"。这里的函数被warpTheFunction替代了。它重写了我们函数的名字和注释文档(docstring)。


```python
@timer
def sleep_n_seconds(n=10):
    """Pause processing for n seconds.  
    
    Args:    
    n (int): The number of seconds to pause for.  
    """  
    time.sleep(n)
    
print(sleep_n_seconds.__doc__)
```

    None



```python
print(sleep_n_seconds.__name__)
```

    wrapper


### fix: The timer decorator


```python
from functools import wraps
def timer(func):
    """A decorator that prints how long a function took to run.  """
    @wraps(func)
    def wrapper(*args, **kwargs):
        # When wrapper() is called, get the current time.   
        t_start = time.time()
        # Call the decorated function and store the result.   
        result = func(*args, **kwargs)
        # Get the total time it took to run, and print it.   
        t_total = time.time() - t_start   
        print('{} took {}s'.format(func.__name__, t_total))
        return result
    return wrapper
```


```python
@timer
def sleep_n_seconds(n=10):
    """Pause processing for n seconds.  
    
    Args:    
    n (int): The number of seconds to pause for.  
    """  
    time.sleep(n)
    
print(sleep_n_seconds.__doc__)
```

    Pause processing for n seconds.  
        
        Args:    
        n (int): The number of seconds to pause for.  
        



```python
print(sleep_n_seconds.__name__)
```

    sleep_n_seconds



```python
print(sleep_n_seconds.__defaults__)
```

    None


### Access to the original function


```python
sleep_n_seconds.__wrapped__
```




    <function __main__.sleep_n_seconds(n=10)>



## Decorators that take arguments


```python
def run_three_times(func):
    def wrapper(*args, **kwargs):
        for i in range(3):      
            func(*args, **kwargs)
    return wrapper

@run_three_times
def print_sum(a, b):  
    print(a + b)
    
print_sum(3, 5)
```

    8
    8
    8


### A decorator factory


```python
def run_n_times(n):
    """Define and return a decorator"""
    def decorator(func):
        def wrapper(*args, **kwargs):
            for i in range(n):        
                func(*args, **kwargs)
        return wrapper
    return decorator
    
run_three_times = run_n_times(3)

@run_three_times
def print_sum(a, b):  
    print(a + b)
    
@run_n_times(3)
def print_sum(a, b):  
    print(a + b)
```

Using run_n_times()


```python
@run_n_times(3)
def print_sum(a, b):  
    print(a + b)

print_sum(3, 5)
```

    8
    8
    8



```python
@run_n_times(5)
def print_sum(a, b):  
    print("Hello!")

print_sum(3, 5)
```

    Hello!
    Hello!
    Hello!
    Hello!
    Hello!


## Timeout(): a real world example


```python
import signal

def raise_timeout(*args, **kwargs):
    raise TimeoutError()

# When an "alarm" signal goes off, call raise_timeout()
signal.signal(signalnum=signal.SIGALRM, handler=raise_timeout)
# Set off an alarm in 5 seconds
signal.alarm(5)
# Cancel the alarm
signal.alarm(0)
```




    5




```python
def timeout_in_5s(func): 
    @wraps(func)
    def wrapper(*args, **kwargs):
        # Set an alarm for 5 seconds   
        signal.alarm(5)
        try:
            # Call the decorated func
            return func(*args, **kwargs)
        finally:
            # Cancel alarm     
            signal.alarm(0)
    return wrapper
```


```python
@timeout_in_5s
def foo(): 
    time.sleep(10) 
    print('foo!')
    
foo()
```


    ---------------------------------------------------------------------------

    TimeoutError                              Traceback (most recent call last)

    <ipython-input-174-0108488cb4f8> in <module>
          4     print('foo!')
          5 
    ----> 6 foo()
    

    <ipython-input-173-5c170f9616ff> in wrapper(*args, **kwargs)
          6         try:
          7             # Call the decorated func
    ----> 8             return func(*args, **kwargs)
          9         finally:
         10             # Cancel alarm


    <ipython-input-174-0108488cb4f8> in foo()
          1 @timeout_in_5s
          2 def foo():
    ----> 3     time.sleep(10)
          4     print('foo!')
          5 


    <ipython-input-171-a920ac223708> in raise_timeout(*args, **kwargs)
          2 
          3 def raise_timeout(*args, **kwargs):
    ----> 4     raise TimeoutError()
          5 
          6 # When an "alarm" signal goes off, call raise_timeout()


    TimeoutError: 



```python
def timeout(n_seconds):    
    def decorator(func): 
        @wraps(func)
        def wrapper(*args, **kwargs):
            # Set an alarm for 5 seconds   
            signal.alarm(n_seconds)
            try:
                # Call the decorated func
                return func(*args, **kwargs)
            finally:
                # Cancel alarm     
                signal.alarm(0)
        return wrapper
    return decorator


@timeout(5)
def foo(): 
    time.sleep(10) 
    print('foo!')
    
foo()
```


    ---------------------------------------------------------------------------

    TimeoutError                              Traceback (most recent call last)

    <ipython-input-177-8ff2689a19ab> in <module>
         20     print('foo!')
         21 
    ---> 22 foo()
    

    <ipython-input-177-8ff2689a19ab> in wrapper(*args, **kwargs)
          7             try:
          8                 # Call the decorated func
    ----> 9                 return func(*args, **kwargs)
         10             finally:
         11                 # Cancel alarm


    <ipython-input-177-8ff2689a19ab> in foo()
         17 @timeout(5)
         18 def foo():
    ---> 19     time.sleep(10)
         20     print('foo!')
         21 


    <ipython-input-171-a920ac223708> in raise_timeout(*args, **kwargs)
          2 
          3 def raise_timeout(*args, **kwargs):
    ----> 4     raise TimeoutError()
          5 
          6 # When an "alarm" signal goes off, call raise_timeout()


    TimeoutError: 



```python
@timeout(20)
def bar(): 
    time.sleep(10) 
    print('bar!')
    
bar()
```

    bar!


### Exercise: Tag your functions

You've decided to write a decorator that will let you tag your functions with an arbitrary list of tags. You could use these tags for many things:

- Adding information about who has worked on the function, so a user can look up who to ask if they run into trouble using it.
- Labeling functions as "experimental" so that users know that the inputs and outputs might change in the future.
- Marking any functions that you plan to remove in a future version of the code.
- tc.


```python
def tag(*tags):
    # Define a new decorator, named "decorator", to return
    def decorator(func):
        # Ensure the decorated function keeps its metadata
        @wraps(func)
        def wrapper(*args, **kwargs):
            # Call the function being decorated and return the result
            return func(*args, **kwargs)
        wrapper.tags = tags
        return wrapper
    # Return the new decorator
    return decorator

@tag('test', 'this is a tag')
def foo():
    pass

print(foo.tags)
```

    ('test', 'this is a tag')


### Exercise: Check the return type


```python
def returns_dict(func):
  # Complete the returns_dict() decorator
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        assert(type(result) == dict)
        return result
    return wrapper

@returns_dict
def foo(value):
    return value

try:
    print(foo([1,2,3]))
except AssertionError:
    print('foo() did not return a dict!')
```

    foo() did not return a dict!



