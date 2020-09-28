---
# Course title, summary, and position.
linktitle: Introduction to SAS Programming
summary: Learn how to input and describe raw data, manipulate variables, merge and subset datasets, compute simple statistics, and perform regression analysis.
weight: 1

# Page metadata.
title: Overview
date: "2018-09-09T00:00:00Z"
lastmod: "2018-09-09T00:00:00Z"
draft: false  # Is this a draft? true/false
toc: true  # Show table of contents? true/false
type: docs  # Do not modify.

# Add menu entry to sidebar.
# - name: Declare this menu item as a parent with ID `name`.
# - weight: Position of link in menu.
menu:
  fin280:
    name: Overview
    weight: 1
---

## *Course Description*

## **Data Input**

SAS is one of most user-friendly programming language that inputs data from a wide variety of formats. In this section, you will learn to input data from text files (*.txt*, *.dat*), excel files (*.xls*, *.xlsx*), and comma-separated files (*.csv*); and using a plethora of delimiters.


___


## **Data Manipulation**

In this section, you will learn how to prepare the inputted data and perform meaning transformations - basic arithmetic operations, log and exponent operations, and test conditional statements (*IF-THEN-ELSE*).


___


## **Some useful PROCEDURES**


- *CONTENTS* Procedure - to find the contents of a SAS data-set. This typically generally the name, the label, and the other attributes such as type (string/numeric), default length, current format, and informat of the variables currently present in the dataset. It also provides the administrator permission for the dataset (read only or read/write) along with the date of creation and the version of SAS used to create the dataset.
- *SORT* Procedure - to sort the values of a variable or a group of variables. An alphabetical sort or a descending numeric sort are also possible.
- *PRINT* Procedure - to print the values of a variable or a group of variables on-screen. When its prudent to see the execution of a particular section of the code, this procedure comes in handy.
- *MEANS* - to find the descriptive statistics of a variable or a group of variables. The descriptive statistics commonly include the number of observations (*N*), the arithmetic average (*Mean*), the standard deviation (*Stddev*), the minimum (*Min*), the maximum (*Max*), the 50th percentile (*Median*), the 1st Percentile (*p1*), the 99th Percentile (*p99*), the 1st Quartile (*p25*), the 3rd Quartile (*p75*), and the inter-quartile range (*iq*). 
- *UNIVARIATE* - similar to the *MEANS* procedure.

*MEANS* and *UNIVARIATE* procedures can also be used to find descriptive statistics conditionally. For example, across data groups such as age groups, sex, or income levels. When trying to understand the data, it is sometimes prudent to also analyze other characteristics of the data other than its descriptive statistics. For example, it helps to know the number of missing values, zeros, or negative values of a variable or a group of variables. Unfortunately, there is no standard SAS commands that does this, but it is easy to write our own statements. We do, however, have commands that help us do distributional testing (test of normality) or find correlations among variables.


___



## **Compute test of differences**


- T-test - Test of Differences in Means
- Rank-sum test - Test of Differences in Medians
- Chi-square - Test of Differences in Proportions
- CORR - Test of Correlations and Multicollinearity


___


## **Ordinary Least Squares**


- with F-tests
- with heteroscedasticity-consistent standard errors
- produce residual/predicted outputs for residual/predicted plots


___


## **Probit/Logit Regression**


- PROBIT models
- LOGISTIC models



___


## **Merging and subsetting a dataset**



___


## *Course materials*

Course notes are available at `http://hermansahni.com/tutorials/fin280`. Additionally, SAS Institute will provide practice exams.
