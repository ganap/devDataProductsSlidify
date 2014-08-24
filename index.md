---
subtitle    : 
title       : Black Scholes Pricing Model
author      : ganap
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

The Black-Scholes option pricing model (BSOPM) has been one of the most important developments in finance in the last 50 years

Has provided a good understanding of what options should sell for

Has made options more attractive to individual and institutional investors

---

## Intuition Into the Black-Scholes Model

The valuation equation has two parts

      - One gives a “pseudo-probability” weighted expected stock price (an inflow)
      
      - One gives the time-value of money adjusted expected payment at exercise (an outflow)

The value of a call option is the difference between the expected benefit from 
acquiring the stock outright and paying the exercise price on expiration day

---
## Determinants of the Option Premium

Asset Price (S)

Strike price (K)

Time until expiration (time)

Volatility (v)

Dividends (div)

Risk-free interest rate (r)

---

# Pricing of a call 

```r
   S <- 100; K <- 110; v  <- .2; r  <- 0.05; div <- 0.07; dt  <- 0.25
   kCall <- function(S){  
      d1  <- (log(S / K) + (r - div + 0.5 * v^2) * dt) / (v * dt^0.5)
      d2  <- d1 - v * dt^0.5
      return(exp(-div*dt)* pnorm(d2))
    }    
    DeltaCall <- function(S){      
      d1  <- (log(S / K) + (r - div + 0.5 * v^2) * dt) / (v * dt^0.5)
      d2  <- d1 - v * dt^0.5    
      return(exp(-div * dt) * pnorm(d1))
    }
 PriceCall <- function(S){
      return(S * DeltaCall(S) - K * kCall(S))
    }
   PriceCall(S)
```

```
## [1] 0.9342
```
The price of call with the above parameters is ` 0.9342`

---

## Problems Using the Black-Scholes Model

Does not work well with options that are deep-in-the-money or substantially out-of-the-money

Produces biased values for very low or  very high volatility stocks

    - Increases as the time until expiration increases
  
May yield unreasonable values when an option has only a few days of life remaining


