# ANALYSIS 

## 1. What are the most in-demand skills for Business Analyst  the top 3 most popular data roles?
To find the most in demand  skills for these stratitegically selected roles, the data set is cleaned and  filtered for these job titles in  a chosen geographical area (United States). The top 5 skills for each job title is collected and plotted  in a subplot horizontal bar chart.
This query serves to inform and advise  myself and other job seekers to about the most required skills for the select data roles.

View my notebook with detailed steps here: [here](3_project\2_skill_count.ipynb)

### Visualize Data
```python
fig,ax=plt.subplots(len(job_titles),1)

sns.set_theme(style='ticks')
for i,job_title in enumerate(job_titles):
    df_plot = df_merged[df_merged['job_title_short']== job_title].head(5)
    sns.barplot(data=df_plot,x='skill_percent', y='job_skills', ax=ax[i], hue='skill_percent',palette='dark:b_r',legend=False)
    #df_plot.plot(kind= 'barh', x='job_skills', y='skill_count', ax=ax[i], title=job_title,legend=False)
    
plt.show()
```
### Results
View the visualization for the top skills
![Here](3_project\images\skill_demand_BA_and_top_3_jobs.png)

### Insights
- Python and SQL skills are both demanded for all four jobs with Data Scientist jobs requiring Python the most. SQL appears to be the bread and butter for Data Engineers but it is closely matched by Python. Business analyst jobs appear to require python the least with 19% of the total Business analyst jobs requiring it.
- Business Analyst jobs do not show a clear favorite in skill reqiurement as more than half(52%) of jobs posted do not require its seemely leading skills. Python SQL and Tableau are common all in demand skills for Business Analyst,Data Analysts and Data Scientists, with the last two reqiuring more statistical tools/skills in SAS and or R
- Data Engineer appears to be the most Technical and fairly outlandish among the 4 jobs as it requiring cloud management skills.






