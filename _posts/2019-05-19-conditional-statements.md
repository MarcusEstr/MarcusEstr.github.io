---
title: "Conditional Statements"
date: 2019-05-19T15:34:30-04:00
categories:
  - Python
  - Class
tags:
  - syntax
  - DataQuest
  - Python for Data Science Fundamentals
---
# 1. If Statements

Say that we wanted to use this app data set to give an average rating of free apps and average rating of non-free apps. Currently we cannot do this since the free and paid apps are all scattered together in the data set. 

Here's an example using an if statement to save the rating in our list if the price is 0.0 - free.

```python
ratings = []
for row in apps_data[1:]:
    rating = float(row[7])
    price = float(row[4])
    
    if price == 0.0: # if free
        ratings.append(rating)
```

- Assign the rating as a float to a variable named `rating`.
- Assign the price as a float to a variable named `price`. The price also comes as a string, so we need to convert it to a float.
- If the price is equal to `0.0`, we append the rating to the `ratings` list (if the price is `0.0`, then it means the app must be free). Whenever `price` is not equal to `0.0`, the code `ratings.append(rating)` is not executed.

- The `if` statement starts with `if`, it continues with `price == 0.0`, and it ends with `:`.
- We use the `==` operator to check whether price is **equal** to `0.0`. Be careful not to confuse `==` with `=` (recall that `=` is a variable assignment operator in Python, we use it to assign values to variables, and it doesn't tell us anything about equality).
- `ratings.append(rating)` is indented four spaces to the right relative to the `if` statement.

```python
# INITIAL CODE
    #2. assign price of an app as a float
    #3. if price is 0.0 then append value to new list.
    #4. outside loop body, compute average rating of free apps.
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

free_apps_ratings = []
for row in apps_data[1:]:
    rating = float(row[7])
    # Complete the code from here
    price = float(row[4])
    if price == 0.0: 
        free_apps_ratings.append(rating)
        
avg_rating_free = sum(free_apps_ratings) / len(free_apps_ratings)
```

# 2. Booleans

`==` operator returns True or False. These are **boolean values**.

```python
print(4 == 4) #True
print(4 == 7) #False
```

If statements must always be followed by:

* A boolean value.
* or an expression that evaluates to a boolean value.

```python
#If a_price is equal to 0 then print string for it being free.
#If price is equal to 1 then print a string saying it's not free.
a_price = 0
if a_price == 0:
    print("This is free")
if a_price == 1:
    print("This is not free")
```

## Solution

Now let's take a moment to find out the average rating of free apps:

```python
# INITIAL CODE
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

free_apps_ratings = []
for row in apps_data[1:]:
    rating = float(row[7])
    price = float(row[4])   
    if price == 0.0:
        free_apps_ratings.append(rating)
    
avg_rating_free = sum(free_apps_ratings) / len(free_apps_ratings)
```

# 3. The Average Rating of Non-Free Apps

`==` is not the only operator. There is also such a thing as "not equal" which is represented by `!=`. 

```python
print(2 != 0)
#True
print(2 != 2)
#False
```

To see the average rating of non-free apps, the previous solution code can be used here again just changed to seek out non-free items.

## Solution

```python
# INITIAL CODE
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

non_free_apps_ratings = []
for row in apps_data[1:]:
    rating = float(row[7])
    price = float(row[4])   
    if price != 0.0:
        non_free_apps_ratings.append(rating)
    
avg_rating_non_free = sum(non_free_apps_ratings) / len(non_free_apps_ratings)
```

# 4. The Average Rating of Gaming Apps

It's possible to use this sort of logic in other ways with the data set. For example, how aabout finding the average rating based on the genre 'gaming'? 

```python
games_ratings = []

for row in apps_data[1:]:
    rating = float(row[7])
    genre = row[11] #prime_genre field
    
    if genre == 'Games':
        games_ratings.append(rating)
        
avg_rating_games = sum(games_ratings) / len(games_ratings)
print(avg_rating_games)
#3.685007767...
```

## Solution

Similarly, we can find the average rating excluding gaming apps.

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

non_games_ratings = [] #initialize empty list

for each_row in apps_data[1:]:
    rating = float(each_row[7])
    genre = each_row[11]
    if genre != 'Games':
        non_games_ratings.append(rating)

avg_rating_non_games = sum(non_games_ratings) / len(non_games_ratings)
#3.34...
```



# 5. Multiple Conditions

Of course this leads up to the fact that an if statement can have multiple conditions simultaneously evaluated. 

```python
app1_price = 0
app_genre = 'Games'

if app1_price == 0 and app1_genre == 'Games':
    print('This is a free game!')
    
print(app1_price == 0 and app1_genre == 'Games')
#This is a free game!
#True
```

With this in mind, let's see how Python evaluates combinations of booleans. In its simplest terms, the return boolean of `True` only occurs when *all* booleans are `True`. If any boolean is `False` then the resulting boolean must also be `False`.

* True and True = True
* True and False = False
* False and True = False
* False and False = False

## Solution

```python
#Calculate the average rating of Free Game apps.
# INITIAL CODE
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

free_games_ratings = []
for row in apps_data[1:]:
    rating = float(row[7])
    price = float(row[4])
    genre = row[11]
    # Complete code from here
    if price == 0.0 and genre == 'Games':
        free_games_ratings.append(rating)
avg_rating_free_games = sum(free_games_ratings) / len(free_games_ratings)
```



# 6. The or Operator

The `or` operator is another way of using multiple criteria in an if statement. However, it does not require both booleans to evaluate to `True`. Only one needs to be `True`. In this case, if there is something with only `False`s then that will be the only instance to return `False`.

* True or True = True
* True or False = True
* False or True = True
* False or False = True

## Solution

```python
#Compute the average rating of apps whose genre is either 'Social Networking' or 'Games'
# INITIAL CODE
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

games_social_ratings = []
for row in apps_data[1:]:
    rating = float(row[7])
    genre = row[11]
    # Complete code from here
    if genre == 'Social Networking' or genre == 'Games':
        games_social_ratings.append(rating)
avg_games_social = sum(games_social_ratings) / len(games_social_ratings)
```



# 7. Combining Logical Operators

It is possible to combine these different logical operators(`and`, `or`) for a single if statement. This requires careful input so as to evaluate the booleans in the proper order/as desired.

```python
free_games_social_ratings = []

for row in apps_data[1:]:
    rating = float(row[7])
    genre = row[11]
    price = float(row[4])
    
    if (genre == 'Social Networking' or genre == 'Games') and price == 0:
        free_games_social_ratings.append(Rating)
```

In the above example, the items in the parenthesis (or statement) is evaluated first. If true, then it proceeds to check the AND statement of price == 0. Provided that is true as well, then code can proceed into if block.

## Solution

```python
#Compute the average rating on free apps whose genre is either Social Networking or Games.
#Now compute the average rating on non-free apps whose genre is either Social Networking or Games.
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

free_games_social_ratings = []
non_free_games_social_ratings = []
for row in apps_data[1:]:
    rating = float(row[7])
    genre = row[11]
    price = float(row[4])
    
    if (genre == 'Social Networking' or genre == 'Games') and price == 0:
        free_games_social_ratings.append(rating)
        
    if (genre == 'Social Networking' or genre == 'Games') and price != 0:
        non_free_games_social_ratings.append(rating)
        
avg_free = sum(free_games_social_ratings) / len(free_games_social_ratings)

# Non-free apps (average)
avg_non_free = sum(non_free_games_social_ratings) / len(non_free_games_social_ratings)
```



# 8. Comparison Operators

The comparison operators used in Python follow a similar design to other languages. 

* Equal is `==`
* Not equal is `!=`
* Greater than is `>`
* Greater than or equal to is `>=`
* Less than is `<`
* Less than or equal to is `<=`

If we had the question to see how many apps were rated 4.0 or greater, that could be accomplished in two ways:

```python
#First method is to use len to count the appended list
apps_4_or_greater = []

for row in apps_data[1:]:
    rating = float(row[7])
    if rating >= 4.0:
        apps_4_or_greater.append(rating)
        
len(apps_4_or_greater) #4781

#Second method is to increment a variable each time the if block is entered.
no_of_apps = 0

for row in apps_data[1:]:
    rating = float(row[7])
    if rating >= 4.0:
        n_of_apps = n_of_apps + 1
        
print(n_of_apps) #4781
```

## Solution

```python
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)
rating_price_greater_nine = []

for row in apps_data[1:]:
    rating = float(row[7])
    price = float(row[4])
    if price > 9:
        rating_price_greater_nine.append(rating)
        
#Get average rating of apps priced higher than $9.
avg_rating = sum(rating_price_greater_nine) / len(rating_price_greater_nine)

#Get number of apps priced higher than $9.
n_apps_more_9 = len(rating_price_greater_nine)

#Get number of apps priced less than or equal to $9.
n_apps_less_9 = len(apps_data[1:]) - len(rating_price_greater_nine)
```

# 9. The else Clause

To check for and execute different code based on criteria, you could just have a bunch of if statements after another. However, that would become a bit cumbersome and possibly cause issues. Not to mention it will make the process take longer, because we're evaluating the same item against multiple criteria when that is not necessary. This is where else` comes in.

```python
for app in apps_data:
    price = app[1]
    
    if price == 0.0:
        app.append('free')
    else:
        app.append('non-free')
```

The code only goes to and attempts the `else` if the `if` is false. otherwise, it will skip over the else clause entirely. 

The `if` and `else` together make up a compound statement. You can have an `if` clause by itself, but you cannot have an `else` clause by itself.

## Solution

```python
#Label each app as free or non-free depending on its price. Ensure that a new column label is created as well in the 0th (header) row.
# INITIAL CODE
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

for app in apps_data[1:]:
    price = float(app[4])
    # Complete code from here
    if price == 0.0:
        app.append('free')
    else:
        app.append('non-free')
apps_data[0].append('free_or_not')
print(apps_data[:5])
```

# 10. The elif Clause

Sometimes an `if` and `else` compound statement isn't enough to get what logic you want. FOr example, you may want to have *multiple* criteria being evaluated in the statement. Not just "this" or "anything else". This is where `elif` comes in.

```python
for app in apps_data:
    price = app[1]
    
    if price == 0.0:
        app.append('free')
    elif price > 0.0 and price < 20:
        app.append('affordable')
    elif price >= 20 and price < 50:
        app.append('expensive')
    elif price >= 50:
        app.append('very expensive')
```

The code begins with the very first `if` statement. If that evaluates to false, then it continues on to the first `elif`. If that evaluates to false then it continues down until finishing. If at any point something evaluates to true, then that specific block executes and then this compound statement is exited because it has completed.

Depending on the circumstances, the final `elif` can be that or an `else` depending on if you want to capture "anything else" circumstance or not. The `else` statement cannot include a boolean expression.

## Solution

```python
# INITIAL CODE
opened_file = open('AppleStore.csv')
from csv import reader
read_file = reader(opened_file)
apps_data = list(read_file)

for app in apps_data[1:]:
    price = float(app[4])
    # Complete code from here
    if price == 0:
        app.append('free')
    elif price > 0 and price < 20:
        app.append('affordable')
    elif price >= 20 and price < 50:
        app.append('expensive')
    elif price  >= 50:
        app.append('very expensive')
        
apps_data[0].append('price_label')
print(apps_data[:5])
```

