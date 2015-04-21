---
title       : Pythagorean Winning Percentage
subtitle    : Predicting MLB Final Win-Loss Totals
author      : Saul Jackman
job         : Course Project for Developing Data Products
framework   : io2012        # {io2012, hsltml5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, shiny, interactive]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides

--- 

## Is Your Team Really Good or Really Lucky?

<a href = "https://thejkreview.files.wordpress.com/2012/04/moneyball-poster.jpg"><img style="float: left" src="moneyball.png" height = "500", width = "350"></a>

* Suppose you are a fan of a baseball team, and halfway through the season, your team has the best record in its division, meaning if the season ended today, your team would make the playoffs.
* You want to predict what your team's final win-loss record will be, and whether they will make the playoffs.
* The best way to predict your team's final record is not to assume they will have exactly the same record in the second half of the season as they did in the first half.
* Rather, you should look at how many runs your team has scored, and how many it has allowed.

--- .class #id 

## Calculating Pythagorean Winning Percentage

* Pythagorean winning percentage is a function of runs scored and runs allowed.
  * A team's pythagorean (expected) winning percentage is:
$$  E[\frac{\mbox{Wins}}{\mbox{Wins}+\mbox{Losses}}] = \frac{\mbox{Runs Scored}^{1.81}}{\mbox{Runs Scored}^{1.81}+\mbox{Runs Allowed}^{1.81}} $$
  * This is demonstrated via the following code:

```r
win_percentage <- function(RS,RA) {
  round((RS^1.81)/((RS^1.81)+(RA^1.81)),3)
}
```

--- .class #id 

## Calculating Pythagorean Win-Loss Records

* The winning percentage can then be multiplied by 162 (the number of games in a major league baseball season) to calculate the team's win total; subtract the win total from 162 to determine the expected number of losses:

```r
Record <- function(RS,RA) {
  win_percent <- (RS^1.81)/((RS^1.81)+(RA^1.81))
	wins <- round(win_percent*162,0)
	losses <- round(162-(win_percent*162),0)
	paste(wins, losses, sep = "-")
}
```

--- .class #id 

## Example:  2005 Washington Nationals

* On July 1, Nationals had a record of 47 wins and 31 losses, leading their division.
  * Projecting that out to a full season, they were on pace to finish with 98 wins and 64 losses.
* They had scored 322 runs, and allowed 324 runs.
  * Using the pythagorean theorem, they were predicted to finish with 81 wins and 81 losses:



```r
Record(322,324)
```

```
## [1] "81-81"
```

* Their final record that season was:  81 wins and 81 losses.


