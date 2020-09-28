---
title: Test of differences
linktitle: Test of differences
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  fin280:
    parent: Overview
    weight: 6

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 6
---


In this tutorial, you will learn to describe a dataset using CONTENTS procedure, to sort (double sort and multiple sort) a dataset using the SORT procedure, and print certain results to the log file (screen) using the PRINT procedure.


## CONTENTS Procedure

This procedure is used to find the contents (variable names, label, and description) of a SAS data-set.

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
- [x] Compute test of differences
- [ ] Ordinary Least Squares
- [ ] Probit/Logit Regression
- [ ] DO loops 
- [ ] WHILE loops
- [ ] NESTED loops


___
