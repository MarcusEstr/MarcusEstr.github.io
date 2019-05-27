---
title: "Functions - Intermediate"
date: 2019-05-26T15:34:30-04:00
toc: true
toc_label: Functions - Intermediate
toc_sticky: true
categories:
  - Python
tags:
  - Syntax
  - DataQuest
  - Python for Data Science Fundamentals
  - Class
  - Notes
---

# 1. Interfering with the Built-in Functions

Here's an example of a function defined in the previous notes to find the sum of a list.

```python
def find_sum(a_list):
    a_sum = 0
    jfor element in a_list:
        a_sum += element
    return a_sum

list_1 = [5, 10, 15]
find_sum(list_1) #30
```

Notice that it is named `find_sum()`. Why not name it simply `sum()`? Well, the name `sum()` is actually a built in function. So if our custom function were renamed to just `sum()` then the built in `sum()` function would not run - only our custom written function.

Using built in function names for our own function is extremely discouraged. 

## Solution

```python
a_list = [1, 8, 10, 9, 7]
print(max(a_list)) #10 - Ok before function definition

def max(a_list):
    return "No max value returned"

max_val_test_0 = max(a_list)
print(max_val_test_0) #"No max value returned" - changed to our max function

del max #deletes the max() function we wrote

print(max(a_list)) #10 - back to using built in max function
```

# 2. Variable Names and Built-in Functions

Just like functions, it's also a best practice to avoid naming variables with built in function names.

```python
sum = 5 + 12 #17
list_1 = [5, 10, 15]
sum(list_1)
#TypeError: 'int' object is not callable
#It is taking sum(list_1) not as the funciton call but as 
#17(list_1), which of course makes no sense.

```

It's generally easy to tell when a name you're trying to use already exists because it will get highlighted by a different color. 

# 3. Default Arguments

Functions can be set up to have a **default argument**, ie, when an argument is given a default value. In this way we don't have to pass the defaulted argument, but can if desired.

```python
def add_value(x, constant=10):
    return x + constant

add_value(3)
#13
```

## Solution

```python
# INITIAL CODE
def open_dataset(file_name='AppleStore.csv'):
    
    opened_file = open(file_name)
    from csv import reader
    read_file = reader(opened_file)
    data = list(read_file)
    
    return data

apps_data = open_dataset() #since there is only one parameter in the function and it has a default, we don't actually have to pass anything.
```

# 4. The Official Python Documentation

Python documentation: <https://docs.python.org/3/>

Whenever something is unclear, documentation is always a great place to go. For example, here is the documentation for the `open()` function.

>`open`(*file*, *mode='r'*, *buffering=-1*, *encoding=None*, *errors=None*, *newline=None*, *closefd=True*, *opener=None*) 
>Open *file* and return a corresponding [file object](https://docs.python.org/3/glossary.html#term-file-object). If the file cannot be opened, an [`OSError`](https://docs.python.org/3/library/exceptions.html#OSError) is raised.

This shows that there are many parameters for `open()`! And that all of them aside from `file` have default arguments. That's why we have not been modifying them. Thus far we have been accepting their defaults and only need to pass in `file`.

## Solution

```python
#round(number[, ndigits])
one_decimal = round(3.43, 1)
#3.4
two_decimals = round(0.23321, 2)
#0.23
five_decimals = round(921.2225227, 5)
#921.22252
```

# 5. Multiple Return Statements

There's nothing to stop us from allowing for multiple potential return statements from a function. In the end, only one return statement can run, but we can make our choices through an if-else statement to direct which one is utilized.

```python
def sum_or_difference(a, b, do_sum=True):
    if do_sum:
        return a + b
    else:
        return a - b
    
print(sum_or_difference(10, 5, do_sum=True)) 
print(sum_or_difference(10, 5, do_sum=False))
#15
#5
```

In a simple case like this, the else clause isn't particularly required.

```python
def sum_or_difference(a, b, do_sum=True):
    if do_sum:
        return a + b

    return a - b
    
print(sum_or_difference(10, 5, do_sum=True)) 
print(sum_or_difference(10, 5, do_sum=False))
#15
#5
```

## Solution

```python
# INITIAL CODE
def open_dataset(file_name='AppleStore.csv', header=True):
    opened_file = open(file_name)
    from csv import reader
    read_file = reader(opened_file)
    data = list(read_file)
    
    if header: #if there is a header row, then remove it before sending data set back
        return data[1:] 
    
    return data #if header=False, then send back the data set in its entirety

apps_data = open_dataset()
```

# 6. Returning Multiple Variables

Earlier we only returned one value. But why not return multiple? Depending on the requirements of the code, you can choose to do so.

```python
def sum_and_difference(a, b):
    a_sum = a + b
    difference = a - b
    return a_sum, difference #separate variables with a comma to return both

sum_diff = sum_and_difference(15, 5)
sum_diff #(20, 10)
```

The example above shows the output `(20, 10)` which is a **tuple**. This is similar to a list but uses parenthesis instead of brackets. The big difference between them is that you **cannot modify existing values in a tuple**. In a list you can. Tuples are immutable. 

## Solution

```python
# My code
# INITIAL CODE
def open_dataset(file_name='AppleStore.csv', header=True):        
    opened_file = open(file_name)
    from csv import reader
    read_file = reader(opened_file)
    data = list(read_file)
    
    if header:
        return  data[:1], data[1:]
    else:
        return data
    
all_data = open_dataset()
header = all_data[0][0]
apps_data = all_data[1]
```

This worked and solved the problem. However, there is this message on screen afterward:

> For line `return data[:1], data[1:]`, select the header row without using list slicing. Otherwise, the header row is returned as a list of lists, which confuses the answer checker.

That's why I had to look in extra specificity to get header variable. So here is a cleaned up version of the code.

```python
# INITIAL CODE
def open_dataset(file_name='AppleStore.csv', header=True):        
    opened_file = open(file_name)
    from csv import reader
    read_file = reader(opened_file)
    data = list(read_file)
    
    if header:
        return data[0], data[1:] #tuple returned
    else:
        return data
    
all_data = open_dataset()
header = all_data[0]
apps_data = all_data[1]
```

# 7. More About Tuples

We can easily assign variables from the returned tuples.

```python
def sum_and_difference(a, b):
    a_sum = a + b
    difference = a - b
    return a_sum, difference

a_sum, a_diff = sum_and_difference(15, 5)
print(a_sum)
print(a_diff)
#20
#10
```

## Solution

```python
def open_dataset(file_name='AppleStore.csv', header=True):        
    opened_file = open(file_name)
    from csv import reader
    read_file = reader(opened_file)
    data = list(read_file)
    
    if header:
        return data[1:], data[0] #body, header
    else:
        return data
    
apps_data, header = open_dataset() #assign variables for both returned values in the tuple from open_dataset function.
```

# 8. Functions - Code Running Quirks

Parameters and return statements are an optional component of functions. Without a return statement, the function actually returns a `None` value. 

Python does not run code within a function until we call that function. 

# 9. Scopes - Global and Local

```python
def print_constant():
    x = 3.14
    print(x)
    
print_constant() #3.14
print(x) #NameError: name 'x' is not defined
```

Why does this occur? Because the variable `x` is not accessible outside of the function where it was defined. `x` is saved to temporary memory which only exists during function execution. Once print_constant finishes running, the variable is erased.

Notice too that the scopes are isolated between the main program and the function body. As shown in the example below, we defined x outside the function and within it. So within the function x is 3.14, but outside it remains 10.

```python
x = 10
def print_constant():
    x = 3.14
    print(x)
    
print_constant()
x
#3.14
#10
```

**Global scope**: Variables defined in the main program.

**Local scope**: Variables defined inside a function. 

## Solution

```python
e = 'mathematical constant'
a_sum = 1000
length = 50

def exponential(x):
    e = 2.72
    print(e) #2.72
    return e ** x

def divide():
    print(a_sum) #1000
    print(length) #50
    return a_sum / length

result = exponential(5) #148.88...
print(e) #mathematical constant

result_2 = divide() #20.0
```

# 10. Scopes - Searching Order

Why was the divide() function functional? This is because Python first searches in local scope of divide() function. When it did not find the variables specified, it then moves back to search the global scope. 

**Local scope is always prioritized relative to global scope**. 

The opposite does not apply. If Python does not see a variable in the global scope, it will not start looking into local scopes of functions. 

