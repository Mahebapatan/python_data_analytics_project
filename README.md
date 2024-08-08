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













