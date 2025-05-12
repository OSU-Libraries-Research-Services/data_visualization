---
title: Lesson 3. Wikipedia
# subtitle: Lesson 3. Wikipedia
license: CC-BY-4.0
github: https://github.com/Murphy465/data_visualization_myst
subject: Tutorial
authors:
  - name: Sarah Anne Murphy
    orcid: 0000-0002-7787-6890
    affiliations:
      - The Ohio State University Libraries
date: 2025-05-05
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
This lesson introduces `pandas.read_html`, a useful tool for extracting tables from HTML, and continues to explore BeautifulSoup, a Python library designed for parsing XML and HTML documents. We will start by gathering artists found on the __[List of Rock and Roll Hall of Fame inductees](https://en.wikipedia.org/wiki/List_of_Rock_and_Roll_Hall_of_Fame_inductees)__ webpage in Wikipedia. We will then assemble discographies for 2-3 of our favorite artists.

## Data skills | concepts
- Search parameters
- HTML
- Web scraping
- Pandas 

## Learning objectives
1. Extract and store tables and other HTML elements in a structured format
2. Apply best practices for managing data

This tutorial assumes you already have a basic understanding of Python, including how to iterate through lists and dictionaries to extract data using a for loop. To learn basic Python concepts visit the Python - Mastering the Basics tutorial.

# LESSON 3

Lessons 1 and 2 introduced the basic steps for any webscraping or API project:

1. Review and understand copyright and terms of use.
2. Check to see if an API is available.
3. Examine the URL
4. Inspect the elements
5. Identify Python libraries for project
6. Write and test code

:::{admonition} Exercise 1: Examine Copyright | Terms of Use
:class: sidebar note
:icon: False

Locate and read the terms of use for the  __[Rock and Roll Hall of Fame](https://en.wikipedia.org/wiki/List_of_Rock_and_Roll_Hall_of_Fame_inductees)__ inductees found on Wikipedia.

1. What are the copyright restrictions for this resource? 
2. What are the terms of use?
:::

:::{seealso} Solution
:class: dropdown

Read Wikipedia __[Creative Commons Attribution-ShareAlike 4.0 License](https://en.wikipedia.org/wiki/Wikipedia:Text_of_the_Creative_Commons_Attribution-ShareAlike_4.0_International_License)__

:::

:::{admonition} Exercise 2: API available?
:class: sidebar note
:icon: False

Is an API available?
:::

:::{seealso} Solution
:class: dropdown

Yes, but it may take some time to learn how to use.  It is not necessary to use for this lesson.

:::

:::{admonition} Exercise 3: Examine the URL
:class: sidebar note
:icon: False
:label: examine-the-url

Select 2-3 inductees from the Performers category and locate their album discography on Wikipedia. Examine the structure of the URL for each album discography page.

:::

:::{seealso} Solution
:class: dropdown


**Example:**\
 Parliament-Funkadelic\
https://en.wikipedia.org/wiki/Parliament_discography\
https:// + en.wikipedia.org/ + wiki/ + Parliament_discography

https://en.wikipedia.org/wiki/Funkadelic_discography\
https:// + en.wikipedia.org/ + wiki/ + Funkadelic_discography
:::

:::{admonition} Exercise 4: Inspect the elements
:class: sidebar note
:icon: False

Go to the discography page for each artist you selected. Are there differences in how the tables are structured and presented on each page? For example, do tables have a title or header? Inpsect the elements and think about how you might use BeautifulSoup to gather the headers for each table.

:::

:::{seealso} Solution
:class: dropdown

```{code-cell} python
import requests
from bs4 import BeautifulSoup

import requests
from bs4 import BeautifulSoup

url='https://en.wikipedia.org/wiki/Parliament_discography'
response=requests.get(url).text
soup=BeautifulSoup(response, 'html.parser')
headers=soup.find_all('div', {'class':'mw-heading2'})
for header in headers:
    print(header.find('h2').text)
```
:::

:::{admonition} Exercise 5: Identify Python libraries
:class: sidebar note
:icon: False

List the Python libraries you may need to import for this project.

:::

:::{seealso} Solution
:class: dropdown

```{code-block}
import requests
import pandas as pd
from bs4 import BeautifulSoup

```
:::

# Pandas
## .read_html() 

iReads HTML tables directly into DataFrames with __[.read_html()](https://pandas.pydata.org/docs/reference/api/pandas.read_html.html)__ . This extremely useful tool extracts all tables present in specified URL or file, allowing each table to be accessed using standard list indexing and slicing syntax.

The following code instructs Python to go to the Wikipedia __[List of states and territories of the United States](https://en.wikipedia.org/wiki/List_of_states_and_territories_of_the_United_States)__ and retrieve the second table.

:::{code-cell} python
import pandas as pd

tables=pd.read_html('https://en.wikipedia.org/wiki/List_of_states_and_territories_of_the_United_States')
tables[1]
:::



:::{admonition} Exercise 6: .read_html()
:class: sidebar note
:icon: False

Visit the Wikipedia __[List of Rock and Roll Hall of Fame inductees]('https://en.wikipedia.org/wiki/List_of_Rock_and_Roll_Hall_of_Fame_inductees)__ and extract the Performers table.

:::

::::{seealso} Solution
:class: dropdown

```{code-block} python
import pandas as pd

tables=pd.read_html('https://en.wikipedia.org/wiki/List_of_Rock_and_Roll_Hall_of_Fame_inductees')
performers=tables[0]
performers
```
::::
# BeautifulSoup
## .find_previous() and .find_all_previous()

Similar to .find_next() and .find_all_next, __[.find_previous](https://beautiful-soup-4.readthedocs.io/en/latest/#find-all-previous-and-find-previous)__ and __[.find_all_previous()](https://beautiful-soup-4.readthedocs.io/en/latest/#find-all-previous-and-find-previous)__ gathers the previous instance of a named tag.

:::{admonition} Exercise 7: Gather discographies
:class: sidebar note
:icon: False

Gather the discography tables from the discography Wikipedia pages for the 2-3 artists you identified in {ref}`examine-the-url`.

1. Identify base url
2. Store the secondary_url parts for each artist in a list, such as ...
```{code-block} python
artists=['Cyndi_Lauper_discography','Joe_Cocker_discography','The_White_Stripes_discography']
```
3. Create a for loop to iterate through each artist in your list. 
4. Use .read_html to gather the discography tables each artist on your list. 

```{tip}
Use index slicing to focus on one artist page first as you work through steps 4 and 5.
```
4. Create an empty list for headers to gather table headers for each artist.
5. Use requests with BeautifulSoup and .find_previous() to gather the headers for each table and append each header to your headers list. Check to see if your table headers match the html tables you gathered with .read_html

```{tip}
Headers do not always exist for each table. You may need to use a try-except block and/or if statements to accurately construct your header list.
```

:::

::::{seealso} Solution
:class: dropdown

```{code-block} python
import requests
from bs4 import BeautifulSoup
import pandas as pd

artists=['Cyndi_Lauper_discography','Joe_Cocker_discography','The_White_Stripes_discography']
base_url='https://en.wikipedia.org/wiki/'


for artist in artists[0:1]:

    url=base_url+artist
    response=requests.get(url).text
    soup=BeautifulSoup(response, 'html.parser')
    
    #FIND TABLES
    html_tables=pd.read_html(url)

    #FIND TABLE_HEADERS
    response = requests.get(url)
    response.encoding = 'utf-8'
    soup = BeautifulSoup(response.content, 'html.parser')
    
    tables=soup.find_all('table')
    # tables=soup.find_all('table', {'class':'wikitable'})
    table_number=0
    
    
    headers=[]
    
    for table in tables:

        if table.find_previous('div',{'class':'mw-heading2'}) is not None:
            h2=table.find_previous('div',{'class':'mw-heading2'}).text.split('[')[0]
        else:
            h2='None'
        if table.find_previous('div',{'class':'mw-heading3'}) is not None:
            h3=table.find_previous('div',{'class':'mw-heading3'}).text.split('[')[0]
            # print(f"table_number_{table_number}: {h3}")
        else:
            h3='None'
        print(f"table_number_{table_number}: {h2}, {h3}")
        table_number += 1   
```
::::

# Managing files
There are several best practices and considerations for effectively __[managing research data](https://guides.osu.edu/rdm-best-practice/organization)__ files. When extracting and locally storing data in individual files, using standardized file naming conventions not only helps you organize and utilize your files efficiently but also facilitates sharing and collaboration with others in future projects. 

- Use short, descriptive names.
- Use (`_`) underscores or (`-`) dashes instead of spaces in your file names. Use leading zeros for sequential numbers to ensure proper sorting. 

`file_001_20250506.txt`\
`file_002_20250506.txt`

- Use all lowercase for directory and filenames if possible. 
- Avoid special characters, including `~!@#$%^&*()[]{}?:;<>|\/`
- Use standardized dates YYYYMMDD to track versions and updates.
- Include version control numbers to keep track of projects.

## os module
The os module tells Python where to find and save files.

### os.mkdir('path')
Creates a new directory in your project folder or another specified location. Makes a directory in your project folder or another folder you specify. If a directory by the same name already exists in the path specified, os.mkdir will raise an `OSError`. Use a try-except block to handle the error.

:::{code-block}
import os

try:
    os.mkdir(artist)
except FileExistsError:
    print(f"Directory '{artist}' already exists.")
except Exception as e:
    print(f"An error occurred: {e}")
:::

:::{admonition} Exercise 8: 
:class: sidebar note
:icon: False

1. Make a directory for each artist in your project folder.
2. Use pd.read_csv to create a file for each table. Incorporate the table number and header in the filename.
```{tip}
Increment counter variables for table numbers
```

:::

::::{seealso} Solution
:class: dropdown

```{code-block}
import requests
from bs4 import BeautifulSoup
import pandas as pd
import os

artists=['Cyndi_Lauper_discography','Joe_Cocker_discography','The_White_Stripes_discography']
base_url='https://en.wikipedia.org/wiki/'


for artist in artists:

    url=base_url+artist
    response=requests.get(url).text
    soup=BeautifulSoup(response, 'html.parser')
    
    #FIND TABLES
    html_tables=pd.read_html(url)

    #FIND TABLE_HEADERS
    response = requests.get(url)
    response.encoding = 'utf-8'
    soup = BeautifulSoup(response.content, 'html.parser')
    
    tables=soup.find_all('table')
    # tables=soup.find_all('table', {'class':'wikitable'})
    table_number=0
    
    
    headers=[]
    
    for table in tables:

        if table.find_previous('div',{'class':'mw-heading2'}) is not None:
            h2=table.find_previous('div',{'class':'mw-heading2'}).text.split('[')[0]
        else:
            h2='None'
            
        
        headers.append([h2.lower().replace(' ','_'),table_number])
        print(f"table_number_{table_number}: {h2}")
        table_number += 1   
        
    position=0
    for each_header in headers:
        if each_header[1] != None:
            table_name=each_header[0]
            number=each_header[1]
            artist_directory=artist.replace('_discography','').lower()
            try:
                os.mkdir(artist_directory)
            except FileExistsError:
                print(f"Directory '{artist_directory}' already exists.")
            except Exception as e:
                print(f"An error occurred: {e}")
            filename=artist_directory+'/table_number_'+str(number)+'_'+table_name+'.csv'
            print(filename)
            html_table=html_tables[position]
            html_table.to_csv(filename)
        elif each_header[0] != None:
            table_name=each_header[0].lower().replace(' ','_')
            number=each_header[2]
            print(number)
            print(table_name)
            artist_directory=artist.replace('_discography','').lower()
            try:
                os.mkdir(artist_directory)
            except FileExistsError:
                print(f"Directory '{artist_directory}' already exists.")
            except Exception as e:
                print(f"An error occurred: {e}")
            filename=artist_directory+'/table_number_'+str(number)+'_'+table_name+'.csv'
            print(filename)
            html_table=html_tables[position]
            html_table.to_csv(filename)
        position += 1
```

::::





















