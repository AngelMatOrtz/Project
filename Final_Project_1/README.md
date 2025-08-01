# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my Notebook with steps:
[2_Skill_Demand.ipynb](2_Skill_Demand.ipynb)

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

![Visualizatio for top skills](Images/skill_demand_percents_for_data_roles.png)


# The Analysis

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

![Trending Top Skills for Data Analyst in the US](images/Trending_skills_Data_Analyst.png)


### **Insights:**

- SQL consistently ranks as the most in-demand skill throughout the year, though its popularity tapers slightly over time.  
- Excel shows a sharp rise in demand beginning in September, ultimately overtaking Python and Tableau by year’s end.  
- Python and Tableau maintain steady levels of demand with minor fluctuations, underscoring their continued importance for data analysts.  
- Power BI, while not as prominent as the other tools, exhibits a modest upward trend in demand as the year concludes.