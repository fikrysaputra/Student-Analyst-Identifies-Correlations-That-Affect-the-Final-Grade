# Student Analyst Identifies Correlations That Affect the Final Grade
This project do Analyst about Student and find which high correlation factor that affect final grade to student.
Dataset source https://www.kaggle.com/datasets/whenamancodes/student-performance

# About Dataset
This data approach student achievement in secondary education of two Portuguese schools. The data attributes include student grades, demographic, social and school related features) and it was collected by using school reports and questionnaires. Two datasets are provided regarding the performance in two distinct subjects: Mathematics (mat) and Portuguese language (por). In [Cortez and Silva, 2008], the two datasets were modeled under binary/five-level classification and regression tasks. Important note: the target attribute G3 has a strong correlation with attributes G2 and G1. This occurs because G3 is the final year grade (issued at the 3rd period), while G1 and G2 correspond to the 1st and 2nd period grades. It is more difficult to predict G3 without G2 and G1, but such prediction is much more useful (see paper source for more details). **This Project only find for Mathematics**

| Column      | Description                                                                                                                                                    |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `school`    | Student's school (binary: 'GP' - Gabriel Pereira or 'MS' - Mousinho da Silveira)                                                                               |
| `sex`       | Student's sex (binary: 'F' - female or 'M' - male)                                                                                                             |
| `age`       | Student's age (numeric: from 15 to 22)                                                                                                                         |
| `address`   | Student's home address type (binary: 'U' - urban or 'R' - rural)                                                                                               |
| `famsize`   | Family size (binary: 'LE3' - less or equal to 3 or 'GT3' - greater than 3)                                                                                     |
| `Pstatus`   | Parent's cohabitation status (binary: 'T' - living together or 'A' - apart)                                                                                    |
| `Medu`      | Mother's education (numeric: 0 - none, 1 - primary education (4th grade), 2 - 5th to 9th grade, 3 - secondary education, or 4 - higher education)              |
| `Fedu`      | Father's education (numeric: 0 - none, 1 - primary education (4th grade), 2 - 5th to 9th grade, 3 - secondary education, or 4 - higher education)              |
| `Mjob`      | Mother's job (nominal: 'teacher', 'health' care related, civil 'services' (e.g., administrative or police), 'at_home', or 'other')                            |
| `Fjob`      | Father's job (nominal: 'teacher', 'health' care related, civil 'services' (e.g., administrative or police), 'at_home', or 'other')                            |
| `reason`    | Reason to choose this school (nominal: close to 'home', school 'reputation', 'course' preference, or 'other')                                                 |
| `guardian`  | Student's guardian (nominal: 'mother', 'father', or 'other')                                                                                                   |
| `traveltime`| Home to school travel time (numeric: 1 - <15 min., 2 - 15 to 30 min., 3 - 30 min. to 1 hour, or 4 - >1 hour)                                                  |
| `studytime` | Weekly study time (numeric: 1 - <2 hours, 2 - 2 to 5 hours, 3 - 5 to 10 hours, or 4 - >10 hours)                                                              |
| `failures`  | Number of past class failures (numeric: n if 1<=n<3, else 4)                                                                                                   |
| `schoolsup` | Extra educational support (binary: yes or no)                                                                                                                  |
| `famsup`    | Family educational support (binary: yes or no)                                                                                                                 |
| `paid`      | Extra paid classes within the course subject (Math or Portuguese) (binary: yes or no)                                                                          |
| `activities`| Extra-curricular activities (binary: yes or no)                                                                                                                |
| `nursery`   | Attended nursery school (binary: yes or no)                                                                                                                    |
| `higher`    | Wants to take higher education (binary: yes or no)                                                                                                             |
| `internet`  | Internet access at home (binary: yes or no)                                                                                                                    |
| `romantic`  | In a romantic relationship (binary: yes or no)                                                                                                                 |
| `famrel`    | Quality of family relationships (numeric: from 1 - very bad to 5 - excellent)                                                                                  |
| `freetime`  | Free time after school (numeric: from 1 - very low to 5 - very high)                                                                                           |
| `goout`     | Going out with friends (numeric: from 1 - very low to 5 - very high)                                                                                           |
| `Dalc`      | Workday alcohol consumption (numeric: from 1 - very low to 5 - very high)                                                                                      |
| `Walc`      | Weekend alcohol consumption (numeric: from 1 - very low to 5 - very high)                                                                                      |
| `health`    | Current health status (numeric: from 1 - very bad to 5 - very good)                                                                                            |
| `absences`  | Number of school absences (numeric: from 0 to 93)                                                                                                              |

These grades are related with the course subject, Math :
| Grade | Description                                             |
|-------|---------------------------------------------------------|
| `G1`  | First period grade (numeric: from 0 to 20)              |
| `G2`  | Second period grade (numeric: from 0 to 20)             |
| `G3`  | Final grade (numeric: from 0 to 20, serves as the target output) |

# Exploratroy Data Analyst
Check Column
```python
df_student.columns
```
Index(['school', 'sex', 'age', 'address', 'famsize', 'Pstatus', 'Medu', 'Fedu',
       'Mjob', 'Fjob', 'reason', 'guardian', 'traveltime', 'studytime',
       'failures', 'schoolsup', 'famsup', 'paid', 'activities', 'nursery',
       'higher', 'internet', 'romantic', 'famrel', 'freetime', 'goout', 'Dalc',
       'Walc', 'health', 'absences', 'G1', 'G2', 'G3'],
      dtype='object')
# Check Null Data
```python
df_student.isnull().sum()
```

# Check Duplicate
```python
df_student.duplicated().sum()
```
 idx | school | sex | age | address | famsize | Pstatus | Medu | Fedu | Mjob   | Fjob    | ... | famrel | freetime | goout | Dalc | Walc | health | absences | G1 | G2 | G3 |
|-----|--------|-----|-----|---------|---------|---------|------|------|--------|---------|-----|--------|----------|-------|------|------|--------|----------|----|----|----|
| 395 | GP     | F   | 18  | U       | GT3     | A       | 4    | 4    | at_home | teacher | ... | 4      | 3        | 4     | 1    | 1    | 3      | 6        | 5  | 6  | 6  |
| 396 | MS     | M   | 19  | R       | GT3     | T       | 1    | 1    | other   | services| ... | 4      | 3        | 2     | 1    | 3    | 5      | 0        | 6  | 5  | 0  |

Duplicates data is eligimates, didn't need to handling

# Show Student that have 0 Final Grade
G1	first period grade (numeric: from 0 to 20)
G2	second period grade (numeric: from 0 to 20)
G3	final grade (numeric: from 0 to 20, output target)
```python
df_student_zero_g3 = df_student[df_student["G3"] == 0.0]
df_student_zero_g3
```

# Describe
```python
df_student.describe()
```
| Statistic | Age       | Medu      | Fedu      | Traveltime | Studytime | Failures | Famrel    | Freetime  | Goout     | Dalc      | Walc      | Health    | Absences  | G1        | G2        | G3        |
|-----------|-----------|-----------|-----------|------------|-----------|----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
| Count     | 397.000   | 397.000   | 397.000   | 397.000    | 397.000   | 397.000  | 397.000   | 397.000   | 397.000   | 397.000   | 397.000   | 397.000   | 397.000   | 397.000   | 397.000   | 397.000   |
| Mean      | 16.705    | 2.748     | 2.521     | 1.451      | 2.033     | 0.335    | 3.945     | 3.234     | 3.108     | 1.479     | 2.290     | 3.557     | 5.695     | 10.882    | 10.688    | 10.378    |
| Std Dev   | 1.280     | 1.097     | 1.091     | 0.697      | 0.839     | 0.743    | 0.894     | 0.996     | 1.113     | 0.889     | 1.287     | 1.389     | 7.988     | 3.333     | 3.770     | 4.605     |
| Min       | 15.000    | 0.000     | 0.000     | 1.000      | 1.000     | 0.000    | 1.000     | 1.000     | 1.000     | 1.000     | 1.000     | 1.000     | 0.000     | 3.000     | 0.000     | 0.000     |
| 25%       | 16.000    | 2.000     | 2.000     | 1.000      | 1.000     | 0.000    | 4.000     | 3.000     | 2.000     | 1.000     | 1.000     | 3.000     | 0.000     | 8.000     | 9.000     | 8.000     |
| 50%       | 17.000    | 3.000     | 2.000     | 1.000      | 2.000     | 0.000    | 4.000     | 3.000     | 3.000     | 1.000     | 2.000     | 4.000     | 4.000     | 11.000    | 11.000    | 11.000    |
| 75%       | 18.000    | 4.000     | 3.000     | 2.000      | 2.000     | 0.000    | 5.000     | 4.000     | 4.000     | 2.000     | 3.000     | 5.000     | 8.000     | 13.000    | 13.000    | 14.000    |
| Max       | 22.000    | 4.000     | 4.000     | 4.000      | 4.000     | 3.000    | 5.000     | 5.000     | 5.000     | 5.000     | 5.000     | 5.000     | 75.000    | 19.000    | 19.000    | 20.000    |

# Gender Distribution
![gender](image/gender.png)

# Age Distribution
![age](image/age.png)

# Travel Time Distribution
![travel](image/travel.png)

# Study Time Distribution
![study](image/study.png)

# Free Time After School Distribution
![free](image/free.png)

# Go Out With Friends Distribution
![out](image/out.png)

# Absences Distribution
![absen](image/absen.png)

# Mother Education Distribution
![medu](image/medu.png)

# Father Education Distribution
![fedu](image/fedu.png)

# First Period Grade
![g1](image/g1.png)

# Second Period Grade
![g2](image/g2.png)

# Final Grade
![g3](image/g3.png)

# Find Variable Correlation and G3
In this case, Median is used to find correlation
![failurecrr](https://github.com/user-attachments/assets/908b3c50-4a3a-4d45-9974-9b6d709b39d1)
![dalc](https://github.com/user-attachments/assets/3dcc2b23-9849-41bc-b2cc-86eefab8de2c)
![crrs](https://github.com/user-attachments/assets/24bd533f-c7ab-4595-b7d4-466640b74731)
![crr](https://github.com/user-attachments/assets/8d4feef5-d885-48ed-8d99-adae9997a50b)
![activities](https://github.com/user-attachments/assets/383dfd11-68be-4745-84ff-0835bba055a3)
![walc](https://github.com/user-attachments/assets/a9f60da3-0650-450a-9273-b083b6506ad5)
![travelcrr](https://github.com/user-attachments/assets/d9de33a9-a1c3-424d-ab4a-fa18d28930c9)
![studytimecrr](https://github.com/user-attachments/assets/0c90ab55-c513-45b1-8118-4d561e8e9568)
![scsupp](https://github.com/user-attachments/assets/c7c375ec-f0b1-4c2a-aec5-6f6ff3049ad8)
![romantic](https://github.com/user-attachments/assets/077e8af0-8369-4711-9ee8-2d80e0c6166c)
![paid](https://github.com/user-attachments/assets/7c26b55a-f263-423f-9df1-5f3b0c2bb803)
![mjobcrr](https://github.com/user-attachments/assets/23c4f67b-cf0d-48eb-9c9a-b9653c2fd2d2)
![meducrr](https://github.com/user-attachments/assets/03250b84-ecb9-4af3-8aa4-c7b38919e44a)
![internet](https://github.com/user-attachments/assets/6026a0c5-3aa1-4f4c-97ae-a31b0e86a30a)
![highercrr](https://github.com/user-attachments/assets/a0dc5963-3813-48da-bcff-6c4ff095668e)
![gooutcrr](https://github.com/user-attachments/assets/1ff3ea7e-2210-4308-a864-fa46e6d2ffc8)
![fjobcrr](https://github.com/user-attachments/assets/14dc9d7e-da62-466a-81f4-ab27dcb1cc10)
![famsup](https://github.com/user-attachments/assets/bfc58521-560c-4892-8fcc-09c9c68d1639)
![famrelcrr](https://github.com/user-attachments/assets/5b7d530d-a364-4add-b74e-dd0af7fb8cbc)


# Correlation Coefficient and Heatmap
![crrg3](https://github.com/user-attachments/assets/67dc11a9-0335-4ceb-87e0-062f9ef3fa8f)

Heatmap
![heatmap](https://github.com/user-attachments/assets/64702d9d-fd0f-431f-872b-0122520b6af6)


# Conclusion
In summary, prior grades (G1 and G2) are the most significant predictors of the final grade, while factors like parental education and study time contribute positively, though to a lesser extent. Past failures negatively affect final grades. Age, family relations, and social activities (like going out) have relatively minor correlations with G3. Although these factors do play a role in student life, they are less predictive of final academic outcomes compared to prior grades and study-related variables. The analysis concludes that academic consistency (G1 and G2), parental education, study habits, and minimal past failures are key factors influencing a student's final grade (G3).
