---
title: Assignment 2
date: 15-03-2022
---

# Technical Description

## public int getRain(int month, int day)
returns the random amount of rain generated for the specified day by creating upper/lower bounds and estimating between them
- subtracts 1 from month so the index is 0-based
- checks if the month is in bounds (0 <= month < 12)
- If checks pass, gets the max and min rainfal for the given month
- gets the max rainfal for next month by adding 1 to the index. Takes the mod 12 of the new month so that December (11) cycles round to January (0)
- calculates the difference between the max of this and next month
- calculates how far through the month a given day is based on the number of days in a month, returns a double as a percent (kind of, X100
- sets the max RainfallDifference variable to account for not being through the entire month.
- sets the maxRainToday variable as an upper boundary for the value by adding the max difference to the max rainfall
- multiplies maxRainToday by a random float between 0 and 1 (makes it smaller) and assigns it to the int variable rain
- if this value is smaller than the minRainThisMonth, return that value, else return the random scaled value

## PrecipitationGraph()
This constructor generages rainfall data for every day of every month and assigns it to the rainfall array.
- sets the rainfall matrix array to have 12 rows (one for each month)
- starts a for loop that iterates over the range 0-11 as the variable month
- for every month/row in the array,  the method initialises a column for every day in that month respectively.
- the method then starts another for loop that iterates over every day in the month and adds estimated rainfall data to that column.

## private int[] prepareData()
### method name matches another method!

- Initialises a new int array of length 12 
- cycles through each month, calculates the average rainfall across all days in that month, scales it (default is 1), and then adds it to the array.
- returns an int array of the average scaled rainfall for every month


## private void verticalGraph(int[] array)
display a vertical graph representing rainfall
- takes in an array of integers & initialises a star string called stars
- sets the ArrayMax (not pascal case) integer to the maximum value in the array
- starts a for loop, with int i starting as ArrayMax, and iterating down once each loop until 0 (each ROW in the veritcal graph)
- resets stars to "|"
- starts another for loop that interates through every index in the given array as integer j
- if the value at this index in the array is greater than i, append a star to that column in the stars string, else append a space
- prints the row to stdout
- at the end of nested for loopps, initialises Strings dottedLine and dateLine to "|"
- starts a new for loop interating through the indices of the array as int i (this is to display the bottom row)
- appends "---" to dottedLine
- formats the index (i) + 1 to double digit form
- prints dottedLine and then dateLine, followed by a newline character

# Specification
# Aditional Features
## Vertical and Horizontal graphs do not have second axis values to indicate amount of rainfall

Printed graphs display a number of stars representing (scaled) rainfall every month, however there are no labels on the y/x axis respectively that indicate how much rainfall this actually is and what a star represents.
