# Decoding Pinball Wizardry: A Data-Driven Analysis
### Douglas Malcolm
### Contact Info: LinkdIn | Email

## Overview
What makes a pinball player great? 
This analysis looks to answer that quesion by uncovering patterns in pinball tournament player data.

In this project I... 
- Developed a **Python web scraper** to extract and collect pinball tournament player data
- Performed data cleaning and preprocessing using **pandas**
- Built **data visualizations** to help make sense of the data
- Employed **machine learning** sklearn library to construct linear regression models
- Interpreted statistical test results to derive **meaningful conclusions**

## Background
- [pinball takes skill] - keith elwin is proof
add a couple skill pointers
- Pinball is booming - link todayshow clip and stats
- I have played pinball competitively for 8 years, I love the game, etc
pic of me playing pinball
- Are there any patterns among players who become great?

## The Data
The International Flipper Pinball Association [(IFPA)](https://www.ifpapinball.com/) is *the* organization that oversees and tracks competitive pinball. It has a webpage for each of its players showing information like name, age, years active, tournament finishes, and rating. Since the IFPA lacks a robust API, I decided to develop my own web scraper in Python to extract all of the relevant player data.

Here is an example player profile:

[my profile pic]

The data to extract...

[table of data label bolded, followed by description of data points]

### Python Web Scraper

```Python
from bs4 import BeautifulSoup
import requests
import lxml

# Retrives html from IFPA website
html_text = requests.get('https://www.ifpapinball.com/player.php?p=' + str(i + 1)).text
soup = BeautifulSoup(html_text, 'lxml')

# Finds keywords I am looking for
total_events = str(soup.find(string="Total Events").findNext("td").text)

# Writes this text into csv file 
with open('Local File Path', 'a') as f:
    f.write(total_events + "\n")
```

This code **extracts and enables us to use the IFPA player data** by using BeatifulSoup, Requests, and lxml libraries to access and parse the website's html. After finding the data we want in the html, we record the data into a cvs file for ease of use. Looping this gave **111888** rows of data, a set of data for each competitive pinball player.

### Exploring the Data

To get a quick grasp of our data, we can look at the distributions and descriptive statistics for each variable we extracted.

[Histogram 1] [Descriptive Statistics 1]
[Histogram 2] [Descriptive Statistics 2]
[Histogram 3] [Descriptive Statistics 3]
[Histogram 4] [Descriptive Statistics 4]
...

## The Model













