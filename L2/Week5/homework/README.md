# Week 4 Assignment - Traders@SMU Alpha Program

## Overview

This directory contains materials for Level 2, Week 4 of the Alpha Program.

## Learning Objectives

- Understand advanced portfolio theory
- Learn factor modeling techniques
- Develop skills in advanced risk management

## Assignment Instructions

Complete the following tasks:
 Using Z-score data and the buy/sell rules 
we have used today, generate buy and sell 
signals and plot them on a graph with the 
stock price to show when you would buy 
and sell. Do this for 3 stocks of your 
choosing (no AAPL). Use whatever date, 
time, and frequency parameters you would 
like. Put short positions in yellow and long 
positions in green. 

STOCK 1- SPY
<img width="1721" height="1347" alt="image" src="https://github.com/user-attachments/assets/4aa1ba3a-b93f-415c-9a37-9ba772903af9" />

STOCK 2- META
<img width="1710" height="1296" alt="image" src="https://github.com/user-attachments/assets/6c8fe0e6-3dec-436e-befc-8e7eb1a4273a" />

STOCK 3- GC (Gold CME Futures)
<img width="1722" height="1301" alt="image" src="https://github.com/user-attachments/assets/ee67a311-a8d0-4289-9566-f31b93f9e39b" />


I have a code in Python as well that plots this, these specific screenshots come from Tradingview via Pinescript 5
It seems like the strategy works very well for longing, maybe some drawdown for shorts though. I think this strategy could be best used to DCA into long term stocks/indexes you like, finding decent entry prices. The settings on here are similar to those we had last meeting, +-4 stop price, exit around 0 (Plotting that in pinescript gave me some issues for whatever reason), and entries around +-2. I found some success with 2.5 as well for entries. This code uses daily closes, so meant for longer term investing. 
## Submission Guidelines

- Complete all tasks in this directory
- Submit your work by creating a pull request with branch name `L2-W4-submission`
- Deadline: 10/15/25
  

## Resources

- [Resource 1]
- [Resource 2]
- [Resource 3] 
