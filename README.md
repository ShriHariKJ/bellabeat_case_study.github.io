###### bellabeat_case_study.github.io
# Case study (Bellabeat) : How Can a Wellness Technology Company Play It Smart?
![Bellabeat](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/491fb9578fc6aa5e5ccce7599187fa4fb377fb4f/Images/Designer%20(1).png)
Image courtesy: Copilot

## Introduction

This repository contains a case study analysis of Bellabeat, a high-tech manufacturer of health-focused products for women. The analysis aims to understand how different customer segments, such as casual users and subscription-based members, utilize Bellabeat’s smart devices and to provide insights for designing a new marketing strategy. The insights discovered will help guide the marketing strategy for the company and will be presented to the Bellabeat executive team. The goal is to unlock new growth opportunities for Bellabeat by analyzing smart device fitness data.

## Scenario

You are a junior data analyst working on the marketing analytics team at Bellabeat. Bellabeat's future success hinges on expanding its presence in the global smart device market, and your team is tasked with understanding how consumers are using their smart devices. By analyzing smart device data, your goal is to gain insights into consumer behavior and preferences, ultimately guiding the development of a targeted marketing strategy. However, before implementation, your recommendations must be vetted and approved by Bellabeat executives, supported by compelling data insights and professional data visualizations.

## About the Company

Founded in 2013 by Urška Sršen and Sando Mur, Bellabeat has swiftly become a leading manufacturer of health-focused smart products for women. Their line includes devices tracking activity, sleep, stress, and reproductive health, offering users valuable insights for informed decisions. With a global presence and a commitment to digital marketing, Bellabeat engages consumers through various platforms like Google, Facebook, and Instagram. By personalizing experiences and leveraging data insights, Bellabeat aims to empower women with tailored solutions, driving growth in the wellness industry.

## Stakeholders

Key stakeholders include Urška Sršen (cofounder and Chief Creative Officer), Sando Mur (cofounder), and the Bellabeat marketing analytics team.

## The Business Task

The objective of this case study is to develop marketing strategies focused on enhancing the conversion of casual users into members for Bellabeat's products. Sršen and the marketing analytics team aim to examine Bellabeat's consumer data, particularly regarding smart device usage, to extract actionable insights. The key inquiries include:

* What are some trends in smart device usage?
* How could these trends apply to Bellabeat customers?
* How could these trends help influence Bellabeat marketing strategy?

### Bellabeat Products

* __Bellabeat app__: The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions. The Bellabeat app connects to their line of smart wellness products.
* __Leaf__: Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress.
* __Time__: This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.
* __Spring__: This is a water bottle that tracks daily water intake using smart technology to ensure that you are appropriately hydrated throughout the day. The Spring bottle connects to the Bellabeat app to track your hydration levels.
* __Bellabeat membership__: Bellabeat also offers a subscription-based membership program for users. Membership gives users 24/7 access to fully personalized guidance on nutrition, activity, sleep, health and beauty, and mindfulness based on their lifestyle and goals.

Sršen has tasked us with analyzing smart device usage data to gain insights into how consumers utilize non-Bellabeat smart devices. Subsequently, we are to select one Bellabeat product and apply these insights to our presentation.

## Data Preparation

In this phase, I will be utilizing the FitBit Fitness Tracker Data from Mobius, which includes data from 30 participants. The data, which spans from March 2016 to May 2016, can be accessed from the provided source. Although the datasets are not current and most data is recorded during certain days of the week, they are suitable for this case study and will enable me to answer the key business questions.

The data has been generated from a distributed survey via Amazon Mechanical Turk, with the consent of the 30 FitBit users. This is public data that I can use to explore how different user segments are utilizing their FitBit devices. However, it’s important to note that data-privacy issues prohibit me from using users’ personally identifiable information. This means that I won’t be able to connect tracker data to individual users to determine if their habits have changed over time.

The chosen data is comprehensive, with minute-level output for physical activity, heart rate, and sleep monitoring. Each user’s data is stored in a distinct dataset. These datasets are structured in a tabular format, each containing multiple identical columns. When combined, these datasets comprise a total of 18 CSV files [Kaggle Data](https://www.kaggle.com/arashnic/fitbit). The limitations of the dataset, such as the small sample size and the uneven distribution of data recording, will be taken into consideration during the analysis. The insights derived from these datasets will enable me to categorize, consolidate, and contrast the trends between different user segments.

## Data Processing: From Raw to Refined

### Tools Utilized 
R Studio was the preferred tool for this data processing task, primarily due to its robustness and efficiency in managing large datasets. Furthermore, R Studio’s comprehensive support from open-source libraries like dplyr and ggplot2 made it a perfect fit for the task. R Studio is particularly favored for its advanced data visualization capabilities and its ease of use in statistical analysis. This makes it an excellent tool for data cleaning, transformation, and analysis.

### Data Cleaning
The initial step after consolidating the datasets into individual dataframe was to identify columns and rows with missing data. 
* The total number of rows for daily_activity dataframe was 940 rows. It was found that it has 33 unique ids.
* The total number of rows for calories dataframe was 940 rows. It was found that it has 33 unique ids.
* The total number of rows for sleep dataframe was 413 rows. It was found that it has 24 unique ids.
* The total number of rows for weight dataframe was 67 rows. It was found that it has 8 unique ids.

Further investigation based on Product Focus, Marketing Strategy, Data Quality and User Engagement considerations, it may be advisable to exclude data points with fewer than 500 steps from the analysis.

Given that number of unique ids is 33, the sample size is too small and data exclusion for steps. Given these limitations, additional data is required and insights gained from analyzing available data shall not be taken as conclusive.

After removing rows, the data was ready for further processing and analysis but may not provide accurate analysis.

## Data Transformation

During the data transformation process, several steps were applied to different data frames:

- **`daily_activity` Data Frame:**
  - Renames the column "ActivityDate" to "Date" after converting its values to datetime format using the `mdy()` function, which interprets the input as month-day-year.
  - Removes the original "ActivityDate" column from the dataframe using the `select(-ActivityDate)` operation.

- **`sleep` Data Frame:**
  - Renames the column "SleepDay" to "Date" following conversion to datetime format with hour, minute, and second precision using the `mdy_hms()` function.
  - Calculates two new columns, "TotalHoursAsleep" and "TotalHoursInBed," by dividing the existing columns "TotalMinutesAsleep" and "TotalTimeInBed" by 60, respectively, representing sleep durations in hours with two decimal places.
  - Removes the original columns "TotalMinutesAsleep," "TotalTimeInBed," and "SleepDay" from the dataframe.

- **`hourly_intensities` Data Frame:**
  - Extracts the hour component from the "ActivityHour" column after converting its values to datetime format using `mdy_hms()` and then using the `hour()` function.
  - Removes the original "ActivityHour" column from the dataframe.

- **Filtering and Merging:**
  - Filters the `daily_activity` dataframe to include only rows where the "TotalSteps" column has values greater than or equal to 500.
  - Merges the filtered `daily_activity` with the `sleep` dataframe based on common columns "Id" and "Date" using the `merge()` function.

- **Removing Duplicates and Calculations:**
  - Removes duplicate rows from the merged dataframe using the `distinct()` function.
  - Creates a new column named "NoSleepHours" in the merged dataframe, `activity_sleep_merged`, representing the difference between "TotalHoursInBed" and "TotalHoursAsleep" for each row.
  
## Data Analysis to Derive Insights

In this phase, I delved into the refined data to discern the distinct usage patterns of Bellabeat's smart devices, aiming to uncover insights into how people are already utilizing their products.

Certainly! Here's a slightly more detailed description of each analysis:

1. **Average Steps:**
   - Calculates the mean of the "TotalSteps" column to understand the average number of steps recorded across all observations, providing an overview of overall activity levels.

2. **Average Steps per User:**
   - Groups the dataset by "Id" and computes the mean of "TotalSteps" for each user individually, allowing for insight into the average steps taken by different users, highlighting variations in activity levels among users.

3. **Hourly Steps:**
   - Analyzes hourly step data to explore the distribution of steps throughout the day, helping identify peak activity periods and any patterns in activity levels over time.

4. **Weekly Steps:**
   - Examines weekly step data to observe step trends across different days of the week, enabling the identification of trends and patterns in activity levels throughout the week.

5. **Calories Burned Analysis:**
   - Investigates the relationship between total steps and calories burned using a scatter plot, providing insights into the correlation between physical activity (steps) and energy expenditure (calories burned), aiding in understanding the effectiveness of activity levels in burning calories.

6. **Sleep Analysis:**
   - Explores the relationship between total sleep duration and sedentary hours using a scatter plot, aiming to understand how sleep duration correlates with sedentary behavior, which can provide insights into sleep quality and patterns.

7. **Activity Level Analysis:**
   - Visualizes the distribution of activity levels (e.g., Very Active Minutes, Fairly Active Minutes, Lightly Active Minutes, Sedentary Minutes) using a pie chart, offering insights into how time is allocated across different activity intensities, aiding in understanding overall activity patterns.

8. **Active vs. Non-Active Users:**
   - Categorizes users as "Active" or "Non-Active" based on activity levels and calculates the number of active and non-active users, providing an overview of user engagement levels and distribution among different activity levels.

9. **Very Active Minutes per Day:**
   - Calculates the total very active minutes per day to analyze patterns of high-intensity activity across different days of the week, aiding in understanding peak activity periods and trends in vigorous physical activity.

These analyses collectively offer insights into user behavior, including physical activity levels, sleep patterns, and user engagement, which can inform decision-making and strategies for improving user experience and engagement.

## Communicating Findings Through Visualizations

In this phase, I utilized R Studio to craft insightful visualizations that effectively communicate the outcomes of my analysis. The visualizations, along with the derived insights, can be accessed at the provided location. R Studio, with its powerful graphics capabilities, was instrumental in this process. Please note that the specific libraries used for visualization may vary based on the requirements of the analysis. The presentation explaining the visualization is attached here. [Presentation_of_findings](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bf288e0225d7556634069954b96b62c082fd4272/Presentation/Bellabeat_Data_Analysis.pptx)

## Principal Discoveries and Insights

1. **Calories Burned vs Very Active Minutes:** The positive correlation between very active minutes and calories burned suggests that increased physical activity leads to higher energy expenditure. This could indicate that users who engage in more active minutes could potentially achieve better fitness or weight loss results.
![Calories Burned vs Very Active Minutes](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization/calories_burned_vs_very_active_minutes_plot.jpg)

2. **Calories Burned vs Total Steps:** The positive correlation between total steps taken and calories burned. This suggests that the more steps a user takes, the more calories they burn. This insight could be particularly useful for users aiming to increase their physical activity or manage their weight. It also underscores the importance of regular movement and exercise in daily calorie expenditure.
![Calories Burned vs Total Steps](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization/calories_burned_vs_total_steps_plot.jpg)

3. **Total Sleep Time vs Sedentary Hours:** The negative correlation between total sleep time and sedentary hours could suggest that users who sleep more tend to be less sedentary. This could be due to various factors such as better rest leading to increased activity or longer sleep durations reducing available time for sedentary activities.
![Total Sleep Time vs Sedentary Hours](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization/total_hours_asleep_vs_sedentary_plot.jpg)

4. **Weekly Steps:** The pattern of physical activity varying throughout the week could suggest lifestyle habits such as work schedules or weekly routines influencing physical activity. The peak on Tuesday might suggest mid-week being the most active period for most users.
![Weekly Steps](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization/weekly_step_plot.jpg)

5. **Total Hours Asleep vs Hours In Bed (with Total Hours In/Out of Bed):** The positive correlation suggests that as the total hours in bed increase, the total hours asleep also tend to increase. However, there are some outliers which could be further investigated to understand the reasons behind them.
![Total Hours Asleep vs Hours In Bed](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization/total_hours_assleep_Vs_in_bed_plot.jpg)

6. **Calories Burned vs Total Steps (with Sedentary Minutes):** The different colors of the data points represent various levels of sedentary minutes. This could suggest that even with a high step count, the amount of sedentary time can significantly impact the total calories burned.
![Calories Burned vs Total Steps(with Sedentary Minutes)](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization/calories_vs_steps_for_sedentiary_plot.jpg)

7. **Hourly Steps:** The bar graph shows a clear pattern of activity throughout the day, with peaks during certain hours. This could suggest that users are more active during specific times of the day.
![Hourly Steps](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization/hourly_step_plot.jpg)

8. **Total Hours Asleep During the Week:** This shows a progressive increase in sleep duration from Monday to Sunday, with the least sleep on Monday (around 4 hours) and the most on Sunday (approaching 6 hours), indicating that the individual tends to sleep more on the weekends compared to the weekdays.
![Total Hours Asleep During the Week](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization/average_sleep_by_day_of_week_plot.jpg)

9. **Very Active Minutes per day:** This shows the individual’s activity level varies significantly throughout the week. The least active day is Sunday with just over 1000 minutes of activity, while the most active day is Saturday with nearly 2,000 minutes. The activity level on weekdays also varies, with Monday and Friday around 1,500 minutes and Tuesday to Thursday exceeding 1,500 minutes.
![Very Active Minutes per day](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization/active_minutes_per_day_plot.jpg)

## Suggestions for Bellabeat App

**Trends in Smart Device Usage:**

1. **Active Minutes and Calories Burned:** Users who engage in more active minutes tend to burn more calories.

2. **Total Steps and Sedentary Minutes:** Even with a high step count, the amount of sedentary time can significantly impact the total calories burned.

3. **Sleep Time and Sedentary Hours:** Users who sleep more tend to be less sedentary.

4. **Weekly Steps:** Physical activity varies throughout the week, with a peak on Wednesday.

**Application to Bellabeat Customers:**

1. **Active Minutes and Calories Burned:** Bellabeat customers could use this information to set personal goals for active minutes to increase their calorie burn.

2. **Total Steps and Sedentary Minutes:** This information could help Bellabeat customers understand the importance of reducing sedentary behavior, even if they meet their daily step goals.

3. **Sleep Time and Sedentary Hours:** Understanding the correlation between sleep time and sedentary behavior could help Bellabeat customers improve their sleep habits and overall health.

4. **Weekly Steps:** This information could help Bellabeat customers plan their weekly schedules to incorporate more physical activity.

**Influence on Bellabeat Marketing Strategy:**

1. **Active Minutes and Calories Burned:** Bellabeat could highlight how their products support users in achieving their activity goals and improving their fitness or weight loss results.

2. **Total Steps and Sedentary Minutes:** Bellabeat could educate users about the importance of reducing sedentary behavior through in-app articles, notifications, or personalized insights.

3. **Sleep Time and Sedentary Hours:** Bellabeat could enhance their sleep analysis features and market these to users who are looking to improve their sleep quality and overall health.

4. **Weekly Steps:** Bellabeat could provide users with insights into their weekly activity patterns and encourage them to increase activity on less active days. This could be a key point in their marketing campaigns.

## Recommendations

1. **Personalized Activity Goals:** Given the variation in activity levels throughout the week, Bellabeat could offer personalized activity goals that adapt to a user's weekly routine. For example, the app could suggest lower activity goals on Sundays when users tend to be less active and higher goals on Saturdays when they are most active.

2. **Sleep Improvement Features:** As users tend to sleep more on the weekends, Bellabeat could provide features to help users improve their sleep during the weekdays. This could include sleep tracking, sleep hygiene tips, or relaxation techniques to help users fall asleep faster.

3. **Sedentary Behavior Alerts:** Considering the wide range of sedentary minutes observed in the "Calories Burned vs Total Steps" visualization, Bellabeat could implement features that encourage users to move more during their sedentary periods. This could include reminders to stand up or walk around after a certain period of inactivity.

4. **Educational Content:** Bellabeat could provide educational content about the benefits of regular physical activity and good sleep habits. This could help users understand the importance of these behaviors for their overall health and motivate them to reach their activity and sleep goals.

5. **Marketing Strategy:** These insights could inform Bellabeat's marketing strategy. For example, they could highlight how their products support users in achieving their activity goals and improving their sleep. They could also target their marketing efforts towards the beginning of the week when users are typically less active, encouraging them to start their week off strong.

## Conclusion

The analysis of smart device usage data has provided valuable insights into consumer behavior and preferences. By leveraging these insights, Bellabeat can develop targeted marketing strategies to drive growth and enhance user experience. Moving forward, continuous monitoring and analysis of user data will be essential for maintaining a competitive edge in the wellness industry.

---
*Note: These insights and recommendations are based on visualizations created using R Studio
For more details, please refer to the [full analysis](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/blob/951db3f16ad262035bb88021bc9e5ba1a990faf0/Scripts/Bellabeat_Data_Analysis_Script) and [visualizations](https://github.com/ShriHariKJ/bellabeat_case_study.github.io/tree/bc413a27ccab85a54c0315d2954dbb3b046fc716/Visualization) in this repository.*
