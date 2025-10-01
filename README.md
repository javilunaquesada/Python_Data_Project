# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles in the US?

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions, and got the top 5 skills for each role. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I am targeting.

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](Project\2_Skill_Demand.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_percentage[df_skills_percentage['job_title_short'] == job_title].head(5)
    # df_plot.plot(kind='barh', x='job_skills', y='skill_percent', ax=ax[i], title=job_title)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_xlim(0, 78)                 # sets the range of x for the three graphics: [0, 78]

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va='center')

    if i != len(job_titles) - 1:   # remove the numbers in de x axe except for the last one
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=15)
fig.tight_layout(h_pad=0.5) # fix the overlap between the images
plt.show()
```

### Results

![Visualization of Top Skills for Data Nerds](Project\Images\skill_demand_all_data_roles.png)

### Insights

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).
- SQL is the most requested skill for Data Analyst and Data Scientists; it is in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, apperaring in 68% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analyst and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau)

## 2. How are in-demand skills trending for Data Analyst?

### Results
![Trending Top Skills for Data Analyst in the US](Project\Images\trending_skills.png)

### Insights
- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel experienced a significant increase in demand starting around September.
- Both Python and Tableau show relatively stable demand throughout the year. Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.

## 3 How well do job and skills pay for Data Analysts?

#### Results

![Salary distributions of Data Jobs in the US](Project\Images\salary_distrib.png)

#### Insights
- There's a significant variation in salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to $600K, indicating the high value placed on advanced data skills and experience in the industry.
- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with fewer outliers.
- The median salaries increase with the seniority and specialization of the roles. Senior roles (Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.
