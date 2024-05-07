# Python 
## Day 9
String, Tuple -> Immutable
Dictionary, List, Set -> Mutable
### Statement and Expression
Expression is something that returns a value <br>
Statement:
```python
gl = if (5>7);
```
Expression:
```python
# Returns a value a or b
result =  (b, a) [a < b] # Returns a value a or b
print(result) 
```

### Immutability Explanation

```python
quote3 = "Dream is not something-that you see in sleep, Dream is something that does not let you sleep."
```

#### Case 1:
```python
print(quote3[0])
#Error
quote3[0] = 'Y'
print(quote3)
```
Error!!: We cannot modify a string that is already present

#### Case 2:
```python
quote3 = "Cool"
```
No Error!! - Because whole of the String is changed and this is related to the memory location in which the String is stored

## Slicing (Continued)
### Negative values in start and end of slicing
```python
quote = "Dream"

print(quote[1:3]) # re

print(quote[-1]) # m

print(quote[-4:-1]) # rea
```

### Using skip in slicing
```python
quote1 = "Dream is something"
# print(quote[<start>:<end>:<skip>])

print(quote1[1:10:2]) # ra ss

print(quote1[1:10:1]) # ream is s

print(quote1[::-1]) # gnihtemos si maerD
```
 1    2   3   4   5<br>
 D     R    E    A   M<br> 
 -5  -4  -3  -2  -1

## Why using myenv on VS
It contains a Python.exe file and here we are using Python version 3.<br>
Suppose a new version comes up. Suppose version 4 and any of the functions does not work in Python 4 suppose this function is .upper() which is changed to .upperCase(). <br>
There will be errors at all places and test the files again.
Global Python gets updated.<br>
If we have a local copy of Version 3 copied n our PC then there will be no problem created even if the version gets updated.
This makes the code safer.<br>

Purpose - To safeguard from Updates<br>

venv - Virtual Environment 

If we don't create a local Python then global Python will be used.<br>

Whenever we activate .\myenv\Scripts\Activate.ps1 then we are currently using Local Python.
<hr>

#### Task 1 : 
After the 🔑<br>
message = "    🚨🔍📱🔑secret_code✌️"<br>
code = "SECRET_CODE✌️"<br>
output = # Your code<br>
if (output == code):<br>
  print("You are an hacker 🎊")<br>
else:<br>
  print("Try again")<br>
 Output<br>
 "You are an hacker"<br>
 or<br>
 "Try again"<br>

## : -> slicing operator

```python
message = "    🚨🔍📱🔑secret_code✌️"
code = "SECRET_CODE✌️"
key = message.find('🔑')
output = message[key+1:].upper()
 
if output == code:
    print("You are an hacker 🎊")
else:
    print("Try again")
```

#### Task 2: 
Remove junk [**, (] to find the secret code<br>
message1 = <pre>     🚨🔍📱🔑****secret_code✌️(((</pre>
```python
message = "    🚨🔍📱🔑****secret_code✌️((("
code = "SECRET_CODE✌️"
key = message.find('🔑')
output = message[key+1:].upper().strip("*").strip("(")

print(output)
 
if output == code:
    print("You are an hacker 🎊")
else:
    print("Try again")
```

### len() function
Returns the length of a String
```python
print(len("abc123"))
```

## List
```python
marks = [98, 75, 40, 80, 90, 45, 80, 60]
#list or array
print(type(marks))
#Length of List
print(len(marks))

#Slicing
print(marks[0]) #98

print(marks[-1]) #60   
print(marks[0:4]) # First 4 elements - The output is also a list
#OR
print(marks[:4])

# Reverse the list
print(marks[::-1])
```
### Why? Do we need a list
To store multiple values in a variable

### We can have a list of 
<ol>
<li>
Integers
</li>
<li>
Float
</li>
<li>
Boolean
</li>
<li>
String
</li>
<li>
List of list
</li>
</ol>


### To add a value to the list
```python
marks.append(78) # Adds value at the end
print(marks) # [98, 75, 40, 80, 90, 45, 80, 60, 78]
```

### Add value 65 after 40

```python
sci = 65
marks.insert(3, sci)
print(marks)
```

### Adding two lists
```python
grocery_list = [1000, 1500, 400]
fruits_list = [2000, 500]
#[1000, 1500, 400, 2000, 500]
final_purchase_list = grocery_list + fruits_list
print(final_purchase_list)
```

### Removing Last element from the List
```python
heights = [198, 175, 140, 1777]
heights.pop()
print(heights)
```
### To delete a value at particular index
```python
heights = [198, 175, 140, 1777]
heights.pop(1)
print(heights)
```

### Lists are mutable 
### We can use len() on String, List, 
### Appending lists - Memory location 
```python
price_list = [1000, 1500, 400]
price_list_copy = price_list
price_list1 = [1000, 1500, 400]

print(price_list_copy.append(600))
print(price_list)
print(price_list_copy)
print(price_list1)

(price_list.append(700))
print(price_list)
print(price_list_copy)
print(price_list1)

(price_list1.append(800))
print(price_list)
print(price_list_copy)
print(price_list1)

# Final lists displayed together
print(price_list, price_list_copy, price_list1)
```

### Why this happens in the above example : Copy by reference
The extra copy is not stored separately
price_list will store the memory address(suppose x1) of items and price_list_copy will also store the same memory address (i.e. x1) this is sharing of memory so that usage of RAM is less.
This is called copy by reference.

### To check address of List
```python
print(id(price_list), id(price_list1), price_list_copy)
``` 

### Copy by value
Copy by value faced during copy by reference
```python
p1 = [1000, 1500, 400]
#Using .copy()
p2 = p1.copy()
#Using slicing
p3 = p1[:]

print(p1, p2)
print(id(p1), id(p2), id(p3))
```

### Remove -> .pop(), .remove()
### Add -> .append(), .insert()
### Copy -> : (slice), .copy()

### Difference between pop and remove
```python
h1 = [198, 175, 140, 1777]
h1.pop(1) # pop - uses index to remove a value
h1.remove(1777) # remove - uses value to remove a value
print(h1)
```
### Repetition
```python
cloned_treasures = ["Gold Coin"]*3
print(cloned_treasures)
```

### split (str->list) vs join(list->str)
```python
shop_stock = "vanilla, lime, chocolate"
shop_stock_list = shop_stock.split(",")

print(shop_stock_list, shop_stock_list[2])

avatar = ["Fire", "Water", "Earth", "Air"]
print(",".join(avatar))
print("|".join(avatar))
```

#### Task :
scrambled_message = "world the save to time no is there".

Reverse this line in order of words
 
Output: There is no time to save the world
```python
scrambled_message = "world the save to time no is there"
o = scrambled_message.split(" ")[::-1]
print(" ".join(o))
```
### Using slicing operator to replace values
```python
avatar = ["Fire", "Water", "Earth", "Air"]
avatar[1:3] = ["Diamond", "Platinum", "Gold"]
print(avatar)
```

## Loops
We use loops to repeat a certain block of code

### Types
<ol>
<li>While</li>
<li>for</li>
</ol>

### while Loop

#### without while
```python
countdown = 1

print(countdown)
countdown = countdown+1
print(countdown)
countdown = countdown+1
print(countdown)
countdown = countdown+1
print(countdown)
countdown = countdown+1
print(countdown)
```

#### using while loop
```python
countdown = 1
while countdown < 6:
      print(countdown)
      countdown = countdown + 1 
```

### DRY Principle - Do not Repeat Yourself
If we repeat code several times it is a code smell that is there is some chance to make the code better. In without while we used DRY principle and made the code better using while loop.

### WET Principle

#### Task 1: Build pattern | Clue: repetition operator(*) using while
✨<br>
✨✨<br>
✨✨✨<br>
✨✨✨✨<br>
✨✨✨✨✨<br>
```python
no_of_stars = 5

i = 1

while i <= no_of_stars:
    print("✨"*i)  
    i = i + 1
```

### for Loop and range()


range(3)        | range(end)<br>
range(1, 3)     | range(start, end)<br>
range(1, 50, 2) | (start, end, skip)<br>

```python
# range starts at 0 

# Range format: range(<start>, <end>, <skip>)

for countdown in range(6):
    print(countdown)
```
```python
for countdown in range(1, 6):
    print(countdown)
```
```python
for countdown in range(1, 6, 2):
    print(countdown)
```

#### Task 2: Build pattern | Clue: repetition operator(*) using for
✨<br>
✨✨<br>
✨✨✨<br>
✨✨✨✨<br>
✨✨✨✨✨<br>

```python
n=int(input("Enter number of lines: "))
for i in range(1,n+1):
    print("✨"*i)
```

#### Task 3: Double player stats
player_stats = [10, 20, 30]<br>
Double the player stats
Output: [20, 40, 60]<br>
3.1. Using while loop
```python
player_stats = [10, 20, 30]
idx = 0
while idx < len(player_stats):
    player_stats[idx] = player_stats[idx] * 2
    idx = idx + 1
    
print(player_stats)
```

3.2. Using for loop
```python
player_stats = [10, 20, 30]
idx = 0
while idx < len(player_stats):
    player_stats[idx] = player_stats[idx] * 2
    idx = idx + 1
    
print(player_stats)
```

### How to modify an array which should not change using indices
```python
player_stats =[10, 20, 30]
powered_up_stats = []
for idx in range(len(player_stats)):
    powered_up_stats.append(player_stats[idx]*2)
    
print(powered_up_stats)
print(player_stats)
```

### Printing the list using value
```python
player_stats = [10, 20, 30]
for stat in player_stats:
    print(stat)
```
### Modify the array using value 
```python
player_stats =[10, 20, 30]
powered_up_stats = []
for stat in player_stats:
    powered_up_stats.append(stat*2)
    
print(powered_up_stats)
print(player_stats)
```
Consider the above example to understand list comprehension

### List Comprehension
Gives a copy of the result and will not modify the original array.
We need to get the value of the array actually we do not need the range i.e. no need of the indices of list. The above methods give value using index but in the below example we can print the value directly.
```python
player_stats =[10, 20, 30]
# Double the player stat for each stat in players_stats
powered_up_stats_1 = [stat * 2 for stat in player_stats]
print(powered_up_stats_1)
print(player_stats)
```
#### Task 4:
avengers = [<br>
    "Hulk",<br>
    "Iron man",<br>
    "Black widow",<br>
    "Captain america",<br>
    "Spider man",<br>
    "Thor"]<br>

 Output<br>
[4, 8, 11, 15, 10, 4]<br>
--Task 4.1 - Using for loop<br>
```python
avengers = [
    "Hulk",
    "Iron man",
    "Black widow",
    "Captain america",
    "Spider man",
    "Thor"
]
name_length = []
for avenger in avengers:
    name_length.append(len(avenger))
print(name_length)
```

--Task 4.2 - Using List comprehension

```python
avengers = [
    "Hulk",
    "Iron man",
    "Black widow",
    "Captain america",
    "Spider man",
    "Thor"
]
avenger_count = [len(avenger) for avenger in avengers]
print(avenger_count)
```
#### Task 5:  We only want the values greater than 10 from Task 4
--5.1. Using for loop
```python
avengers = [
    "Hulk",
    "Iron man",
    "Black widow",
    "Captain america",
    "Spider man",
    "Thor"
]
avenger_count = [len(avenger) for avenger in avengers]
print(avenger_count)
large_count = []
for count in avenger_count:
    if count > 10:
        large_count.append(count)
print(large_count)
```
--5.2: Using Loop Comprehension
```python
avengers = [
    "Hulk",
    "Iron man",
    "Black widow",
    "Captain america",
    "Spider man",
    "Thor"
]
name_length = []
for avenger in avengers:
    name_length.append(len(avenger))
print(name_length)
# Select count from avengers_count where count > 10
# Give me count for each count in avengers_count where count > 10
large_count_1 = [count for count in avenger_count if count > 10] 
print(large_count_1)
```

#### Task 6:
avengers = [<br>
    "Hulk",<br>
    "Iron man",<br>
    "Black widow",<br>
    "Captain america",<br>
    "Spider man",<br>
    "Thor",<br>
Output<br>
[
    "Black widow",<br>     "Captain america"<br>
]

--Task 5.1 - for loop
```python
avengers = [
    "Hulk",
    "Iron man",
    "Black widow",
    "Captain america",
    "Spider man",
    "Thor"
]
big_name = []
for avenger in avengers:
    if(len(avenger)>10):
        big_name.append(avenger)
print(big_name)
```
 
---Task 5.2 - List comprehension
```python
avengers = [
    "Hulk",
    "Iron man",
    "Black widow",
    "Captain america",
    "Spider man",
    "Thor"
]
big_name_1 = [avenger for avenger in avengers if len(avenger)>10]
print(big_name_1)
# Printing the names in Capital
print([avenger.upper() for avenger in avengers if len(avenger)>10])
```

## Dictionary
The data in a dictionary should be in the form of key value pairs.<br>
The key value of a dictionary should be unique.<br>
 
```python
person = {
    "name" : "Lionel Messi",
    "age" : 36,
    "country" : "Argentina",
    "sport" : "football"
}
```
### Accessing value of a dictionary
```python
print(person["name"])
print(person["age"])
print(type(person))
```

### Update Value
```python
person["age"] += 1
print(person)
```

### Methods
--Printing the keys of a dictionary
```python
print(person.keys())
```
--Printing the values of a dictionary
```python
print(person.values())
```
## Tasks for Dictionary
```python
books = [
    {
        "title": "Infinite Jest",
        "rating": 4.5,
        "genre": "Fiction"
    },
    {
        "title": "The Catcher in the Rye",
        "rating": 3.9,
        "genre": "Fiction"
    },
    {
        "title": "Sapiens",
        "rating": 4.9,
        "genre": "History"
    },
    {
        "title": "A Brief History of Time",
        "rating": 4.8,
        "genre": "Science"
    },
    {
        "title": "Clean Code",
        "rating": 4.7,
        "genre": "Technology"
    },
]
```
#### Task 1: 
Highly rated books | 4.7 or more<br>
Output:<br>
['Sapiens', 'A brief history', 'Clean code']<br>

-- 1.1: Using for loop
```python
highly_rated_books = []
for book in books:
    if book["rating"] >= 4.7:
        highly_rated_books.append(book["title"])
        
print(highly_rated_books)
```

-- 1.2: Using List comprehension
```python
highly_rated_books1 = [book["title"] for book in books if book["rating"] >= 4.7]
print(highly_rated_books1)
```

## Tuples
Tuples are same as list its just that tuples are immutable and lits are mutable
```python
person_l = ["Sanjana", "India", 20]
person = ("Sanjana", "India", 20)

print(person[0], person[2])
#Error
person[0] = "Sneha"
print(person[0])
```

Whatever functions are available in tuple are available in list but the opposite is not true.
remove -> .pop(), .remove() - ❌
add -> .append(), .insert() - ❌

#### Methods
```python
print(person.count(20))
print(person.index("India"))
```
## Sets
<ol>
<li>Mutable</li>
<li>Unique</li>
<li>No order (cannot access values using indices)</li>
</ol>

```python
empty_dict = {}
tech_gadgets = {"Smartphone", "Laptop", "Smartwatch", "Tablet", "Tablet"}
empty_set = set()
print(type(empty_set))
print(type(tech_gadgets))
print(tech_gadgets)

print(tech_gadgets[0]) 
#Error - because there is no order in a set so there is no point in mentioning the indices
```

### .add()
```python
tech_gadgets.add("E-Reader")
tech_gadgets.add("Laptop")
# No error and no change because laptop is already present in the set
print(tech_gadgets)
```

#### Convert list to set
```python
colors = ["red", "green", "blue", "red", "pink", "blue"]
```
--1.1: Using .add()
```python
unique_colors = set()
for color in colors:
    unique_colors.add(color)
print(unique_colors)
```

--1.2: Using set()
```python
print(set(colors))
```

# 5 types of Data Structures learned
## String
## List
## Tuple
## Dictionary
## Set

## Types of Comprehension
### List
### Dictionary
### Set

