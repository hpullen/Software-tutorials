# Python overview

Two potential ways to run python code:
1. Put code in a file called `something.py` and run on the command line via `python something.py`.
2. Open a jupyter notebook by typing `jupyter notebook` on the command line. Create a file called `something.ipynb`, in which you can write and run blocks of python code.

## Python data types

Python has several built-in data types. The most important ones are:
- `int`: an integer
- `float`: a floating-point number (i.e. a number with a decimal point)
- `bool`: True/False
- `list`: a list of variables of any type
- `string`: a string of text (essentially a list of characters)
- `dict`: pairs of **keys** and **values**, which can be of any type (within reason)

Some more details about each type are given below.

### Ints/floats
Integers and floating-point numbers. These are initialised by defining a variable as a number:
```
a = 4   # An integer
b = 3.2   # A float
```
(Note: the `#` symbol is used for **comments** in python.)

Ints and floats can be manipulated in all the ways you would expect: 
```
ab_sum = a + b # Addition
ab_product = a * b # Multiplication
ab_ratio = a / b # Division
a_sq = a ** 2 # Power
```
They can also be converted to one another with the `int` and `float` functions:
```
a_float = float(a)  # Cast an int as a float
b_int = int(b)   # Cast a float as an int
```
Some useful shortcuts for arithmetic operations are the symbols `+=`, `-=` and `*=`:
```
a += 1 # Add to a variable
b -= 0.5 # Subtract from a variable
c *= 2 # Multiply a variable
```

### Booleans
A boolean is a binary variable that can either be `True` or `False` (note: the capital letter is essential in python!). They can be created from the result of a statement using variable comparison operators:
- `==`: equality
- `>`: greater than
- `>=`: greater than or equal to
- `<`: less than
- `<=`: less than or equal to
For example:
```
a = 1
a_is_1 = a == 1 # This will be True
a_gt_2 = a > 2 # This will be False
a_le_5 = a <= 5 # This will be True
```
Comparisons can be chained together using the keywords `and` and `or`:
```
a = 2
b = 3
test_and = a < 5 and b > a
test_or = a == 2 or b >= 0
```
There are shortcuts to test multiple variables at once:
```
test_and_shortcut = a and b < 10
test_or_shortcut = a or b == 2
```
A boolean can be used in arithmetic, where it acts like a `1` if it's `True`, or a `0` if it's `False`. For example, if you wanted to add 1 to a number only if some condition was met:
```
condition_met = True
a = 10 + 1 * condition_met
```

### Lists
A python list is a collection of variables. Lists are surrounded by square brackets (`[]`). To define a list:
```
my_list = [1, 2, 3, 4]
```
Items in the list can be accessed by their index (starting with 0), e.g.:
```
third_item = my_list[2]
```
Items can be accessed from the back of the list using a minus sign, such that the `-1` index refers to the last element in the list:
```
second_to_last_item = my_list[-2]
``` 
Colons can be used to select a range of list elements, e.g. to get a new list containing only the first 10 items:
```
first_ten = my_list[0:10]
``` 
A shortcut when you want to take items up to either the start or end of the list is to omit the `0` before the colon (or the `-1` after the colon for the end of the list, e.g.:
```
first_ten = my_list[:10]
last_ten = my_list[-10:]
```

You can also create an empty list with `[]` and then `append` to it:
```
my_list = []
my_list.append(10)
my_list.append(4)
```
Lists can be added to one another with `+`, and their length can be found with `len(my_list)`.


### Strings
Strings contain text. In python, they are either surrounded by single quotes (`''`) or double quotes (`""`), e.g.
```
my_string1 = 'hello world'
my_string2 = "this is another string"
```
Strings can be added to one another with the `+` and `+=` operators. They have some useful [functions](https://www.w3schools.com/python/python_ref_string.asp), which are applied using a `.` after the name of the variable: `my_string.some_function()`. A few useful functions are:
- `my_string.capitalize()`: return string with the first character converted to upper case
- `my_string.endswith(value)`: return `True` if the string ends with `value`
- `my_string.find(value)`: search for `value` in the string and return the position at which it was found
- `my_string.lower()`: return string converted to lowercase
- `my_string.split(separator)`: split the string at the specified separated, and return a list of the separated parts
- `my_string.startswith(value)`: return `True` if the string starts with `value`
- `my_string.strip()`: return string with any spaces at beginning and end removed
- `my_string.upper()`: return string converted to uppercase

The length of a string can be testing using the `len` function (also works on lists/dicts), e.g.:
```
my_string = "some text here"
str_len = len(my_string)
```

Specific characters from the string can be obtained by indexing in a similar manner to list indexing (starting with 0), e.g.:
```
first_char = my_string[0]
last_char = my_string[-1]
```

To make a string out of existing variables, you can use **f-strings**. These are strings prefaced with an `f`; inside the string, you can then insert variables using curly braces `{}`. For example:
```
name = 'my_name'
age = 10
to_print = f'My name is {name}. I am {age} years old.'
print(to_print)
```
When used with floating point numbers, f-strings can be used to set the number of decimal places. E.g. to print to 2 decimal places:
```
a = 0.3258952
print(f'a = {a:.2f}')
```

### Dicts
A python dictionary is a list of pairs of **keys** and their associated **values**. They are surrounded by curly braces (`{}`), and follow the format `{key: value}`. To define a dict:
```
my_dict = {
    'a': 10,
    'b': 23,
    'c': 2
}
```
Values can be added and accessed by specifying the key in square brackets:
```
my_dict['d'] = 5 # Add a new key:value pair
c = my_dict['c'] # Access an existing value via its key
```
You can get lists of the keys and values via the following functions:
```
values = my_dict.values()
keys = my_dict.keys()
```

### Checking the type
To find out what type a variable is, use the `type` function:
```
x = 3
print(type(x))
```
You can also verify whether a variable is a particular type using the `isinstance` function, which returns a boolean. E.g. to check whether `x` is an integer:
```
x = 5
if isinstance(x, int):
    print('x is an integer')
```

### Converting between types
Many variables can be converted from one type to another by surrounding the variable by the type name followed by parentheses. Note that sometimes this will cause an error; for example, you can't convert a text string like `"abc"` to a float!

Converting a (valid) string to an integer:
```
my_string = "20"
my_int = int(my_string)
```

Converting an integer to a string:
```
my_int = 60
my_string = string(my_int)
```

Note that when converting floats to strings, you might want to use the **f-string** functionality described in the strings section above, as this allows you to specific the number of decimal places.

A potential source of error comes from converting a float to an integer:
```
my_float = 50.8
my_int = int(my_float)
```
This always rounds the float **down** - so in the example above, `my_int` will be 50. If you wish to round the integer, you can instead use the `round` function:
```
my_float = 50.8
my_int = round(my_float)
``` 

### Tuples and sets
Some less common built-in types you might occasionally encounter:
- **tuples**: Like a list, but with a specific order (and unchangeable); surround by parentheses `()`
- **sets**: Like a list, but can only contain unique items; surrounded by braces `{}`. A quick hack to remove any non-unique items from a list is to convert the list to a set and back again:
```
my_list_unique = list(set(my_list))
```

## Coding basics

### Print statements
To print out text, use the `print` function. If given multiple arguments, this will print each argument with a space inbetween.
```
a = 5
print('The value of a is', a)
```

### If statements
The format of an `if` statement in python is:
```
if condition:
    # Do something
elif other_condition:
    # Do something else
else:
    # Do something else
```
The condition can be any boolean (or combination of booleans using the `and` and `or` keywords).

The `in` keyword is often useful for testing whether a string contains a character, or whether a list/dict contains a particular value/key. For example:
```
my_list = [3, 4, 5]
if 3 in my_list:
    print('3 is in the list!')
```

### For loops
The format of a `for` loop in python is:
```
for i in some_list:
    # Do something
```
Here, `some_list` can be a python **list**. The list can be defined beforehand, or when the loop is initiated, e.g.:
```
for i in [1, 2, 4, 6, 7]:
    # Do something
```
To loop through a **range of numbers**, use the `range` function:
```
for i in range(min, max):
    # Do something
```
Note that this will cover values from `min` to `max - 1`. If no `min` is specified, the range will start at zero.

To loop through the key:value pairs in a **dict**:
```
for k, v in my_dict.items():
    # Do something
```

It can sometimes be useful to put `if` statements inside a loop. If you want to end the loop early if some condition is met, use the `break` keyword:
```
for i in [1, 2, 4, 5]:
    if i == 2:
        break
    # Do something
```
If you want to just skip one iteration of the loop, use the `continue` keyword:
```
for i in [1, 2, 3, 5]:
    if i == 3:
        continue
    # Do something
```

### List comprehensions
List comprehensions are a shorthand way to loop over items in a list and create a new list. For example, if you wanted to multiply every element in a list by 2:
```
my_list = [1, 5, 6, 7, 19]
my_list_doubled = [i * 2 for i in my_list]
```
This can also used combined with a condition, e.g. to select values less than 10 only and multiple them by 2:
```
my_list_lt_10 = [i * 2 for i in my_list if i < 10]
```
The `range` keyword can be useful here, e.g. to create a list of consecutive even numbers less than 20 you could run:
```
my_list = [i * 2 for i in range(10)]
```
The same principle can be applied to dictionaries; see more [here](https://www.python.org/dev/peps/pep-0274/). A basic example that creates a dictionary of integers and their squares is:
```
squares = {i: i ** 2 for i in range(10)}
```

### While loops
The format of a `while` loop is:
```
while condition:
    # Do something
```
This will continue to loop until the condition is met.

### Try/except
Sometimes, attempting to execute code can cause the code to produce an **error**. If you think this might happen, you can use a `try`/`except` block to catch this error and deal with the consequences. In general, this follows the format:
```
try:
    # Do something which could produce an error
except:
    print('There was an error!')
```
More details [here](https://www.w3schools.com/python/python_try_except.asp).

## Reading/writing files

### Reading from a text file
A text file in python can be opened using:
```
file = open('my_file.txt')
```
The variable `file` is a special file object in python. You can loop through the lines in a file with:
```
for line in file:
    # Do something with the line
```
The variable `line` is a string containing the text from each line. To loop through the words in a line, you can use the `split` function to split up the line into words:
```
for line in file:
    for word in line.split():
        # Do something with the word
```

### Writing to a text file
A text file can be opened for writing in the same way as reading, except that the argument `'w'` should be given to indicate that the file should be writeable:
```
file = open('my_file.txt', 'w')
```
To write text to the file:
```
file.write('some text')
```
To save and close the file:
```
file.close()
```

## Functions
Functions in python are created using the `def` keyword. The body of the function is then indented. For example:
```
def divide_by_two(x):
    return x / 2
```
To return multiple values, separate them with a comma:
```
def get_square_and_cube(x):
    return x ** 2, x ** 3
```
This function could then be called with
```
x = 10
x_sq, x_cub = get_square_and_cube(x)
```
The arguments of a function can be given **default values** by setting them with an `=` sign in the function definition. In this case, if the user doesn't specify those arguments when the function is called, the default value will be used. E.g.:
```
def multiply(x, factor=2):
    return x * factor
```
The function can also be called with the names of the arguments as **keywords**. This makes it easier to call functions with a lot of arguments. E.g.:
```
def make_plot(x, y, colour='blue', width=10, height=5):
    # Some code...

x = [1, 3, 4, 5]
y = [3, 5, 6, 7]
make_plot(x, y, width=2)
```
This would use the default values for `colour` and `height`, but set the value of `width` to 2.

## Importing packages
Many different python packages exist. These add new functions and data types (**classes**) to your python session. Packages are imported using the `import` keyword at the top of a file. E.g. to import the `numpy` package and use it to access the `sqrt` function:
```
import numpy
x = 5
sqrt_x = numpy.sqrt(5)
```
It is often convenient to give the package an **alias**, especially if the package name is long. This is done with the `as` keyword. E.g. to refer to `numpy` by the alias `np` (this is a common convention):
```
import numpy as np
x = 5
sqrt_x = np.sqrt(5)
```
If a package is large, you may wish to just import one class or function. This is done with the `from` keyword. E.g. to just import the `sqrt` function from numpy:
```
from numpy import sqrt
x = 5
sqrt_x = sqrt(5)
```
Note that you don't need to type out the package name when you use a function imported in this way.

You can also import your own functions from a file in the same directory. For example, if you saved a file called `custom_funcs.py` containing the following:
```
def func1(x):
    return x * 2

def func2(x):
    return x * 3
```
you could access these functions in a different file by importing them:
```
from custom_funcs import func1, func2
```

## Installing packages and managing environments
An easy way to install many python packages is by using pip on the command line, e.g.:
```
pip install numpy
```

Python environments provide a way to manage which versions of which packages are available for a given project. One way to manage environments on the command line is by installing [miniconda](https://docs.conda.io/en/latest/miniconda.html). Once installed, you can use this to create an environment from a file specifying the environments settings; this typically includes things like environment name, python version, and packages to include. The environment is then created by running:
```
conda env create --file environment.yml
```
where `environment.yml` is the name of the environment file.

This creates an environment with the name specified in the file. The environment is then activated by running:
```
conda activate env_name
```
where `env_name` is the name of the environment.

Each environment has its own version of python and its own set of python packages. Once activated, any python-related commands run from the command line (such as Jupyter) will use the environment's python and packages. If a package isn't installed for that environment, you won't be able to use it. If you try to import a package and it can't be found, check that you're in the right environment! You can see your activate environment by running `conda info`, or see which packages are present in your current environment by running `conda list`.

Any further packages can be added to the environment using `pip` once the environment has been activated, e.g. you could run
```
pip install numpy
```
which would allow numpy to be imported from any python sessions launched in this environment in future.

To exit the environment (returning to your default environment), run
```
conda deactivate
```

## Common packages

### Numpy
The [numpy](https://numpy.org/) package contains many useful mathematical functions and constants, as well as a new data type: the **numpy array**.

Arrays are similar to lists, but much more powerful when you want to mathematically manipulate your data. For example, you can easily apply an operation to every element of an array:
```
import numpy as np
x = np.array([1, 5, 6, 2])
x_sq = x ** 2
```
or add each element of two arrays together:
```
a = np.array([3, 4, 6])
b = np.array([2, 4, 1])
c = a + b
```
Some useful numpy functions are `numpy.ones()` and `numpy.zeros()`, which can be used to create an array of ones or zeros. The function `numpy.arange()` can be used to make an array of evenly-spaced numbers spanning some range. Note that arrays can be multidimensional; more info on arrays [here](https://numpy.org/doc/stable/reference/generated/numpy.array.html). 

### Matplotlib
The [matplotlib](https://matplotlib.org/) package is used for producing plots. It can be imported with
```
import matplotlib.pyplot as plt
```
To plot two lists of values against one another:
```
x = [1, 2, 3, 4, 5]
y = [6, 7, 8, 9, 10]
plt.plot(x, y)
plt.show()
```
The style of the plot can be set via additional arguments; see the "notes" section [here](https://matplotlib.org/3.3.2/api/_as_gen/matplotlib.pyplot.plot.html).

To produce a scatter plot rather than a line plot:
```
plt.scatter(x, y)
plt.show()
```
More details on formatting the style of the scatter plot [here](https://matplotlib.org/3.3.2/api/_as_gen/matplotlib.pyplot.scatter.html).

Matplotlib can also produce a histogram of a 1D dataset:
```
plt.hist(x)
plt.show()
```

By default, multiple uses of matplotlib in one file will plot graphs on the **same axes**. To make additional plots, use `plt.figure()` before plotting.

The `subplots` function can be used to create multiple axes on a single plot. E.g. to make a 2-by-2 set of plots:
```
fig, ax = plt.subplots(2, 2)
ax[0, 0].plot(x, y)
ax[0, 1].scatter(x, y)
ax[1, 0].plot(x, x ** 2)
ax[1, 1].hist(x)
fig.show()
```

Matplotlib figures can be saved to a PNG file. To save the most recently created figure:
```
plt.savefig('my_figure.png', dpi=150)
```
where `dpi` sets the dots-per-inch of the saved PNG (i.e. the image resolution).
To save a specific figure that you have created (e.g. to save the subplot created earlier called `fig`):
```
fig.savefig('my_subplot.png')
```

Setting titles and axis labels of the most recently created figure:
```
plt.plot(x, y)
plt.title('Plot of x vs y')
plt.xlabel('x')
plt.ylabel('y')
```
Or, to set titles and axis labels of a specific axis (such as an axis in a subplot):
```
fig, ax = subplots(2)
ax[0].set_title('The first subplot')
ax[0].set_xlabel('x')
ax[0].set_ylabel('y')
```

To add a **legend** to a figure containing more than one plot, you should provide the `label` keyword to each item plotted. For example, to plot two functions on the same axes and show a legend:
```
x = np.arange(0, 100, 1) # Create array of numbers from 1 - 100
x_sq = x ** 2
x_cub = x ** 3
plt.plot(x, x_sq, label='x squared')
plt.plot(x, x_cub, label='x cubed')
plt.legend()
plt.show()
```
The legend is automatically populated with the labels of the plotted items.


### Pandas

Pandas is a package for manipulating tables of data. See an example notebook [here](docs/software_tips/pandas_intro.ipynb).
