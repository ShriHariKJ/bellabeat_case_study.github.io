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


