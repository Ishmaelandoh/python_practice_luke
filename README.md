# Overview

This is my first data analysis project using python.
I sourced data from lukebarousse huggingface repository and also got help and direction from his github repository and youtube channel. this project aims to analyze the data jobs in the United States. i compared data jobs by their counts,median,salaries and skill trends using internal python libraries and methods as well as external libraries like pandas,matplotlib,seaborn for visualization. 


The focus of the project was to draw reliable insights about Data Analyts jobs and the skills commonly required by employers in the United States. Comparisons were made with other select data jobs.I considered Business analyst jobs in the top skills analysis , Although Business Analyst is not a top 3 job by demand.

Through a series of python scripts, i explored key questions like: what are the; trend in the top data analyst skills, most in demand data analytics skills, highest paid data analyst skills, most optimal skills to learn considering salary and demand.

# The Questions
This project seeks to answer the following Questions :
1. What are the top skills for Business analysts jobs and the  top(3) Data jobs. 
2. What is the trend in the most in demand data analyst skills
3. How well do the data jobs and their skills pay
4. What are the most optimal Data Analyst skills to learn 


# Tools I Used
This exploration has been made possible by the power of some key data tools:

-Python: This has been my primary tool for this project. By accessing pre-defined functions,libraries and methods, I was able to extract and prepare the data for this project. The following libraries were key:

1. Pandas: This library has been crucial in the preparation and analysis of the data 
2. Matplotlib: This was used in visualization process
3. Seaborn : This library was used to create advanced visuals

-Jupyter Notebooks: This tools was used to run and edit  the python scripts by allowing  Notes and other great features.
-Visual Studio Code: This is the text editor for this project
-Git & GitHub : This tool was used for version control. You can find notes of this project in this repository




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

## 2. What's the Trend like for in-demand Data Analyst skills

To analyze the trend for the top skills for Data analyst jobs in 2023, I cleaned and filtered the dataframe. I then exploded and pivoted the dataframe by the skills and month respectively. The pivoted dataframe was then re-evaluated to calculated the percentages for each skill-month pair. The dataframe is then filtered for the top 5 columns and plotted using the seaborn library.

This query serves to help us understand th trend in the skills most required for Data Analyst jobs in the USA. I sought to understand the which skills are changing trend and at what pace are they changing.

View my notebook with detailed steps here:[here](3_project\3_skill_trend.ipynb)

## Visualize Data 
```python
sns.set_theme(style='ticks')
sns.lineplot(data=df_plot_pc, dashes=False,palette='tab10', legend=False)
plt. ylabel('LIKELIHOOD OF REQUEST FOR SKILL')
plt.xlabel('2023')
sns.despine()

from matplotlib.ticker import PercentFormatter
ax= plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))


for i in range(5):
    plt.text(11.5,df_plot_pc.iloc[11,i], df_plot_pc.columns[i])

plt.title('TREND OF DEMAND FOR THE TOP 5 DATA ANALYST SKILLS(USA)')
plt.tight_layout()
plt.show()
```
## Results
View the visualization of the skills trend here:![here](3_project\images\skill_trend_lineplot.png)
*Bar graph visualizing the trend in the top 5 skills for Data Analyst in 2023.*

### Insights
* Sql remain the most cosistently demanded skill for data analyst jobs but this demand shows a decline starting from November
- Excel comes in second as the most in-demand skills throught the year. It starts to rise and the end of the year.
+ Tableu and python have similar trend for the most part of the year. Python appears to be on an upward trajectory at the year end.
* Sas trends steadily within the year but significantly below the other skills
- Overall, None of these skills appear to take a nose dive to wards 0% so essentially they all remain important skills to learn in preparation for data analyst roles in the near future.


## 3. How well do jobs and skills pay for Data analyst
Her we compare Data analyst job's salaries to similar data jobs. 

view my notebook for detailed steps here: [Here](3_project\4_salary_analyses.ipynb)

### Visualize data
```python
sns.boxplot(data=df_US,x= 'salary_year_avg', y='job_title_short', order=job_order)
plt.xlim(0,700000)
plt.ylabel('')
plt.xlabel('SALARY')
ax= plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))
plt.title('SPREAD OF SALARIES OF TOP DATA JOBS IN USA')
plt.show()
```

### Results
view visualization for salary comparison here![here](3_project\images\boxplot.png)
*Boxplot showing the salary distribution for top 6 data jobs*

### Insight
-Median Salary:

Data Analysts have the lowest median salary compared to the other jobs. The median appears to be around $80K.
Senior Data Analysts earn significantly more, with a median around $130K.

-Salary Spread:

Data Analyst salaries are concentrated between $50K and $120K, with few outliers above $200K.
Senior roles like Senior Data Scientists and Senior Data Engineers have a wider salary spread, with a median near $180K to $200K and some salaries extending towards $600K or higher.

-Range of Salaries:

The range of salaries for Data Analysts is narrower compared to higher-level roles, such as Senior Data Scientists and Senior Data Engineers, whose salaries span from below $100K to well above $300K or $400K.
Data Scientists and Data Engineers (non-senior) have mid-level salary distributions, with salaries generally between $100K and $250K, still wider than Data Analysts.

-Outliers:

Outliers for Data Analysts are fewer and lower, while roles like Senior Data Scientists show many high outliers, indicating that top performers or specific markets can pay much more.
In summary, Data Analysts earn significantly less on average compared to higher-level positions like Data Scientists, Data Engineers, and Senior roles. Their salary distribution is also much narrower, with fewer high-paying opportunities.



## 4. What is the pay level of of the most in-demand data analyst skills
The purpose of this query is to understand how  much the high demand data analyst skills earns. We also sought to investigate the non-popular skills that earns more than these high-demand skills.




View my notebook for detailed of the query here[here](3_project\4_salary_analyses.ipynb)

### Visualize Data 
```python
fig,ax=plt.subplots(2,1)

sns.set_theme(style='ticks')
sns.barplot(df_plot_s, x='median', y='job_skills', ax=ax[0], hue='median', palette='dark:b_r',legend=False)
ax[0].set_title('TOP 10 HIGHEST PAID DATA ANALYST SKILLS')
ax[0].set_xlabel('MEDIAN SALARY (USD)')
ax[0].set_ylabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x,pos: f"${int(x/1000)}K"))
```

### Results
view visualization for salary comparison![here](3_project\images\high_pay_vs_high_demand.png)
* Subplotted barplots showing and comparing the median salaries of Top data analyst jobs by demand and by pay*

### Insights
-Highest Paid Skills:

Dplyr, Bitbucket, and GitLab are the top three highest-paid skills, with median salaries close to $200K.
Other skills like Hugging Face, Solidity, and Couchbase also command high median salaries, ranging from $125K to $175K.
These highly paid skills are specialized and associated with advanced or niche technologies, particularly in data management, machine learning (Hugging Face), and blockchain (Solidity).

-Most In-Demand Skills:

Common tools like Python, Tableau, and R are the most in-demand skills, with median salaries around $100K to $125K.
Widely used software such as Excel, SQL, and Power BI also appear in this list, but their median salaries are lower compared to the highly specialized skills from the top chart.

-Earnings Disparity:

The highest-paid skills command salaries that are nearly double those of the most in-demand skills. This suggests that while the in-demand skills are more common in the job market, specialized and emerging tools and platforms offer significantly higher pay.
In summary, the highest-paid data analyst skills are specialized and less common, while the most in-demand skills are more widespread but offer comparatively lower median salaries.

## 5. What is the most optimal skills  to learn for a Data Analyst job seeker according to 2023 data
This analysis was done as a capstone to the previous queries in this project. I sought to evaluate the most worthwhile Data Analyst skill for anyone in the United states looking to enter the Data Analysis field in the near future.
The seaborn library was used to create a scatter plot that shows a correlation of the median salaries and the demand level of Data Analysts skills with a minimum annual regional(USA) demand of 5%.



View my notebook for details of this query[Here](3_project\5_optimal_skill.ipynb)

### Visualize Data
```python
sns.set_theme(style='ticks')
sns.scatterplot(data= df_plot, x='skill_perc',y='median_salary', hue='technology')
plt.xlabel('RELATIVE SKILL DEMAND')
plt.ylabel('MEDIAN SALARY')
plt.title('CORELATION OF THE DEMAND LEVEL AND SALARY FOR TOP DATA ANALYST SKILLS')
```

### Results

Click here for the Visualisation of my queries results ![Here](3_project\images\optimal_skills_scat.png)
*Scatterplot visualizing the relationship between earnings and demand for data analyst skills in 2023*


### Insights
- Programming Skills:

Python has a high median salary (~$96K) and relatively high demand (~30%), making it both lucrative and highly sought after.
SQL is the most in-demand skill (around 55% demand) with a salary of ~$92K, making it essential for many data analyst roles.
Go appears to have a lower demand (~15%) but a salary around $90K, indicating it is specialized yet well-compensated.

- Database Skills:

Oracle and SQL Server offer some of the highest salaries (~$96K and ~$94K, respectively), with moderate demand (~10-15%), suggesting that expertise in these database systems can lead to higher earnings, despite not being as common as SQL.

- Analyst Tools:

Tableau and Power BI have mid-level demand (around 20-30%) and salaries in the range of ~$88K to ~$92K.
Excel and PowerPoint are more common (Excel having 50% demand) but offer lower median salaries ($82K to ~$84K). These tools, while widely used, are associated with lower compensation compared to more specialized tools.

- Cloud Skills:

Oracle is the only cloud-related tool present, with high salaries (~$96K) but lower demand compared to more widely adopted tools like SQL and Python.


# What I Learned
By doing this project i have learned to understand and use python and its libraries to extract, clean and analyze data, drawing insights that would not have been noticed other wise. By exploring the US job market, I have understood the skills i have to focus on as this project has clearly highlighted the need to consider optimal skills. Specifically, i have learned about:
 
 - Relevance of Data Preparation: Dta preparation has been very crucial in the project as it has helped me avoid errors and saved me from drawing unfounded insights.
 - Advance python Usage: I have learned to use advance python and queries types to draw and visualize insights about the US job market
 

 # Challenges I faced 
 I faced a few challenges in the course of this project, notably:
 - I was not able to install the adjustText library. hence i was unable to introduce pointers data points that are too close to each other in the scatterplot and lineplot.
 - I felt the visualization on the top skills for Business analyst and top 3 data jobs ![Here](3_project\images\skill_demand_BA_and_top_3_jobs.png). could have been better if the diagram was large enough to allow larger text and allignment. 


# Conclusion
 Despite the glaring constraint of time, as the analysis, recommendation and insights derived fromthis prject could soon appear irrelevant from changes in the job market in the future, this project nevertheless serves as a base for future projects analysing trends, compensations and overall optimality and relevance of data skills and tools. The project  has proven to be very informative and will prove to be a reliable guid for any one hoping to enter the field of Data science in the very near future.

 Skills like SQL and Python are highly in-demand and well-compensated, making them essential for most data analyst roles. However, specialized skills like Oracle and SQL Server command higher salaries despite lower demand, while widely used tools like Excel and PowerPoint offer lower pay.