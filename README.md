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
![image](https://github.com/user-attachments/assets/fd892a7c-0ca2-4894-b492-9e79e7d8c8cb)



### Insights

- Python is the most sought-after skill across all top three data roles, particularly for Data Scientists (72%) and Data Engineers (65%). 
- SQL is highly requested for both Data Analysts and Data Scientists, with over 50% of job postings listing it as a requirement. 
- Data Engineers, however, need more specialized cloud skills like AWS, Azure, and Spark, whereas Data Analysts and Data Scientists are expected to be proficient in analysis and visualization tools such as Excel and Tableau.

