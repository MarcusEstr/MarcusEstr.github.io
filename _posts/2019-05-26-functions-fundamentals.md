---
title: "Functions - Fundamentals"
date: 2019-05-18T15:34:30-04:00
toc: true
toc_label: Functions - Fundamentals
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

# 1. Functions

Functions include commands such as `print()`, `sum()`, `len()`, `min()`, `max()`. Here is a more specific explanation for the traits of a function generally:

* It takes input.
* It does something with the input.
* It provides an output.

Although it may not be obvious to the user how `len()` generates the length of an input, it's easy to create code that provides that ability.

```python
list_1 = [21, 0, 72, 2, 5]

length = 0
for element in list_1:
    length += 1
    
print(length)
#5
```

## Solution

```python
#Create the code that could be how sun() function operates:
a_list = [4444, 8897, 6340, 9896, 4835, 4324, 10, 6445,
          661, 1246, 1000, 7429, 1376, 8121, 647, 1280,
          3993, 4881, 9500, 6701, 1199, 6251, 4432, 37]

sum_manual = 0

for element in a_list:
    sum_manual += element

print(sum_manual) #103945
print(sum(a_list)) #103945
```

# 2. Built-In Functions

The functions that we were already using, such as `sum()` and `len()` are built into the Python language. As such, we can just start using them without needing anything else or defining them on our own.

When there is a need to accomplish a repetitive task frequent and there is no built-in function, then it's possible to create your own function. 

```python
#Create a frequency table for the ratings list. Example 1.
ratings = ['4+', '4+', '4+', '9+', '12+', '12+', '17+', '17+']
content_ratings = {}

#loop through each rating in ratings list,
#then see if the current rating exists in content_ratings dictionary.
#Initialize to 1 if a new rating, or increment if existing rating in dictionary.
for element in ratings: 
    if element in content_ratings:
        content_ratings[element] += 1
    else:
        content_ratings[element] = 1
        
print(content_ratings)
```

# 3. Creating Our Own Functions

Before working on the frequency table function some more, here's an easier example. This would be a way to create a function which squares a given input number. 

## Define a Function Example

```python
#square() function definition:
def square(a_number):
    squared_number = a_number * a_number
    return squared_number
```

This definition has the following traits:

* Start with `def` statement which stands for define.
* Provided the function name `square`.
* Provided an input variable and surrounded it by parenthesis `(a_number)`.
* Line ends with `:` character.
* Indented code is what we want to be executed by `square()` function. In this case, multiple the input number by itself to provide the square of `a_number`.
* End with `return` statement which returns the output `squared_number`.

``Solution

```python
#Define square() function.
def square(a_number):
    squared_number = a_number * a_number
    return squared_number

#Use square function in a slightly longer way.
a_number = 10
squared_10 = square(a_number)
print(squared_10)

#Use square function in a slightly shorter way.
squared_16 = square(a_number = 16)
print(squared_16)
```

#4. The Structure of a Function

```python
#square() function definition:
def square(a_number): #Header
    squared_number = a_number * a_number #body
    return squared_number #return statement
```

## Solution

```python
#Function for adding 10 to a number.
def add_10(a_number):
    added_number = a_number + 10
    return added_number

add_30 = add_10(a_number=30)
add_90 = add_10(a_number=90)
```

#5. Parameters and Arguments

Earlier we showed using a square function like `square(a_number = 16)` which seemed a bit too much. Of course, we don't need to do it that way.

```python
#a_number is the Input Variable. AKA Parameter.
def square(a_number):
    squared_number = a_number * a_number
    return squared_number

square(6)
#36
```

In the above example, `square(6)`, 6 is assigned as the input variable (AKA parameter) in the square function.

If we wanted, we could make this function definition even simpler. You can return an entire expression instead of just a variable.

```python
def square(a_number):
    #Omit variable assignment
    return a_number * a_number

square(a_number=6)
#36
```

It's up to you to determine how to define your functions and how many lines of code they need. If the return statement has too much going on, then it's probably a better idea to split some things up into other lines of code.

## Solution

```python
def square(a_number):
    return a_number * a_number

squared_6 = square(6) #36
squared_11 = square(11) #121
```

# 6. Extract Values from Any Column

Here is an example of extracting values from the `cont_ratings` column of our apps_data data set.

```python
content_ratings = []
for row in apps_data[1:]:
    content_ratings = row[10]
    content_ratings.append(content_ratings)
```

## Solution

Write a function `extract()` that can extract any column from the app_data data set. Previously we were hard coding the column we wanted.

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

#extract function first creates an empty list to store what we're going to be returning. an_index is the column number we pass in.
def extract(an_index):
    element_list = []
    #Go through each row in app_data. Collect the specified field from the row based on variable index number. Then add the field to our list.
    for row in apps_data[1:]:
        element = row[an_index]
        element_list.append(element)
    return(element_list)
    #When for loop finishes, return the now filled list.  
genres = extract(11)
```

# 7. Creating Frequency Tables

The `extract()` function created in the previous section is used to extract the values for any column we want from the apps_data data set. That's not all that is needed to create a frequency table. There must also be a function that actually generates a frequency table based off the list created and returned from `extract()`!

The following example first creates an empty dictionary. Then the list is looped through to see if the iteration variable is in the dictionary. If it is, then the key-value pair is incremented by 1. If not, then the key-value pair is created in the dictionary and initialized to value of 1. 

```python
ratings = ['4+', '4+', '4+', '9+', '9+', '12+', '17+']
content_ratings = {}

for c_rating in ratings:
    if c_rating in content_ratings:
        content_ratings[c_rating] += 1
    else:
        content_ratings[c_rating] = 1
        
content_ratings
#{'12+': 1, '17+': 1, '4+': 3, '9+': 2}
```

## Solution

```python
# CODE FROM THE PREVIOUS SCREEN
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

def extract(index):
    column = []    
    for row in apps_data[1:]:
        value = row[index]
        column.append(value)    
    return column

#Create function that generates a frequency table from a list.
def freq_table(genres):
    frequency_table = {}
    #go through each record in the provided list. If the current item is in our newly-created dictionary, then increment value. If it's not in our newly-created dictionary, then add key-value pair and initialize to value 1.
    for record in genres:
        if record in frequency_table:
            frequency_table[record] += 1
        else:
            frequency_table[record] = 1
    return frequency_table

genres = extract(11)
#put our genres list into the freq_table function. Then store the frequency_table dictionary to a variable named genres_ft.
genres_ft = freq_table(genres)
```

# 8. Writing a Single Function

The previous example used two functions, `extract()` and `freq_table()` in order to create the frequency table. In another previous example, we were able to create a frequency table in a shorter way. See below for reminder:

```python
content_ratings = {}

for row in apps_data[1:]:
    c_rating = row[10] #extract value we want here.
    if c_rating in content_ratings: #if value is in our dictionary...
        content_ratings[c_rating] += 1
    else:
        content_ratings[c_rating] = 1
```

## Solution

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

rating_dictionary = {}

#Function which makes frequency table for the User Ratings.
def freq_table(index_num):
    #look through each row of the dataset...
    for row in apps_data[1:]:
        u_rating = row[index_num] #User Rating column
        #If specified rating at row[index_num] is in new dictionary or not..
        if u_rating in rating_dictionary:
            rating_dictionary[u_rating] += 1
        else:
            rating_dictionary[u_rating] = 1      
    return rating_dictionary

ratings_ft = freq_table(7)
```

# 9. Reusability and Multiple Parameters

In this code (see below), it directly iterated over apps_data data set within the function definition. Note this code is the same as Solution for section 8, but written in a way that would be easier to use for other columns naming-wise:

```python
def freq_table(index):
    frequency_table = {}
    
    #iterate over apps_data within function definition.
    for row in apps_data[1:]: 
        value = row[index]
        if value in frequency_table:
            frequency_table[value] += 1
        else:
            frequency_table[value] = 1
    return frequency_table
```

Notice that the apps_data data set was hardcoded into the function. What if we wanted to be able to use another data set with that same function? Fortunately, this is possible. Just like we were able to use the `index` as a parameter, so too can we make other parts of this code parameters that pass into the function. 

We desire functions to be reusable. So as much specificity to specific columns, datasets, rows, etc should be removed as possible. We basically only want the pure "function" in there, and can pass anything specific in as parameters. Ie: `freq_table(index, data_set)`.

```python
#Adding function takes two parameters (a, b) and returns the sum.
def add(a, b):
    a_sum = a + b
    return a_sum

add(a=9, b=11)
```

## Solution

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

# INITIAL FUNCTION
#Now function takes an index AND data set.
def freq_table(index, data_set):
    frequency_table = {}
    
    for row in data_set[1:]: #now referring to data_set parameter
        value = row[index]
        if value in frequency_table:
            frequency_table[value] += 1
        else:
            frequency_table[value] = 1
            
    return frequency_table

ratings_ft = freq_table(7, apps_data)
```

# 10. Keywords and Positional Arguments

```python
#We want to use subtract function to do 10 - 7 = 3:
def subtract(a, b):
    return a - b

#keyword arguments
subtract(a=10, b=7) #3, correct
subtract(b=7, a=10) #3, correct

#position arguments
subtract(10, 7) #3, correct
subtract(7, 10) #-3, incorrect
```

As shown above, Python allows for keyword arguments or positional arguments when calling functions. Keyword arguments will always give your input in the way you desire, but take more text to write out. 

Positional arguments are passed to the function in the order they are listed. That is why swapping them around can yield incorrect/unexpected answers.

## Solution

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

def freq_table(data_set, index):
    frequency_table = {}
    
    for row in data_set[1:]:
        value = row[index]
        if value in frequency_table:
            frequency_table[value] += 1
        else:
            frequency_table[value] = 1
        
    return frequency_table

content_ratings_ft = freq_table(apps_data, 10) #positional

ratings_ft = freq_table(data_set=apps_data, index=7) #keyword

genres_ft = freq_table(index=11, data_set=apps_data) #keyword
```

# 11. Combining Functions

Functions may at times need to be set up to reference other functions. For example, we want to create a function for finding the mean of a list of numbers. This requires first finding the sum and then finding the length of the list. 

```python
def find_sum(a_list):
    a_sum = 0
    for element in a_list:
        a_sum += element
    return a_sum

def find_length(a_list):
    length = 0
    for element in a_list:
        length += 1
    return length

#mean function uses find_sum and find_length as part of its code:
def mean(a_list_of_numbers):
    sum_list = find_sum(a_list_of_numbers)
    len_list = find_length(a_list_of_numbers)
    mean_list = sum_list / len_list
    
    return mean_list

list_1 = [10, 5, 15]
mean(list_1) #we invoke mean() function.
#10
```

Just a quick note that technically the `mean()` function could have been written even more simply:

```python
def mean(a_list_of_numbers):
    return find_sum(a_list_of_numbers) / find_length(a_list_of_numbers)
```

## Solution

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

#extract any column we want from data set
def extract(data_set, index):
    column = []    
    for row in data_set[1:]:
        value = row[index]
        column.append(value)    
    return column

#finds sum of elements in a list
def find_sum(a_list):
    a_sum = 0
    for element in a_list:
        a_sum += float(element)
    return a_sum

#finds length of a list
def find_length(a_list):
    length = 0
    for element in a_list:
        length += 1
    return length

#find mean for any column we want from a data set
def mean(data_set, index):
    returned_list = extract(data_set, index)
    return find_sum(returned_list) / find_length(returned_list)

avg_price = mean(apps_data, 4)
```

# 12. Debugging Functions

No programmer is perfect which means there will be many times that running code will result in an error. What is important is to know how to read these errors to resolve the problem(s).

## Solution

```python
#Erroneous code:
# INITIAL CODE
def extract(data_set, index):
    column = []
    
    for row in data_set[1:]:
        value = row[index]
        column.append(value)
    
    return column

def find_sum(a_list):
    a_sum = 0
    #missing colon (:) syntax.
    for element in a_list 
    #Element came in as a string, but to sum it we need to change the datatype.
    #Ex: float(element)
        a_sum += element
    return a_sum

def find_length(a_list):
    length = 0
    for element in a_list:
        length += 1
    return length

def mean(data_set, index):
    column = extract(data_set, index)
    #find_sum function typoed as find_sm.
    return find_sm(column) / find_length(column)

avg_price = mean(apps_data, 4)
avg_rating = mean(apps_data, 7)
```

