# Data Analyst Profile

Douglas Malcolm
 
Email: dougmalcolm87@gmail.com

LinkedIn: ()
 
### Education

B.S., Mathematics &nbsp; | &nbsp; The University of Maryland, Baltimore County (*May, 2024*)

### Technical Skills

SQL, Excel, PowerBI, Tableu, Python(Pandas, NumPy, Sklearn)

---

# Projects

## Decoding Pinball Wizardry: A Data-Driven Analysis

<img align="right" src="/assets/edited_wizard.jpeg" width="250" height="333">

### Overview

_Tools Used: **Python, Excel, PowerBI**_

What makes a pinball player *great*? 

This analysis looks to answer that quesion by uncovering patterns in pinball tournament player data.

In this project I... 
- Developed a **Python web scraper** to extract and collect pinball tournament player data
- Performed data cleaning and preprocessing using **pandas**
- Built **data visualizations** to help make sense of the data
- Employed **machine learning** sklearn library to construct linear regression models
- Interpreted statistical test results to derive **meaningful conclusions**

### Background

Pinball is a mix of skill and luck. Being able to accurately hit the shots you want, regain ball control after wild trajectories, and nudging the machine to affect the ball path are a couple examples of skills that can extend an otherwise short game. At the same time though, one player may immediately drain after missing a shot whereas another player may miss ten shots before the game decides their ball is done. Playing sufficiently many games is where the skill differences shine through though - the bad and good luck balances out and the better player tends to come out on top. This is why players like Jason Zahler and Escher Lefkoff are able to consistently get 1st place at huge 100+ player tournaments; There are enough tournament rounds for their superior pinball skills to shine through the luck. 

If you are curious about how to play pinball skillfully and what that actually looks like, [this youtube playlist from Abe Flips](https://www.youtube.com/watch?v=ch7H19SHkXE&list=PL31W94V2HVSW7ksDyZ_183rUBxiSQon75) is by far the best resource for learning. 

Personally, I have been playing in tournaments for 7 years now, and I absoultely love both pinball and thrill of competition. So naturally I was curious... what makes a pinball player great? 

### The Data
The International Flipper Pinball Association [(IFPA)](https://www.ifpapinball.com/) is *the* organization that oversees and tracks competitive pinball. It has a webpage for each of its players showing information like name, age, years active, tournament finishes, and rating. Since the IFPA lacks a robust API, I decided to develop my own web scraper in Python to extract all of the relevant player data.

Here is an example player profile:

<img src="/assets/sample_profile.png">

For each tournament player in the IFPA, the following data is collected...

Data to Collect | Description
--- | ---
Name | Player Name
Age | Player Age
Age Started | Age at time of first tournament; found by (Age - Years Active)
Years Active | Number of years playing in tournaments					
Total Events | Total number of tournaments					
Rating | Measure of pinball skill; Glicko Rating System					
Ranking | Measure of pinball skill and dedication; Compares best 15 tournament results

Both Rating and Ranking are measures of pinball skill. Rating will increase from strong tournament finishes and will decrease from weak tournament finishes. Ranking sums your top 15 best tournament results and compares them against everyone else's top 15 best tournament results. As a result, Ranking does not decrease from weak tournament finishes. This ends up inflating the Ranking of players who play in many many tournaments compared to those who player in fewer tournaments. Consequently, I personally subjectively believe that **Rating** is a better measure of pinball skill rather than ranking. Therefore moving forward, we will use Rating as the dependent variable of interest. 

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

This sample code **extracts and enables us to use the IFPA player data** by using BeatifulSoup, Requests, and lxml libraries to access and parse the website's html. After finding the data we want in the html, we record the data into a cvs file for ease of use. Looping this gave **111,888** rows of data, specifically collecting name, age, years active, total events, rating, and ranking for each competitive pinball player.

#### Exploring the Data

To get a quick grasp of our data, we can look at the distributions and descriptive statistics for each variable we extracted.

Rating is not very accurate with only a couple of tournament performance data points. So when looking at rating analysis going forward, we will filter for only those with 5+ Total Events played. This will consequently capture more serious players and bump up the average rating from 1047 to 1174.

<img src="/assets/distributions_new.PNG">

| Variable | Sample Size | Mean | Median | Std. Deviation | Minimum | Maximum |
| --- | --- | --- | --- | --- | --- | --- |
Age | 10,506 | 42.1 | 43 | 11.9 | 6 | 85 |
Age Started | 10,510 | 37.9 | 38 | 11.6 | 5 | 83 |
Years Active | 116,468 | 1.3 | 0 | 2.8 | 0 | 42
Total Events | 116,308 | 12.5 | 2 | 39.6 | 1 | 1113
Rating | 32,538 | 1174 | 1162 | 192 | 437 | 2149
Ranking | 49,112 | 23879 | 23325 | 14326 | 1 | 51013

Takeaways:

- A whopping **95.36%** of all IFPA players have only played in 1 tournament.
- The average pinball tournament player is **42.1** years old, and has played for **1.3** years in **12.5** tournaments.
- 95% of pinball players with 5+ total events have ratings between 790 and 1558, with an average of **1174** representing 'average skill level'.


### The Model

Now let's build a model to determine which factors lead to pinball greatness, and to what degree. 

#### Building the Model

So, which factors have a statistically significant effect on rating? We will filter for only players with 10 or more total tournaments to ensure a large enough sample size for rating to be more accurate.

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

#### Results

After ensuring independent residuals that are normal and homoscedastic about 0, removing insignificant explanatory variables, and checking for low multicollinearity through VIF scores, we arrive at the final model.

<img src="/assets/regression.PNG">

**Age Started**, **Years Active**, and **Total Events** are the only explanatory variables that have a statistically significant effect on rating.

We can also look directly at how each of these variables are correlated with rating:

<img src="/assets/events.PNG">

<img src="/assets/years.PNG">

<img src="/assets/started.PNG">

#### Calculator



### Discussion

Practically, it makes sense that the age you start playing at and the number of tournaments you play in are big factors contributing to pinball skill. However, this is not the full picture.

#### Limitations

Many players choose not to enter their age when making their IFPA profile. Additionally, many players have only played in one or two tournaments [**can get exact % of this from pandas**]. This means that the model only trained on **X players, or X%** of the total number of **N players**. That large chunk of bad data hurt to discard, as the model only improves with more data.

Furthermore, it's imperative to highlight that starting one's journey in pinball later in life and participating in a modest number of tournaments does not prohibit one from acheiving greatness in pinball. Look at [player name], who started at the age of [x], has only played in [y] tournaments, and yet has the [zth] best rating in the world!

Realistically, there are many other qualitative factors that have an enormous impact on one's pinball skill such as; love of the game, openness to failing and learning, degree of access to pinball machines, etc. Although starting young and playing alot have a real impact, there is no doubt that anyone who falls in love with pinball can improve and become great. Where there's a will, there's a path.








