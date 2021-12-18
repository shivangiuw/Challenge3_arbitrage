# Time series data analysis for arbitrage opportunities using pandas

##Arbitrage is the almost-simultaneous purchase and sale of an asset to profit from a difference in the asset's price between markets.

*Finding arbitrage opportunities involves comparing the pricing data from two exchanges at the same time, in intervals that you define down to the minute, to find the dislocation.
*In this analysis, we examine the time-series pricing data of Bitcoin from  two exchanges (Bitstamp and Coinbase) from the first three months of 2018 (January 2018 to March 2018) to determine if any arbitrage opportunities exist for Bitcoin.

*Analysis report is at the end of the file.

---

## Technologies

This analysis leverages python 3.7 with the following packages:

* [pandas] (https://pandas.pydata.org/docs/getting_started/index.html)- for data analysis

* [jupyter lab] (https://jupyterlab.readthedocs.io/en/stable/)- for working with notebooks, code, data and plots

* [path] (https://docs.python.org/3/library/os.path.html) - for CSV file paths to read 

* [matlplotlib] (https://matplotlib.org/stable/users/installing/index.html)- for data visualization 

---

## Installation Guide

```
 conda install pandas
 pip install jupyterlab
 python -m pip install -U matplotlib
 ```
---

## Usage 

We perform the following phases of financial analysis:

1.`Collect the data` from CSV in a Jupyter notebook file.
(using read_csv and Path module)
2.`Prepare the datasets` for analysis by cleaning missing and erroneous data.
(using .isnull(), .duplicated(), dropna().str.replace() and .astype())
3.`Analyze the data` at a high level through summary statistics and visualizations, and use this information to select areas for deeper analysis. 
(using .loc for slicing the data for different periods to analyze, .plot() and .describe() to visualize and get summary statistics for the data under consideration.

---

## Analysis Report

During analysis we try to understand the trend in the exchanges to determine whether arbitrage opportunities still exist in the Bitcoin market, for which we follow the below steps:

1. Plot the dataframes for the full period to see the bitcoin prices(Closing prices) trend at both exchanges and overlay the plots to see the difference in bitcoin prices at the same time in both the exchanges thus arbitrage spread or opportunities 
`Observation:` We observe from the plots that there was disparity in bitcoin prices between the two exchanges many of the times in the beginning, however it lessened further in the timeframe which shows that the profitable arbitrage opportunities should also be lesser in the later time as compared to earlier.

2. For deeper analysis, divide the data in to three periods i.e. early (January), Middle (Februray) and late(March) and plotting the sliced dataframe of bitcoin closing prices in Bitstamp and Coinbase, for early and late in the periods and generating summary statistics.
`Observation:` Looking at the graphs for the month of January'18 and March'18 for the bitcoin closing prices at the two exchanges,it is clear that the degree of spread changed between the exchanges has changed as time progressed, and it has narrowed over time.
Also, the number of instances when the bitcoin has been trading at two different prices at two exchanges are lesser in later month as compared to earlier.

3. For focussed analysis, we choose three dates i.e. one that is early in the dataset(28th Jan.2018), one from the middle of the dataset(28th Feb.2018), and one from the later part of the time period(30th March 2018, to evaluate for arbitrage profitability. We plot the dataframes, sliced for the different periods to see the degree of arbitrage spread, calculate the `arbitrage spread` on these dates, generate the summary statistics and then create a box plot.

`Assumption:` We calculate arbitrage spread by subtracting closing price column of lower priced exchange from that of higher priced exchange, which was verified by assuming one exchange as higher priced and calculating the spread by subtracting prices at lower priced exchange from it and vice versa, and generating summary of spread data like count, mean,etc. The scenario which gives positive or higher mean of arbitrage spread is better option thus gives the right higher and lower priced exchange.

`Observation:` It is observed that for the first two dates in the the dataset i.e 28 Jan.,18 and 28 Feb.18, most of the times, the prices in bitstamp exchange were higher than coinbase exchange whereas on the later date i.e. 30 March,18, coinbase exchange had higher bitcoin prices than bitstamp. Although, the instances or number of opportunities for arbitrage on the three dates were almost similar, but the arbitrage has very much narrowed down from spread mean in January (247.55) to February (7.7558) and further in to March (1.4195) as evident from the arbitrage spread data summary for the three dates depicted below.

  `28th Jan.2018`           `28th Feb.2018`         `30th Mar.2018`
count    1436.000000    count    1430.000000     count    1440.000000
mean      247.552326    mean        7.755825     mean        1.419507
std        68.343472    std        11.296502     std         8.918465
min        55.030000    min       -35.000000     min       -30.000000
25%       210.022500    25%         0.145000     25%        -4.412500
50%       251.180000    50%         7.815000     50%         1.205000
75%       290.925000    75%        15.207500     75%         6.640000
max       439.010000    max        46.000000     max        56.920000

4. For each of the three dates, we calculate the `spread returns`. To do so, divide the instances that have a positive arbitrage spread (that is, a spread greater than zero) by the price of Bitcoin from the exchange we are buying on (that is, the lower-priced exchange). We further determine the number of times the trades with positive returns exceed the 1% minimum threshold that we need to cover our costs and generate the summary statistics of your spread returns that are greater than 1%

`Observation:` Looking at the summary data of spread returns for the three dates under consideration i.e. early, middle and late in the dataset, we can see that early in the dataset i.e. 28th January 2018, there were ample of opportunities for arbitrage i.e. 1436 (arbitrage spread) wherein 1378 trades were profitable (i.e.the trades with positive returns exceed the 1% minimum threshold to cover the costs). However the number of instances when the spread return would have been positive(greater than 0) or profitable  have narrowed down quitely in periods middle(28th Feb.2018) and late(30th March 2018) in the dataset, which is evident from the summary statistics which shows 0 profitable trades(spread returns>1%), though they had positive spread returns(spread returns>0) 1080 times and 797 times respectively in the mentioned periods.


5. For each of the three dates, calculate `the potential profit, in dollars`, per trade. To do so, multiply the spread returns that were greater than 1% by the cost of what was purchased. Generate summary and plot the results.

`Observation:` The potential profits per trade on the early date (28th Jan.2018) were in three figures with mean of 253.931996, max, value as 439.010000 and standard deviation of 62.057953, whereas there was no potential profit per trade in the middle and later dates as there were no profitable trades in these periods which exceeded the minimum threshold of 1% to cover the cost.The observation is confirmed by looking at the plots.

6. Calculate the `potential arbitrage profits` that you can make on each day. To do so, sum the elements in the profit_per_trade DataFrame.

`Observation:` The potential arbitrage profit for 28th Jan.2018 was $ 349918.2900000001, however it narrowed down down to $0.00 in 28th March 2018.

7. Using the `cumsum` function, plot the cumulative sum of each of the three DataFrames. Can you identify any patterns or trends in the profits across the three time periods?

`Observation:`The cumulative profits for the date 28th Jan.2018 started at $ 275.38 at the beginning of the day and soared to $ 349918.29 at the end of the day. There were no profits at the dates chosen in middle and late in the dataset.


From the above analysis, we can understand that although there were  good opportunities for arbitrage and potential profits covering the cost,they narrowed down to spreads which can not cover the cost or trades which are not profitable. From the plots and summary of the full period in the datasheet and the sliced dataframes for the different periods, we can see that even though there are almost equal instances in the early, middle and late in the period in the datset, when bitcoin trades at the different prices at the two exchanges, the  spread between the two has narrowed down so much with the time that there cannot be potential profitable arbitrage trades.

