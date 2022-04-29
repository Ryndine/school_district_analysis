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

<img src=""
