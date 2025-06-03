---
title: Lesson 8. Scopus
# subtitle: Lesson 3. Wikipedia
license: CC-BY-4.0
github: https://github.com/Murphy465/data_visualization_myst
subject: Tutorial
authors:
  - name: Sarah Anne Murphy
    orcid: 0000-0002-7787-6890
    affiliations:
      - The Ohio State University Libraries
date: 2025-06-02
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

🚧 THIS PAGE IS UNDER CONSTRUCTION

Elsevier provides API access to its __[Scopus]( https://dev.elsevier.com/sc_apis.html)__ database to academic researchers. This allows researchers to programmatically retrieve metadata about publications, authors, institutions, and more.

This tutorial introduces __[pybliometrics](https://pybliometrics.readthedocs.io/en/stable/)__ an API wrapper designed to simplify retrieving data from Scopus's multiple __[API access points](https://dev.elsevier.com/sc_api_spec.html)__. An API wrapper is a python library or module that handles requests, authentication, parsing, and more. 

**Pybliometrics** will help you to ...

- Construct URLs for Scopus API calls
- Store and handle API keys and institutional tokens
- Parse JSON responses
- Handle rate limits and errors

## Data skills | concepts
- API keys
- API wrappers

## Learning objectives
1. Install and use an API wrapper to authenticate, request, parse, and store data.
2. Interpret documentation and apply concepts to write functional code.

# LESSON 8

## Getting started

To use the Scopus APIs, researchers must first request an API key via the __[Elsevier’s Developers Portal]( https://dev.elsevier.com/index.jsp)__ and agree to comply with Elsevier’s API usage policies.

When requesting an API key, be ready to provide a few details:

-	**Your use case** - What you’re planning to do with the data?
-	**The type of Scopus metadata** you want to access - like publications, author or institutional profiles, or citations.
-	**How much data** you expect to retrieve - for example, "around 3,500 records."
-	**What your final product will be** – such as a research paper, website, or something else.

It's a good idea to read through the  __[Getting Started guide for Scopus APIs]( https://dev.elsevier.com/sc_apis.html)__ before submitting your request. It will help you understand how the API works and what to expect. Also, be aware if you usually work off campus, you may need to request an institutional token and answer a few additional questions. Otherwise, you will need to use your API key while connected to your university's network.

Once you have your API key and institutional token, if needed, install the stable version of pybliometrics from __[PyPI](https://pypi.org/project/pybliometrics/)__:

```{code-block}
pip install pybliometrics
```
The first time you use pybliometrics, you will be prompted to input your API key and institutional token. These will be saved in `~/.config/pybliometrics.cfg`.

:::{code-cell}
import pybliometrics
:::

## ScopusSearch
__[ScopusSearch](https://pybliometrics.readthedocs.io/en/stable/reference/scopus/ScopusSearch.html)__ is one of the 11 API interfaces available to interact with Elsevier's Scopus database through the pybliometrics library. The ScopusSearch class in pybliometrics allows you to ...

- Query Scopus using all fields available in Scopus advanced search except “INDEXTERMS()” and “LIMIT-TO()”.
- Filter results
- Retrieve metadata

The search returns a list of named tuples that can be converted into a DataFrame with pandas for futher analysis or export to CSV. 

### Step 1. Construct query 

To get started with the the ScopusSearch class in pybliometrics, we will begin by searching for publications that were:
- Funded by the **National Science Foundation (NSF)** 
- Authored by researchers affiliated with **The Ohio State University**
- Published between **2000** and **2001**. 

:::{code-block}
#identify libraries needed for project
from pybliometrics.scopus import ScopusSearch
import pandas as pd
import time

#initializes the class
pybliometrics.scopus.init() 

#query
q='(FUND-SPONSOR ( "National Science Foundation") AND AFFIL ("Ohio State University")) AND PUBYEAR > 2020 AND PUBYEAR < 2022' 

#search (creates an object)
s=ScopusSearch(q, verbose=True) #setting verbose to True turns on a progress bar for search
:::

### Step 2. Retrieve and store results

`s.results` retrieves the list of named tuples. Each item in s.results is an object with attributes.

`article_title=s.results[0].title`
Looks at the first tuple in the list, finds the attribute **title** and assigns the attribute to the variable **article_title**.

`journal_title=s.results[5].publicationName`
Looks at the sixth tuple in the list, finds the attribute **publicationName** and assigns the attribute to the variable **journal_title**.

You can use loop through the list of tuples or use list indexing to pull specific attributes out of `s.results` or you can immediately create a DataFrame to filter, analyze, and store your search results.

:::{code-block}
results=pd.DataFrame(s.results)

#examine DataFrame shape
print(results.shape)

#examine column names
print(results.columns)

#export results to csv file
results.to_csv('results.csv', encoding='utf8')

:::




## AuthorSearch

Learning to read and interpret documentation is an **essential skill** for anyone working with data. Good documentation can

- **Uncover powerful or lesser-known features** that can enhance your project.
- **Introduce optional parameters** that help you fine-tune your queries -- for example, setting `enncoding=utf8`, specifying column headers, or filtering results.
- **Define error messages** and guide you through troubleshooting when things don't work as expected.
- **Save your time** by offering accurate, up-to-date information - often more reliable that what you'll findi n scattered or outdated online forums. 

:::{admonition} Exercise: AuthorSearch
:class: sidebar note
:icon: False

The AuthorSearch class in pybliometrics connects to the Scopus AuthorSearch API and allows you to retrieve detailed information about authors indexed in Scopus. To practice reading, interpreting, and applying concepts from the pybliometrics AuthorSearch documentation: 

1. Create a list of unique author_ids from the publication results you obtained in Step 2. 
2. Use the [pybliometrics.scopus.AuthorSearch](https://pybliometrics.readthedocs.io/en/stable/reference/scopus/AuthorSearch.html) documentation to write Python code that retrieves the following data for the first 10 unique author_id:
    - author_id
    - author_surname
    - author_givenname
    - author_initials
    - author_affiliation
    - author_city
    - author_country
3. Export results to .csv file. 

:::

:::{seealso} Solution
:class: dropdown

```{code-block}
from pybliometrics.scopus import AuthorSearch
unique_author_ids=[]
author_ids=results.author_ids.tolist()

for each_list in author_ids:
    individual_ids=each_list.split(';')
    for each_id in individual_ids:
        if each_id not in unique_author_ids:
            search_string='AU-ID('+str(each_id)+')' + ' OR '
            unique_author_ids.append(search_string)


#query first 10 unique author ids
unique_author_ids=unique_author_ids[0:10]

#construct query
query=''.join(unique_author_ids).rstrip(' OR').strip()

#search
s_author=AuthorSearch(query, verbose=True)

#insert results into DataFrame
results_authors=pd.DataFrame(s_author.authors)

#select columns
results_authors=results_authors[['surname','initials','givenname','affiliation','city','country']]
```

:::




