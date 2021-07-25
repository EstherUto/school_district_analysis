# School District Analysis

## Table of Contents

- [Overview of School District Analysis](#overview-of-school-district-analysis)
- [Analysis Results](#analysis-results)
  * [School District Analysis](#school-district-analysis)
  * [School Summary](#school-summary)
  * [Thomas High School students](#thomas-high-school-students)
    + [Effect of removing THS Ninth Graders math and reading scores by grade](#effect-of-removing-ths-ninth-graders-math-and-reading-scores-by-grade)
    + [Effect of removing THS Ninth Graders on scores by school spending](#effect-of-removing-ths-ninth-graders-on-scores-by-school-spending)
    + [Effect of removing THS Ninth Graders on scores by school size](#effect-of-removing-ths-ninth-graders-on-scores-by-school-size)
    + [Effect of removing THS Ninth Graders on scores by school type](#effect-of-removing-ths-ninth-graders-on-scores-by-school-type)
- [Summary](#summary)

## Overview of School District Analysis

The purpose of this analysis is to assist a school district data analyst, hereby refered to as client, in analyzing student scores from math and reading tests in various school districts and charters. The goal is to find the performance trends of the students in each school based on grades. Also to show if and how they are affected by factors such as school spending, school size and school type. The hope is that this analysis would assist the school board make the right decisions for each school to improve. At the point of this analysis, the total budget the school board had allocated to the 15 schools of interest was $24,649,428.

*Please note the data used for this analysis is protected under the Family Educational Rights and Privacy Act of 1974 (FERPA)*

## Analysis Results
**_Please refer to the `resources` folder to find the student and school `.csv` data sets. Please review the `PyCitySchools.ipynb` and `PyCitySchools_Challenge.ipynb` for full codes_**

As part of this analysis, the ninth graders that attend Thomas High School (THS) were a point of interest therefore two code files were made. One that included their grades (`PyCitySchools.ipynb`) and one that did not include the grades of the ninth graders at THS (`PyCitySchools_Challenge.ipynb`).

The first course of action was to clean up the names of the students. Meaning, prefixes and suffixes (i.e. "Dr. ", "Mr. ","Ms. ", "Mrs. ", "Miss ", " MD", " DDS", " DVM", " PhD") were removed from the student names. 
 
### School District Analysis

The student data set provided has a total of 39,170 students spread across 15 schools. To avoid working with two different variables and dataframes (df), the `student_data_df` and `school_data_df` were merged into a `school_data_complete_df` using the code below which resulted in Figure 1

```
# Combine the data into a single dataset
school_data_complete_df = pd.merge(student_data_df, school_data_df, how="left", on=["school_name", "school_name"])
school_data_complete_df.head()
```

**_FIGURE 1_**

As requested by the client, the ninth grade students scored were removed from the dataframe during the analysis. There are a total of 461 ninth grade students that attend THS, therefore the "new" student count becomes 38,709. The `.loc` method was used to make the ninth grade students test scores NaN as shown below.

```
student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"), "reading_score"] = np.nan
student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"), "math_score"] = np.nan
```

The district summary showing the total budget, the average scores for both math and reading, the percentage of students that passed in each test and the percentage of students that passed both their math and reading tests is shown in the image below.

**_FIGURE 2_**

From the values in the image, it is obvious that students on average do better in the reading test than in the math test with slightly over 85% of students have a reading score of 70% or higher. It seems however there is still room for improvement when it comes to students passing both math and reading with only about 65% of students succeeding in both tests.

### School Summary

The nest course of action was to find the breakdown of the budget per school and how much on average is invested per student in the school. The figure below shows a detailed information breakdown by school.

**_FIGURE 3_**

The average investment per student across the board is about $620.07. Huang High School has the highest allocated budget per student but the school's students have one of the lowest overall passing scores. On the other hand Wilson High School has the lowest allocated budget per student with one of the highest overall passing scores. This shows that a higher budget per student does not always provide good results. Griffin High School was the only school whose budget per student is above the mean budget per student with a relatively high overall passing result.

### Thomas High School students

The data for THS students was calculated relative to all students that took the test from thr 9th grade to the 10th grade. To this point, including them into the total count but not considering their grades causes for the summary values of THS to look very average and giving the impression the school would have to improve one way or the other. To remedy this, the 9th grade students and their data was removed and the variables for the THS students were recalculated. 

**_FIGURE 4_**

The sharp increase in test scores and overall passing is due to proper measurement as so far the 9th grade scores were not considered even if they were counted in the initial calculations. In comparison to the analysis first done including the grades of the 9th grade students, there is no major difference showing that students of all grades attending THS are performing extremely well in their courses.

#### Effect of removing THS Ninth Graders math and reading scores by grade

There was no effect of removing the THS 9th grades scores on the math and reading scores by grade for both THS and other schools.

#### Effect of removing THS Ninth Graders on scores by school spending

There was a small change in the scores by school spending when the THS 9th graders were not included. Figure 5 shows the school spending when including THS 9th graders and figure 6 shows excluding them.

**_FIGURE 5 School Spending including Thomas High School Ninth Graders_**


**_FIGURE 6 School Spending excluding Thomas High School Ninth Graders_**


In the spending bracket of $585 to $644, there is a an increase in scores across the board. Although there doesn't seem to be an effect when the spending is less that $585 or greater than $644.

#### Effect of removing THS Ninth Graders on scores by school size

There was no effect on the scores by school size for both THS and other schools.

#### Effect of removing THS Ninth Graders on scores by school type 

There was no effect on the scores by school type for both THS and other schools.


## Summary

There were a few slight differences when removing the THS 9th graders including:
- A slight decrease in the student grades for THS students meaning the 9th graders are excellent scorers.
- On the other hand, an increase in the grades across the school district in spending ranges between $585 to $644 per student. This may be due to less competition between the students.

