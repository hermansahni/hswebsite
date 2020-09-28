---
title: Merging/Subsetting
linktitle: Merging/Subsetting
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  fin280:
    parent: Overview
    weight: 4

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---


In this tutorial, you will learn to merge two datasets and to subset a dataset (i.e., limit dataset to observations that meet a given criteria). We will also perform certain post-merge operations - left join, right join, and full merge. There are other procedures that can accomplish the same feat and, in some cases, more efficiently too. For example, PROC SQL.


## Merge two datasets

Consider the following data on student performance. The course includes three quizzes (100 points each), two exams (200 points each), and a group project (500 points). The quizzes, exams, and project contributes 20%, 40%, and 40%, respectively, to the student's grade. Project is a group activity and every student in a particular group gets the same score. Class has 20 students.

#### **Cumulative Score is given as follows:**

$$
\begin{align}
\text{Score} = &0.2 \times \frac{(\text{Quiz1} + \text{Quiz2} + \text{Quiz3})}{3} + \\\\\\ 
               &0.4 \times \frac{(\text{Exam1} + \text{Exam2})}{4} + \\\\\\
               &0.4 \times \frac{\text{Project}}{5} 
\end{align}
$$

#### **I. Final grading scale is given as follows:**

| Letter Grade | Score    |
|:------------:|:--------:|
| A+           | 93 & up  |
| A            | 87       |
| A-           | 85       |
| B+           | 83       |
| B            | 77       |
| B-           | 75       |
| C+           | 73       |
| C            | 67       |
| C-           | 65       |
| D+           | 63       |
| D            | 57       |
| D-           | 55       |
| F            | Below 55 |

#### **II. Group assignment is as follows:**

| Student I.D. | Group Number |
|:------------:|:------------:|
| 1            |1             |
| 2            |1             |
| 3            |1             |
| 4            |1             |
| 5            |1             |
| 6            |2             |
| 7            |2             |
| 8            |2             |
| 9            |2             |
|10            |2             |
|11            |3             |
|12            |3             |
|13            |3             |
|14            |3             |
|15            |3             |
|16            |4             |
|17            |4             |
|18            |4             |
|19            |4             |
|20            |4             |

To input raw data on group ids and form a dataset, run the code below.

*SAS code:*

```c

data group_info; /* Creating a SAS data-set called "group_info" which identifies 
                    which group a student belongs to */
  
 infile datalines dlm = "|"; /* Raw data is inputed in the code itself using "DATALINES".
                                Just copy and paste the data after the DATALINE; 
                                Use any delimiter of your choice. 
                                Here, strike "|" is used. */
  
 input id group ; /* identifies input variables, in that order */
  
 label /* labelling input variables */
  id    = "Student I.D."
  group = "Group I.D."
 ;
  
DATALINES; 
 1|1
 2|1
 3|1
 4|1
 5|1
 6|2
 7|2
 8|2
 9|2
10|2
11|3
12|3
13|3
14|3
15|3
16|4
17|4
18|4
19|4
20|4
;
run;

```

Click {{% staticref "files/fin280/group.png" "newtab" %}}here{{% /staticref %}} to view how the `group_info` dataset looks like.

#### **III. Individual scores on the three quizzes are as follows:**

| Student I.D. | Quiz 1 | Quiz 2 | Quiz 3 |
|:------------:|:------:|:------:|:------:|
| 1            | 33     | 61     | 76     |
| 2            | 84     | 77     | 87     |
| 3            | 50     | 63     | 98     |
| 4            | 91     | 92     | 59     |
| 5            | 61     | 83     | 58     |
| 6            | 96     | 36     | 61     |
| 7            | 78     | 65     | 80     |
| 8            | 77     | 69     | 50     |
| 9            | 74     | 31     | 54     |
|10            | 65     | 58     | 33     |
|11            | 38     | 42     | 83     |
|12            | 68     | 71     | 29     |
|13            | 70     | 19     | 87     |
|14            | 68     | 53     | 65     |
|15            | 18     | 38     | 67     |
|16            | 31     | 14     | 72     |
|17            | 44     | 58     | 18     |
|18            | 69     | 16     | 65     |
|19            | 68     | 43     | 76     |
|20            | 53     | 39     | 56     |

To input raw data on the three quizzes and form a dataset, run the code below.

*SAS code:*

```c

data quiz; /* Creating a SAS data-set called "quiz" */
 
 infile datalines dlm = " "; /* Raw data is inputed in the code itself using "DATALINES".
                                Just copy and paste the data after the DATALINE; 
                                Use any delimiter of your choice. 
                                Here, "space" is used. */
 
 input id quiz1 quiz2 quiz3 ; /* identifies input variables, in that order */
 
 label /* labelling input variables */
  id    = "Student I.D."
  quiz1 = "Quiz 1"
  quiz2 = "Quiz 2"
  quiz3 = "Quiz 3"
 ;
 
DATALINES; 
 1 33 61 76
 2 84 77 87
 3 50 63 98
 4 91 92 59
 5 61 83 58
 6 96 36 61
 7 78 65 80
 8 77 69 50
 9 74 31 54
10 65 58 33
11 38 42 83
12 68 71 29
13 70 19 87
14 68 53 65
15 18 38 67
16 31 14 72
17 44 58 18
18 69 16 65
19 68 43 76
20 53 39 56
;
run;

```

Click {{% staticref "files/fin280/quiz.png" "newtab" %}}here{{% /staticref %}} to view how the `quiz` dataset looks like.

#### **IV. Individual scores on the two exams are as follows:**

| Student I.D. | Exam 1 | Exam 2 |
| -------------| -------| -------|
| 1            | 158    | 111    |
| 2            | 168    | 142    |
| 3            | 142    | 174    |
| 4            | 181    | 125    |
| 5            | 159    | 175    |
| 6            | 156    | 152    |
| 7            | 119    | 119    |
| 8            | 114    | 138    |
| 9            | 137    | 127    |
|10            | 152    | 120    |
|11            | 191    | 180    |
|12            | 102    | 139    |
|13            | 171    | 188    |
|14            | 112    | 199    |
|15            | 156    | 163    |
|16            | 167    | 104    |
|17            | 112    | 110    |
|18            | 168    | 193    |
|19            | 144    | 161    |
|20            | 195    | 121    |

To input raw data on the two exams and form a dataset, run the code below.

*SAS code:*

```c

data exam; /* Creating a SAS data-set called "exam" */
  
 infile datalines dlm = ","; /* Raw data is inputed in the code itself using "DATALINES".
                                Just copy and paste the data after the DATALINE; 
                                Use any delimiter of your choice. 
                                Here, "comma" is used. */
  
 input id exam1 exam2 ; /* identifies input variables, in that order */
  
 label /* labelling input variables */
  id    = "Student I.D."
  exam1 = "Exam 1"
  exam2 = "Exam 2"
 ;
  
DATALINES; 
 1,158,111
 2,168,142
 3,142,174
 4,181,125
 5,159,175
 6,156,152
 7,119,119
 8,114,138
 9,137,127
10,152,120
11,191,180
12,102,139
13,171,188
14,112,199
15,156,163
16,167,104
17,112,110
18,168,193
19,144,161
20,195,121
;
run;

```

Click {{% staticref "files/fin280/exam.png" "newtab" %}}here{{% /staticref %}} to view how the `exam` dataset looks like.

#### **Group scores on the project is as follows:**

| Group   I.D. | Score |
| -------------| ------|
| 1            | 486   |
| 2            | 452   |
| 3            | 378   |
| 4            | 313   |

To input raw data on the project scores and form a dataset, run the code below.

*SAS code:*

```c

data project; /* Creating a SAS data-set called "project" */
  
 infile datalines dlm = "!"; /* Raw data is inputed in the code itself using "DATALINES".
                                Just copy and paste the data after the DATALINE; 
                                Use any delimiter of your choice. 
                                Here, exclamation "!" is used. */
  
 input group project ; /* identifies input variables */
  
 label /* labelling input variables */
  group   = "Group I.D."
  project = "Project Score"
 ;
  
DATALINES; 
1!486
2!452
3!378
4!313
;
run;

```

Click {{% staticref "files/fin280/project.png" "newtab" %}}here{{% /staticref %}} to view how the `project` dataset looks like.


#### **Merge all datasets**

#### **One-to-One Merge:**

*One-to-One Merge* is a merging philosophy where each observation in first data-set is merged onto exactly one observation in the second data-set using the common variable. Note: Sorting by the common variable is a requisite for merging.

In this case, the three data-sets (group_info, quiz, and exam) are merged using the common variable Student I.D. `id`.

*SAS code:*

```c

proc sort data=group_info ;
 by id;
run;
 
proc sort data=quiz ;
 by id;
run;
 
proc sort data=exam ;
 by id;
run;

data merged_data1; 
 merge group_info quiz exam ; 
 by id;
run;

```

Click {{% staticref "files/fin280/mergeddata1.png" "newtab" %}}here{{% /staticref %}} to view how the `merged_data1` dataset looks like.

#### **Many-to-One Merge:**

*Many-to-One Merge* is merging philosophy where each observation in second data-set is mapped onto more than one observation in the first data-set using the common variable. Note: Sorting by the common variable is a requisite for merging.

In this case, the `merged_data1` dataset is merged using the common variable Group I.D. `group` to the `project` dataset.

*SAS code:*

```c

proc sort data=merged_data1 ;
 by group;
run;
 
proc sort data=project ;
 by group;
run;

data merged_data; 
 merge merged_data1 project ; 
 by group;
run;

```

Click {{% staticref "files/fin280/mergeddata.png" "newtab" %}}here{{% /staticref %}} to view how the `merged_data` dataset looks like.



___


#### **Full code:**


*SAS code:*

```c

/************************************************************/
/* datset which identifies which group a student belongs to */
/************************************************************/
data group_info; 
 infile datalines dlm = "|";    
 input id group ; 
 label 
  id    = "Student I.D."
  group = "Group I.D."
 ;
 
DATALINES; 
 1|1
 2|1
 3|1
 4|1
 5|1
 6|2
 7|2
 8|2
 9|2
10|2
11|3
12|3
13|3
14|3
15|3
16|4
17|4
18|4
19|4
20|4
;
run;
 
proc sort data=group_info ; 
 by id;
run;

/************************************************************/
/* Creating a SAS data-set called "quiz"                    */
/************************************************************/
data quiz; 
 infile datalines dlm = " ";   
 input id quiz1 quiz2 quiz3 ;   
 label 
  id    = "Student I.D."
  quiz1 = "Quiz 1"
  quiz2 = "Quiz 2"
  quiz3 = "Quiz 3"
 ;
  
DATALINES; 
 1 33 61 76
 2 84 77 87
 3 50 63 98
 4 91 92 59
 5 61 83 58
 6 96 36 61
 7 78 65 80
 8 77 69 50
 9 74 31 54
10 65 58 33
11 38 42 83
12 68 71 29
13 70 19 87
14 68 53 65
15 18 38 67
16 31 14 72
17 44 58 18
18 69 16 65
19 68 43 76
20 53 39 56
;
run;
 
proc sort data=quiz ; 
 by id;
run;

/************************************************************/
/* Creating a SAS data-set called "exam"                    */
/************************************************************/
data exam;    
 infile datalines dlm = ",";    
 input id exam1 exam2 ;    
 label 
  id    = "Student I.D."
  exam1 = "Exam 1"
  exam2 = "Exam 2"
 ;
   
DATALINES; 
 1,158,111
 2,168,142
 3,142,174
 4,181,125
 5,159,175
 6,156,152
 7,119,119
 8,114,138
 9,137,127
10,152,120
11,191,180
12,102,139
13,171,188
14,112,199
15,156,163
16,167,104
17,112,110
18,168,193
19,144,161
20,195,121
;
run;
 
proc sort data=exam ; 
 by id;
run;

/************************************************************/
/* Merge "group_info", "quiz", and "exam" by variable "id". */
/************************************************************/
data merged_data1; 
 merge group_info quiz exam ;
 by id;
run;
 
proc sort data=merged_data1 ;
 by group;
run;
 
/************************************************************/
/* Creating a SAS data-set called "project"                 */
/************************************************************/
data project; 
 infile datalines dlm = "!";    
 input group project ; 
 label 
  group   = "Group I.D."
  project = "Project Score"
 ;
   
DATALINES; 
1!486
2!452
3!378
4!313
;
run;
  
proc sort data=project ;
 by group;
run;

/************************************************************/
/* Merge "merged_data1" and "project" by variable "group".  */
/************************************************************/
data merged_data; 
 merge merged_data1 project ;
 by group;
	quiz = (quiz1 + quiz2 + quiz3)/3 ;        /* computing quiz score       */
	exam = (exam1 + exam2)/4 ;                /* computing exam score       */
	proj = project/5 ;                        /* computing project score    */
	cscore = 0.2*quiz + 0.4*exam + 0.4*proj ; /* computing cumulative score */
 
 /* assigning letter grades to the computed cumulative scores for each student */
 if cscore >= 93                 then lettergrade = "A+" ; 
 if cscore >= 87 and cscore < 93 then lettergrade = "A"  ; 
 if cscore >= 85 and cscore < 87 then lettergrade = "A-" ; 
 if cscore >= 83 and cscore < 85 then lettergrade = "B+" ; 
 if cscore >= 77 and cscore < 83 then lettergrade = "B"  ; 
 if cscore >= 75 and cscore < 77 then lettergrade = "B-" ; 
 if cscore >= 73 and cscore < 75 then lettergrade = "C+" ; 
 if cscore >= 67 and cscore < 73 then lettergrade = "C"  ; 
 if cscore >= 65 and cscore < 67 then lettergrade = "C-" ; 
 if cscore >= 63 and cscore < 65 then lettergrade = "D+" ; 
 if cscore >= 57 and cscore < 63 then lettergrade = "D"  ; 
 if cscore >= 55 and cscore < 57 then lettergrade = "D-" ; 
 if cscore <  55                 then lettergrade = "F"  ; 
 
 label cscore      = "Cumulative Score"
       lettergrade = "Letter Grade"
 ;
 
 drop quiz exam proj ;
 
run;


```

Click {{% staticref "files/fin280/fullcode1.png" "newtab" %}}here{{% /staticref %}} to view how the `merged_data` dataset looks like.


___



## Subsetting datasets

To create a subset of a data-set. For example, consider the final `merged_data` dataset created in the previous section. 

#### Form subset datasets using numerical operations

*SAS code:*

```c

/************************************************************/
/* create the data-set "grade_b" to retain all students who */
/* got a "B" grade                                          */
/************************************************************/
data grade_b ; 
 set merged_data; 
 if 75 <= cscore < 85 then output grade_b ; 
run;


```


#### Form subset datasets using Boolean operators.

*SAS code: Option 1*

```c

/************************************************************/
/* create the data-set "grade_b1" to retain all students who*/
/* got a "B" grade                                          */
/************************************************************/
data grade_b1 ; 
 set merged_data; 
 if lettergrade = "B-" or 
    lettergrade = "B"  or 
    lettergrade = "B+" then output grade_b1 ; 
run;


```

*SAS code: Option 2*

```c

/************************************************************/
/* create the data-set "grade_b2" to retain all students who*/
/* got a "B" grade                                          */
/************************************************************/
data grade_b2 ; 
 set merged_data; 
 if lettergrade = "B-" | 
    lettergrade = "B"  |  
    lettergrade = "B+" then output grade_b1 ; 
run;


```

#### Form subset datasets using IN operators.

*SAS code:*

```c

/************************************************************/
/* create the data-set "grade_b3" to retain all students who*/
/* got a "B" grade                                          */
/************************************************************/
data grade_b3 ; 
 set merged_data; 
 if lettergrade in ("B-", "B", "B+") then output grade_b3 ; 
run;


```

#### Form subset datasets using LIKE (wildcard) operators.

*SAS code:*

```c

/************************************************************/
/* create the data-set "grade_c" to retain all students who*/
/* got a "C" grade                                          */
/************************************************************/
data grade_c ; 
 set merged_data; 

 /* any lettergrade that starts with the letter 'C' */ 
 if lettergrade =: 'C' then output grade_c  ; 

run;


```


#### Form all the above datasets in one step, use the code below.

*SAS code:*

```c

data grade_b grade_b1 grade_b2 grade_b3 grade_c ; 
 
 set merged_data; 
 
 /* create the data-set "grade_b" to retain all students who got a "B" grade */
  if 75 <= cscore < 85  then output grade_b ; /* using numerical operations */
 
 /* create the data-set "grade_b1" to retain all students who got a "B" grade */
  if lettergrade = "B-" or 
     lettergrade = "B"  or 
     lettergrade = "B+" then output grade_b1 ; /* using OR operator */
 
 /* create the data-set "grade_b2" to retain all students who got a "B" grade */
  if lettergrade = "B-" |  
     lettergrade = "B"  |  
     lettergrade = "B+" then output grade_b2 ; /* using OR "|" operator */
 
 /* create the data-set "grade_b3" to retain all students who got a "B" grade */
  if lettergrade in ("B-","B","B+") then output grade_b3 ; /* using IN operator */
 
 /* using LIKE (wildcard) operator: 
    any lettergrade that starts with the letter 'C' are retained */
 if lettergrade =: 'C'  then output grade_c  ; 
 
run;


```

#### Form subset datasets using observation number (in-built function). 

For example, keep only the students with the top (bottom) five scores in the data-set. *Hint: A descending sort puts the top scorers on top, whereas an ascending sort puts the sottom scorers on the top.*


*SAS code:*

```c

proc sort data=work.merged_data; /* Sort the main data-set */
 by descending cscore; /* descending sort */
run;
 
data top5; /* Creating a SAS data-set "top5" */
 set merged_data; 
 if _n_ <= 5; /* retain only the first 5 observations */
run;
 
proc sort data=work.merged_data; /* Sort the main data-set */
 by cscore; /* ascending sort */
run;
 
data bottom5; /* Creating a SAS data-set "bottom5" */
 set merged_data;  
 if _n_ <= 5; /* retain only the first 5 observations */
run;


```


___


## Practice Exercises

Repeat the grade computation if the three quizzes (100 points each), two exams (200 points each), and a project (500 points) contributes 20%, 40%, and 30%, respectively, to the student's grade. The remaining 10% of the grade is based on class participation (100 points). Groups 1 and 2 obtained 85 points each in class participation. Groups 3 and 4 obtained 65 points each in class participation. 

#### **Cumulative Score, now, is given as follows:**

$$
\begin{align}
\text{Score} = &0.2 \times \frac{(\text{Quiz1} + \text{Quiz2} + \text{Quiz3})}{3} + \\\\\\ 
               &0.4 \times \frac{(\text{Exam1} + \text{Exam2})}{4} + \\\\\\
               &0.3 \times \frac{\text{Project}}{5} + \\\\\\ 
               &0.1 \times \text{Class Participation}
\end{align}
$$

Also, all plus-minus grade levels are abolished. The new grade scheme is as follows.


| Letter Grade | Score    |
|:------------:|:--------:|
| A            | 90 & up  |
| B            | 80       |
| C            | 70       |
| D            | 60       |
| F            | Below 50 |

All other information remains the same as before. Create grade, top5, and bottom5 datasets, and PRINT them on screen.



___



# Road map


- [x] Data Input
- [x] Data Manipulation
- [x] Some useful PROC steps
- [x] Merging and subsetting a dataset
- [ ] Compute descriptive statistics
- [ ] Compute test of differences
- [ ] Ordinary Least Squares
- [ ] Probit/Logit Regression
- [ ] DO loops 
- [ ] WHILE loops
- [ ] NESTED loops


___
