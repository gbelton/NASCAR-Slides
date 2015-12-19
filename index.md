---
title       : NASCAR Predictors 
subtitle    : Predictor variables for NASCAR race outcomes
author      : Gerald A. Belton
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap, shiny, interactive]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

<style>
em {
  font-style: italic
}
</style>

<style>
strong {
  font-weight: bold;
}
</style>

## Background and Goal

- NASCAR is the second-highest rated sport on television in the United States (NFL is #1)
- Fantasy Racing on websites such as http://www.fox50.com/fox-50-fantasy-racin/ is also very popular
- Some of my co-workers have formed a private group on that site for internal competition, and I would love to beat them all next season (I was terrible last season).
- **Goal:** use machine learning techniques to predict the order of finish of NASCAR Sprint Cup races.


--- 

## Progress Towards Goal
- The prediction function still needs some work
- *createNASCARdatabase.R* and *updater.R* scrape two websites to collect data on races
- The Shiny app takes a driver and track as inputs, and calculates a number of predictor functions:
  - the driver's average finishing position across the entire database (career avg finish) along with a histogram of all of his finishes
  - his average finish in the most recent 5 races and most recent 10 races
  - the driver's average finish at the selected track
  - his average finish at tracks of the same NASCAR type (Short, Intermediate, Superspeedway, Road)
  - his average finish at tracks of the same AccuPredict type (Flat, Steep, Large, Restrictor Plate, Road)

---

## Sample Code


```r
load("NASCARdata.RDa")
keepvars <- c("Date", "Site", "Driver", "CarNumber", "Finish")
NASCAR.data <- NASCAR.data[keepvars]
#### Calculate driver's career average finish
careerAvg <- function(driver) {
     temp <- NASCAR.data[ which(NASCAR.data$Driver==driver), 5]
     CA <- mean(temp)
     return(CA)
}
paste0("Dale Earnhardt Jr.'s career average finish is ", careerAvg("Dale Earnhardt Jr."))
```

```
## [1] "Dale Earnhardt Jr.'s career average finish is 15.4771573604061"
```

---

## Future Development

- The Shiny App demonstrates the current predictor variables which are calculated from the database. Using these variables, we are getting R^2 values around 38%.
- We plan to experiment with some additional variables to see if they improve R^2.
  - Most recent race finish
  - Current season finish
  - Starting position
- We also plan to apply the prediction function to each race of the 2015 season and determine how many points we would have earned in the Fantasy Racin' game.
- The most important question: would that be enough points to beat my co-workers scores?


