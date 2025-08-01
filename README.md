# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my Notebook with steps:
[2_Skill_Demand.ipynb](Final_Project_1\2_Skill_Demand.ipynb)

### Data Visualization

```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_count[df_skills_count['job_title_short'] == job_title].head(5)
    df_plot.plot(kind='barh', x='job_skills', y='skill_count', ax=ax[i], title=job_title)
    ax[i].invert_yaxis()
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)

fig.suptitle('Counts of Top Skills in Job Postings', fontsize=15)
fig.tight_layout(h_pad=0.5)
plt.show()
```
### Results

![Visualizatio for top skills](Final_Project_1\Images\skill_demand_percents_for_data_roles.png)

### **Insights:**

- SQL is a universal requirement:
It's the top or second-most requested skill for all roles — Data Analyst (51%), Data Engineer (68%), and Data Scientist (51%). This makes SQL a non-negotiable baseline skill for anyone entering the data field.

- Python dominates in technical roles:
Python is essential for Data Scientists (72%) and Data Engineers (65%) but less emphasized for Data Analysts (27%). It’s key for automation, modeling, and working with large datasets.

- Tool demand varies by role:

    Data Analysts: Excel (41%) and Tableau (28%) for reporting and dashboards

    Data Engineers: AWS (43%), Azure (32%), Spark (32%) for infrastructure and pipelines

    Data Scientists: R (44%) and Python (72%) for analysis and modeling
    This reflects each role’s distinct workflow focus — from reporting to engineering to advanced analytics.



## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python
from matplotlib.ticker import PercentFormatter

df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()
```

### Results

![Trending Top Skills for Data Analyst in the US](Final_Project_1\Images\trending_skills_data_analyst.png)

### **Insights:**

- SQL consistently ranks as the most in-demand skill throughout the year, though its popularity tapers slightly over time.  
- Excel shows a sharp rise in demand beginning in September, ultimately overtaking Python and Tableau by year’s end.  
- Python and Tableau maintain steady levels of demand with minor fluctuations, underscoring their continued importance for data analysts.  
- Power BI, while not as prominent as the other tools, exhibits a modest upward trend in demand as the year concludes.


## 3. How well do jobs and skills pay for Data Analyst


### Salary Analysis

#### Visualize Data

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
# Results
![Salary Distribution of Data Jobs in the US](Final_Project_1\Images\salary_distrution_for_data_roles.png)

*Box plot Visualization of roles for top 6 data jobs.*

### **Insights:**

- Senior roles command significantly higher median salaries:
Senior Data Scientists and Senior Data Engineers have the highest median salaries among all roles shown. This reflects the market value of experience and leadership in advanced analytics and engineering. Their boxes are also shifted further right on the x-axis, confirming higher pay bands.

- Data Analysts earn the lowest, with a tighter salary range:
Data Analysts show the narrowest interquartile range (IQR) and the lowest median salary. This indicates more uniformity in pay but also suggests a ceiling in salary potential for entry-level or non-technical analytics roles compared to engineering or senior positions.

- Outlier presence increases with technical or seniority level:
Technical and senior roles (e.g., Senior Data Scientist, Data Engineer) display a high number of outliers extending well beyond $200K–$300K, hinting at lucrative opportunities in niche or high-demand sectors like big tech, finance, or specialized consulting. In contrast, roles like Data Analyst have fewer extreme outliers, suggesting less variation in salary extremes.


## 3. How well do jobs and skills pay for Data

### Highest Paid and Most Demanded Skills for Data

#### Visiualize data
```python

fig, ax = plt.subplots(2, 1)

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()
```
### Results


![The Highest Paid & Most In Demand Skills for Data Analyst in the US](Final_Project_1\Images\highest_paying_demanded_skills.png)

*Two bar graph visualizations displaying the highest paid skills and most in demand skills for Data Analyst in the US*

### **Insights:**

- Highest-paid skills are niche and tool-specific, not mainstream:
The top-paying skills for Data Analysts — like dplyr, bitbucket, hugging face, solidity, and gitlab — are specialized tools or platforms used in advanced or domain-specific workflows (e.g., blockchain, MLOps, DevOps). These skills aren't as broadly adopted, but companies needing them are willing to pay a premium due to scarcity.

- Most in-demand skills are foundational, not necessarily high-paying:
Languages and tools like python, tableau, sql, excel, and power bi dominate the demand chart. These are core to most Data Analyst roles and widely taught — but because supply is high, their median salaries are lower. This reflects the tradeoff between skill ubiquity and compensation.

- There’s a clear disconnect between demand and compensation:
None of the top 10 highest-paid skills appear in the most in-demand list — and vice versa. This shows that the most common skills are not necessarily the most lucrative. Analysts looking to boost earnings should consider layering rare, high-paying tools (like hugging face or solidity) on top of core skills to differentiate themselves in the job market.

## 4. What is the most optimal skill to learn for Data Analyst?

#### Visualize Data

```python
from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show()
```
### Results 

![Most Optimal Skills for Data Analyst in the US](Final_Project_1\Images\optimal_skills_data_analyst.png)

*Scatter plot visualizing the most optimal skills for Data Analyst in the US*

#### Insights:

- Python offers top salary with moderate demand:
Despite appearing in fewer job postings than Excel or SQL, Python commands the highest median salary (~$98K). This suggests that roles requiring Python are more technical, higher-level, or in organizations willing to pay more for automation and data manipulation expertise.

- SQL has the highest demand but not the highest pay:
SQL shows up in nearly 60% of data analyst job postings — making it the most in-demand skill — but its salary (~$91K) is not the highest. This indicates SQL is foundational and expected across roles but not necessarily tied to higher compensation alone.

- Niche tools like Oracle and Go yield strong pay despite low demand:
Skills like Oracle ($97K) and Go ($90K) are associated with fewer job postings (<10%) but offer strong salaries, likely due to specialized use in enterprise systems or backend-heavy analyst roles. These can be valuable differentiators for candidates in niche markets.