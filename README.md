# The Analysis 
Each Jupyter notebook for this project aimed at investigating specific aspects of the data job market. Here’s how I approached each question:
## 1. What are the most demanded skills for the top 3 most popular data roles?
To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here: [2_skills_count.ipynb](2_Skills_Count.ipynb)

### Visualize Data
```Python
#Plot Percentage Count 
fig, ax = plt.subplots(len(top_3), 1)

sns.set_theme(style='ticks')
#Display Plots for the top 3 Job Titles
for i, job_title in enumerate(top_3):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5) #Top 5 Skills
    sns.barplot(data=df_plot, x='skill_percent',y= 'job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 70)
    # remove the x-axis tick labels for better readability
    if i != len(top_3) - 1:
        ax[i].set_xticks([])

    # label the percentage on the bars
    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va='center')
   
fig.suptitle('Likelihood of Skills Requested in Job Postings in Germany', fontsize=15)
fig.tight_layout(h_pad=0.8)  #Fix the overlap
plt.show()
```

### Results
![Visualization of top Skills for Data Roles in Germany](images\skills_demand.png)

### Insights
- Python is the most requested skill for Data Engineers and Data Scientists, with it in over half the job postings for both roles. For Data Analysts, SQL is the most sought-after skill, appearing in 41% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Power BI).
- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (62%) and Data Engineers (53%).

## How are in-demand skills trending for Data Analysts?
To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.