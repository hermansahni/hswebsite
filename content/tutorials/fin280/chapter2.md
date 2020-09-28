---
title: Data Manipulation
linktitle: Data Manipulation
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  fin280:
    parent: Overview
    weight: 2

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

In this tutorial, you will learn to prepare independent variables.  Specifically, you will perform basic arithmetic operations, compute log and exponent of a variable, and test conditional variables using IF-THEN-ELSE statements.


## Arithmetic operations

Download the same {{% staticref "files/fin280/airfare.txt" "newtab" %}}airfare{{% /staticref %}} data to used before. *Always place files in the `C:\data` folder.*


*SAS code:*

```c

data airfaredata;
 infile 'C:\data\airfare.txt' delimiter='|' ;
 input year origin $ destin $ id dist passen fare bmktshr 
       ldist y98 y99 y00 lfare ldistsq concen lpassen  ; 
run;

```


___



## Adding variables


*SAS code:*

```c

data datman;/* creating a new sas data-set called "datman" */

/**********************************************************************************
the set statement inherits all the variables from the data-set "airfaredata"
**********************************************************************************/
 set airfaredata;
  
/**********************************************************************************
creating a new variable through other arithmetic operators
**********************************************************************************/
 year9899      = y98     + y99    ; /* (a) addition        */
 zeros         = bmktshr - concen ; /* (b) subtraction     */
 perconcen     = concen  * 100    ; /* (c) multiplication  */
 fare_per_mile = fare/dist        ; /* (d) division        */
  
/**********************************************************************************
compute square of an existing variable. different ways to compute a square of an 
existing variable: 1) logdistsq = logdist**2 ; 2) logdistsq = logdist*logdist ;
alternately, for squareroot of an existing variable: logdistsqrt = logdist**0.5;
**********************************************************************************/
 logdistsq   = ldist**2   ; /* (e) squared     */
 logdistsqrt = ldist**0.5 ; /* (f) square-root */
   
 serialno = _n_;         /*(g) adding a column of serial number */
run;

```


___



## Computing log/exp


*SAS code:*

```c

data datman ;

 set airfaredata;
  
 logdist  = log(dist) ; /* (h) logarithm */
 distance = exp(ldist); /* (i) exponent  */  
run;

```


## IF-THEN-ELSE

```c

Conditional statements: 
           if <condition> 
                     then <what to do if condition is true> ;
                     else <what to do if condition is false> ;

```
 
for example, let us conditionally create a year dummies - `year98`, `year99`, `year00`, from an existing variable `year`.

```c

           year98 = 1 if the value for the variable year is 1998; otherwise = 0
           year99 = 1 if the value for the variable year is 1999; otherwise = 0
           year00 = 1 if the value for the variable year is 2000; otherwise = 0

```


*SAS code:*

```c

data datman ;

 set airfaredata;

/* Two ways to create year dummies */
 
/* First way: */
 if year = 1998 then year98 = 1; 
                else year98 = 0; /* dummy that represents year=1998 */
 if year = 2000 then year00 = 1; 
                else year00 = 0; /* dummy that represents year=2000 */

/* Second way: */
 year99 = 0;
 if year = 1999 then year99 = 1; 

run;

```

#### All the above steps can be accomplished in one DATA step


*SAS code:*

```c

data airfaredata ;

  informat origin destin $40.;
    format origin destin $40.;
  
  infile 'C:\data\airfare.txt' delimiter='|';
  
  input year     /* 1997, 1998, 1999, 2000           (numeric)  */
        origin $ /* flight's origin                  (character)*/
        destin $ /* flight's destination             (character)*/
        id       /* route identifier                 (numeric)  */
        dist     /* distance, in miles               (numeric)  */
        passen   /* avg. passengers per day          (numeric)  */
        fare     /* avg. one-way fare, $             (numeric)  */
        bmktshr  /* fraction market, biggest carrier (numeric)  */
        ldist    /* log(distance)                    (numeric)  */
        y98      /* =1 if year == 1998               (numeric)  */
        y99      /* =1 if year == 1999               (numeric)  */
        y00      /* =1 if year == 2000               (numeric)  */
        lfare    /* log(fare)                        (numeric)  */
        ldistsq  /* ldist^2                          (numeric)  */
        concen   /* = bmktshr                        (numeric)  */
        lpassen  /* log(passen)                      (numeric)  */
; 

 year9899      = y98     + y99    ; /* (a) addition       */
 zeros         = bmktshr - concen ; /* (b) subtraction    */
 perconcen     = concen  * 100    ; /* (c) multiplication */
 fare_per_mile = fare/dist        ; /* (d) division       */

 logdistsq   = ldist**2   ; /*(e) squared     */
 logdistsqrt = ldist**0.5 ; /*(f) square-root */
   
 serialno = _n_;         /*(g) adding a column of serial number */
 
 logdist  = log(dist) ; /*(h) logarithm: logvar_a = log(var_a)   ;*/
 distance = exp(ldist); /*(i) exponent:  var_a    = exp(logvar_a);*/  
 
/* Two ways to create dummies */
/* First way: */
 if year = 1998 then year98 = 1; 
                else year98 = 0; /* dummy that represents year=1998 */
 if year = 2000 then year00 = 1; 
                else year00 = 0; /* dummy that represents year=2000 */
 
/* Second way: */
 year99 = 0;
 if year = 1999 then year99 = 1; 
 
run;

```

___



## Practice Exercises

#### Manipulate the data

#### Click {{% staticref "files/fin280/ceopay.txt" "newtab" %}}here{{% /staticref %}} to download the data. Do the following calculations.

#### Variable order in the data - CEO name, Company name, Salary, Bonus, Total pay, and Year. 

- Did you know that the cash pay is the sum of salary (`salary`) and bonus (`bonus`)? Compute Cash Pay.
- When total pay (`pay`) is missing, replace those missing values with salary (`salary`) plus bonus (`bonus`).
- What is the non-cash pay (stock options, loan reimbursements) that the CEO receives? *Hint:* Non-Cash Pay = Pay minus Cash Pay.
- Create the following dummies - (a) meaningful pay (pay > 0) (b) zero non-cash pay (non-cash pay = 0).
- Create variables - (a) cashpay-to-pay percentage (b) noncashpay-to-pay percentage.
- Keep only those observations with meaningful pay. (or) Alternately delete observations when pay is non-meaningful.


___



# Road map


- [x] Data Input
- [x] Data Manipulation
- [ ] Some useful PROC steps
- [ ] Merging and subsetting a dataset
- [ ] Compute descriptive statistics
- [ ] Compute test of differences
- [ ] Ordinary Least Squares
- [ ] Probit/Logit Regression
- [ ] DO loops 
- [ ] WHILE loops
- [ ] NESTED loops


___
