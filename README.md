# Overview

Welcome to my analysis of the data job market, specifically targeting data analyst roles. This project aims to enhance understanding and navigation of the job market by examining the most lucrative and in-demand skills. The data, obtained from Luke Barousse's Python Course, serves as the basis for this analysis, offering detailed insights into job titles, salaries, locations, and critical skills. Using a range of Python scripts, I investigate key questions such as the most sought-after skills, salary trends, and the relationship between demand and salary in the field of data analytics.



# The Questions

Here are the questions I aim to address in my project:

1. Which skills are most sought after for the top three most popular data roles?
2. What are the trends in in-demand skills for Data Analysts?
3. How do job roles and skills impact salary for Data Analysts?
4. What are the optimal skills for Data Analysts to acquire, considering both high demand and high pay?

# Tools I Used

For my in-depth exploration of the data analyst job market, I utilized several key tools:

Python: The core of my analysis, enabling me to process and extract valuable insights from the data. I employed various 

Python libraries:

Pandas:     Used for data manipulation and analysis.
Matplotlib: Employed for visualizing the data.
Seaborn:    Assisted in creating more sophisticated visuals.

Jupyter Notebooks: Facilitated running my Python scripts while integrating notes and analysis.

Visual Studio Code: My primary environment for executing Python scripts.

Git & GitHub: Crucial for version control and sharing my code and analysis, supporting collaboration and project management.

# Data Preparation and Cleanup

This section details the steps undertaken to prepare the data for analysis, focusing on ensuring its accuracy and usability.

Import & Clean Up Data

``` python

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

# Filter US Jobs

To concentrate my analysis on the U.S. job market, I apply filters to the dataset to focus specifically on roles located in the United States.

``` python
df_US = df[df['job_country'] == 'United States']
```

# The Analysis

## 1. Whar are the most demanded skills for the top 3 most popular data roles?

To identify the most in-demand skills for the top three most popular data roles, I filtered the most sought-after positions and compiled the top five skills for each of these roles. This analysis provides valuable insights into the key skills to focus on, depending on the specific role you aim to pursue.

View my notebook with detailed steps here:
[skills count ](Project\skills_count.ipynb)

### Visualize Data

``` python 
fig, ax = plt.subplots(len(job_title_list),1)
for i, title in enumerate(job_title_list):
    df_plot = df_count_skills[df_count_skills['job_title_short'] == title].head(5)
    df_plot.plot(kind='barh', x='job_skills', y='skill_count', ax=ax[i], title=title)
    ax[i].invert_yaxis()
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)
plt.suptitle('Counts of Top 5 skills in job postings', fontsize=20)
plt.tight_layout(h_pad=0.5) 
plt.show()
```

### Results 

![Chart for  top skills for top 3 data jobs](Project\Images\skill_demand_top3_data_roles.png)


### Insights

- Python is the most sought-after skill across all top three data roles, particularly for Data Scientists (72%) and Data Engineers (65%). 
- SQL is highly requested for both Data Analysts and Data Scientists, with over 50% of job postings listing it as a requirement. 
- Data Engineers, however, need more specialized cloud skills like AWS, Azure, and Spark, whereas Data Analysts and Data Scientists are expected to be proficient in analysis and visualization tools such as Excel and Tableau.

## 2. How are in-demand skills trending for Data Analysts?

### Visualize data 

```python

from matplotlib.ticker import PercentFormatter
plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))
for i in range(5):
    plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i])
plt.show()

```
### Results

![Trending Top skills for Data Analysts in the US]
(Project\Images\trending top skills for data analysts in US.png)

*Bar graph vizualizing the trending top skills for data analysts in the US in 2023.* 

### Insights

- SQL remains the most consistently sought-after skill throughout the year, though there is a gradual decline in its demand.
- Excel sees a notable rise in demand starting around September, eventually surpassing both Python and Tableau by the year's end. 
- Python and Tableau maintain relatively stable demand, with some fluctuations, but continue to be essential skills for data analysts. Meanwhile, Power BI, though less in demand compared to the others, shows an upward trend toward the end of the year.

# 3. How well do jobs and skills pay for Data Analysts?

## Salary Analysis for Data Nerds

### Visualize data

```Python 

sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order_list)
sns.set_theme(style='ticks')

plt.title('Salary distributions in the United States')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0, 600000)
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```

### Results
![Salary Distributions of data jobs in US]
()

*Box plot visualizing the distribution*

### Insights

- Salary ranges vary significantly across different job titles. Senior Data Scientist roles often have the highest earning potential, reaching up to $600K, reflecting the industry's strong emphasis on advanced data skills and experience.

- Senior Data Engineers and Senior Data Scientists exhibit a notable number of outliers on the higher end of the salary spectrum, indicating that exceptional skills or circumstances can lead to significantly higher pay in these roles. In contrast, Data Analyst positions show more consistency in salary with fewer outliers.  

- Median salaries tend to rise with the seniority and specialization of roles. Senior Data Scientist and Senior Data Engineer positions not only command higher median salaries but also exhibit a wider range in typical compensation, reflecting greater variability as responsibilities increase.


### Highest paid skills vs pay for In-Demand skills for Data Analysts?

#### Visualize data

```Python 

fig, ax = plt.subplots(2,1)
sns.set_theme(style='ticks')

#visualization for Top 10 highest paid skills for Data Analysts in US
sns.barplot(data=df_DA_US_top_pay_skills, x='median', y=df_DA_US_top_pay_skills.index, hue='median', ax=ax[0], palette='dark:g_r')
ax[0].legend().remove()
ax[0].set_title('TOP 10 Highest paid skills for Data Analysts in US')
ax[0].set_xlabel('')
ax[0].set_ylabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))

sns.barplot(data=df_DA_US_popular_skills_pay, x='median', y=df_DA_US_popular_skills_pay.index, hue='median', ax=ax[1], palette='dark:b_r')
ax[1].legend().remove()
ax[1].set_title('TOP 10 In-Demand skills for Data Analysts in US')
ax[1].set_xlabel('')
ax[1].set_ylabel('')
ax[1].set_xlim(ax[0].get_xlim())
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))
plt.tight_layout()
plt.show()
```

### Results
![Highest paid skills vs In-demand skills for data analysts]
()

*Two separate bar plots visualizing highest paid skills vs in-demand skills*

### Insights

- The top graph shows that specialized technical skills such as 'dpyrl', 'Bitbucket', and 'GitLab' are linked to higher salaries, with some reaching up to $200K. This suggests that advanced technical proficiency can significantly enhance earning potential.

- The bottom graph reveals that foundational skills such as 'Excel', 'PowerPoint', and 'SQL' are the most in-demand, although they may not command the highest salaries. This underscores the importance of these core skills for data analysts.

- There is a clear distinction between the highest-paying skills and the most in-demand skills. Data analysts aiming to maximize their career potential should focus on developing a diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.

# 4. What is the most optimal skill to learn for Data Analysts?


#### visualize data 

``` python
sns.scatterplot(
    data = df_DA_skills_color_coding,
    x='skill_percent',
    y='median_salary',
    hue='technology',
    
)


plt.show()
```

#### Results

![most optimal skills for data analysts in th US]
()

*A scatter plot visuliazing the most optimal skills to learn for a data analyst in the US.*

#### Insights

- The scatter plot reveals that programming skills (highlighted in blue) generally cluster around higher salary ranges, suggesting that expertise in programming could lead to greater earning potential within the data analytics field.

- Database skills (highlighted in orange), such as Oracle and SQL Server, are linked with some of the top salaries among data analyst tools, highlighting the high demand and value placed on data management and manipulation skills in the industry.

- Analyst tools (highlighted in green), including Tableau and Power BI, are commonly featured in job postings and command competitive salaries, indicating their essential role in current data roles. This category not only offers strong salary prospects but also demonstrates versatility across various data-related tasks.

# Conclulsion


This exploration of the data analyst job market has proven highly insightful, shedding light on the key skills and trends shaping this dynamic field. The findings offer valuable guidance for those aiming to advance their careers in data analytics. As the market evolves, continuous analysis will be crucial for staying competitive. This project serves as a solid foundation for future investigations and emphasizes the need for ongoing learning and adaptability in the data field.













