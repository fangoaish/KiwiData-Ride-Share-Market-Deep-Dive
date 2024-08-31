# Analysis of Ride-Sharing Market Growth Strategy

## Project Overview
This project aims to analyze and understand the performance and behavior of drivers based on ride data. By leveraging data from driver onboarding, ride details, and ride event timestamps, we can gain insights into driver activity, ride efficiency, and the impact of prime-time pricing. The analysis aims to uncover insights into **_driver lifetime value_**, **_driver retention_**, and **_factors contributing to driver churn_**.


![image](https://github.com/user-attachments/assets/d9ca1da7-10db-4214-952d-d9db99422af9)


## Business Objectives

It aims to optimize driver performance and customer satisfaction by analyzing data to increase driver lifetime value (LTV), extend driver tenure, predict and mitigate churn, and optimize high-value driver segments. This involves calculating LTV and tenure, identifying churn indicators, tailoring strategies for valuable segments, and enhancing revenue and ride efficiency with optimal pricing strategies and improved service reliability.


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
<img width="1440" alt="截圖 2024-06-25 21 14 19" src="https://github.com/user-attachments/assets/6afcfc35-37db-4f8a-8c0c-79fb4f810fe7">
<img width="1440" alt="截圖 2024-06-25 21 14 22" src="https://github.com/user-attachments/assets/242ccf07-081a-4d8a-b67b-6942ac1f1abe">


## Analysis Overview
https://github.com/fangoaish/Pythong__Ride_Sharing_Market_Deep_Dive/blob/main/Driver_performance_and_ride_metrics.pptx.pdf


## Analysis Conclusion
- Key Insights: Most rides are under 10 km and 33 minutes. The average LTV is $1531 and the driver lifetime is 55 days, with a churn rate of 15.9%.
- Factors Affecting LTV: For each unit increase in total earnings, the LTV increases by approximately 0.25 units.
- Churn Indicators: Longer wait times and lower earnings predict driver churn; optimizing dispatch and improving compensation can reduce turnover.
- Segment-Specific Approaches: Retain top performers (average LTV revenue $1157) with personalized rewards, and boost mid-value driver engagement with targeted incentives. Improve low-frequency driver engagement through feedback-driven improvements and tailored promotions.

The analysis will help identify patterns and trends in ride distances, durations, and the effects of PrimeTime on ride metrics, ultimately contributing to optimized driver performance and customer satisfaction.
