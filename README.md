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

I utilized the BeatifulSoup and Requests libraries to be able to access and parse the html from the IFPA website.

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```















here is more background
