# Overview

Welcome to my analysis of the data job market, specifically focusing on data analyst roles. This project aims to enhance our understanding of the job landscape by exploring the highest-paying and most in-demand skills for data analysts.

I sourced data from Kaggle, which offers comprehensive insights into job titles, salaries, locations, and essential skills. Using Python scripts, I investigate key questions, including the most sought-after skills, salary trends, and the relationship between demand and salary in the field of data analytics.

# The Questions

Below are the questions I want to answer in my project:

1. What are the most demanded skills for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. What are the salary trends for Data Analysts in relation to their skills?
4. Which skills offer the best combination of high demand and high salary for Data Analysts?
5. What are the emerging high-demand skills for Machine Learning professionals?
6. Which cloud computing skills are driving the highest salaries and demand in the industry?
7. What are the most valuable skills for Software Engineers in terms of demand and salary?

# Tools I Used

For my deep dive into the data analyst job market, I harnessed the power of several key tools:

- **Python:** The core of my analysis, enabling me to extract critical insights. I employed the following libraries:

      **Pandas:** For data manipulation and analysis.

      **Matplotlib:** To create visual representations of the data.

      **Seaborn:** For more advanced visualizations.

  **Jupyter Notebooks:** The tool I used to run my Python scripts which let me easily include my notes and analysis.

- **Visual Studio Code:** My go-to for executing my Python scripts.
- **Git & GitHub:** Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

# Data Preparation and Cleanup

This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.

## Import & Clean Up Data

I start by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure data quality.

```python
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Loading Data
df = pd.read_csv('C:/Users/HP/jupyter lab csvs/data_jobs.csv')

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```

## Filter US Jobs

To focus my analysis on the U.S. job market, I apply filters to the dataset, narrowing down to roles based in the United States.

```python
df_US = df[df['job_country'] == 'United States']

```

# The Project Analysis

## **1. What are the most demamded skills for Machine learning And Cloud Engineer and Software Engineer**

### The steps i took

To identify the most in-demand skills for the most demamded skills for Machine learning, Cloud Engineer and Software Engineer in the United States, I first filtered the dataset to include only job positions based in the US, then i selected the specific jobs i needed and ectracted the top 5 skills for each of these roles. This analysis highlights the specific job titles and their key skills, helping me understand which skills to focus on based on the role I am targeting.

View my notebook with detailed steps here:
[1_Skill_Demand.ipynb](Project\1_Skill_demand_Engineer.ipynb)

### Visualizing the data

```python
# Create subplots with a separate plot for each job title in filtered_job_titles
fig, ax = plt.subplots(len(filtered_job_titles), 1)

sns.set_theme(style='ticks')

# Loop through each job title to create individual bar plots
for i, job_title in enumerate(filtered_job_titles):
    # Filter the DataFrame for the top 5 skills of the current job title
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)


    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

    # Set subplot title to the current job title and remove unnecessary labels
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].legend().remove()  # Remove legend to reduce clutter
    ax[i].set_xlim(0, 80)    # Set x-axis limit to 80% for consistency

    # Annotate each bar with the skill percentage
    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 2, n, f'{v:.0f}%', va='center')

    # Hide x-axis ticks for all but the last subplot to save space
    if i != len(filtered_job_titles) - 1:
        ax[i].set_xticks([])


fig.suptitle('Likelihood Of Skills Requested In US Job Posting', fontsize=20)

# Adjust layout to prevent overlap between subplots
fig.tight_layout(h_pad=0.5)
plt.show()

```

### The Result

![Visualization of Top Kills for Data Roles in the United States](Project\Images\engineering.png)

### Key Insights:

Here are some insights from the image showing the "Likelihood of Skills Requested in US Job Posting" for three roles— Machine Learning Engineer, Cloud Engineer and Software Engineer:

1. **Machine Learning Engineer Dominance**:

   - The most requested skill for Machine Learning Engineers is **Python**, at **70%**, indicating its critical importance in this field.

2. **Common Skills Across Roles**:

   - **SQL** appears prominently across all three roles: 32% for Cloud Engineers, 33% for Machine Learning Engineers, and 40% for Software Engineers, highlighting its versatility and demand.

3. **Role-Specific Skills**:

   - **Cloud Engineers** prioritize skills like **Azure** (15%) and **AWS** (25%), suggesting a focus on cloud platforms.
   - For **Software Engineers**, skills such as **Java** (21%) and **Tableau** (18%) are also significant, indicating a blend of development and data visualization skills.

4. **Comparative Demand**:
   - **Python** is highly sought after in both Cloud Engineering (30%) and Software Engineering (39%), showing its broad applicability.

### Conclusion:

The data emphasizes the importance of Python and SQL across various technical roles, while also pointing to specific skills tailored to each position. This insight can guide job seekers in prioritizing their skill development based on market demand.

## **2. What are the most demanded skills for the top 3 most popular data roles?**

### The steps i took

To identify the most in-demand skills for the top 3 most popular data roles in the United States, I first filtered the dataset to include only job positions based in the US, then i selected the most popular positions and extracted the top 5 skills for each of these roles. This analysis highlights the most popular job titles and their key skills, helping me understand which skills to focus on based on the role I am targeting.

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](Project\2_Skill_Demand.ipynb)

### Visualizing the data

```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enmerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] ==
    job_title].head(5)[::-1]
    sns.barplot(data = df_plot, x='skill_percent', y ='job_skills', ax=ax[i],
    hue='skill_count', palette='dark:b_r')

plt.show()
```

### The Result

![Visualization of Top Kills for Data Roles in the United States](Project\Images\output.png)

### Insights

Here are some insights from the image showing the "Likelihood of Skills Requested in US Job Posting" for three data roles—Data Analyst, Data Engineer, and Data Scientist:

### 1. **Common Skills Across Roles:**

- **SQL** is a crucial skill across all three roles, showing a high demand in job postings:
  - **Data Analyst:** 51%
  - **Data Engineer:** 68%
  - **Data Scientist:** 51%
- **Python** is another key skill highly sought after, especially for Data Engineers (65%) and Data Scientists (72%).

### 2. **Role-Specific Skills:**

- **Data Analyst:**
  - Apart from SQL, **Excel** (41%), **Tableau** (28%), and **Python** (27%) are important. This suggests a blend of data manipulation and visualization skills is necessary.
- **Data Engineer:**
  - Besides SQL and Python, cloud computing skills like **AWS** (43%), **Azure** (32%), and big data technologies like **Spark** (32%) are crucial. This highlights a need for expertise in data storage, processing, and cloud platforms.
- **Data Scientist:**
  - While Python (72%) is the most sought-after skill, **R** (44%) and **SAS** (24%) also feature prominently, indicating that statistical analysis and advanced analytics are highly valued.

### 3. **Focus on Python:**

- **Python** is a highly demanded skill for Data Scientists (72%) and Data Engineers (65%), making it an essential skill to learn and master for those aiming for these roles.

### 4. **Visualization and Reporting Tools:**

- For Data Analysts, visualization tools like **Tableau** (28%) and **Excel** (41%) are more important compared to Data Engineers and Data Scientists. This reflects the role's focus on data visualization and report generation.

### 5. **Advanced Tools and Platforms for Engineers:**

- Data Engineers need to be proficient in cloud platforms (AWS, Azure) and big data tools (Spark). This contrasts with the requirements for Data Analysts and Data Scientists, emphasizing the importance of different toolsets based on the role.

### 6. **Emerging Trends in Data Science Roles:**

- Both **Data Scientist** and **Data Engineer** roles prioritize cloud and programming skills more than Data Analysts, showing the evolving nature of these roles toward handling larger datasets and performing more complex analysis.

### Conclusion:

If you are targeting a career in any of these fields, focus on mastering **SQL** and **Python** as they are essential across all roles. For Data Analysts, enhancing skills in tools like **Excel** and **Tableau** is beneficial. Data Engineers should invest in cloud computing skills, and Data Scientists should consider learning both **Python** and **R** along with a solid foundation in SQL and statistical tools.

## **3. How are in-demand skills trending for Data Analytics.**

### The steps i took

To identify the trending skills for Data Analyst roles in the United States, I first filtered the dataset to include only relevant job postings. I extracted the month of each job posting and expanded the skills listed for each posting into separate rows. I then created a pivot table to calculate the monthly count of each skill. Next, I normalized these counts by the total number of job postings per month to obtain the percentage representation of each skill. Finally, I converted the month numbers to their respective names for better visualization and used a line chart to plot it.

### Visualize data

```python
df_plot = df_da_us_skills_percent.iloc[:, :5]

sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills For Data Analyst in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i])
```

### Result

![Skills trend visualization](Project\Images\skills_trend.png)

### Insights gotten from the data

The line chart shows the trending top skills for Data Analysts in the US throughout the year 2023, based on the likelihood of each skill appearing in job postings.

1. **SQL Dominance**: SQL remains the most in-demand skill for Data Analysts in the US, consistently staying above 50% likelihood in job postings throughout the year. Although there is a slight decline in demand from February to December, it remains the top skill.

2. **Excel's Stable Demand with Some Fluctuations**: Excel is the second most demanded skill and shows relatively stable demand throughout the year, ranging between 35% to 45%. However, there is a noticeable dip in September, followed by a slight upward trend towards the end of the year.

3. **Python and Tableau Competing Closely**: Python and Tableau show similar patterns in demand, ranging around 25% to 35%. There is a slight increase during mid-year for both skills, but a decline towards the later months, indicating that they are equally prioritized but secondary to SQL and Excel.

4. **Power BI's Niche Demand**: Power BI, while not as prominent as other skills, shows a consistent demand, hovering around 15% to 25% throughout the year. There is a minor fluctuation in demand, with a slight dip around mid-year.

5. **Overall Declining Trend in Demand**: Most skills show a slight decline in demand toward the latter half of the year (July to October), which might suggest seasonal trends or market saturation.

### Conclusion

- **Key Skills to Focus On**: SQL and Excel remain critical skills for Data Analysts, with Python and Tableau being valuable secondary skills.
- **Market Dynamics**: The market demand for skills can fluctuate slightly month-by-month, suggesting that continuous learning and keeping up with emerging tools are important for aspiring Data Analysts.

### 4. How Well Do Jobs and Skills Pay for Data Analysts?

To identify the highest-paying roles and skills for data analysts, I focused exclusively on jobs in the United States and examined their median salaries. Initially, I analyzed the salary distributions of common data roles such as Data Scientist, Data Engineer, and Data Analyst to determine which positions offer the highest compensation.

View my notebook with detailed steps here: [4_Salary_Analysis](Project\4_Salary_Analysis.ipynb).

#### Visualize Data

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```

#### Results

![Salary Distributions of Data Jobs in the US](Project\Images\salary_box.png)  
_Box plot visualizing the salary distributions for the top 6 data job titles._

#### Insights

- There's a significant variation in salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to $600K, indicating the high value placed on advanced data skills and experience in the industry.

- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with fewer outliers.

- The median salaries increase with the seniority and specialization of the roles. Senior roles (Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.

### Highest Paid & Most Demanded Skills for Data Analysts

Next, I narrowed my analysis and focused only on data analyst roles. I looked at the highest-paid skills and the most in-demand skills. I used two bar charts to showcase these.

#### Visualize Data

```python

fig, ax = plt.subplots(2, 1)

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analystsr')
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()

```

#### Results

Here's the breakdown of the highest-paid & most in-demand skills for data analysts in the US:

![The Highest Paid & Most In-Demand Skills for Data Analysts in the US](Project\Images\salary.png)

_Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US._

### Key Insights:

Here are the insights derived from the image regarding the highest-paid and most in-demand skills for data analysts in the U.S.:

1. **Highest Paid Skills**:

   - Skills like **dplyr**, **bitbucket**, and **gitlab** are among the top earners, indicating that expertise in data manipulation and version control can lead to higher salaries.
   - **Solidity** and **hugging face** are also notable, suggesting that knowledge in blockchain technology and natural language processing frameworks is highly valued.

2. **Salary Range**:

   - The highest-paid skills reflect median salaries that can reach up to **$200K**, showcasing significant earning potential for data analysts with specialized skills.

3. **Most In-Demand Skills**:

   - Skills such as **Python**, **Tableau**, and **SQL Server** are frequently sought after, emphasizing their importance in the data analytics field.
   - **R** and **SAS** are also in demand, indicating a need for statistical analysis capabilities.

4. **Salary vs. Demand**:
   - There is a clear distinction between the highest-paid skills and the most in-demand ones, suggesting that while some skills command high salaries, they may not be as widely sought after compared to foundational skills like Python and SQL.

### Conclusion:

The data highlights the importance of both specialized and foundational skills in data analytics. While high-paying skills can significantly boost earning potential, the most in-demand skills remain essential for career advancement in the field.

## 5. What are the most optimal skills to learn for Data Analysts?

To identify the most optimal skills to learn—those that are both highest paid and in high demand—I calculated the percentage of skill demand alongside the median salaries. This analysis allows for a clear identification of the skills that offer the best balance of earning potential and market need.

View my notebook with detailed steps here: [5_Optimal_Skills](Project\5_Optimal_Skills.ipynb).

#### Visualize Data

```python
from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show()

```

#### Results

![Most Optimal Skills for Data Analysts in the US](Project\Images\most_optimal.png)  
_A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US._

#### Insights:

- The skill `Oracle` appears to have the highest median salary of nearly $97K, despite being less common in job postings. This suggests a high value placed on specialized database skills within the data analyst profession.

- More commonly required skills like `Excel` and `SQL` have a large presence in job listings but lower median salaries compared to specialized skills like `Python` and `Tableau`, which not only have higher salaries but are also moderately prevalent in job listings.

- Skills such as `Python`, `Tableau`, and `SQL Server` are towards the higher end of the salary spectrum while also being fairly common in job listings, indicating that proficiency in these tools can lead to good opportunities in data analytics.

### Visualizing Different Techonologies

Let's visualize the different technologies as well in the graph. We'll add color labels based on the technology (e.g., {Programming: Python})

#### Visualize Data

```python
from matplotlib.ticker import PercentFormatter

# Create a scatter plot
scatter = sns.scatterplot(
    data=df_DA_skills_tech_high_demand,
    x='skill_percent',
    y='median_salary',
    hue='technology',  # Color by technology
    palette='bright',  # Use a bright palette for distinct colors
    legend='full'  # Ensure the legend is shown
)
plt.show()

```

#### Results

![Most Optimal Skills for Data Analysts in the US with Coloring by Technology](Project\Images\optimal_skills.png)  
_A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US with color labels for technology._

#### Insights:

Here are the insights derived from the image on the most optimal skills for data analysts:

### Key Insights:

1. **High-Paying but Less Common Skills**:

   - **Oracle** stands out with the highest median salary (~$97K) but is required by a lower percentage of data analyst jobs (~10%). This indicates that Oracle expertise is highly valued but not as commonly sought after in the data analyst field, making it a niche but lucrative skill.
   - **Python** is also a high-paying skill (around $95K) and is in relatively high demand (~35%). Its combination of high demand and salary makes it one of the most optimal skills for data analysts.

2. **Skills with High Demand but Moderate Salaries**:

   - **SQL** and **Excel** have high demand among employers (about 60% and 45% of job postings, respectively). However, their median salaries (~$92K and ~$84K) are slightly lower compared to some other high-paying skills. This suggests that these skills are fundamental but do not necessarily command the highest salaries.

3. **Balanced Demand and Salary**:

   - **Tableau** and **SQL Server** are in the sweet spot with a balanced combination of good demand (20-35%) and solid salaries (around $90K-$92K). These skills are both relatively common and well-compensated, making them good targets for data analysts seeking a versatile skill set.

4. **Lower-Paying, High-Demand Skills**:

   - Skills like **PowerPoint**, **Excel**, and **Word** are in high demand but come with lower median salaries ($82K-$85K). These tools are essential for daily tasks but do not significantly boost earning potential on their own.

5. **Niche Skills with Moderate Demand and Salaries**:
   - **SAS**, **R**, and **Power BI** fall in the middle of the spectrum, offering moderate salaries (~$89K-$91K) and a balanced level of demand (~15-20%). They represent specialized skills that can add value but do not stand out in terms of either demand or pay.

### Conclusion:

These insights suggest that data analysts can optimize their earning potential by focusing on in-demand skills like Python, SQL, and Tableau, while niche skills like Oracle offer opportunities for those seeking top pay in specific areas.

- The scatter plot shows that most of the `programming` skills (colored blue) tend to cluster at higher salary levels compared to other categories, indicating that programming expertise might offer greater salary benefits within the data analytics field.

- The database skills (colored orange), such as Oracle and SQL Server, are associated with some of the highest salaries among data analyst tools. This indicates a significant demand and valuation for data management and manipulation expertise in the industry.

- Analyst tools (colored green), including Tableau and Power BI, are prevalent in job postings and offer competitive salaries, showing that visualization and data analysis software are crucial for current data roles. This category not only has good salaries but is also versatile across different types of data tasks.

**What I have Learned From This Project**

During this project, I gained a deeper understanding of the data analyst job market while honing my technical skills in Python, particularly in data manipulation and visualization. Here are some key takeaways:

- **Advanced Python Skills**: I extensively used libraries like Pandas for data manipulation, Seaborn and Matplotlib for visualization, and others to streamline complex data analysis tasks.
- **The Importance of Data Cleaning**: I learned that rigorous data cleaning and preparation are essential for accurate analysis. This step ensures the reliability of the insights drawn from the data.
- **Strategic Skill Alignment**: The project highlighted the value of aligning one’s skills with market demand. Understanding the interplay between skill demand, salary, and job opportunities can guide more strategic career planning in tech.

**Insights**

This project offered several valuable insights into the data analyst job market:

- **Correlation Between Skill Demand and Salary**: There is a strong link between the demand for certain skills and the salaries they command. High-demand, specialized skills like Python and Oracle are often associated with higher compensation.
- **Evolving Market Trends**: The project revealed shifts in skill demand, underscoring the dynamic nature of the data job market. Staying updated on these trends is crucial for career growth in data analytics.
- **Economic Value of Skills**: Identifying skills that are both in-demand and well-compensated helps data analysts prioritize learning paths that maximize economic returns.

**Challenges I Faced**

While rewarding, the project came with its own set of challenges that provided valuable learning experiences:

- **Data Inconsistencies**: Managing missing or inconsistent data required meticulous cleaning and thoughtful handling to preserve the integrity of the analysis.
- **Complex Data Visualization**: Crafting effective visual representations of complex data sets was challenging but vital for communicating insights clearly and persuasively.
- **Balancing Breadth and Depth**: Finding the right balance between diving deep into specific analyses and maintaining an overview of the broader data landscape was a constant challenge, requiring careful judgment to ensure comprehensive yet focused analysis.

**Conclusion**

This exploration into the data analyst job market has been highly informative, highlighting key skills and trends that shape this evolving field. The insights gained not only enhance my understanding but also offer practical guidance for anyone aspiring to advance in data analytics. As the market continues to evolve, ongoing analysis will be crucial to stay ahead. This project lays a solid foundation for future investigations and emphasizes the importance of continuous learning and adaptation in the data field.
