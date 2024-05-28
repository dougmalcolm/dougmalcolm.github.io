# Decoding Pinball Wizardry: A Data-Driven Analysis
#### Douglas Malcolm
#### Contact Info: LinkdIn | Email

## Overview
What makes a pinball player great? 
This analysis looks to answer that quesion by uncovering patterns in pinball tournament player data.

In this project I... 
- Developed a **Python web scraper** to extract player data from the [International Flipper Pinball Associaion](https://www.ifpapinball.com/).
- Performed data cleaning and preprocessing using the **pandas** library.
- Built **data visualization graphs** to help make sense of the data.
- Employed the **machine learning** sklearn library to construct and refine linear regression models.
- Conducted a thorough analysis to interpret the finalized model and derive **meaningful conclusions**. 

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

#### Python Web Scraper

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

This code...
1. Uses BeatifulSoup, Requests, and lxml libraries to access and parse the IFPA website's html
2. Finds the data we want in the html
3. Records the data in a cvs file
enabling us to use our player data.
















here is more background
