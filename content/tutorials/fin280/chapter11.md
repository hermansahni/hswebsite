---
title: NESTED loops
linktitle: NESTED loops
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  fin280:
    parent: Advanced Topics
    weight: 11

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 11
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



## SORT Procedure

### *Ascending sort*

This procedure is used to sort variables (or a group of variables) by its values, either in the ascending order or the descending order. *Set `C:\data` directory as the WORK directory.*

To sort {{% staticref "files/fin280/jrank.sas7bdat" %}}Dataset 3{{% /staticref %}} by JOURNAL NAME variable in the **ascending** order, run the code below.

*SAS code:*

```sas

proc sort data = work.jrank ;
 by title ;
run;

```

*Output:*

{{< figure library="true" src="fin280/jrank_sort1.jpg" title="Journal ranking sorted by `TITLE`" numbered="true" lightbox="true" >}}

### *Descending sort*

To sort {{% staticref "files/fin280/jrank.sas7bdat" %}}Dataset 3{{% /staticref %}} by JOURNAL RANK variable in the **descending** order, run the code below. *Set `C:\data` directory as the WORK directory.*

*SAS code:*

```sas

proc sort data=work.jrank ;
 by descending rank;
run;

```

### *Multiple sort*

Now, consider {{% staticref "files/fin280/gdata.sas7bdat" %}}this{{% /staticref %}} data. To sort {{% staticref "files/fin280/gdata.sas7bdat" %}}this{{% /staticref %}} data first by `TICKER`, then by **descending** `DATE1`, again then by **descending** `DATE2`, and create a new dataset TEMP that contains the sorted data; run the code below. *Set `C:\data` directory as the WORK directory.*

*SAS code:*

```sas

proc sort data=work.gdata out=work.temp;
 by ticker descending date1 descending date2 ;
run;

```


___



## PRINT Procedure

### Print all variables 

Consider {{% staticref "files/fin280/in401k.sas7bdat" %}}this{{% /staticref %}} data. To print the values of a variable on-screen (first 15 observations), run the code below. *Set `C:\data` directory as the WORK directory.*

*SAS code:*

```sas

proc print data=work.in401k (obs=15);
run;

```

Click {{% staticref "files/fin280/print-results.pdf" "newtab" %}}here{{% /staticref %}} to view the printed log file in pdf.

### Print selected variables 

To print the values of *selected* variable on-screen (first 15 observations), run the code below. *Set `C:\data` directory as the WORK directory.*

*SAS code:*

```sas

proc print data=in.in401k (obs=15);
 var e401k inc age ;
run;

```

Click {{% staticref "files/fin280/print-results1.pdf" "newtab" %}}here{{% /staticref %}} to view the printed log file in pdf.



___





# Road map


- [x] Data Input
- [x] Data Manipulation
- [x] Some useful PROC steps
- [x] Merging and subsetting a dataset
- [x] Compute descriptive statistics
- [x] Compute test of differences
- [x] Ordinary Least Squares
- [x] Probit/Logit Regression
- [x] DO loops 
- [x] WHILE loops
- [x] NESTED loops


___
