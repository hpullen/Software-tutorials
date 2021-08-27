# Python basics

## How to run python code

There are multiple ways to run python code:
1. Creating a script (e.g. `my_script.py`) containing python code and running it on the command line with `python my_script.py`;
2. Running `python` on the command line to open a python prompt, and running code one line at a time;
3. Loading a jupyter notebook (you need to have jupyter installed - see [packages](#python-packages) section;
4. Using an IDE such as [spyder](https://www.spyder-ide.org/).

## Data types

**Variables** are created in python by assigning something to a variable name using the `=` symbol. E.g. to create a variable called `a` containing the number 1, you would write
```
a = 1
```

You don't need to specify the **type** of variable - python will infer it automatically.

The most important basic data types to know about in python are:
1. `int` (integers)
2. `float` (floating point numbers)
3. `bool` (booleans i.e. True/False)
4. `str` (strings i.e. text
5. `list` (lists of items)
6. `dict` (dictionaries of keys and items)

The `print` function can be used to print any variable, e.g.:
```
my_var = 10
print("the variable is", my_var)
```

Variables can be converted to different types by surrounding them by type name and parentheses. E.g. to convert an int to a float and a string:
```
my_int = 5
my_float = float(my_int)
my_string = str(my_int)
```

### Ints and floats

When you assign a number to a variable, python will automatically detect the type as an `int` if there is no decimal point, or `float` if there is. Ints and floats can be combined with all of the expected mathematical operations:
- Addition: `c = a + b`
- Subtraction: `c = b - a`
- Multiplication: `c = a * b`
- Division: `c = b / a`
- Powers: `a_squared = a ** 2`

To add something to an existing variable, you can use the `+=` operator, e.g.:
```
a = 5
a += 1
```
Similarly, you can use the `-=`, `*=`, and `\=` operators to quickly subtract, multiple or divide a variable.

### Booleans

A boolean is a binary variable containing either `True` or `False`, and can be created with the `True` and `False` keywords (must have a capital letter!) E.g.
```
my_bool = True
```

These can then be used in `if` statements, where the code inside is only executed if the boolean is `True`:
```
if my_bool:
  print("condition met")
```
(see more in the [conditionals](#conditionals) section.)

Booleans can also be created by checking/comparing other variables. Comparison symbols include:
- `==`: equal to
- `!=`: not equal to
- `<`: less than
- `>`: greater than
- `<=`: less than or equal to
- `>=`: greater than or equal to

E.g. to create a boolean whose value depends on whether one number is larger than another:
```
a = 10
b = 5
a_largest = 10 > 5
```

Booleans can be changed together with the `and` and `or` keywords, e.g.
```
a_is_5_or_10 = a == 5 or a == 10
```

### Strings

Strings contain text and are surrounded by either single quotes (`''`) or double quotes(`""`); it doesn't matter which. E.g. to make a string:
```
my_name = "Hannah"
```

There are many useful functions and opertations for manipulation strings. 

- Strings can be **combined** with the `+` symbol:
  ```
  first_name = "Hannah"
  last_name = "Pullen"
  full_name = first_name + " " + last_name
  ```

- You can find the **length** of a string using the `len` function: `str_length = len("some string")`

- Strings can be converted to **upper** or **lower** case:
  ```
  mixed_case = "thIs IS a StrInG"
  lower_case = mixed_case.lower()
  upper_case = mixed_case.upper()
  ```
  
- You can check whether strings **contain** a given character using the `in` keyword: 
  ```if "a" in some_string:
    print("this string contains an a!")
  ```

- You can access a specific character of a string by its index (note: indices in python start at 0!) e.g. to access the 2nd character:
  ```
  my_str = "some string"
  second_char = my_str[1]
  ```
  This behaviour is very similar to a [list](#list).
  
- A useful mechnanism for formatting strings in python (assuming you have python 3) is the **f-string**. Just put an `f` in front of the quotes, and then you can insert variables into your string via curly braces. E.g.:
  ```
  first_name = "Hannah"
  last_name = "Pullen"
  full_name = f"{first_name} {last_name}"
  ```
  
  You can also insert other data types into a string in this way, e.g. you can insert a float and set its number of decimal places. The following code would set the float to 2 decimal places:
  ```
  num = 5.6326632
  my_str = f"The number is {num:.2f}"
  ```
  
### Lists

A list is a collection of variables, which can be of any type.

Lists are created with square brackets:
```
my_list = [1, 5, 2, 6, 10]
```

You can also create an empty list:
```
empty_list = []
```

Similar to strings, you can use the `in` keyword to get a boolean that tells you whether or not a given item is in a list, e.g.
```
my_list = [1, 2, 4, 5]
if 3 in list:
  print("3 is in the list!")
```

#### Adding to lists

Items can be added to a list with the `append` function:
```
my_list = [1, 2]
my_list.append(3)
```

Lists can also be added together, or used to extend a list:
```
my_list = [1, 2]
my_list += [3, 4]
```
or 
```
my_list = [1, 2]
my_list.extend([1, 2])
```
would both result in `my_list` being equal to `[1, 2, 3, 4]`

#### Extracting items from lists

Items can be 

### Dictionaries

## Conditionals and loops

## Functions

## Classes

## Python packages

## Python environments
