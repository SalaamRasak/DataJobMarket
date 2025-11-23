# Overview
Welcome to my analysis of the data job market project. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the most available jobs and in-demand skills. Through a series of Python scripts, I explored key questions, such as the most demanded skills, available data jobs, salary trends, among others.

# The Questions
Below are the questions I answered in my project:
1. What are the top three jobs posted in the United State monthly?
3. What are the salary distributions of Data Analyst, Data Engineer, and Data Scientist in the United States?
4. How well do jobs and skills pay for Data Analysts?
5. What are the optimal skills for data analysts to learn? (High Demand AND High Paying) 

# Tools I Used
- **Python:** The backbone of my analysis, allowing me to analyze the data and find critical insights. I also used the following Python libraries:
    - **Pandas Library:** This was used to analyze the data. 
    - **Matplotlib Library:** I visualized the data.
    - **Seaborn Library:** Helped me create more advanced visuals. 
- **Jupyter Notebooks:** The tool I used to run my Python scripts which let me easily include my notes and analysis.
- **Visual Studio Code:** My go-to for executing my Python scripts.
- **Git & GitHub:** Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

```python
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Loading Data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```

## Filter US Jobs
To focus my analysis on the U.S. job market, I applied filters to the dataset, narrowing down to roles based in the United States.

```python
df_US = df[df['job_country'] == 'United States']

```

# The Analysis
## 1. What are the top three jobs posted in the United State monthly?

```python
df_US_pivot[top_three].plot(kind='line', linewidth=3, linestyle=':', colormap='viridis') 
plt.xlabel('Job Posted by Months')
plt.ylabel('Number of Jobs Posted')
plt.title('Top Three Most Posted Jobs in the US by Months')
plt.show()
```

### Results

<img src="/Images/most_posted_jobs.png" alt="Top 3 posted jobs in the US" width="600">

### Insight:
- Data Analyst has the highest number of jobs posted, while Data Engineer has the least number of jobs posted. 

## 2. What are the salary distributions of Data Analyst, Data Engineer, and Data Scientist in the United States?

```python
job_titles = ['Data Analyst', 'Data Engineer', 'Data Scientist']
df_US = df[(df['job_title_short'].isin(job_titles)) & (df['job_country'] == 'United States')].copy()
df_US = df_US.dropna(subset=['salary_year_avg'])
job_list = [df_US[df_US['job_title_short']== job_title]['salary_year_avg'] for job_title in job_titles]
plt.figure(figsize=(8, 6))
sns.boxplot(data=df_US, x='salary_year_avg', y='job_title_short', order=job_titles)
plt.title('Salary Distribution in the United States')
plt.xlabel('Yearly Salary ($USD)')
plt.ylabel('')
ax = plt.gca() 
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda y, _: f'${int(y/1000)}K'))
plt.show()
```
### Results
<img src="/Images/Salary Distributions.png" alt="Salary Distributions of Data Analyst, Data Engineer, and Data Scientist in the US" width="600">

### Insight:
- Data Scientist appears to have the highest average salary in the US, while Data Analyst has the least average salary. 

## 3. What is the number of jobs posted in the first quarter? 

```python
df_US_pivot[top_three_jobs_Q1].loc[df_US_pivot.index.isin(['January', 'February', 'March'])].plot(kind="bar") 
```

#### Results
<img src="/Images/Quarter1.png" alt="Salary Distributions of Data Analyst, Data Engineer, and Data Scientist in the US" width="600">

# What I Learned
Throughout this project, I deepened my understanding of the data analyst job market and enhanced my technical skills in Python, especially in data manipulation and visualization. Here are a few specific things I learned:

- **Advanced Python Usage**: Utilizing libraries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualization, and other libraries helped me perform complex data analysis tasks more efficiently.
- **Data Cleaning Importance**: I learned that thorough data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accuracy of insights derived from the data.
- **Strategic Skill Analysis**: The project emphasized the importance of aligning one's skills with market demand. Understanding the relationship between skill demand, salary, and job availability allows for more strategic career planning in the tech industry.

