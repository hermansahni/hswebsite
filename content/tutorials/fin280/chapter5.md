---
title: Descriptive statistics
linktitle: Descriptive statistics
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  fin280:
    parent: Overview
    weight: 5

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---


In this tutorial, you will learn to perform basic tests to obtain descriptive statistics of the sample using the MEANS procedure and the UNIVARIATE procedure.


## MEANS Procedure

This procedure is widely used in "data cleansing" or "exploratory data analysis" tasks to determine if incorrect or "bad" values of analysis variables are contained in the data set that must be transformed or removed prior to further analysis (Ref - https://support.sas.com/resources/papers/proceedings/proceedings/sugi29/240-29.pdf). 


used to find the contents (variable names, label, and description) of a SAS data-set.

Click {{% staticref "files/fin280/gdata.sas7bdat" %}}here{{% /staticref %}} to download the data. *Always place files in the `C:\data` folder. Also, set `C:\data` directory as the WORK directory.*

To find its contents, run the code below.

*SAS code:*

```sas

proc contents data=work.gdata ;
run ;

```

Click {{% staticref "files/fin280/gdata.html" "newtab" %}}here{{% /staticref %}} to view the html output of the contents. *Set `C:\data` directory as the WORK directory.*


To output the contents to a pdf, run the code below.

*SAS code:*

```sas

ods pdf file="C:\data\contents.pdf" ;
 proc contents data=work.gdata ;
  run;
 quit;
ods pdf close;

```

Click {{% staticref "files/fin280/gdata.pdf" "newtab" %}}here{{% /staticref %}} to view the pdf output of the contents.


### Practice Exercises

#### Find the contents of the following data-sets

- {{% staticref "files/fin280/in401k.sas7bdat" %}}Dataset 1{{% /staticref %}}
- {{% staticref "files/fin280/hlhddat.sas7bdat" %}}Dataset 2{{% /staticref %}}
- {{% staticref "files/fin280/jrank.sas7bdat" %}}Dataset 3{{% /staticref %}}


___





# Road map


- [x] Data Input
- [x] Data Manipulation
- [x] Some useful PROC steps
- [x] Merging and subsetting a dataset
- [x] Compute descriptive statistics
- [ ] Compute test of differences
- [ ] Ordinary Least Squares
- [ ] Probit/Logit Regression
- [ ] DO loops 
- [ ] WHILE loops
- [ ] NESTED loops


___
