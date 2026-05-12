# Introduction
## Overview
Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for data analysts.

The data sourced from Luke Barousse's Python Course which provides a foundation for my analysis, containing detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in data analytics.

## The Questions
### Below are the questions I want to answer in my project:

1. What are the skills most in demand for the top 3 most popular data roles?  
2. How are in-demand skills trending for Data Analysts?  
3. How well do jobs and skills pay for Data Analysts?  
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying)

# Tools I Used
### For my deep dive into the data analyst job market, I harnessed the power of several key tools:
- **Python:** The backbone of my analysis, allowing me to analyze the data and find critical insights. I also used the following Python libraries:
  - **Pandas Library:** This was used to analyze the data.
  - **Matplotlib Library:** I visualized the data.
  - **Seaborn Library:** Helped me create more advanced visuals.
- **Jupyter Notebooks:** The tool I used to run my Python scripts which let me easily include my notes and analysis.
- **Visual Studio Code:** My go-to for executing my Python scripts.
- **Git & GitHub:** Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.


# Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:
[1_Skill_Demand.ipynb](1_Skills_Demand.ipynb)

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

View my notebook with detailed steps here:
[2_Skills_Trend.ipynb](2_Skills_Trend.ipynb)

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

## 3. How well do jobs and skills pay for Data Analysts?

View my notebook with detailed steps here:
[3_Salary_Analysis.ipynb](3_Salary_Analysis.ipynb)

### Salary Analysis for Data Nerds

#### Visualize Data

```python
sns.boxplot(data=df_us_top6, x='salary_year_avg', y='job_title_short', order=job_order)
sns.set_theme(style='ticks')

plt.title('Salary Distributions in the United States')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0, 600000)
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```

#### Results

![Salary Distributions of Data Jobs in the US](images\salary_distribution.png)
*Box plot visualizing the salary distributions for the top 6 data job titles.*

#### Insights

- There’s a significant variation in salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to $600K, indicating the high value placed on advanced data skills and experience in the industry.

- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with fewer outliers.

- The median salaries increase with the seniority and specialization of the roles. Senior roles (Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.

### Highest Paid & Most Demanded Skills for Data
#### Visualize Data
```python
fig, ax = plt.subplots(2, 1)

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=top_pay, x='median',
            y=top_pay.index, hue='median', ax=ax[0],
            palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(data=top_skills, x='median',
            y=top_skills.index, hue='median', ax=ax[1],
            palette='light:b')

plt.show()

```
#### Results
##### Here's the breakdown of the highest-paid skills & most in-demand skills for data analysts in the US:

![The Highest-Paid Skills & Most In-Demand Skills for Data Analysts In The US](images\top_skills_most_in_demand.png)

*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.*

#### Insights:

- The top graph shows specialized technical skills like `dplyr`, `Bitbucket`, and `Gitlab` are associated with higher salaries, some reaching up to $200K, suggesting that advanced technical proficiency can increase earning potential.

- The bottom graph highlights that foundational skills like `Excel`, `PowerPoint`, and `SQL` are the most in-demand, even though they may not offer the highest salaries. This demonstrates the importance of these core skills for employability in data analysis roles.

- There's a clear distinction between the skills that are highest paid and those that are most in-demand. Data analysts aiming to maximize their career potential should consider developing a diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.

## 4. What is the most optimal skill to learn for DA?

View my notebook with detailed steps here:
[4_Optimal_Skills.ipynb](4_Optimal_Skills.ipynb)

### Visualizing Data

```python
sns.scatterplot(
    data = df_plot,
    x = 'skill_percent',
    y = 'median_salary',
    hue = 'technology'
)

texts = []
for i, txt in enumerate(df_da_skills_high_demand.index):
    texts.append(plt.text(df_da_skills_high_demand['skill_percent'].iloc[i], df_da_skills_high_demand['median_salary'].iloc[i], txt))

adjust_text(texts, arrowprops=dict(arrowstyle='->', color='red'))
sns.despine()
sns.set_theme(style = 'ticks')
plt.xlabel('Percent of Skills in DA')
plt.ylabel('Median Yearly Salary')
plt.title(f'Most Optimal Skills for Data Analysts')

ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y,_: f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter())

plt.tight_layout()
plt.show()
```
#### Results

![Most Optimal Skills for Data Analysts in the US](images\optimal_skills.png)

*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US.*

#### Insights

- The scatter plot shows that most of the `programming` skills (colored blue) tend to cluster at higher salary levels compared to other categories, indicating that programming expertise might offer greater salary benefits within the data analytics field.

- Analyst tools (colored green), including Tableau and Power BI, are prevalent in job postings and offer competitive salaries, showing that visualization and data analysis software are crucial for current data roles. This category not only has good salaries but is also versatile across different types of data tasks.

- The database skills (colored orange), such as Oracle and SQL Server, are associated with some of the highest salaries among data analyst tools. This indicates a significant demand and valuation for data management and manipulation expertise in the industry.

# What I Learned  
Throughout this project, I deepened my understanding of the data analyst job market and enhanced my technical skills in Python, especially in data manipulation and visualization. Here are a few specific things I learned:  
- **Advanced Python Usage:** Utilizing libraries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualization, and other libraries helped me perform complex data analysis tasks more efficiently.  
- **Data Cleaning Importance:** I learned that thorough data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accuracy of insights derived from the data.  
- **Strategic Skill Analysis:** The project emphasized the importance of aligning one's skills with market demand. Understanding the relationship between skill demand, salary, and job availability allows for more strategic career planning in the tech industry.  

# Insights 
This project provided several general insights into the data job market for analysts:  
- **Skill Demand and Salary Correlation:** There is a clear correlation between the demand for specific skills and the salaries those skills command. Advanced and specialized skills like Python and Oracle often lead to higher salaries.  
- **Market Trends:** There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Understanding these trends is essential for career growth in data analytics.  
- **Economic Value of Skills:** Understanding which skills are both in-demand and well-compensated can guide career decisions.

# Challenges I Faced
### During this project, I encountered several challenges that turned into valuable learning opportunities:

- **Data Inconsistencies 🗂️**    
Managing missing or inconsistent data entries required careful cleaning and validation to maintain the integrity of the analysis.

- **Complex Data Visualization 📊**         
Designing clear and effective visualizations for complex datasets was difficult. It took effort to balance readability with the need to convey meaningful insights.

-   **Balancing Breadth and Depth ⚖️**  
Deciding how deeply to explore each skill or trend while still keeping a broad overview of the job market was a constant challenge. Too much detail risked losing the bigger picture, while too broad an approach could miss important insights.

#### 👉 These challenges helped me strengthen my skills in data cleaning, visual storytelling, and scope management, ensuring that my analysis was both comprehensive and insightful.

# Conclusion
#### This exploration into the data analyst job market has been incredibly informative, highlighting the critical skills and trends that shape this evolving field. The insights I got enhance my understanding and provide actionable guidance for anyone looking to advance their career in data analytics. As the market continues to change, ongoing analysis will be essential to stay ahead in data analytics. This project is a good foundation for future explorations and underscores the importance of continuous learning and adaptation in the data field.


