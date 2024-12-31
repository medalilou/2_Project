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

## 2.How are in-demand skills trending for Data Analysts?
To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.
View my notebook with detailed steps here: [3_Skills_Trend.ipynb](3_Skills_Trend.ipynb)

### Visualize Data
```Python
# Plot Line Chart of the Top 5 Skills for Data Analysts in Germany
df_DA_GE_Pivot.iloc[:, :5].plot(kind='line')

sns.set_theme(style='ticks')
sns.despine() # remove top and right spines
plt.title('Trending Top Skills for Data Analysts in Germany')
plt.ylabel('Count')
plt.xlabel('2023')
plt.ylim(0, 500)

plt.show()
```

### Results
![Trending Top Skills for Data Analysts in Germany in 2023.](images\skills_trend.png)

### Insights
- SQL remains the most consistently demanded skill throughout the year.
- Python experienced a significant increase in demand starting around September.
- Power BI, Excel and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts.

## 3. How well do jobs and skills pay for Data Analysts?
To identify the highest-paying roles and skills, I only got jobs in Germany and looked at their median salary. But first I looked at the salary distributions of common data jobs like Data Scientist, Data Engineer, and Data Analyst, to get an idea of which jobs are paid the most.

View my notebook with detailed steps here: [4_Salary_Analysis.ipynb](4_Salary_Analysis.ipynb)

### Visualize Data
```Python
# Plot Boxplot of Salary Distributions for Data Jobs in Germany
sns.boxplot(data=df_top6, x='salary_year_avg', y='job_title_short', order=job_order)
sns.set_theme(style='ticks')
sns.despine()

plt.title('Salary Distributions of Data Jobs in 2023')
plt.xlabel('Yearly Salary')
plt.ylabel('')
plt.xlim(0, 500000) 
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
### Results
![Salary Distributions of Data Jobs in 2023.](images\Salary Distributions of Data Jobs.png)

### Insights
- There's a significant variation in salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to $500K, indicating the high value placed on advanced data skills and experience in the industry.
- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with fewer outliers.
- The median salaries increase with the seniority and specialization of the roles. Senior roles (Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.

## Highest Paid & Most Demanded Skills for Data Analysts