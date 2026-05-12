# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](1_Skills_Demand.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_count[df_skills_count['job_title_short'] == job_title].head(5)
    df_plot.plot(kind = 'barh', x = 'job_skills', y = 'skill_count', ax = ax[i], title = job_title)
    ax[i].invert_yaxis()
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)
```
### Results

![Visualization of TOP Skills for Data Nerds](images\skill_demand_of_top_data_roles.png)

### Insights

- Data Scientist roles have the highest demand for Python at 72%.
- SQL demand is strongest in Data Engineer postings at 68%.
- Data Analysts rely heavily on SQL (51%) and Excel (41%).
- AWS appears prominently only in Data Engineer roles (43%).
- Azure and Spark are tied at 32% for Data Engineers.
- R is a major requirement for Data Scientists (44%) but not shown for other roles.
- Tableau demand is highest for Data Analysts (28%) and lower for Data Scientists (24%).
- SAS demand is relatively low across all roles, highest in Data Scientists at 24%.

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python
sns.lineplot(data = skills_percent, dashes = False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()
plt.title('Trending Top Skills for DA in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
from matplotlib.ticker import PercentFormatter, FuncFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(1, decimals=0))
plt.legend().remove()

for i in range(4):
    plt.text(11.5, skills_percent.iloc[-1, i], f'{skills_percent.columns[i].replace('_percent','')}')
plt.show()
```

### Results

![Trending Top Skills for Data Analysts in the US](images\skills_trend.png)

*Bar graph visualizing the trending top skills for data analysts in the US in 2023.*

### Insights:

- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end of the year.
- Both Python and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts.
- Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.
