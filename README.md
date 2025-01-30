# Arrest Analysis Project

## Project Overview
The Arrest Analysis Project aims to analyze arrest data to identify trends, patterns, and disparities in arrest rates. By examining demographics, crime types, arrest locations, and outcomes, this project provides insights that can help inform law enforcement practices and criminal justice policies. The analysis was conducted using SQL for data manipulation, Excel for data cleaning, and Tableau for visualizations.

The dataset used in this analysis can be accessed via [data.world](https://data.world/rubyn/ses-demographics-arrests-analysis/), and interactive visualizations are available on [Tableau](https://public.tableau.com/app/profile/ruby4573/viz/ArrestsintheUnitedStates/ArrestsintheUnitedStates).

## Dataset
The analysis is based on the **Arrest Analysis** dataset, which includes detailed records of arrests, offender demographics, offense types, arrest outcomes, and geographic information. The dataset can be accessed via [data.world](https://data.world/rubyn/ses-demographics-arrests-analysis/). Data cleaning, normalization, and feature engineering techniques were applied to ensure the analysis is accurate and meaningful.

## Introduction
This dataset provides a detailed view of arrests across various regions, with a focus on demographic factors, crime types, and the locations where arrests occur. The goal of this analysis is to uncover insights that could improve criminal justice practices, reduce disparities, and optimize resource allocation.

## Project Objectives
1. Analyze demographic factors (e.g., race, age, gender) in relation to arrest patterns.
2. Identify the most common crime types and arrest outcomes across different regions and time periods.
3. Explore geographic trends in arrests, including regional disparities.
4. Provide actionable recommendations to improve criminal justice policies based on the analysis.

## Methodology
1. **Data Cleaning and Preparation**:
   - Addressed missing values, outliers, and inconsistencies in the dataset.
   - Merged datasets using SQL queries to combine arrest, demographic, and offense data.

2. **SQL for Data Transformation**:
   - Used SQL to clean, join, and filter data across multiple tables. Example queries:
     - Combined arrest and demographic data based on common identifiers such as `person_id`.
     - Created calculated fields to classify crime types and calculate the time between offenses and arrests:
       ```sql
       SELECT 
           arrest_data.person_id, 
           arrest_data.arrest_date, 
           demographic_data.age, 
           demographic_data.race, 
           CASE 
               WHEN offense_type = 'Drug' THEN 'Drug-related Crime'
               WHEN offense_type = 'Property' THEN 'Property Crime'
               ELSE 'Other'
           END AS crime_type
       FROM 
           arrest_data
       JOIN 
           demographic_data 
       ON 
           arrest_data.person_id = demographic_data.person_id;
       ```

   - Cleaned data by removing duplicates and resolving missing demographic values using filtering and `COALESCE()`:
     ```sql
     SELECT * FROM arrest_data
     WHERE age IS NOT NULL 
     AND race IS NOT NULL;
     ```

   - **State Populations and Proportions**: The following SQL query was used to combine state population data with arrest demographic data, enabling detailed analysis of arrest rates across various demographic groups for different states and years:

     ```sql
     -- Sample SQL Query to combine state population data with arrest demographics data
     SELECT 
         state_population,
         state_white_population,
         state_proportion_of_white,
         state_black_population,
         state_proportion_of_black,
         state_asian_population,
         state_proportion_of_asian,
         state_indian_population,
         state_proportion_of_indian,
         state_pacific_population,
         state_proportion_of_pacific,
         state_two_or_more_races_population,
         state_proportion_of_two_or_more_races,
         state_non_hispanic_population,
         state_proportion_of_non_hispanic,
         state_hispanic_population,
         state_proportion_of_hispanic
     FROM 
         state_pop_and_proportions, ses_arrests_demographics_v1
     WHERE 
         state_pop_and_proportions.state = ses_arrests_demographics_v1.state
         AND state_pop_and_proportions.year = ses_arrests_demographics_v1.year
     ORDER BY 
         state_pop_and_proportions.state, state_pop_and_proportions.year;
     ```

   This SQL query helps merge the state population data and arrest demographics, allowing us to analyze arrest trends across different demographic groups for each state over time.

3. **Exploratory Data Analysis (EDA)**:
   - Performed visualizations and statistical analysis to explore the relationships between demographic factors, crime types, and arrest outcomes.
   - Investigated correlations between arrest locations and crime types, and how these factors relate to demographics.

4. **Segmentation and Clustering**:
   - Applied clustering techniques (e.g., K-means clustering) to group arrests based on shared characteristics such as location, time of day, and crime type.
   - Analyzed the differences in arrest patterns across these clusters.

5. **Predictive Modeling**:
   - Built predictive models to estimate arrest outcomes based on demographic and crime-related factors.
   - Evaluated the models' performance using accuracy, precision, recall, and F1 score.

## Visual Representations

### Arrest Type Distribution
Bar charts showing the distribution of different types of arrests across various regions, highlighting common offenses and arrest outcomes.

### Demographics and Arrest Trends
Heatmaps and scatter plots displaying the relationship between age, gender, and race with arrest types and outcomes.

### Crime Types and Arrest Locations
Maps and plots showing the geographic distribution of arrests for different crime types, revealing trends in specific locations.

### Arrest Outcome Prediction
A chart comparing the accuracy of different predictive models for arrest outcomes, including precision and recall rates.

## Key Findings
- **Demographic Disparities**:
  - Certain demographic groups, especially younger individuals and certain racial groups, experience higher arrest rates.
  - Male individuals are arrested more frequently than females, with the highest rates occurring among young adults.

- **Common Crime Types**:
  - Drug-related crimes are the most common offenses leading to arrests, followed by property crimes like burglary and theft.
  - Violent crimes, while less frequent, tend to result in more severe arrest outcomes.

- **Geographic Patterns**:
  - Urban areas show higher arrest rates compared to rural areas, with some neighborhoods showing higher concentrations of particular crimes.
  - Some regions exhibit significant racial disparities in arrests, indicating potential issues in law enforcement practices.

- **Arrest Outcome Insights**:
  - Arrest outcomes are often influenced by the severity of the offense, the criminal history of the individual, and regional law enforcement practices.
  - Predictive models show that prior criminal history and geographic location are key factors in determining the likelihood of certain arrest outcomes.

## Conclusion
The Arrest Analysis project reveals important insights into arrest patterns, highlighting demographic disparities and geographic trends. By focusing on these findings, law enforcement agencies and policymakers can work to reduce disparities, improve resource allocation, and enhance criminal justice practices.

## Recommendations for Improvement
- **Address Demographic Disparities**: Law enforcement should focus on reducing disparities in arrest rates based on race and age, particularly in urban areas.
- **Optimize Resource Allocation**: Use predictive models to allocate law enforcement resources more effectively, targeting high-risk areas and times for crimes.
- **Policy Reforms**: Implement reforms to address racial biases in arrests and create programs that promote fairer treatment across all demographic groups.

## Future Directions
1. **Deeper Demographic Analysis**: Investigate further the reasons behind racial and age-related disparities in arrest rates and outcomes.
2. **Sentencing Analysis**: Examine how arrest patterns influence sentencing outcomes, particularly for marginalized communities.
3. **Predictive Analytics for Crime Prevention**: Leverage machine learning models to predict crime hotspots and deploy resources proactively.

---

This README provides a comprehensive overview of the Arrest Analysis Project. The analysis was completed by a team of 4, who collaborated on the data analysis and final reporting. For interactive visualizations, check out the project on [Tableau](https://public.tableau.com/app/profile/ruby4573/viz/ArrestsintheUnitedStates/ArrestsintheUnitedStates).

The dataset used in the analysis can be accessed via [data.world](https://data.world/rubyn/ses-demographics-arrests-analysis).
