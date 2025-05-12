---
title: Python - Mastering the Basics
# subtitle: 
license: CC-BY-4.0
github: https://github.com/Murphy465/data_visualization_myst
subject: Tutorial
authors:
  - name: Sarah Anne Murphy
    orcid: 0000-0002-7787-6890
    affiliations:
      - The Ohio State University Libraries
date: 2025-05-02
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3

---

## Data skills | concepts
- Python

## Learning objectives
1. Contruct variables, manipulate strings, and loop through lists
2. Build and navigate dictionaries
3. Define and use functions
3. Export data to .csv files

This tutorial is designed to help the **ABSOLUTE** beginner, or anyone who is relatively new to Python and working towards confidently applying their Python skills to research projects.

## Getting started
### Setup Python

A simple way to quickly download and set up Python and several Python libraries on your computer is to install [Anaconda](https://www.anaconda.com/download) on your personal device. Anaconda is a distribution of the Python programming language that serves as a package management system, allowing you to install, run, and update packages and their dependencies effortlessly. Anaconda automatically installs over 250 packages which are essential for analysis and data visualization, including pandas, numpy, matplotlib, and more. Additionally, Anaconda enables you to manage packages without needing to use command-line prompts, making it user-friendly and convenient.

### Setup IDE

Integrated Development Environments (IDEs) bundle code editors, debuggers, compilers, terminals, plugins and more into one software application to streamline the coding process. [Spyder](https://docs.spyder-ide.org/current/index.html), an IDE designed by and for scientists, engineers, and data analysts is installed with the Anaconda package. [Visual Studio Code](https://youtu.be/1kKTYsQdaPw?si=JbZb6Byg8iRTSS0u) is another quality IDE that offers quick feedback as you iteratively create your code. Either IDE will allow you to interactively write code, explore your data, and more.

# Absolute vs relative paths
By default the directory (aka folder) from which you run your Python script is set as your current working directory (cwd). This is where Python looks for files to read and write. In VS Code, you can set your working directory using the Explorer icon in the top left of the Activity bar. Add or open a file for your project and Python will store your code and any data files created by your code in this space. In Spyder, you can set your working directory by clicking on the folder icon in the upper right of the Toolbar.

If you want to store the files you are working with in the same folder as your Python script, you can use a relative path to point Python to a file.

`relative_filepath_of_text = "path.txt`

This works because Python establishes the current working directory as the reference point for relative file paths. If you want to store files in a different folder from your Python script, use an absolute path.

`absolute_filepath_of_text = "C:/path/to/your/directory/file.txt"`

# Read or write files
To read a text file, you must open it first in Python. Python will open your file and return it as a file object.

**Syntax:**\
  `open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)`

- file is the path name, absolute or relative to the current working directory
- mode is an optional string that specifies the mode in which the file is opened. The default is 'r', or open for reading in text mode. The modes are:

| **Character** | **Meaning**                                                                                   |
|:-------------:|:---------------------------------------------------------------------------------------------------:|
| `'r'`         | open for reading (default)                                                                               |
| `'w'`         | open for writing, truncating the file first  
| `'x'`         | open for exclusive creation, failing if the file already exists 
| `'a'`         | open for writing, appending to the end of file if it exists     |
| `'b'`      | binary mode          |
| `'t'`          | text mode (default) |
| `'+'`         | open for updating (reading and writing |

- encoding is the name of the encoding used to decode or encode the file. This should only be used in text mode. 
  - utf-8 (most common)
  - utf-16
  - utf-32  

```{code-cell} python
carmen_ohio=open('Carmen_Ohio.txt', mode='r', encoding='utf-8')
print(carmen_ohio)
```

**.read()**\
The syntax `open('Carmen_Ohio.txt', mode='r', encoding='utf-8')` opens carmen_ohio as a file object. To read the file object as text, use the `.read()` method 

```{code-cell} python
carmen_ohio=open('carmen_ohio.txt', mode='r', encoding='utf-8').read()
print(carmen_ohio)
```

**.write()**\
If you do not specify a mode, Python will default to reading text files with mode='r'. To write text files, set the mode to `mode='w'`. **Note** We rename our file first to avoid overwriting the original text.

```{code-cell} python
open('carmen_ohio_revised.txt', mode='w', encoding='utf-8')
```

Again, this creates an object. To add text to a file, use the `.write()` method.

```{code-cell} python
:tags: ["remove-output"]

open('carmen_ohio_revised.txt', mode='w', encoding='utf-8').write("Let's firm thy friendship again!!!")
```

Now our file reads:
```{code-cell} python
open('carmen_ohio_revised.txt', mode='r', encoding='utf-8').read()
```
# Variables

Python data types include:

:::{table} 
:label: table
:align: center

|   Name   | Abbr | Type | Description | Example |
| :--- | :--- | :--- | :--- | :--- |
| Strings | str | sequence | text | "The Ohio State University" |
| Integers | int | numeric | whole numbers | 1870 |
| Floats | float | numeric |decimal numbers | 3.14 |
| Booleans | bool | boolean | True/False conditions | True |
| Lists | list | sequence | ordered collection of items | ["The Ohio State University" , 1870 ] |
| Dictionaries | dict | mapping | key-value pairs | {"institution_name" : "The Ohio State University","year_founded" : 1870 } |
| Tuples | tuple | sequence | ordered immutable collection of items | ("The Ohio State University", 1870) |

:::

Lists, dictionaries, and strings can be modified after they are created, making them mutable. In contrast, tuples are immutable and cannot be altered once defined.

**Variables** are assigned a value with the `=` sign.

```{code-cell} python
institution_name = "The Ohio State University"
year_founded = 1870
university_facts = {"institution_name": "The Ohio State University", "year_founded" : 1870, "school_colors" : "scarlet & grey", "mascot" : "Brutus Buckeye", "students" : 60046, "endowment": 7.9 }
fact_list = ["The Ohio State University", 1870, "scarlet & grey","Brutus Buckeye", 60046, 7.9 ]
```

Variable names can include upper and lower case letters, digits, and underscores. However, they must not start with a number, contain spaces, include punctuation other than an underscore, or use reserved Python keywords. 

**Reserved Python keywords**

`False, True, None, and, as, assert, async, await, def, del, elif, else, break, class, continue, except, finally, for, from, global, if, import, in, is, lambda, nonlocal, not, or, pass, raise, return, try, while, with, yield`

To check the type of a Python variable, use the type() function.

```{code-cell} python
type(university_facts)
```
**Math Operators**

Python supports basic arithmetic operations such as addition, subtraction, multiplication, and division. A list of basic math operators is below. For more details, refer to Python's documentation on **[math](https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex)** operators.

| **Opeartion**          | **Result**           |   
| :----------| :-------- |
| x + y     | sum of x and y     | 
| x - y       | difference of x and y       | 
| x * y       | product of x and y     | 
| x / y | quotient of x and y      | 
| x // y       | floored quotient of x and y      | 
| x % y    | remainder of x/y     | 
| -x      | x negated     | 
| +x      | x unchanged   |
| abs(x)  | absolute value or magnitude of x |
| int(x)  | x converted to integer |
| float(x) | x converted to floating point |
| pow(x,y) | x to the power y |
| x**y | x to the power y |

Here Python assigns the number 10 to the variable **x** and the number 15 to the variable **y**. The sum of **x+y** is assigned to the variable **z**.

```{code-cell} python
x=10
y=15
z=x+y
print(z)
```
```{admonition} Exercise 1: Find data type
:class: sidebar note
:icon: False
Find the data type for the variable institution name

```

:::{seealso} Solution
:class: dropdown

```{code-block} python
type(institution_name)

```

:::
# Working with strings
Strings represent characters or textual data in Python. Since a string can include any character, it can also contain numbers. Strings are placed between either single `' '` or double `" "` quotation marks.

`'this is a string'`\
`"this is also a string"`

The initial and the closing quote must match.

**Consider:**\
`"The Readers' Advisory Guide to Horror Fiction"`\
`'"Did you take the trash out?" she asked.'`

You can also escape any character in Python by placing a backslash `\` before it. This tells Python to ignore the character. 

`'The Readers\' Advisory Guide to Horror Fiction'`

We can assign a string to a variable ...

```{code-cell} python
banned_book = "Brave New World"
```

**Slicing strings**\
Python is a zero indexed language. What does this mean? The first position in any Python sequence is always indexed at zero `0`. To isolate the first letter of a string, the **syntax** is:

`string[0]`

```{code-cell} python
banned_book[0]
```

To return a range of characters, the syntax is:

`string[start index:end index]` 

The end index tells Python where to stop, but is not returned as part of the string. To slice the word `Brave` from the string ...

```{code-cell} python
banned_book[0:5]

```

If the start index is not included, Python will automatically start the range at the `0` index position.

```{code-cell} python
banned_book[:5]

```
Conversely, if an end index is not included, Python will return every character after the start position.

```{code-cell} python
banned_book[5:]

```

**Negative Indexing**\
If you need to extract the zip code from an address, you can use negative indexing in Python to retrieve characters from the end of the string.

```{code-cell} python
library = "Thompson Library, 1858 Neil Avenue Mall, Columbus, OH 43085"
zipcode = library[-5:]

zipcode

```

```{admonition} Exercise 2: Slice Carmen Ohio
:class: sidebar note
:icon: False
1. Find the first 250 characters in Carmen Ohio
2. Find the last 250 characters in Carmen Ohio
3. Find a second sentence in Carmen Ohio


```

:::{seealso} Solution
:class: dropdown

```{code-block} python
carmen_ohio=open('carmen_ohio.txt', mode='r', encoding='utf-8').read()

# first 250 characters
carmen_first_250=carmen_ohio[:250]
print(carmen_first_250)

# last 250 characters
carmen_last_250=carmen_ohio[250:]
print(carmen_last_250)

# second sentence
carmen_sentence=carmen_ohio[33:62]
print(carmen_sentence)

```

:::

**String Methods**
| **String Method** | **Explanation**                                                                                   |
|:-------------|:---------------------------------------------------------------------------------------------------|
| `string.lower()`         | makes the string lowercase                                                                                |
| `string.upper()`         | makes the string uppercase  
| `string.title()`         | makes the string titlecase 
| `string.strip()`         | removes lead and trailing white spaces     |
| `string.replace('old string', 'new string')`      | replaces `old string` with `new string`          |
| `string.split('delim')`          | returns a list of substrings separated by the specified delimiter |
| `string.join(list)`         | opposite of split(), combines the elements in the given list into a single string using the specified separator.                                                                        |
| `string.startswith('some string')`       | tests whether string begins with `some string` |                                                       |
| `string.endswith('some string')`       |  tests whether string ends with `some string`   |
| `string.isspace()`       |  tests whether string is a space |

**Note:** This list is not comprehensive. See [String Methods](https://docs.python.org/3/library/stdtypes.html#string-methods) in the Python documentation to learn more.

**Replace Characters**\
Let's try replacing the word `praise` in the first sentence of carmen_ohio with `wonders` using the `replace` method.

**Syntax**\
`string.replace('old string', 'new string')`

```{code-cell} python
first_sentence=carmen_ohio[:32]
revised_first_sentence=first_sentence.replace('praise','wonders')

print("original first sentence: "+ first_sentence)
print("revised first sentence: "+revised_first_sentence)

```
```{admonition} Exercise 3: Strings
:class: sidebar note
:icon: False
1. Isolate a sentence in carmen_ohio
2. Print the isolated sentence
3. Create a new sentence and try replacing a word
4. Print the new sentence in uppercase text

```
:::{seealso} Solution
:class: dropdown

```{code-block} python
carmen_ohio=open('carmen_ohio.txt', mode='r', encoding='utf-8').read()

# isolate a sentence
carmen_sentence=carmen_ohio[:333]

# print the isolated sentence
print(carmen_sentence)

# create a new sentence and try replacing a word
new_sentence=carmen_sentence.replace('gladdest','happiest')

# print the new sentence
print(new_sentence.upper())


```

:::

**Lowercase | Uppercase**\
The .lowercase( ) and .uppercase( ) string methods are useful for normalizing data.

| **String Method** | **Explanation**                                                                                   |
|:-------------|:---------------------------------------------------------------------------------------------------|
| `string.lower()`         | makes the string lowercase                                                                                |
| `string.upper()`         | makes the string uppercase  
| `string.title()`         | makes the string titlecase 

**Example:**

```{code-cell} python
name1 = "McMurty, Larry"
name2 = "Mcmurty, Larry"
name3 = "mcmurty, larry"

name1_rev = name1.upper()
name2_rev = name2.upper()
name3_rev = name3.upper()

print(name1_rev)
print(name2_rev)
print(name3_rev)

```

**Split Strings with a Delimiter**\
By default, Python splits strings using a space. Let's try splitting Carmen_Ohio using newline `\n` as a delimiter.

```{code-cell} python
newline_free_carmen=carmen_ohio.split('\n')
newline_free_carmen
```

Did you notice that this returned a list of lines for each row in Carmen_Ohio? The `.split()` method returns a list of strings separated by the delimiter of your choosing. If we use the `split()` method on Carmen_Ohio and leave the delimiter blank ...

```{code-cell} python
:tags: ["scroll-output"]
carmen_split=carmen_ohio.split()
carmen_split
```

# Conditionals and comparisons
Conditionals use the `if` statement to allow you to control the flow of your program, based on whether a condition is True or False. 

![Cute piglet](images/cute_piglet.jpg)

- If Wilbur is a pig print his name
- If Wilbur is handsome say "He's really cute!"
- If Charlotte is Wilbur's best friend say "yes" else say "no."

**Step 1: Assign variables**

```{code-cell} python
wilbur_species='pig'
wilbur_handsome='handsome'
wilbur_likes_charlotte=True
```

**Step 2: Create if statements**

```{code-cell} python
if wilbur_species == 'pig':
    print('Wilbur')
    
if wilbur_handsome=='handsome':
    print("He's really cute!") #remember to use double quotes because of the apostrophe
    
if wilbur_likes_charlotte==True:
    print('Charlotte is Wilbur\'s best friend') #or cancel out the apostrophe
else:
    print('no')
```

Conditionals use the statements `if, elif, and else` to tell Python to execute code only if certain conditions are met. The first line of an `if statement` always starts with a *comparison* followed by a colon. The second line tells Python what to do. It is always indented.

```{code-cell} python
if wilbur_likes_charlotte==True:
     print("Charlotte is Wilbur's best friend") 
```

The `elif` and `else` statements tell Python to do something else if the previous condition/comparison is not met. `elif` is short for *else if*. You can evaluate more than one condition with the `elif` statement. Python will first evaluate whether the `if` statement is True, then whether the next `elif` statement is True, then whether the following `elif statement` etc... 

```{code-cell} python
if wilbur_likes_charlotte==True:
    print('yes')
else:
    print("Charlotte is Wilbur's best friend") 
```

| **Comparison Operator** | **Explanation**                                                                                   |
|:-------------:|:---------------------------------------------------------------------------------------------------:|
| `x == y `         | `True` if x is equal to y                                                                                |
| `x != y `         | `True` if x is not equal to y                                               |
| `x > y`       |  `True` if x is greater than y                                                        |
| `x < y`       |   `True` if x is less than y  
| `x >= y`       |   `True` if x is greater than or equal to y |
| `x <= y`      | `True` if x is less than or equal to y`                                                                             |
                                                                      
```{admonition} Exercise 4: Conditionals |  Comparisons
:class: sidebar note
:icon: False

wilbur_age=1\
charlotte_age=4\
farmer_age=42

Is Wilbur older than Charlotte? Verify Wilbur's age with a conditional statement.

```

:::{seealso} Solution
:class: dropdown

```{code-block} python

wilbur_age=1
charlotte_age=4
farmer_age=42

print('IS WILBUR OLDER THAN CHARLOTTE?')

if wilbur_age > charlotte_age:
    print("Wilbur is older than Charlotte.")
else:
    print("Wilbur is younger than Charlotte.")

```

:::

**Logical Operators**

Use the logical operators `and`, `or`, and `not` to check if two or more conditions are true.

| **Logical Operator** | **Explanation**                                                                                   |
|:-------------:|:---------------------------------------------------------------------------------------------------:|
| `x and y `         | `True` if x and y are both True                                                                               |
| `x or y `         | `True` if either x or y is True                                               |
| `not y`       |  `True` if x is not True   

**Is this Wilbur?**

![guinea pig](images/guineapig.jpg)    

```{code-cell} python
y="guinea pig"

if not y:
    print('Wilbur')
else:
    print(y)
```

**The `in` keyword**

An alternative way to check if the word "guinea" is in variable y is to use the `in` keyword in your conditional statement. The `in` keyword checks to see whether a string is within another string using the `in` keyword.

```{code-cell} python
if 'guinea' not in y:
    print('Not a guinea pig')
```

# Lists and Loops

Lists are ordered sequences of items that are mutable, meaning they can be modified. They are enclosed in square brackets `[ ]`, with each item separated by a comma.

```{code-cell} python
characters = ['Han Solo', 'Luke Skywalker', 'C3PO', 'R2D2']
type(characters)
```

Lists can contain any Python data type:

```{code-cell} python
random_list = ['Halloween', 'monster', 2024, ['Snickers', 'M&Ms','Mars Bars'],{'dog': 'Stanley','age':7,'color':'black/tan'}]
#IS THIS A LIST?
type(random_list)
```

**Extracting List Items**

Use the same slicing syntax for both strings and lists in Python.

`list_name[start_index:stop_index:step]`

To extract the first item from characters:

```{code-cell} python
characters[0]
```

Keep in mind, Python uses zero-based indexing. To extract the last 3 items from characters:

```{code-cell} python
characters[-3:]
```

To extract characters from a string:

```{code-cell} python
han_solo='Han Solo'
han_only=han_solo[0:3]
print(han_only)
```

````{admonition} Exercise 5: Extract list items
:class: sidebar note
:icon: False

Is there another method to extract the last 3 items from the list characters?

```{code-block} python

characters = ['Han Solo', 'Luke Skywalker', 'C3PO', 'R2D2']

```
````

:::{seealso} Solution
:class: dropdown

```{code-block} python

characters = ['Han Solo', 'Luke Skywalker', 'C3PO', 'R2D2']
last3_characters_alternative = characters[1:]
print(last3_characters_alternative )

```

:::

````{admonition} Exercise 6: Step through list
:class: sidebar note
:icon: False

Extract every second item from the list numbers.

```{code-block} python
numbers = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
```
````

:::{seealso} Solution
:class: dropdown

```{code-block} python

numbers = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
even_numbers=numbers[1::2]
print(even_numbers)

```
:::

**List Methods**

| **List Method** | **Explanation**                                                                                   |
|-------------|---------------------------------------------------------------------------------------------------|
| `list.append(another_item)`          | adds new item to end of list                                                                                |
| `list.extend(another_list)`        | adds items from another_list to list                                                |
| `list.remove(item)`        | removes first instance of item                                                       |
| `list.sort(reverse=False)`       | sort the order of list                                                                                 |                                                     |
| `list.reverse()`       | reverses order of list                                                                                 |                                                     |

To add an item to a list:

```{code-cell} python
characters = ['Han Solo', 'Luke Skywalker', 'C3PO', 'R2D2']
characters.append('Rey')
print(characters)
```

To remove an item from a list:

```{code-cell} python
characters.remove('Rey')
print(characters)
```

To add items from one list to another list:

```{code-cell} python
characters_new = ['Rey','BB-8']
characters.extend(characters_new)
print(characters)
```

To sort a list alphabetically:

```{code-cell} python
characters.sort()
print(characters)
```

To sort a list in reverse alphabetical order:

```{code-cell} python
characters.sort(reverse=True)
print(characters)
```

**The `for` Loop**

Since lists contain multiple items, it is helpful to use a plural variable name for the list variable. This practice will help you keep track of your variables when iterating through a list.  

The `for` loop instructs Python to examine each item in a sequence (i.e. `list, tuple, dictionary, or string`) and execute a block of code for each item in the sequence. 

**Syntax**\
`for item in sequence:`\
`     #Code to execute for each item`

This statement tells Python to look at each character in the characters list and print the name of the character.

```{code-cell} python
for character in characters:
    print(character)
```

To tell Python to only only print the names of the last 3 characters:

```{code-cell} python
for character in characters[-3:]:
    print(character)
```

Use conditional statements to add a comment for each character:

```{code-cell} python
for character in characters:
    if character == 'BB-8' or character=='R2D2' or character == 'C3PO':
        print(f"{character} is a robot")
    elif character == 'Luke Skywalker':
        print('Luke is Leia\'s brother')
    elif character == 'Han Solo':
        print('Chewbacca is Han Solo\'s friend')
    elif character == 'Rey':
        print("Rey rocks")
```

Note that the statement `f"{character} is a robot"` in the first conditional statement in the for loop above. This is an **f-string**, or a formatted string literal. The f-string is created by prefixing a string with the letter f before the string quotes. This allows you to directly insert variables between curly brackets into a sting.


````{admonition} Exercise 7: Loops
:class: sidebar note
:icon: False

Print the name of each president of The Ohio State University.

```{code-block} python

presidents=["Edward Francis Baxter Orton Sr","Walter Quincy Scott","William Henry Scott","James Hulme Canfield","William Oxley Thompson",
            "George Washington Rightmire","William McPherson","Howard Landis Bevis","Novice Gail Fawcett","Harold Leroy Enarson",
            "Edward Harrington Jennings","E. Gordon Gee","John Richard Sisson","William English Kirwan","Edward Harrington Jennings",
            "Karen Ann Holbrook","Joseph A. Alutto","E. Gordon Gee","Joseph A. Alutto","Michael V. Drake","Kristina M. Johnson",
            "Peter J. Mohler",'Walter "Ted" Carter, Jr.']

```
````

:::{seealso} Solution
:class: dropdown

```{code-block} python

presidents=["Edward Francis Baxter Orton Sr","Walter Quincy Scott","William Henry Scott","James Hulme Canfield","William Oxley Thompson",
            "George Washington Rightmire","William McPherson","Howard Landis Bevis","Novice Gail Fawcett","Harold Leroy Enarson",
            "Edward Harrington Jennings","E. Gordon Gee","John Richard Sisson","William English Kirwan","Edward Harrington Jennings",
            "Karen Ann Holbrook","Joseph A. Alutto","E. Gordon Gee","Joseph A. Alutto","Michael V. Drake","Kristina M. Johnson",
            "Peter J. Mohler",'Walter "Ted" Carter, Jr.']


for president in presidents:
    print(president)

```

:::

**Index or enumerate list items**\
There are various strategies to determine the index position of an item in a list.

One approach is to use a `for` loop along with the built-in `index()` method.

```{code-cell} python
presidents=["Edward Francis Baxter Orton Sr","Walter Quincy Scott","William Henry Scott","James Hulme Canfield","William Oxley Thompson",
            "George Washington Rightmire","William McPherson","Howard Landis Bevis","Novice Gail Fawcett","Harold Leroy Enarson",
            "Edward Harrington Jennings","E. Gordon Gee","John Richard Sisson","William English Kirwan","Edward Harrington Jennings",
            "Karen Ann Holbrook","Joseph A. Alutto","E. Gordon Gee","Joseph A. Alutto","Michael V. Drake","Kristina M. Johnson",
            "Peter J. Mohler",'Walter "Ted" Carter, Jr.']

for president in presidents:
    president_index_position=presidents.index(president)
    president_index_position=president_index_position+1
    print(str(president_index_position)+' '+president)
```

Another approach is to use the built-in `enumerate` function. This example asks Python to return two variables from the presidents list, the `index` position and the `president`.

```{code-cell} python
for index, president in enumerate(presidents):
    print(index, president)
```

The same approach using an f-string to make the returned print statement more clear.

```{code-cell} python
for index, president in enumerate(presidents):
    print(f"{president} was the {index} president of The Ohio State University")
```

Keep in mind, Python uses zero-based indexing. To enhance this script, I can add 1 to each index position and use a conditional statement to append a superscript to each number.

```{code-cell} python
for index, president in enumerate(presidents):
    index=index+1
    if index==1 or index==21:
        superscript='st'
    elif index==2 or index==22:
        superscript='nd'
    elif index==3 or index==23:
        superscript='rd'
    elif index>=4 and index<=20:
        superscript='th'
    print(f"{president} was the {index}{superscript} president of The Ohio State University")
```

**Building lists**\
Create new lists from existing lists using the `for` loop and the `.append()` method. 

To find all states bordering the pacific ocean in the United States:

```{code-cell} python
#FIRST WE START BY ASSIGNING AN EMPTY LIST TO A VARIABLE
pacific_states=[ ]

# NEXT WE NEED A LIST OF ALL THE STATES
united_states=["Alabama","Alaska","Arizona","Arkansas","California","Colorado","Connecticut","Delaware","Florida",
               "Georgia","Hawaii","Idaho","Illinois","Indiana","Iowa","Kansas","Kentucky","Louisiana","Maine",
               "Maryland","Massachusetts","Michigan","Minnesota","Mississippi","Missouri","Montana","Nebraska",
               "Nevada","New Hampshire","New Jersey","New Mexico","New York","North Carolina","North Dakota",
               "Ohio","Oklahoma","Oregon","Pennsylvania","Rhode Island","South Carolina","South Dakota","Tennessee",
               "Texas","Utah","Vermont","Virginia","Washington","West Virginia","Wisconsin","Wyoming"]

#THEN WE USE A FOR LOOP WITH A CONDITIONAL STATEMENT TO FIND THE WESTERN STATES
for state in united_states:
    if state=="Alaska" or state=="California" or state=="Hawaii" or state=="Oregon" or state=="Washington":
        pacific_states.append(state)
        
print(pacific_states)
```

````{admonition} Exercise 8: Building lists
:class: sidebar note
:icon: False

Create a list containing all states bordering the [great lakes](https://www.worldatlas.com/articles/the-eight-us-states-located-in-the-great-lakes-region.html#:~:text=Map%20of%20the%20Great%20Lakes,Michigan%2C%20Minnesota%2C%20and%20Wisconsin.).

```{code-block} python

united_states=["Alabama","Alaska","Arizona","Arkansas","California","Colorado","Connecticut","Delaware","Florida",
               "Georgia","Hawaii","Idaho","Illinois","Indiana","Iowa","Kansas","Kentucky","Louisiana","Maine",
               "Maryland","Massachusetts","Michigan","Minnesota","Mississippi","Missouri","Montana","Nebraska",
               "Nevada","New Hampshire","New Jersey","New Mexico","New York","North Carolina","North Dakota",
               "Ohio","Oklahoma","Oregon","Pennsylvania","Rhode Island","South Carolina","South Dakota","Tennessee",
               "Texas","Utah","Vermont","Virginia","Washington","West Virginia","Wisconsin","Wyoming"]

```
````

:::{seealso} Solution
:class: dropdown

```{code-block} python

great_lakes_states=[]
united_states=["Alabama","Alaska","Arizona","Arkansas","California","Colorado","Connecticut","Delaware","Florida",
               "Georgia","Hawaii","Idaho","Illinois","Indiana","Iowa","Kansas","Kentucky","Louisiana","Maine",
               "Maryland","Massachusetts","Michigan","Minnesota","Mississippi","Missouri","Montana","Nebraska",
               "Nevada","New Hampshire","New Jersey","New Mexico","New York","North Carolina","North Dakota",
               "Ohio","Oklahoma","Oregon","Pennsylvania","Rhode Island","South Carolina","South Dakota","Tennessee",
               "Texas","Utah","Vermont","Virginia","Washington","West Virginia","Wisconsin","Wyoming"]

for state in united_states:
    if state == 'Illinois' or state == 'Indiana' or state == 'Michigan' or state == 'Minnesota' or state == 'New York' or state == 'Ohio' or state =='Pennsylvania' or state == 'Wisconsin':
        great_lakes_states.append(state)

print(great_lakes_states)

```

:::

**Number of items in a list**\
Knowing the number of items in a list is useful when extracting data from a website or querying a database. We can determine the number of items in a list using the len() function.

```{code-cell} python
len(united_states)
```

**Counter variables**\
While we can use the built-in enumerate() function or the index() method to find the index position of an item in a list, sometimes using a counter variable can be advantageous for tracking positions in a list.

```{code-cell} python
count=0
for state in united_states:
    count +=1
    print('Starting record '+str(count)+' '+state)
```

**List Comprehensions**\
List comprehensions combine a `for` loop and `conditional` statement in a single line of code. 

**Syntax**\
`[expression for item in iterable if condition]`

This means that instead of writing ...

```{code-cell} python
pacific_states=[]
for state in united_states:
    if state=="Alaska" or state=="California" or state=="Hawaii" or state=="Oregon" or state=="Washington":
        pacific_states.append(state)
```
... use a list comprehensions to write ...

```{code-cell} python
pacific_states = [state for state in united_states if state=="Alaska" or state=="California" or state=="Hawaii" or state=="Oregon" or state=="Washington"]
print(pacific_states)
```

# Dictionaries
Dictionaries consist of an unordered sequence of `"key":value` pairs separated by commas. Like lists, dictionaries are mutable, meaning they can be changed. Dictionaries are always encased in curly `{ }` brackets, with each key : value pair separated by a comma.

```{code-cell} python
university_facts = {"institution_name": "The Ohio State University", 
                    "year_founded" : 1870, 
                    "school_colors" : "scarlet & grey", 
                    "mascot" : "Brutus Buckeye", 
                    "students" : 60046, 
                    "endowment": 7.9 }

print(university_facts)
```

**Keys**\
To generate a list of all keys in a dictionary use the `.keys()` method. Dictionary keys must be unique and are immutable strings or numbers.

```{code-cell} python
university_facts.keys()
```

**Values**\
To generate a list of all values in a dictionary use the `.values()` method. Dictionary values are not required to be unique and any data type may be used.

```{code-cell} python
university_facts.values()
```

**Access dictionary values**\
Dictionary keys are used to access dictionary values

```{code-cell} python
first_president = {"name":"Edward Francis Baxter Orton Sr", 
              "tenure":"1873-1881"}

print(first_president["name"])
print(first_president["tenure"])
```

**Add key:value pairs**\
Dictionaries, like lists, are dynamic, meaning you can add new key:value pairs to a dictionary at any time. 

```{code-cell} python
first_president = {"name":"Edward Francis Baxter Orton Sr", 
              "tenure":"1873-1881",
              "rank":"first president"}
print(first_president)
```

You can begin with an empty dictionary and add key-value pairs as needed.

```{code-cell} python
state_facts={}
state_facts["state"]="Ohio"
state_facts["nicknames"]=["The Buckeye State","Birthplace of Aviation","The Heart of It All"]
state_facts["capital"]="Columbus"
state_facts["population"]=11785935

state_facts
```

**Modify dictionary values**\
Modify dictionary values using the dictionary name, followed by the key in square brackets, an equal sign and the new value you wish to assign to the key.

```{code-cell} python
state_facts["state"]="Michigan"
state_facts["nicknames"]=["The Great Lake State","The Wolverine State","Water (Winter) Wonderland"]
state_facts["capital"]="Lansing"
state_facts["population"]=10077331

state_facts
```

**Nesting Dictionaries**\
Dictionaries are often nested inside of dictionaries.

```{code-cell} python
states={
    "state1":{'name': 'Ohio',
              'nicknames': ['The Buckeye State','Birthplace of Aviation','The Heart of It All'],
              'capital': 'Columbus',
              'population': 11785935},
    "state2":{
        'name': 'Michigan',
        'nicknames': ['The Great Lake State','The Wolverine State','Water (Winter) Wonderland'],
        'capital': 'Lansing',
        'population': 10077331}
    }

states
```

To access the first state in the dictionary states, use the key "state1" ...

```{code-cell} python
states["state1"]
```

To access the "nicknames" for "state1" ...

```{code-cell} python
states["state1"]["nicknames"]
```

**Loop Through a Dictionary**\
There are multiple ways to iterate through a dictionary. You can loop through:
- Key:value pairs using the `.items()` method,
- Keys using the `.keys()` method, or
- Values using the `.values()` method.

```{code-cell} python
for key, value in states.items():
    print(f"\nKey: {key}")
    print(f"\nValue: {value}")
```

**Loop through a nested dictionary**\
To loop through a nested dictionary ...

```{code-cell} python
for key, value in states.items():
    for k, v in value.items():
        print(f"\nKey: {k}")
        print(f"\nValue: {v}")
```

```{code-cell} python
for state in states.keys():
    print(state)
```

```{code-cell} python
for state in states.values():
    for each_state in state.keys():
        print(each_state)
```

```{code-cell} python
for state in states.values():
    for each_state in state.values():
        print(each_state)
```

```{code-cell} python
for each_dictionary in states:
    print(each_dictionary)
```

```{code-cell} python
for each_dictionary in states:
    print(states[each_dictionary])
```

````{admonition} Exercise 9: Dictionaries
:class: sidebar note
:icon: False

Find the keys for crab species in the dictionary crabs.

```{code-block} python



#From  Alaska Fish and Game website

crabs={"Blue King":
       {"scientific name":"Paralithodes platypus",
        "size":"Up to 18 pounds for a mature male",
        "range":"major concentrations primarily in Bering Sea",
        "diet":["worms","clams","mussels","snails","brittle stars","sea stars","sea urchins","sand dollars","barnacles","crabs","other crustaceans","fish parts","sponges","algae"],
        "predators":["marine fishes","king crab","octopus"]},
       "Dungeness":
       {"scientific name":"Metacarcinus magister",
        "size":"A legal-sized Dungeness crab is 6 1/2 inches in carapace width (shoulder width) and weighs approximately 2 pounds.",
        "range":"Aleutian Islands to Magdalena Bay, Mexico",
        "diet":["worms","small clams", "shrimp","fish"],
        "predators":["humans","sea otter","octopus","Pacific halibut"]},
      "Golden King":
       {"scientific name":"Lithodes aequispinus",
        "size":"5-8 pounds.",
        "range":"Aleutian Islands, Pribilof and Shumagin Islands, Prince William Sound, lower Chatham Strait",
        "diet":["worms","clams","mussels","snails", "brittle stars","sea stars","sea urchins","sand dollars","barnacles","crabs","other crustaceans","fish parts","sponges","algae"],
        "predators":["Pacific cod","sculpins","octopus","halibut","yellowfin sole","other king crabs","sea otters","nemertean worms"]},
      "Red King":
       {"scientific name":"Paralithodes camtschaticus",
        "size":"Females up to 10.5 lbs; Males up to 24 lbs and leg span of five feet",
        "range":"British Columbia to Japan north to the Bering Sea with Bristol  Bay and Kodiak Archipelago being the centers of its abundance in Alaska",
        "diet":["worms","clams","mussels","algae","fish","sea stars","sand dollars","brittle stars"],
        "predators":["Pacific cod","walleye pollock","rock sole","flathead sole","rex sole","Dover sole","arrowtooth flounder","Elasmobranchs","halibut","sculpin","Greenland turbot","Pacific salmon","Pacific herring","otters","seals"]},
       "Tanner":
       {"scientific name":"Chionoecetes bairdi and C. opilio",
        "size":"Mature males typically weigh 1-2 pounds for opilio and 2-4 pounds for bairdi",
        "range":"North Pacific Ocean and Bering Sea",
        "diet":["fish","shrimp","crabs","worms","clams","brittle stars","snails","algae","sponges"],
        "predators":["seals","sea otters","octopi","other crabs","fish"]}
       }

```
````

:::{seealso} Solution
:class: dropdown

```{code-block} python

#From  Alaska Fish and Game website

crabs={"Blue King":
       {"scientific name":"Paralithodes platypus",
        "size":"Up to 18 pounds for a mature male",
        "range":"major concentrations primarily in Bering Sea",
        "diet":["worms","clams","mussels","snails","brittle stars","sea stars","sea urchins","sand dollars","barnacles","crabs","other crustaceans","fish parts","sponges","algae"],
        "predators":["marine fishes","king crab","octopus"]},
       "Dungeness":
       {"scientific name":"Metacarcinus magister",
        "size":"A legal-sized Dungeness crab is 6 1/2 inches in carapace width (shoulder width) and weighs approximately 2 pounds.",
        "range":"Aleutian Islands to Magdalena Bay, Mexico",
        "diet":["worms","small clams", "shrimp","fish"],
        "predators":["humans","sea otter","octopus","Pacific halibut"]},
      "Golden King":
       {"scientific name":"Lithodes aequispinus",
        "size":"5-8 pounds.",
        "range":"Aleutian Islands, Pribilof and Shumagin Islands, Prince William Sound, lower Chatham Strait",
        "diet":["worms","clams","mussels","snails", "brittle stars","sea stars","sea urchins","sand dollars","barnacles","crabs","other crustaceans","fish parts","sponges","algae"],
        "predators":["Pacific cod","sculpins","octopus","halibut","yellowfin sole","other king crabs","sea otters","nemertean worms"]},
      "Red King":
       {"scientific name":"Paralithodes camtschaticus",
        "size":"Females up to 10.5 lbs; Males up to 24 lbs and leg span of five feet",
        "range":"British Columbia to Japan north to the Bering Sea with Bristol  Bay and Kodiak Archipelago being the centers of its abundance in Alaska",
        "diet":["worms","clams","mussels","algae","fish","sea stars","sand dollars","brittle stars"],
        "predators":["Pacific cod","walleye pollock","rock sole","flathead sole","rex sole","Dover sole","arrowtooth flounder","Elasmobranchs","halibut","sculpin","Greenland turbot","Pacific salmon","Pacific herring","otters","seals"]},
       "Tanner":
       {"scientific name":"Chionoecetes bairdi and C. opilio",
        "size":"Mature males typically weigh 1-2 pounds for opilio and 2-4 pounds for bairdi",
        "range":"North Pacific Ocean and Bering Sea",
        "diet":["fish","shrimp","crabs","worms","clams","brittle stars","snails","algae","sponges"],
        "predators":["seals","sea otters","octopi","other crabs","fish"]}
       }

for crab in crabs.keys():
    print(crab)

```

:::
````{admonition} Exercise 10: Dictionaries
:class: sidebar note
:icon: False

Find the diets for each crab species in the dictionary crabs.

```{code-block} python



#From  Alaska Fish and Game website

crabs={"Blue King":
       {"scientific name":"Paralithodes platypus",
        "size":"Up to 18 pounds for a mature male",
        "range":"major concentrations primarily in Bering Sea",
        "diet":["worms","clams","mussels","snails","brittle stars","sea stars","sea urchins","sand dollars","barnacles","crabs","other crustaceans","fish parts","sponges","algae"],
        "predators":["marine fishes","king crab","octopus"]},
       "Dungeness":
       {"scientific name":"Metacarcinus magister",
        "size":"A legal-sized Dungeness crab is 6 1/2 inches in carapace width (shoulder width) and weighs approximately 2 pounds.",
        "range":"Aleutian Islands to Magdalena Bay, Mexico",
        "diet":["worms","small clams", "shrimp","fish"],
        "predators":["humans","sea otter","octopus","Pacific halibut"]},
      "Golden King":
       {"scientific name":"Lithodes aequispinus",
        "size":"5-8 pounds.",
        "range":"Aleutian Islands, Pribilof and Shumagin Islands, Prince William Sound, lower Chatham Strait",
        "diet":["worms","clams","mussels","snails", "brittle stars","sea stars","sea urchins","sand dollars","barnacles","crabs","other crustaceans","fish parts","sponges","algae"],
        "predators":["Pacific cod","sculpins","octopus","halibut","yellowfin sole","other king crabs","sea otters","nemertean worms"]},
      "Red King":
       {"scientific name":"Paralithodes camtschaticus",
        "size":"Females up to 10.5 lbs; Males up to 24 lbs and leg span of five feet",
        "range":"British Columbia to Japan north to the Bering Sea with Bristol  Bay and Kodiak Archipelago being the centers of its abundance in Alaska",
        "diet":["worms","clams","mussels","algae","fish","sea stars","sand dollars","brittle stars"],
        "predators":["Pacific cod","walleye pollock","rock sole","flathead sole","rex sole","Dover sole","arrowtooth flounder","Elasmobranchs","halibut","sculpin","Greenland turbot","Pacific salmon","Pacific herring","otters","seals"]},
       "Tanner":
       {"scientific name":"Chionoecetes bairdi and C. opilio",
        "size":"Mature males typically weigh 1-2 pounds for opilio and 2-4 pounds for bairdi",
        "range":"North Pacific Ocean and Bering Sea",
        "diet":["fish","shrimp","crabs","worms","clams","brittle stars","snails","algae","sponges"],
        "predators":["seals","sea otters","octopi","other crabs","fish"]}
       }

```
````

:::{seealso} Solution
:class: dropdown

```{code-block} python

#From  Alaska Fish and Game website

crabs={"Blue King":
       {"scientific name":"Paralithodes platypus",
        "size":"Up to 18 pounds for a mature male",
        "range":"major concentrations primarily in Bering Sea",
        "diet":["worms","clams","mussels","snails","brittle stars","sea stars","sea urchins","sand dollars","barnacles","crabs","other crustaceans","fish parts","sponges","algae"],
        "predators":["marine fishes","king crab","octopus"]},
       "Dungeness":
       {"scientific name":"Metacarcinus magister",
        "size":"A legal-sized Dungeness crab is 6 1/2 inches in carapace width (shoulder width) and weighs approximately 2 pounds.",
        "range":"Aleutian Islands to Magdalena Bay, Mexico",
        "diet":["worms","small clams", "shrimp","fish"],
        "predators":["humans","sea otter","octopus","Pacific halibut"]},
      "Golden King":
       {"scientific name":"Lithodes aequispinus",
        "size":"5-8 pounds.",
        "range":"Aleutian Islands, Pribilof and Shumagin Islands, Prince William Sound, lower Chatham Strait",
        "diet":["worms","clams","mussels","snails", "brittle stars","sea stars","sea urchins","sand dollars","barnacles","crabs","other crustaceans","fish parts","sponges","algae"],
        "predators":["Pacific cod","sculpins","octopus","halibut","yellowfin sole","other king crabs","sea otters","nemertean worms"]},
      "Red King":
       {"scientific name":"Paralithodes camtschaticus",
        "size":"Females up to 10.5 lbs; Males up to 24 lbs and leg span of five feet",
        "range":"British Columbia to Japan north to the Bering Sea with Bristol  Bay and Kodiak Archipelago being the centers of its abundance in Alaska",
        "diet":["worms","clams","mussels","algae","fish","sea stars","sand dollars","brittle stars"],
        "predators":["Pacific cod","walleye pollock","rock sole","flathead sole","rex sole","Dover sole","arrowtooth flounder","Elasmobranchs","halibut","sculpin","Greenland turbot","Pacific salmon","Pacific herring","otters","seals"]},
       "Tanner":
       {"scientific name":"Chionoecetes bairdi and C. opilio",
        "size":"Mature males typically weigh 1-2 pounds for opilio and 2-4 pounds for bairdi",
        "range":"North Pacific Ocean and Bering Sea",
        "diet":["fish","shrimp","crabs","worms","clams","brittle stars","snails","algae","sponges"],
        "predators":["seals","sea otters","octopi","other crabs","fish"]}
       }

crab_diet=[]
crab_diet_nested={}

for key, value in crabs.items():
    crab=key
    diet=value['diet']
    for food in diet:
        if food == "worms":
            eats_worms="yes"
        else:
            eats_worms="no"
            
    ##Create nested dictionary try 1
    new_crabs_dictionary={crab:
                          {"eats worms": eats_worms}
                            }
    ##Creates a list of dictionaries
    crab_diet.append(new_crabs_dictionary)
    
    ##Create nested dictionary try 2
    if crab not in crab_diet_nested.keys():
         crab_diet_nested[crab]={"eats worms":eats_worms}




    

print(f"crab diet list ")
print(crab_diet) 
print(f"crab diet nested = ")
print(crab_diet_nested)

```

:::

# Functions
Python provides a number of built-in functions to manipulate data and perform tasks, including:
- `print()`
- `type()`
- `enumerate()`

We can also create our own functions to instruct Python on how to handle specific tasks and then *call* these functions to execute them. Defining custom functions is particularly useful when you need Python to perform a specific task several times throughout a program, saving you from repeatedly typing the same code.

Python functions are essentially reusable blocks of code designed to perform specific tasks. Functions begin with the keyword `def`, indicating you are defining a function. This is followed by the function name, parentheses `( )` and a  colon`:`. The subsequent indented code block specifies what the function should do.

```{code-cell} python
def say_hello():
    print("Hello")
```

**Call a function**\
To *call* the function, type the name of the function followed by parentheses `( )`.

```{code-cell} python
say_hello()
```

**Arguments and Parameters**\
If the variable `name` is inserted into the parentheses, a value required by the function to execute its task can be passed into the function. The variable `name` represents a *parameter*. Parameters enable the dynamic definition of variables. 

```{code-cell} python
def say_hello(name):
    print(f"Hello, {name}")
```

When I call the function `say_hello`, the actual name - or value - I pass to the function parentheses is the *argument*.

```{code-cell} python
say_hello("Sarah")
```

The ***parameter*** defines a dynamic variable\
`def function_name(parameter):`

The ***argument*** is the actual value passed into the function\
`function_name(argument)`

If I define a function with a parameter, I must call the function with an argument.

```{code-cell} python
#function defined with a parameter
def say_hello(name):
    print(f"Hello, {name}")
```

```{code-cell} python
#function called with an argument
say_hello("Isla")
```

**Positional vs. keyword arguments**\
Python matches each argument with a parameter in the function definition. By default, arguments are matched to parameters based on the order of the arguments entered. This is known as ***positional arguments***.

```{code-cell} python
def describe_pet(animal_type, pet_name):
    print(f"\nI have a {animal_type}")
    print(f"\nMy {animal_type}'s name is {pet_name.title()}.")
```

```{code-cell} python
#FUNCTION CALLED WITH CORRECT POSITIONAL ARGUMENTS    
describe_pet('dog','stanley') 
```

```{code-cell} python
#FUNCTION CALLED WITH INCORRECT POSITIONAL ARGUMENTS    
describe_pet('stanley','dog') 
```

***Keyword arguments*** use a name_value pair to pass information to a function. This allows you to specifically assign your arguments to a specific parameter, eliminating the need to know the position of function parameters.

```{code-cell} python
def describe_pet(pet_name="name",animal_type='species'):
    print(f"I have a {animal_type}")
    print(f"My {animal_type}'s name is {pet_name.title()}.")


pet_description=describe_pet(pet_name='Charlotte', animal_type='spider')
```

**Return Values**\
So far we've used the `print()` function in our custom-defined functions, which naturally returns a value. Sometimes we ask Python to process data in a function and then `return` a value.

```{code-cell} python
def format_name(first_name, last_name):
    full_name=f"{first_name} {last_name}"
    return full_name.title()

name=format_name('sarah','murphy')
print(name)
```

````{admonition} Exercise 11: Functions
:class: sidebar note
:icon: False

Make a function that transforms a book title to lower case, then call your function.

```{code-block} python

#define your function first. Give it a name and assign a parameter.
    #your code block here
    return #your code here

```
````

:::{seealso} Solution
:class: dropdown

```{code-block} python

def lowercase(title):
    lowercase_title=title.lower()
    return lowercase_title


book="Loansome Dove"
lowercase(book)

```

:::

# Common Python Errors
Python errors are a way a life! You will make errors. Accept this. Keep calm. Use the error messages to troubleshoot your code.

**SyntaxError**\
`SyntaxError: EOL while scanning string literal`\
`SyntaxError: invalid syntax`

The SyntaxError usually indicates you forgot a `:` at the end of the first line of a for loop or and if statement. You also might have forgotten a closing `"`.

```{code-cell} python
:tags: ["raises-exception"]
print("It's a wonderful day!)
```

```{code-cell} python
:tags: ["raises-exception"]
trees=["maple","walnut","oak"]
for tree in trees
    print(tree)
```

**FileNotFound**\
`FileNotFoundError: [Errno 2] No such file or directory: 'sample_file.txt'`

You have an error in your directory path. Check for typos. Copy paste your path into Notepad and replace `\` with `/` if necessary.

```{code-cell} python
:tags: ["raises-exception"]
open('sample_file.txt').read()
```

**TypeError**\
`TypeError: can only concatenate str (not "int") to str`

This occurs when you ask Python to perform a task that is not appropriate for the data type you are working with. Remember you can check data type with the `type()` function.

```{code-cell} python
:tags: ["raises-exception"]
name="Sarah"
name+8
```

```{code-cell} python
type(name)
```

```{code-cell} python
name+str(8)
```

````{tip} 
When writing print functions, avoid a TypeError by using f-strings.



```{code-block} python
#THIS CODE RETURNS A TypeError
dog="Jack"
age=8

print(dog + " is " + age) 

#THIS F-STRING WORKS
print(f"{dog} is {age}") 
```
````

**NameError**\
`NameError: name 'Name' is not defined`

Occurs when then variable you call cannot be found. Look for spelling errors. Help yourself by making a conscious decision to only use lowercase letters for variable names before you start writing your Python program.

```{code-cell} python
:tags: ["raises-exception"]
Name
```

**AttributeError**\
`AttributeError: 'list' object has no attribute 'enumerate'`

If we forget `enumerate()` is a function and try to apply `enumerate()` as a method, an AttributeError will occur.

```{code-cell} python
:tags: ["raises-exception"]
##EXAMPLE WHERE ENUMERATE IS APPLIED AS A METHOD
trees=["maple","walnut","oak"]
for tree in trees.enumerate():
    print(tree)
```
```{code-cell} python
##EXAMPLE WHERE ENUMERATE IS CORRECTLY APPLIED AS A FUNCTION
trees=["maple","walnut","oak"]
for tree in enumerate(trees):
    print(tree)
```

# Export data to .csv
## ... with a function

```{code-cell} python
import csv

#####     STEP 1 - CREATE EMPTY DATASET AND DEFINE CSV HEADINGS     ##### 
dataSet=[]
columns=['institution_name','year_founded','school_colors','mascot','students','endowment'] # for CSV headings

#####     STEP 2 - DEFINE FUNCTION TO WRITE RESULTS TO CSV FILE     #####


def writeto_csv(data,filename,columns):
    with open(filename,'w+',newline='',encoding="UTF-8") as file:
        writer = csv.DictWriter(file,fieldnames=columns)
        writer.writeheader()
        writer = csv.writer(file)
        for element in data:
            writer.writerows([element])


institution_name= "The Ohio State University" 
year_founded = 1870
school_colors = "scarlet & grey"
mascot = "Brutus Buckeye"
students = 60046
endowment = 7.9

dataSet.append([institution_name,year_founded,school_colors,mascot,students,endowment])

writeto_csv(dataSet,'data/university_facts.csv',columns)
```

## ... with pandas

```{code-cell} python
import pandas as pd

results=pd.DataFrame(columns=['institution_name','year_founded','school_colors','mascot','students','endowment'])


institution_name= "The Ohio State University" 
year_founded = 1870
school_colors = "scarlet & grey"
mascot = "Brutus Buckeye"
students = 60046
endowment = 7.9

university_facts = {"institution_name": "The Ohio State University", 
                    "year_founded" : 1870, 
                    "school_colors" : "scarlet & grey", 
                    "mascot" : "Brutus Buckeye", 
                    "students" : 60046, 
                    "endowment": 7.9 }


add_row_to_results=pd.DataFrame(university_facts, index=[0])
results=pd.concat([add_row_to_results, results], axis=0, ignore_index=True)
results.to_csv('data/university_facts.csv', encoding='utf-8')
```







