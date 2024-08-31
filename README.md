# Analysis of Ride-Sharing Market Growth Strategy

## Project Overview
This project aims to analyze and understand the performance and behavior of drivers based on ride data. By leveraging data from driver onboarding, ride details, and ride event timestamps, we can gain insights into driver activity, ride efficiency, and the impact of prime-time pricing. The analysis aims to uncover insights into **_driver lifetime value_**, **_driver retention_**, and **_factors contributing to driver churn_**.


![image](https://github.com/user-attachments/assets/d9ca1da7-10db-4214-952d-d9db99422af9)


## Business Objectives

It aims to optimize driver performance and customer satisfaction by analyzing data to increase driver lifetime value (LTV), extend driver tenure, predict and mitigate churn, and optimize high-value driver segments. This involves calculating LTV and tenure, identifying churn indicators, tailoring strategies for valuable segments, and enhancing revenue and ride efficiency with optimal pricing strategies and improved service reliability.

![Driver_performance_and_ride_metrics pptx](https://github.com/user-attachments/assets/f039d19d-e9ac-4d4a-8d42-d133aaf5061f)



## Data Sources
These three datasets are provided to investigate:

### data/driver_ids.csv 
- **driver_id**: Unique identifier for a driver 
- **driver_onboard_date**: Date on which driver was onboarded 
### data/ride_ids.csv 
- **driver_id**: Unique identifier for a driver 
- **ride_id**: Unique identifier for a ride that the driver completed 
- **ride_distance**: Ride distance in meters 
- **ride_duration**: Ride durations in seconds 
- **ride_prime_time**: PrimeTime applied on the ride 
### data/ride_timestamps.csv 
- **ride_id**: Unique identifier for a ride 
- **event**: event describes the type of event (see below) 
- **timestamps**: Time of event


### Here’s an overview of the event types: 
- **requested_at** passenger requested a ride 
- **accepted_at** driver accepted a passenger request 
- **arrived_at** driver arrived at pickup point 
- **picked_up_at** driver picked up the passenger 
- **dropped_off_at** driver dropped off a passenger at destination
  
### We can make the following assumptions about the Kiwi rate card: 
- Base Fare $2.00 
- Cost per Mile $1.15 
- Cost per Minute $0.22 
- Service Fee $1.75 
- Minimum Fare $5.00 
- Maximum Fare $400.00 

### PrimeTime: 
When the demand for rides exceeds the supply drivers are incentivized to go out and drive more. Therefore for rides during PrimeTime a percentage of the total fare is added to the total fare. This percentage is given in the column ride_prime_time. For example, if the ride fare is $100 and PrimeTime equals 0, then the total fare is $100. But if the PrimeTime is equal to 50, the total fare will be $150. 

Fare and Revenue Calculation: 
1. $2.00 + Duration(min) * 0.22 + Distance(miles) * 1.15 
2. Add prime-time if applicable 
3. Enforce $5 minimum and $400 maximum 
4. Add 1.75 Service Fee 
Revenue: value for Kiwi is 20% of the fare, excluding the service fee


## Data Preparation
### Data Exploration
- to check for missing values, duplicates, and any anomalies in the datasets.
  - Data type 
  - Missing values 
    - I use the cross-check 
      - Dataframe -> shows the numbers of columns & rows
      - dataframe.info() -> shows the Non-Null count
      - Other way to check -> df.isnull().sum()
      - Duplicates 
      - Anomalies

![Driver_performance_and_ride_metrics pptx (2)](https://github.com/user-attachments/assets/d7dc15c5-bdec-4ac9-92d8-7320056cf7eb)



### Data Wrangling
- Handle Anomalies / Null values
- Convert the data type
- Convert the units
- Meters -> miles
- Seconds -> mins

![Driver_performance_and_ride_metrics pptx (3)](https://github.com/user-attachments/assets/25f6c580-9ff9-4cb6-8a9d-ea5420e63293)



## Exploratory Data Analysis
Before diving into the data sea, I'll categorize the hypotheses systematically based on our goal, establishing a structured and logical framework for thoughtful analysis.

- #### **Q:** Average Lifetime Value (LTV) of a Driver?
    - Why do I want to know? 
        - LTV -> driver acquisition and retention strategies.
    - So what?     
        - allocate resources efficiently, optimize marketing spend, and improve profitability by focusing on high-value drivers.
    - Measure by?
        - LTV = (ARPU * GM) / CCR
![Driver_performance_and_ride_metrics pptx (4)](https://github.com/user-attachments/assets/06cfdcb4-8d45-4f4f-a09c-19d01356d794)


- #### **Q:** Main Factors Affecting a Driver’s Lifetime Value?
    - Why do I want to know? 
        - Identifying these factors helps in understanding what drives higher LTV and enables targeted actions to enhance these factors.
    - So what?     
        - tailor strategies to increase driver satisfaction and longevity, leading to higher profits.
    - Measure by?
        - Correlating driver revenue with variables such as ride frequency, ride duration, ride distance, and prime-time percentage.
![Driver_performance_and_ride_metrics pptx (5)](https://github.com/user-attachments/assets/5a6ae426-07b6-42eb-ab65-865353f8d37a)




- #### **Q:**  Average Projected Lifetime of a Driver
    - Why do I want to know? 
        - Understanding the average tenure helps in forecasting driver availability and planning for recruitment and retention efforts.
    - So what?     
        - Knowing the average driver's lifetime aids in maintaining a steady supply of active drivers, which is crucial for meeting customer demand.
    - Measure by?
        - Calculating the time difference between the onboarding date and the last recorded ride for each driver, then averaging these durations.
![Driver_performance_and_ride_metrics pptx (6)](https://github.com/user-attachments/assets/eee8128f-18aa-428c-abee-4ea23481ad9a)




- #### **Q:** Driver Churn Analysis
    - Why do I want to know? 
        - Identifying churn patterns and predictive indicators allows for proactive measures to retain drivers and reduce turnover.
    - So what?     
        - Reducing driver churn leads to lower recruitment costs and a more stable workforce, enhancing service reliability and customer satisfaction.
    - Measure by?
        - Analyzing the time since the last ride for each driver, calculating the churn rate, and using statistical methods to identify churn predictors (e.g., ride frequency, earnings, and engagement levels).
![Driver_performance_and_ride_metrics pptx (7)](https://github.com/user-attachments/assets/6b735de4-482f-4ea4-bff2-39bbd26d29f7)




- #### **Q:** Do All Drivers Act Alike?
    - Why do I want to know? 
        - Customized approaches for different driver segments can enhance overall driver performance and satisfaction, leading to better service delivery.
    - So what?     
        - allocate resources efficiently, optimize marketing spend, and improve profitability by focusing on high-value drivers.
    - Measure by?
        - Segmenting drivers based on variables like ride frequency, revenue, ride duration, and prime-time usage, and comparing the segments.
![Driver_performance_and_ride_metrics pptx (8)](https://github.com/user-attachments/assets/f8852e33-56a4-4182-8766-6d486c6e2f11)




- #### **Q:** Specific Segments of Drivers Generating More Value?
    - Why do I want to know? 
        - Recognizing high-value segments helps in targeting retention efforts and designing incentives to keep these drivers engaged.
    - So what?     
        - Focusing on high-value drivers maximizes revenue and improves overall business performance by prioritizing the most profitable segments.
    - Measure by?
        - Analyzing revenue per driver and segmenting based on performance metrics (e.g., high-value, high-frequency drivers).
![Driver_performance_and_ride_metrics pptx (9)](https://github.com/user-attachments/assets/a2b93421-0f7b-4264-8602-689d6a9c1bf0)



## Analysis Conclusion
- Key Insights: Most rides are under 10 km and 33 minutes. The average LTV is $1531 and the driver lifetime is 55 days, with a churn rate of 15.9%.
- Factors Affecting LTV: For each unit increase in total earnings, the LTV increases by approximately 0.25 units.
- Churn Indicators: Longer wait times and lower earnings predict driver churn; optimizing dispatch and improving compensation can reduce turnover.
- Segment-Specific Approaches: Retain top performers (average LTV revenue $1157) with personalized rewards, and boost mid-value driver engagement with targeted incentives. Improve low-frequency driver engagement through feedback-driven improvements and tailored promotions.

The analysis will help identify patterns and trends in ride distances, durations, and the effects of PrimeTime on ride metrics, ultimately contributing to optimized driver performance and customer satisfaction.
