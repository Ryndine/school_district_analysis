# School District Analysis

## Objective: 
The goal of this project is to provide a statistical analysis into the performance of the provided school districts.

## Tools & databases used:
- Jupyter
- Pandas

## Preparing analysis:

**Cleaning the data:**  

First I quickly check to see if the data contains null values anywhere, which it didn't.

Upon further inspection of the data I see that students have prefixes and suffixes attached to their names. I want to remove these so I have only their first and last names. In order to do this I run this code:
```
# Make a list of all the students to iterate through
student_names = student_data['student_name'].tolist()
# Find the students who have more than a first and last name
students_to_fix = []
for name in student_names:
    if len(name.split()) >= 3:
        students_to_fix.append(name)
# create a list of prefixes
prefixes = []
for name in students_to_fix:
    if len(name.split()[0]) <= 4:
        if name.split()[0] not in prefixes:
            prefixes.append(name.split()[0])
        else:
            pass
print(prefixes)
# create a list of suffixes
suffixes = []
for name in students_to_fix:
    if len(name.split()[-1]) <= 3:
        if name.split()[-1] not in suffixes:
            suffixes.append(name.split()[-1])
        else:
            pass
print(suffixes)
# Lastly I look at the results and pull out all the prefixes and suffixes.
prefixes_suffixes = ['Dr. ', 'Mr. ','Ms. ', 'Mrs. ', 'Miss ', ' MD', ' DDS', ' DVM', ' PhD']
# Then I interate through the students and cleanup their names.
for word in prefixes_suffixes:
    student_data['student_name'] = student_data['student_name'].str.replace(word,'')
# Output results to a new csv for use.
cleaned_file_path = R'Resources\cleaned_students.csv'
if os.path.exists(cleaned_file_path):
    os.remove(cleaned_file_path)
    student_data.to_csv(cleaned_file_path)
else:
    student_data.to_csv(cleaned_file_path)
```
After cleaning I'm merging the data then using many different groupings of the data in order to return statistics.

# School distract data:

<img src="https://github.com/Ryndine/school_district_analysis/blob/main/Analysis/district_statistical_analysis.jpg">

First I just want to see the overall picture the dataset presents. We can see that overall the students are not doing as well as they could be. So I want to break down this data further in order to see the smaller details and if there are correlations in the data.

<img src="https://github.com/Ryndine/school_district_analysis/blob/main/Analysis/per_school_statistics.jpg">

Looking at the overall analysis for each high school the first thing that stands out is charter schools perform much better than district schools, but also have less students in their dataset. However, on average the charter schools are have less budget per student which indicates they're possibly utilizing their budget better.
<br/><br/>
<table>
  <tr>
    <td>Top Schools</td>
  </tr>
  <tr>
    <td><img src="https://github.com/Ryndine/school_district_analysis/blob/main/Analysis/top_schools.jpg"></td>
  </tr>
  <tr>
    <td>Bottom Schools</td>
  </tr>
  <tr>
    <td><img src="https://github.com/Ryndine/school_district_analysis/blob/main/Analysis/bottom_schools.jpg"></td>
  </tr>
 </table>

Looking at the top and bottom schools, we clearly see that all the top schools are charter and all the bottom are district. However, upon further inspection I see that district school have on a low end, nearly more than double the students that the charter schools have. This drastic difference in the amount of students may be influencing the results of the data. The more students a school has the more the averages can fluctuate.

<img src="https://github.com/Ryndine/school_district_analysis/blob/main/Analysis/per_grade_statistics.jpg">
Next I want to expand this data and look at how each grade is performing within each school. According to this table I see that math scores across all schools and grades are worse than reading. Also, for each school there aren't any outliers between each grades, all grades are performing within each other. There doesn't seem to be any favoritism in the school towards any single grade.

<img src="https://github.com/Ryndine/school_district_analysis/blob/main/Analysis/per_student_spending.jpg">
Diving further into the data I want to see if there are corerlations between spending budget and performance. I decided to bin schools based on ranges of the budget per student. Since all the schools had roughly the same spending amount per student. Surprisingly we see that the less budget per student, the better the performance is. Looking back on the data though we know that charters schools overall have less budget so this result actually makes sense. Because of the previous analsysis I can't declare this as causation.

<img src="https://github.com/Ryndine/school_district_analysis/blob/main/Analysis/school_size.jpg">
The next binning I wanted to do was school sizes. The results here verify that the less students a school has the better the results. This falls in line with my previous assumption that it's possible that with the inclusion of more students the datasets become influenced. However, this may be a good indication of causation.

<img src="https://github.com/Ryndine/school_district_analysis/blob/main/Analysis/school_type.jpg">
Final analysis on the data I wanted to break down the overall charter vs district statistics. As expected charter schools out perform district schools.

# Verdict

I think after running these statistical analysis, the main take away is that there seems to be correlation between how many students are in a high school and how well the students perform in that school. According to these results it seems that in order to better influence how well students are educated, the focus may need to be towards expanding how many schools we have and downsizing students per school. Simply increasing budget doesn't indicate that there will be any improvements to education provided to the students.
