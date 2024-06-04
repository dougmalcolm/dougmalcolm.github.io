# Data Analyst

#### Technical Skills: SQL, Excel, PowerBI, Tableu, Python(Pandas, NumPy, Sklearn)

## Education

B.S., Mathematics &ensp; &ensp; &ensp; &ensp; &ensp; &ensp; &ensp; &ensp; &ensp; &ensp; &ensp; &ensp; The University of Maryland, Baltimore County (*May, 2024*)

# Projects

## Decoding Pinball Wizardry: A Data-Driven Analysis

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

[table of data label bolded, followed by description of data points], include age started in here

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

Now let's build a model to determine which factors lead to pinball greatness, and to what degree. Here I will be using **Rating** as the outcome of interest that measures greatness. When pinball players perform poorly in tournaments relative to others their rating goes down, and when they perform well their rating goes up. Because of this, **rating maps on to skill level** very nicely, assuming a player has played in enough tournaments. 

### Building the Model

So, which factors have a statistically significant effect on rating?

Let's use the machine learning sklearn library to build the model:

```Python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

features = ['Age', 'Age Started', 'Years Active', 'Total Events']
target = 'Rating'
X = cleaned_data[features]
y = cleaned_data[target]

X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=101)
Model1 = LinearRegression()
Model1.fit(X_train, y_train)
```

### Results

After transforming data to ensure normality, removing insignificant explanatory variables, and checking for low multicollinearity through VIF scores, we arrive at the final model.

[table of                 coef    std err          t      P>|t|      [0.025      0.975]
const              1410.0744     66.100     21.332      **0.000**    1279.514    1540.635
**Age Started**          -6.9315      1.392     -4.981      **0.000**      -9.680      -4.183
**Cbrt Total Events**    54.4912      7.513      7.253      **0.000**      39.652      69.331
]

**Age Started** and **Total Events** are the only explanatory variables that have a statistically significant effect on rating.

[insert scatter plot of Age Started v Rating]
[insert scatter plot of cbrt(Total Events) v Rating]

### Calculator

In order to easily predict the rating of any pinball player, I have provided a calculator:

[custom calculator]

## Discussion

Practically, it makes sense that the age you start playing at and the number of tournaments you play in are big factors contributing to pinball skill. However, this is not the full picture.

### Limitations

Many players choose not to enter their age when making their IFPA profile. Additionally, many players have only played in one or two tournaments [**can get exact % of this from pandas**]. This means that the model only trained on **X players, or X%** of the total number of **N players**. That large chunk of bad data hurt to discard, as the model only improves with more data.

Furthermore, it's imperative to highlight that starting one's journey in pinball later in life and participating in a modest number of tournaments does not prohibit one from acheiving greatness in pinball. Look at [player name], who started at the age of [x], has only played in [y] tournaments, and yet has the [zth] best rating in the world!

Realistically, there are many other qualitative factors that have an enormous impact on one's pinball skill such as; love of the game, openness to failing and learning, degree of access to pinball machines, etc. Although starting young and playing alot have a real impact, there is no doubt that anyone who falls in love with pinball can improve and become great. Where there's a will, there's a path.








