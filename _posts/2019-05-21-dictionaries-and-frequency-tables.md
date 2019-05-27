---
title: "Dictionaries and Frequency Tables"
date: 2019-05-21T15:34:30-04:00
toc: true
toc_label: Dictionaries and Frequency Tables
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

# 1. Storing Data

It is possible to create lists of lists to make our new sets of data we want to reference. For example:

## Solution

```python
content_ratings = ['4+', '9+', '12+', '17+']
numbers = [4433, 987, 1155, 622]

content_rating_numbers = [content_ratings, numbers]
```

However, this is clearly not the most efficient means of doing things, where we must create a new list of lists to always manage these other created lists. Beyond that, the output does not clearly explain what data item corresponds to which.

# 2. Dictionaries

Dictionaries allow us to assign labels to our elements from the list. Note that the dictionary uses curly braces `{}` rather than square brackets `[]` like a list. Note also that the dictionary follows the pattern of `index:value` pairs where each is separated by a comma.

```python
content_ratings = {'4+':4433, '9+':987, '12+': 1155, '17+': 622}
print(content_ratings)
#{'17+': 622, '12+': 1155, '9+': 987, '4+': 4433}
```

Note that the order the dictionary is set in is not necessarily saved. This is clear from the output which shows the elements in reverse order. Lists do not behave this way. The list elements remain in a fixed position, which is why we can access the element via index numbering.

# 3. Indexing

While dictionaries look and act somewhat differently than lists, we can still access the elements within them in a similar way. For example, you still use indexing. The pattern is `variable_name[index]` where index is the label we assigned to the element.

```python
content_ratings = {'4+':4433, '9+':987, '12+': 1155, '17+': 622}
print(content_ratings['4+'])
#4433
```

## Solution

```python
content_ratings = {'4+': 4433, '9+': 987, '12+': 1155, '17+': 622}
over_9 = content_ratings['9+']
over_17 = content_ratings['17+']
print(over_9) #987
print(over_17) #622
```

# 4. Alternative Way of Creating a Dictionary

Creating a dictionary does not need to require so many steps of setup like it did in the previous example. It's also possible to create an empty dictionary, and add values one by one into the empty dictionary using this pattern `dictionary_name[index] = value` .

```python
content_ratings = {}
content_ratings['4+'] = 4433

print(content_ratings)
#{'4+': 4433}
```

This is very similar to populating an empty list with the append() command.

## Solution

```python
#Create an empty dictionary and add the items in one by one.
content_ratings = {}

content_ratings['4+'] = 4433
content_ratings['9+'] = 987
content_ratings['12+'] = 1155
content_ratings['17+'] = 622

over_12_n_apps = content_ratings['12+']
```

# 5. Key-Value Pairs

The index of a dictionary value is called a key. 

* Key ex: `'4+'`
* Value ex: `4433`
* Key-value pair ex: `'4+': 4433`

Dictionary <u>values</u> can hold any data type, **including** other dictionaries.

Dictionary <u>keys</u> can be most data types, **except** for a list or dictionary.

## TypeError

The TypeError: unhashable type: 'list' (or 'dict') will appear if you attempt to set the key to a dictionary or list.

```python
#This dictionary would error out because there is a list and then a dictionary used as the key.
{4: 'four',
1.5: 'one point five',
'string_key': 'string_value',
True: 'True',
[1,2,3]: 'a list',
{10: 'ten'}: 'a dictionary'}
```

# 6. Checking for Membership

There is a property of dictionaries we can use. It is to check if a certain value exists in the dictionary as a **key**. For example, we can check if '12+' exists in the dictionary using the `in` operator. 

```python
content_ratings = {'4+': 4433, '9+': 987, '12+': 1155, '17+': 622}
'12+' in content_ratings
#True
```

- `True` is returned if `a_value` exists in `a_dictionary` as a dictionary key.
- `False` is returned if `a_value` doesn't exist in `a_dictionary` as a dictionary key.

# 7. Counting with Dictionaries

Dictionary values can be modified. Here are some examples of changing the dictionary.

```python
content_ratings = {'4+': 4433, '9+': 987, '12+': 1155, '17+': 622}

content_ratings['4+'] = 0
content_ratings['9+'] += 13
content_ratings['12+'] -= 1155
content_ratings['17+'] = '622'
print(content_ratings)
#{'4+': 0, '9+': 1000, '12+': 0, '17+': 622}
```

How could we count how many times a rating is used? Here is  way using what we already know how to do:

```python
content_ratings = {'4+': 4433, '9+': 987, '12+': 1155, '17+': 622}
ratings = ['4+', '4+', '4+', '9+', '9+', '12+', '17+']

#Loop through the ratings list. 
for c_rating in ratings:
    #Use in for our if statement to determine if current list element exists as key in the dictionary. If it does, then increment that specific value associated with the key.
    if c_rating in content_ratings:
        content_ratings[c_rating] += 1
content_ratings
#{'12+': 1, '17+': 1, '4+': 3, '9+': 2}
```

## Solution

```python
#Similar to above, but used with reading in CSV dataset rather than using a hand-written list.
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

#initialize dictionary values to 0 because we're going to increment them one by one with the if statement below.
content_ratings = {'4+': 0, '9+': 0, '12+': 0, '17+': 0}

for row in apps_data[1:]:
    c_rating = row[10]
    if c_rating in content_ratings: 
        content_ratings[c_rating] += 1

print(content_ratings)
#{'12+': 1155, '9+': 987, '4+': 4433, '17+': 622}
```

# 8. Finding the Unique Values

The prior example requires the coder to know what the content ratings that were being searched for ahead of time. Of course this won't always be feasible.

A way to find these content rating keys is by first creating an empty dictionary. Then loop through a list (in this case, of ratings). When the rating is already in our dictionary we increment the key's value by one and keep going. 

When the rating is not in the dictionary, we create a new key-value pair. The key becomes the unique rating we just hit upon, and the value is 1.

```python
content_ratings = {}
ratings = ['4+', '4+', '4+', '9+', '9+', '12+', '17+']

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
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

content_ratings = {} #create empty dictionary

#loop through list of lists
for row in apps_data[1:]:
    c_rating = row[10] #assign content rating value to variable. COntent rating is index 10
    #if c_rating exists as key in dictionary, increment value by 1 on that key.
    if c_rating in content_ratings:
        content_ratings[c_rating] += 1
    #else, create new key-value pair in dictionary. set value to 1 to count it.
    else:
        content_ratings[c_rating] = 1
        
print(content_ratings)
```

# 9. Proportions and Percentages

**Frequency**: The number of times a unique value occurs.

## Frequency Table

| Content Rating | Number of Apps (Frequency) |
| -------------- | -------------------------- |
| 4+             | 4433                       |
| 9+             | 987                        |
| 12+            | 1155                       |
| 17+            | 622                        |

4+ occurred 4433 times which gives it a frequency of 4433. 

9+ has a frequency of 987. And so on.

> The proportion of apps with a content rating of `4+` quantifies the number of `4+` apps *relative* to the total number of apps. There are 4,433 apps with a content rating of `4+` and 7,197 apps in total, so the proportion of `4+` apps in our data set is $\frac{4433}{7197}$.

$\frac{4433}{7197}$ results in 0.62. 0.62 is the proportion of apps that have a content rating of 4+. Then 0.62 x 100 yields 62% percent.

## Solution

```python
#Example of finding the frequncy using code similar to what we've already done...
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

genre_counting = {}

for row in apps_data[1:]:
    genre = row[11]
    if genre in genre_counting:
        genre_counting[genre] += 1
    else:
        genre_counting[genre] = 1
        
print(genre_counting)
#{'Productivity': 178, 'News': 75, 'Weather': 72, 'Music': 138, 'Lifestyle': 144, 'Games': 3862, 'Photo & Video': 349, 'Entertainment': 535, 'Business': 57, 'Finance': 104, 'Shopping': 122, 'Book': 112, 'Catalogs': 10, 'Social Networking': 167, 'Travel': 81, 'Reference': 64, 'Medical': 23, 'Food & Drink': 63, 'Utilities': 248, 'Education': 453, 'Health & Fitness': 180, 'Sports': 114, 'Navigation': 46}
```

# 10. Looping over Dictionaries

Frequencies can be transformed into a proportion or percentage easily enough. It just requires math of dividing the frequency by total number of apps. Then, for percentage, multiplying that decimal between 0 and 1 by 100. 

```python
#We don't want to update the dictionary with proportions in this way, however! It would be far too much manual and repetitive work!
content_ratings = {'4+': 4433, '9+': 987, '12+': 1155, '17+': 622}
total_number_of_apps = 7197

content_ratings['4+'] /= total_number_of_apps
content_ratings['9+'] /= total_number_of_apps
content_ratings['12+'] /= total_number_of_apps
content_ratings['17+'] /= total_number_of_apps
```

Of course there's the much better option. It's possible to simply iterate through the dictionary using a for loop. This loops over keys (by default).

```python
content_ratings = {'4+': 4433, '9+': 987, '12+': 1155, '17+': 622}

for iteration_variable in content_ratings:
    print(iteration_variable) #dictionary key
    
#4+
#9+
#12+
#17+
```

If you want to be able to access the values of the dictionary, you could do so like this example below, which grabs the value and divides it by total number of apps:

```python
content_ratings = {'4+': 4433, '9+': 987, '12+': 1155, '17+': 622}
total_number_of_apps = 7197

for iteration_variable in content_ratings:
    content_ratings[iteration_variable] /= total_number_of_apps
    #dictionary value /= total # of apps

print(content_ratings)
#{'4+': 0.615, '9+': 0.137, '12+': 0.160, '17+': 0.0.086}
```

## Solution

```python
#Turn frequencies into percentages.
content_ratings = {'4+': 4433, '12+': 1155, '9+': 987, '17+': 622}
total_number_of_apps = 7197

#First get the proportion by dividing by total # of apps.
#Then get percentage by multiplying proportion by 100.
for iteration_variable in content_ratings:
    content_ratings[iteration_variable] /= total_number_of_apps
    content_ratings[iteration_variable] *= 100
                    
#Find the percentage of apps with content rating of 17+.
percentage_17_plus = content_ratings['17+']
#Find percentage of apps that can be downloaded by a 15 year old. Basically, everything MINUS the 17+ apps.
percentage_15_allowed = 100 - content_ratings['17+']
```

# 11. Keeping the Dictionaries Separate

While overwriting the dictionary works in theory, in reality we probably don't want that to happen. We want to keep multiple dictionaries: one for frequency, one for proportions, and one for percentages.

```python
#Create a new dictionary for the frequencies to be stored
content_ratings = {'4+': 4433, '12+': 1155, '9+': 987, '17+': 622}
total_number_of_apps = 7197
c_ratings_proportions = {} #new dictionary

for key in content_ratings:
    proportion = content_ratings[key] / total_number_of_apps
    c_ratings_proportions[key] = proportion #populate new dictionary
```

## Solution

```python
#Creating and populating proportion and percentage dictionaries
content_ratings = {'4+': 4433, '12+': 1155, '9+': 987, '17+': 622}
total_number_of_apps = 7197

c_ratings_proportions = {}
c_ratings_percentages = {}

for key in content_ratings:
    proportion = content_ratings[key] / total_number_of_apps
    percentage = proportion * 100
    c_ratings_proportions[key] = proportion
    c_ratings_percentages[key] = percentage
```

# 12. Frequency Tables for Numerical Columns

A numerical column, like size in bytes of apps, could have a tremendous amount of unique values. Again, using `size_bytes` as an example, we would actually end up with 7000+ key-value pairs!

This is why we can create **intervals**. For the size bytes field, we could say the first interval is 0 - 10,000,000. Second interval would be another grouping, 10000000 - 50000000. And so on. Basically, we'll have data groups.

With all this said, sometimes choosing an interval will not be straightforward. We can assume that most apps are going to be some MB size, and not many would be over 500MBs. If nothing else, it's helpful to know the minimum and maximum values of the column for use with our interval creation.

##min() and max() Commands

We can easily find the min and max using the commands `min()` and `max()`. These two commands work on a list of integers or floats. It will not work properly with strings. Though we could convert the strings to floats in a new list and then use the commands then.

```python
a_list = [1, 20, 10.5, 4, 0]
print(max(a_list))
#20
print(min(a_list))
#0
```

## Solution

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

data_sizes = []

for row in apps_data[1:]:
    size = float(row[2]) #data_sizes was a string, so must convert first.
    data_sizes.append(size)

min_size = min(data_sizes)
max_size = max(data_sizes)
```

# 13. Filtering for the Intervals

When you have settled on the intervals you want to use, you create a dictionary with intervals as dictionary keys and frequency as dictionary values. To start, though, the values (frequencies) will all be initialized at 0. 

```python
data_sizes = {'0 - 10 MB:' 0, '10 - 50 MB': 0, '50 - 100 MB': 0, '100 - 500 MB': 0, '500 MB +': 0}

for row in apps_data[1:]:
    data_size - float(rlow[2])
    if data_size <= 10000000:
        data_sizes['0 - 10 MB'] += 1
    elif 10000000 < data_size <= 50000000:
        data_sizes['10 - 50 MB'] += 1
    elif 50000000 < data_size <= 100000000:
        data_sizes['50 - 100 MB'] += 1
    elif 100000000 < data_size <= 500000000:
        data_sizes['100 - 500 MB'] += 1
    elif data_size > 500000000: 
        data_sizes['500 MB +'] += 1
```

## Solution

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

#Creating a list which we will use to find the max and min of the rating count column. 
numerical_list = []
for row in apps_data[1:]:
    rating_num = int(row[5])
    numerical_list.append(rating_num)
    
ratings_min = min(numerical_list) #0
ratings_max = max(numerical_list) #2,974,676

#Creating a dictionary to hold our intervals of rating counts.
rating_dictionary = {'0 - 100k': 0, '100k - 500k': 0, '500k - 1m': 0, '1m - 1.5m': 0, '1.5m - 2m': 0, '2m+': 0}

for row in apps_data[1:]:
    rating_num = int(row[5])
    #Looping through apps_data and incrementing the relevant value for specified key.
    if rating_num <= 100000:
        rating_dictionary['0 - 100k'] += 1
    elif 100000 < rating_num <= 500000:
        rating_dictionary['100k - 500k'] += 1
    elif 500000 < rating_num <= 1000000:
        rating_dictionary['500k - 1m'] += 1
    elif 1000000 < rating_num <= 1500000:
        rating_dictionary['1m - 1.5m'] += 1
    elif 1500000 < rating_num <= 2000000:
        rating_dictionary['1.5m - 2m'] += 1
    elif 2000000 < rating_num:
        rating_dictionary['2m+'] += 1
        
print(rating_dictionary)
```

