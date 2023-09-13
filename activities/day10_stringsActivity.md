---
title: "Strings and Regular Expressions"
author: "ECON 122"
date: "Day 10"
output: 
  html_document:
    keep_md: true
---






## Regular Expression Examples

#### Question 1
A Social Security number is an identifier that consists of 9 numbers. In the vector `out` below, replace all SSNs with an `XXX-XX-XXXX` string to annonymize *only* SSN data. Your algorithm should be general enough to handle non-conventional formatting of SSNs.

```r
> x <- "my SSN is 953-29-9402 and my age is 65"
> y <- "My phone number is 612-943-0539"
> z <- "my ssn number is 39502 9485."
> out <- c(x,y,z)
> out
[1] "my SSN is 953-29-9402 and my age is 65"
[2] "My phone number is 612-943-0539"       
[3] "my ssn number is 39502 9485."          
```


### Question 2
The regular expression `"^[Ss](.*)(t+)(.+)(t+)"` detects "scuttlebutt", "Stetson", and "Scattter", but not "Scatter." Why?

## Trump Tweets


```r
> tweets<- read_csv("https://raw.githubusercontent.com/mgelman/data/master/TrumpTweetData.csv")
```

### Question 3 
a. What proportion of tweets (`text`) mention "Hillary" or "Clinton"?  
b. What proportion of these tweets include "crooked"?

### Question 4
Compute the number of web links per tweet  and compare the count distributions by tweet source. Which source has the highest proportion of web links?

  - **Hint:** URLS are `https://t.co/` followed by a string of letters or numbers

### Question 5
Extract all Twitter handles (starting with @)  from Trump tweets. Find and graph the distribution of the 10 most used handles.  

### Question 6
Repeat question 3 but look for times rather than web links. (Times are likely given when announcing an upcoming event on Twitter.)

