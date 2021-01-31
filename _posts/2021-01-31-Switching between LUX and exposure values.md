---
layout: post
title: Switching between LUX and Light Values
slug: luxToEv
---

### How to determine exposure from LED panels LUX specifications

Setting up the conversion functions:


    # From Light Values to LUX
    lv2lux <- function(lv) (2^lv)*2.5  
    
    # From LUX to Light Values
    lux2lv <- function(lux) log(lux/2.5, 2)

Plotting the conversion function:


    # Interactive plot
    
    lv <- seq(3,15,.5)
    lux <- lv2lux(lv)
    plot(lv, lux, type = "l",
         xlab = "Light Values", ylab = "LUX",
         col = "red")

![plot of chunk plot](/figures/plot-1.svg)
