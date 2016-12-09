---
title       : Time Series Analysis on HR Data
subtitle    : Assignment of Data Products Course on Coursera
author      : Steven Zhang
job         : Reproducible Pitch Presentation
logo        : logo.jpg
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Summary

This analysis aims to perform time series analysis on human resouce data. 

This data was made up by a data analyst, in order to use in a HTML5 Dashboard Building.
During the building, the data will follow the following 7 basic principles:
- Use a normal distribution with a gradual increase trend to make up data.
- Generally, each year will have 7% increasement.
- The standard deviation will be one-tenth the mean.
- The 6 departments are named A to F, and their member are 100 to 600.
- For a larger department, their figures will be lower. To be specific, with 100 more members, there will be 0.5% drop in all figures, which based on 100 members with 100% ratio.
- For each month, there will be a standerd fluctuation.
- The final figure should be influenced by a random ratio, which follow a N~(1,0.07) distribution.

---

## Data Description

A data frame with **648** observations on **4** dimensions and **6** measures

| Index | Name | Description | Type |
------- | ----- | ------ | ------ |
| [, 1] | year | Year (2008 - 2016) | Dimension |
| [, 2] | quarter | Quarter (Q1, Q2, Q3, Q4) | Dimension |
| [, 3]	| month | Month (1 - 12) | Dimension |
| [, 4]	| department | department 6 Department (A - F) | Dimension |
| [, 5]	| CapitaIncome | Total Amount of Capita Income | Measure |
| [, 6]	| Profitability | Total Amount of Profit | Measure |
| [, 7]	| NetProfit | Total Amount of Net Profit | Measure |
| [, 8]	| LaborCost | Total Amount of Labor Cost | Measure |
| [, 9]	| LaborCostProfitRatio | Average of Labor Cost | Measure |
| [,10]	| ReturnOnHumanCapital | Average Return on Human Capital | Measure |

---

## Core Code

Due to the size, here is the very core code of my Shiny App.

```
ts1 <- ts(finalColumn, frequency = 4, start = c(2008, 1))
plot(decompose(ts1), xlab = "Year+1") # This plot is the second tab in Shiny App
ts1Train <- window(ts1, start = 2008, end = 2012)
ts1Test <- window(ts1, start = 2012, end = 2017)
ets1 <- ets(ts1Train, model = "MMM")
fcast <- forecast(ets1)
plot(fcast) # This plot comes first in UI
lines(ts1Test, col = "red")
```

---

## Online Resources


