---
title: "Lists and For Loops in Python"
date: 2019-05-18T15:34:30-04:00
toc: true
toc_label: Conditional Statements
toc_sticky: true
categories:
  - Python
tags:
  - Syntax
  - DataQuest
  - Python for Data Science Fundamentals
  - Notes
  - Class
---

# 2. Indexing

A list can contain both mixed and identical data types. Ex: `['Facebook', 0.0, 'USD', 2974676, 3.5]`

## len() command

Len() used to find length of a given list.

```python
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
print(len(row_1)) 
#5
list_1 = [1, 6, 0]
print(len(list_1)) 
#3
list_2 = []
print(len(list_2)) 
#0
```

Each element in the list has an index number. Indexing begins at 0. So first element in the list has an index of 0. 

## Indexing Elements

To pull an element from a list, you can use the index. Note: An easy way to determine index number is to find what number element it is, then simply subtract 1 from it for the index value.

```python
#Retrieve an individual list element with this syntax:
#list_name[index_number]
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
row_1[0]
#'Facebook'
```

## Solution

```python
#given
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
row_2 = ['Instagram', 0.0, 'USD', 2161558, 4.5]
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]

#Assign number of ratings (4th element, 3th index) to variables
ratings_1 = row_1[3]
ratings_2 = row_2[3]
ratings_3 = row_3[3]

#Save sum of the ratings to variable
total = ratings_1 + ratings_2 + ratings_3

#Divide sum by 3 to get average number of ratings
average = total / 3
```

# 3. Negative Indexing

- **Positive indexing**: the first element has the index number 0, the second element has the index number 1, and so on.
- **Negative indexing**: the last element has the index number -1, the second to last element has the index number -2, and so on.

Why use negative indexing? It works best when you need the last element in an index, because it will always be -1.

## IndexError

If at any time you try to index a number that's outside the range of the list, Python will return an IndexError: `IndexError: list index out of range`.

## Solution

```python
#Given lists:
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
row_2 = ['Instagram', 0.0, 'USD', 2161558, 4.5]
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]

#Assign average raitings (last element)  to variables.
rating_1 = row_1[-1]
rating_2 = row_2[-1]
rating_3 = row_3[-1]

#Add ratings together and save them to variable.
total_rating = rating_1 + rating_2 + rating_3

#Divide sum by 3 to get average rating. 
average_rating = total_rating / 3
```

# 4. Retrieving Multiple List Elements

When multiple elements will be needed, we can often put them into a separate list. This way they are isolated for our use rather than needing to iterate from a much larger list all the time.

## Solution

```python
#Given lists:
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
row_2 = ['Instagram', 0.0, 'USD', 2161558, 4.5]
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]
row_4 = ['Temple Run', 0.0, 'USD', 1724546, 4.5]
row_5 = ['Pandora - Music & Radio', 0.0, 'USD', 1126879, 4.0]

#Create new lists with App name, rating count, user rating.
fb_rating_data = [row_1[0], row_1[3], row_1[4]]
insta_rating_data = [row_2[0], row_2[3], row_2[4]]
pandora_rating_data = [row_5[0], row_5[3], row_5[4]]

#Compute average rating via these new list.
avg_rating = (fb_rating_data[2] + insta_rating_data[2] + pandora_rating_data[2]) / 3
```

# 5. List Slicing

Another means of selecting multiple elements from a list at once is using a syntax shortcut known as slicing.

```python
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]

cc_pricing_data = row_3[0:3]
print(cc_pricing_data)
#['Clash of Clans', 0.0, 'USD']
```

To retrieve any list slice we want:

1. We first need to identify the first and the last element of the slice.
2. We then need to identify the index numbers of the first and the last element of the slice.
3. Finally we can retrieve the list slice we want by using the syntax `a_list[m:n]`, where:
   - `m` represents the index number of the first element of the slice; and
   - `n` represents the index number of the last element of the slice **plus one** (if the last element has the index number 2, then we `n`will be 3, if the last element has the index number 4, then `n` will be 5, and so on).

When we need to select the first or last `x` elements (`x` stands for a number), we can use even simpler syntax shortcuts:

- `a_list[:x]` when we want to select the first `x` elements.
- `a_list[-x:]` when we want to select the last `x` elements.

```python
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]

first_3 = row_3[:3]
last_3 = row_3[-3:]

print(first_3)
#['Clash of Clans', 0.0, 'USD']
print(last_3)
#['USD', 2130805, 4.5]
```

## Solution

```python
#Given lists:
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
row_2 = ['Instagram', 0.0, 'USD', 2161558, 4.5]
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]
row_4 = ['Temple Run', 0.0, 'USD', 1724546, 4.5]
row_5 = ['Pandora - Music & Radio', 0.0, 'USD', 1126879, 4.0]

#Select first 4 elements from row_1 using list slicing.
first_4_fb = row_1[:4]

#Select the last 3 elements from row_1 using list slicing.
last_3_fb = row_1[-3:]

#From row_5 get the elements ['USD', 1126879] using list slicing.
pandora_3_4 = row_5[2:4]
```

# 6. List of Lists

A list can contain other lists as elements!

```python
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
row_2 = ['Instagram', 0.0, 'USD', 2161558, 4.5]
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]
row_4 = ['Temple Run', 0.0, 'USD', 1724546, 4.5]
row_5 = ['Pandora - Music & Radio', 0.0, 'USD', 1126879, 4.0]

data_set = [row_1, row_2, row_3, row_4, row_5]
data_set
#[ ['Facebook', 0.0, 'USD', 2974676, 3.5], 
#['Instagram', 0.0, 'USD', 2161558, 4.5], 
#['Clash of Clans', 0.0, 'USD', 2130805, 4.5], 
#['Temple Run', 0.0, 'USD', 1724546, 4.5],
#['Pandora - Music & Radio', 0.0, 'USD', 1126879, 4.0] ]
```

The following functions still work because it is still a list:

- Retrieve the first list element (`row_1`) using `data_set[0]`.
- Retrieve the last list element (`row_5`) using `data_set[-1]`.
- Retrieve the first two list elements (`row_1` and `row_2`) by performing list slicing using `data_set[:2]`.

```python
dat_set = [row_1, row_2, row_3, row_4, row_5]
print(data_set[0])
#['Facebook', 0.0, 'USD', 2974676, 3.5]
print(dat_set[-1])
#['Pandora - Music & Radio', 0.0, 'USD', 1126879, 4.0]
print(dat_set[:2])
#[['Facebook', 0.0, 'USD', 2974676, 3.5], ['Instagram', 0.0, 'USD', 2161558, 4.5]]
```

What happens when you need to select a certain element from one of the lists within the list? You can grab a list out then use the index to access your desired element.

```python
dat_set = [row_1, row_2, row_3, row_4, row_5]
fb_row = data_set[0]
print(fb_row)
#['Facebook', 0.0, 'USD', 2974676, 3.5]

fb_rating = fb_row[-1]
print(fb_rating)
#3.5
```

However, this is kind of just undoing our list of lists. There is a simpler way to get into a list from within a list. We can *<u>chain together two indices</u>*. This is by far the better way in most instances.

```python
dat_set = [row_1, row_2, row_3, row_4, row_5]
print(data_set[0][-1])
#3.5
```

## Solution

```python
#Given lists:
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
row_2 = ['Instagram', 0.0, 'USD', 2161558, 4.5]
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]
row_4 = ['Temple Run', 0.0, 'USD', 1724546, 4.5]
row_5 = ['Pandora - Music & Radio', 0.0, 'USD', 1126879, 4.0]

#Group the five lists together in a list.
app_data_set = [row_1, row_2, row_3, row_4, row_5]

#Sum up ratings element from each list (the last element).
sum_rating = app_data_set[0][-1] + app_data_set[1][-1] + app_data_set[2][-1] + app_data_set[3][-1] + app_data_set[4][-1]

#Divide by number of ratings (5). 
avg_rating = sum_rating / 5
```

# 7. Opening a File

The lists in previous examples were data extracts from the following collection of Apple App data: https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps

With 7k rows of data, this is certainly not something we could set up in lists typed by hand! In this case we should open the file using Python.So we would download the CSV file from Kaggle and save it to our computer.

## open() command

How do we access the file in our Python code? We refer to its location and open it.

```python
opened_file = open('AppleStore.csv')
opened_file
#<_io.TextIOWrapper name='AppleStore.csv' mode='r' encoding='UTF-8'>
```

The output is an object. The file is opened once the `open()` command completes. That's not all that must be done, however.

## reader()

Next is to actually read the file. This is done using a command called `reader()`. To use this command we must import the command from the `csv module`. If we do not import it, then we cannot use the command.

```python
opened_file = open('AppleStore.csv')

from csv import reader
read_file = reader(opened_file)
read_file
#<_csv.reader at 0x7f8afde2bc88>
```

## list()

Now that the file is opened and read in the code, we can access it in various ways. We can for example create a list of the lists that are within the CSV file. 

```python
opened_file = open('AppleStore.csv')

from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)
```

If we were then to print `apps_data`, we would see that the data from the CSV had been split up with 16 columns and 7,198 rows - each row being a list within the list `apps_data`. The very first element (0th index) list in the `apps_data` is the column header names from the CSV (id, track_name, size_bytes, currency, etc). AKA the header row is the 0th index/first element in `apps_data`.

## Solution

```python
#Import from csv to use reader() command
from csv import reader

#Open the file.
opened_file = open('AppleStore.csv')

#Read the opened file.
read_file = reader(opened_file)

#Transform the read file to a list of lists.
apps_data = list(read_file)

#Print length of apps_data.
print(len(apps_data))

#Print first row.
print(apps_data[0])

#Print second and third row.
print(apps_data[1:3])
```

# 8. Repetitive Processes

## for... in

We can repeat a process using `for... in` statements.

```python
app_data_set = [row_1, row_2, row_3, row_4, row_5]

for each_list in app_data_set:
    rating = each_list[-1]
    print(rating)
    
#3.5
#4.5
#4.5
#4.5
#4.0
```

Python is iterating through each element of the `app_data_set` one at a time, setting it temporarily as `each_list`. Meaning, it is going into each list and setting its -1 index value (last item in list) to variable rating, then printing it out.

## Solution

```python
#Given lists:
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
row_2 = ['Instagram', 0.0, 'USD', 2161558, 4.5]
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]
row_4 = ['Temple Run', 0.0, 'USD', 1724546, 4.5]
row_5 = ['Pandora - Music & Radio', 0.0, 'USD', 1126879, 4.0]

app_data_set = [row_1, row_2, row_3, row_4, row_5]

#Print all rows from the app_data_set.
for each_list in app_data_set:
    print(each_list)
#['Facebook', 0.0, 'USD', 2974676, 3.5]
#['Instagram', 0.0, 'USD', 2161558, 4.5]
#['Clash of Clans', 0.0, 'USD', 2130805, 4.5]
#['Temple Run', 0.0, 'USD', 1724546, 4.5]
#['Pandora - Music & Radio', 0.0, 'USD', 1126879, 4.0]

```

# 9. For Loops

For... in is a for loop. 

```python
a_list = [1, 3, 5]

#value = iteration variable
#a_lists = iterable variable
for value in a_list:
    print(value) #this is the body of the loop
    print(value - 1)
```

The indented code in the **body** gets executed the same number of times as elements in the **iterable variable**. If the iterable variable is a list that has three elements, the indented code in the body gets executed three times. We call each code execution an **iteration**, so there'll be three iterations for a list that has three elements. For each iteration, the **iteration variable** will take a different value, following this pattern:

- For the first iteration, the value is the first element of the iterable (if the iterable is the list `[1, 3, 5]`, then the value will be `1`).
- For the second iteration, the value is the second element of the iterable (if the iterable is the list `[1, 3, 5]`, then the value will be `3`).
- For the third iteration, the value is the third element of the iterable (if the iterable is the list `[1, 3, 5]`, then the value will be `5`).

It's entirely possible to initialize code outside of the loop body and use it within the loop as well. 

```python
#Example of a for loop used to sum up values from a list.
a_list = [1, 3, 5]

a_sum = 0
for value in a_list:
    a_sum = a_sum + value
    print(a_sum)
    
print(a_sum)
```

- Initialize a variable `a_sum` with a value of zero *outside* the loop body.
- We loop (or iterate) over `a_list`. For every iteration of the loop, we:
  - Perform an addition (*inside* the loop body) between the current value of the iteration variable `value` and the current value stored in `a_sum` (`a_sum` was defined outside the loop body).
  - Assign the result of the addition back to `a_sum` (inside the loop body).
  - Print the value of the `a_sum` variable (inside the loop body). Notice that the value of `a_sum` changes after each addition. At the end of the loop, `a_sum` has the value `9`, which is equivalent to the sum of the numbers in `a_list` (`1 + 3 + 5`).

## Solution

```python
#Given lists:
row_1 = ['Facebook', 0.0, 'USD', 2974676, 3.5]
row_2 = ['Instagram', 0.0, 'USD', 2161558, 4.5]
row_3 = ['Clash of Clans', 0.0, 'USD', 2130805, 4.5]
row_4 = ['Temple Run', 0.0, 'USD', 1724546, 4.5]
row_5 = ['Pandora - Music & Radio', 0.0, 'USD', 1126879, 4.0]

app_data_set = [row_1, row_2, row_3, row_4, row_5]

#1. initialize sum variable with value of 0 outside of loop body.
rating_sum = 0

#2. Loop over list of lists.
#3. Extract rating of app  and store it to variable named rating. Rating is last element in list.
#4. Add value stored in rating to sum.
for each_list in app_data_set: 
    rating = each_list[-1]
    rating_sum += rating

#5. Outside loop, dividing rating sum by number of ratings. Assign result ot variable.
avg_rating = rating_sum / len(app_data_set)
```

# 10. The Average App Rating

It's time to try using what we've learned on the actual dataset with 7k rows. The problem is that we can't simply copy the code over and run it. 

##TypeError

The very first row (0th index) in the `apps_data` list is the header row. We can't attempt to sum up a STRING with an INTEGER. This yields `TypeError: unsupported operand type(s) for +: 'int' and 'str'`.So we need to skip over the first row in the list.

Theoretically, we'd have two solutions:

1. We remove the first row from `apps_data`, and then we start over the iteration. We do that by:
   - Saving the header row to a separate variable named `header`
   - Saving `apps_data[1:]` back to `apps_data` — `apps_data[1:]` is a list slice that excludes the first row (the header row)

```python
#we try the solution listed above
header = apps_data[0]
apps_data = apps_data[1:]

rating_sum = 0
for row in apps_data:
    rating = row[7]
    rating_sum = rating_sum + rating
#Oh no, get a TypeError!
```

1. We iterate directly over `apps_data[1:]`, which is a list slice that excludes the first row.

```python
rating_sum = 0
for row in apps_data[1:]:
    rating = row[7]
    rating_sum = rating_sum + rating
    
#Oh no, get a TypeError!
```

The problem is that if we really inspect the data we're trying to sum together, it is all surrounded by quotation marks. That means it's all viewed as STRINGS. Fortunately we can use commands such as `int()` or `float()` to get what we need.

```python
rating_sum = 0
for row in apps_data[1:]:
    rating = float(row[7])
    rating_sum = rating_sum + rating
print(rating_sum)
#25383.5
```

## Solution

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

#1. Initialize variable with value of 0.
rating_sum = 0

#2. loop through apps_data list of lists (amke sure you don't include header row). 
#Extract rating of app and store it in variable - make sure it's a float.
#Add value stored to current value of sum.
for each_row in apps_data[1:]:
    rating = float(each_row[7])
    rating_sum += rating
    
#3. Divide rating sum by number of ratings to get average.
avg_rating = rating_sum / len(apps_data[1:])
```

# 11. Alternative Way to Compute an Average

## append() command

Once we create a list, we can add (or **append**) values to it using the `append()`command.

```python
a_list = [1, 2]
a_list.append(3)
print(a_list)
#[1, 2, 3]
```

Now that we know how to append values to a list, we can take the steps below to compute the average app rating:

1. We initialize an empty list.
2. We start looping over our data set and *extract* the ratings.
3. We *append* the ratings to the empty list we created at step one.
4. Once we have all the ratings, we:
   - use the `sum()` command to sum up all the ratings (to be able to use `sum()`, we'll need to store the ratings as floats or integers); and then
   - we divide the sum by the number of ratings (which we can get using the `len()` command).

## Solution

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

#1. Initialize an empty list.
all_ratings = []

#loop through apps_data[1:] list of lists.
#Extract rating of the app and store in a variable.
#Make sure you convert rating from string to float.
#Append value stored to the new list.
for each_row in apps_data[1:]:
    rating = float(each_row[7])
    all_ratings.append(rating)
#3. Compute the sum of all ratings.
#4. Divide the sum of all ratings by number of ratings.
avg_rating = sum(all_ratings) / len(apps_data[1:])
```

