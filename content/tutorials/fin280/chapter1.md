---
title: Data Input
linktitle: Data Input
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  fin280:
    parent: Overview
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

In this tutorial, you will learn how to input data from different file formats - text files (.txt, .dat), excel files (.xls, .xlsx), and comma-separated files (.csv); and also handle a plethora of delimiters.


## Comma-delimited

Click {{% staticref "files/fin280/grades.txt" "newtab" %}}here{{% /staticref %}} to download the comma-delimited data for the program below in .txt format. *Always place files in the `C:\data` folder.*


*SAS code:*

```c

data survey; 
 infile 'C:\data\grades.txt' delimiter=',' ;
 input grade $ from_perc to_perc ; 
run;

```

#### Explanation for the above code ...


```c

data survey; 

```

This line of code creates a SAS data-set called "SURVEY"


```c

infile 'C:\data\grades.txt' delimiter=',' ;

```

This line of code sets the location of input data-set and the delimiter that separates variables. In this case, the input file 'grade.txt' is located at 'C:\data' and all individual variables are sequentially seperated by the comma delimiter.


```c

input grade $ from_perc to_perc ; 

```

This line of code mentions the order and the type of input variables. In this case, the three variables - `grade`, `from_perc`, and `to_perc` are arranged sequentially in the dataset. Also, since `grade` is a text/alphanumeric variable, it is accompanied with a dollar sign `$`; whereas the other two variables are numeric variables.

```c

run ;

```

The "run" command signifies the end of the DATA step.



___



## Tab-delimited

Click {{% staticref "files/fin280/tab.txt" "newtab" %}}here{{% /staticref %}} to download the tab-delimited data for the program below in .txt format. *Always place files in the `C:\data` folder.*


*SAS code:*

```c

data survey; 
 infile 'C:\data\tab.txt' delimiter='09'x ;
 input grade $ from_perc to_perc ; 
run;

```


___



## Strike-delimited

Click {{% staticref "files/fin280/strike.txt" "newtab" %}}here{{% /staticref %}} to download the strike-delimited data for the program below in .txt format. *Always place files in the `C:\data` folder.*


*SAS code:*

```c

data survey; 
 infile 'C:\data\strike.txt' delimiter='|' ;
 input grade $ from_perc to_perc ; 
run;

```


#### A more complicated data-set ... 

Input a long character (text/alphanumeric) data

Click {{% staticref "files/fin280/airfare.txt" "newtab" %}}here{{% /staticref %}} to download the data for the program below in .txt format. *Always place files in the `C:\data` folder.*


*SAS code:*

```c

data airfaredata;
 infile 'C:\data\airfare.txt' delimiter='|' ;
 input year origin $ destin $ id dist passen fare bmktshr 
       ldist y98 y99 y00 lfare ldistsq concen lpassen  ; 
run;

```

Notice anything? Now, try this code.


*SAS code:*

```c

data airfaredata;
 informat origin destin $40. ;
   format origin destin $40. ;
 infile 'C:\data\airfare.txt' delimiter='|' ;
 input year origin $ destin $ id dist passen fare bmktshr 
       ldist y98 y99 y00 lfare ldistsq concen lpassen  ; 
run;

```

#### Explanation for the above code ...

```c

informat origin destin $40. ;

```

Informats are typically used to read or input data from external files called flat files (text files, ASCII files, or sequential files). The `informat` instructs SAS on how to read data into SAS variables SAS informats are typically grouped into three categories: character, numeric, and date/time. 

In this code, `informat` sets the maximum allowed arbitrary length (in this case, 40 characters) for the two variables that denote the city of origin and the destination city of flights. 

```c

  format origin destin $40. ;

```

Formats are typically used to store data in output SAS datasets.

In this code, `format` sets the maximum allowed arbitrary length (in this case, 40 characters) for the two variables that denote the city of origin and the destination city of flights. 

*For more on Informats and Formats, check out [this](https://support.sas.com/content/dam/SAS/support/en/books/the-power-of-proc-format/59498-excerpt.pdf) documentation.*

A well commented DATA step looks like this ... Note that code can be written spanning multiple lines as long as it ends with a semi-colon. Also, the code can be accompanied with explanations (commonly referred to as *comments*) when placed between `/*` and `*/` markings.


*SAS code:*

```c

data airfaredata;/* Creating a SAS data-set called "AIRFAREDATA" */

informat origin destin $40.; /* set informat to length 40: how SAS reads data */
  format origin destin $40.; /* set   format to length 40: how SAS stores data */

  infile 'C:\data\airfare.txt' delimiter='|'; /* input airfare data */
   
/**********************************************************************************
The next lines of code lists the variables inputed along with their description. 
**********************************************************************************/
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
   
run; 

```


___



## Excel (.xls) data


Click {{% staticref "files/fin280/pilldata.xls" %}}here{{% /staticref %}} to download the data for the program below in .xls format. *Always place files in the `C:\data` folder.*


*SAS code:*

```c

proc import out=work.ppill datafile="C:\data\pilldata.xls" dbms=xls replace;
     sheet="datapg";
     getnames=yes;
run;

```


___



## Excel (.xlsx) data


Click {{% staticref "files/fin280/pdata.xlsx" %}}here{{% /staticref %}} to download the data for the program below in .xlsx format. *Always place files in the `C:\data` folder.*


*SAS code:*

```c

proc import out=work.ppill datafile="C:\data\pdata.xlsx" dbms=xlsx replace;
     sheet="datapg"; 
     getnames=yes;
run;

```


___



## Practice Exercises

#### Input the following data-sets


- Among all occupations, what is the importance of Programming Skills?
-- Click [here](https://bit.ly/2lGTvXC) to download the data from ONetOnline.org.


- Civilian Unemployment Rate
-- Click [here](https://fred.stlouisfed.org/data/UNRATE.txt) to download the data from Federal Reserve Bank of St. Louis.


- Total Public Debt as Percent of Gross Domestic Product
-- Click [here](https://bit.ly/2k3RAM3) to download the data from Federal Reserve Bank of St. Louis.


- Education Statistics
-- Click [here](http://databank.worldbank.org/data/download/Edstats_csv.zip) to download the data from World Bank.


___



# Road map


- [x] Data Input
- [ ] Data Manipulation
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
