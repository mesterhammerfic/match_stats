# Match Stats
A predictive analytics projects for Mixed Martial Arts

# Goal
To provide predictions on the stylistic outcome of an MMA match so that even casual fans can find events they 
will enjoy even if they have no prior knowledge of the fighters. Essentially, I am trying to predict how each
fighter will behave in a match.

## Objectives
1. Develop stats using round by round data from UFCStats.com
    * Develop metrics that accurately capture a fighters stylistics tendencies and capabilities
    * Create a way to categorize fighters based on their fighting styles
    * Create a way to measure how a fighter typically responds to certain fighting styles
2. Build a machine learning model that uses these stats to predict how many strikes and takedowns will be 
attempted in each match
3. Deploy this model as a web application that makes predictions on upcoming fights

### Context
The current pay-per-view price of a UFC event is $64.99, which can be a lot of money to spend on an event you 
might not even enjoy. Oftentimes fans are dissapointed by what they thought would be an exciting main event, 
like the matchup between Israel Adesanya and Yoel Romero which drew criticism for it's lack of action. If we
could have predicted that this fight would be boring, many fans might've saved $65. Our goal is to provide 
customers with a way of predicting the likelihood that these fights will be exciting so that they can find 
events they will enjoy.

### Current State
I've developed a more effective effective way to measure fighting performance by using Differentials per Minute.
An example of this would be Takedown Differential per 15 Minutes, which measure how many more takedowns a fighter 
lands than their opponent. This metric is far more effective at measuring a fighters skill level than popular
metrics like takedown accuracy. For example, Conor McGregor, one of the best strikers in MMA, has a takedown 
accuracy of 63%. Khabib Nurmagomedov, regarded as the best wrestler in MMA today, has a takedown accuracy of
only 45%. If taken as a measurement of grappling skill, this stat would not have allowed us to predict that 
throughout their fight, Khabib took Conor down constantly, eventually winning the fight. Using our takedown 
differential, Khabib scores in the top 1% of active UFC fighters, with a 5.14; Conor scores a -.53, which is
a little below the median of -.23.

### Data
The data I'm using is scraped from the official [UFC stats website](http://www.ufcstats.com/statistics/events/completed),
which provides round-by-round data on strikes and grappling techniques used in a fight for each fighter. I scraped data
for every bout up until August 1st. The scraping is cumbersome, and data preparation takes a singificant amount of time, 
so I provided the [data](data/ufcstats_data) in this repository through 5 separate csv files. The data includes 26,244 rounds across 
5,688 bouts from 525 UFC events. 5 tables are then transferred to a local postgresql database with the following schema:

<img src="schema.png"
align="center"
alt="Markdown Monster icon"
width="600"/>

Note: each row in general and strikes represents a single fighter in a single round. The unique identifer is made by combining
the bout_link, fighter_link, and round. General contains information regarding both striking and grappling stats, while
striking contains information only pertaining to significant strike counts. No stat columns are repeated between each table.
