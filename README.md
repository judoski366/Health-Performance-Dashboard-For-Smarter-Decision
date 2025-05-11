# Health-Performance-Dashboard-For-Smarter-Decision
![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/Health%20dashboard.PNG)

## Table Of Content
 - [INTRODUCTION](#INTRODUCTION)
 - [ASK](#ASK)
 - [PREPARE](#PREPARE)
 - [PROCESS](#PROCESS)
 - [ANALYZE](#ANALYZE)
 - [SHARE](#SHARE)
 - [ACT](#ACT)

### INTRODUCTION

Imagine having a personal health assistant that never sleeps — one that tracks your fitness progress, monitors vital signs, and helps you make smarter health decisions, all in real-time. What if you could visualize your wellness journey with just a glance at a dashboard, spotting trends, identifying risks, and optimizing your routine effortlessly?

Welcome to the world of data-driven health tracking! In today’s digital era, information is power, and when it comes to health, having the right insights at the right time can be life-changing. Whether you’re a fitness enthusiast, a healthcare professional, or just someone trying to stay on top of your well-being, a Health Tracker Performance Dashboard can revolutionize the way you monitor your progress.

In this post, I’ll take you through a step-by-step guide to building an interactive dashboard that transforms raw health data into meaningful insights. From choosing the right metrics to designing intuitive visualizations, you’ll learn how to create a powerful tool that makes health tracking smarter and more efficient.

Ready to take control of your health like a pro? Let’s dive in!

---

## ASK

The Health Tracker Performance Dashboard is designed to provide valuable insights into key health metrics, enabling data-driven decisions for better health monitoring and management. Using the six phases of data analysis, this project begins with the Ask (Reason), where we define clear objectives.

Objectives:

* Monitor Key Health Metrics: Track vital signs, fitness levels, and overall health trends using real-time data.
* Identify Patterns and Anomalies: Detect irregularities in health data that may require attention or intervention.
* Enhance Decision-Making: Provide actionable insights to individuals, healthcare professionals, or wellness coaches.
* Improve User Engagement: Design an intuitive, user-friendly dashboard for seamless interaction and data interpretation.
* Optimize Preventive Healthcare: Enable early detection of potential health issues through continuous monitoring.
* Personalize Health Insights: Customize recommendations based on individual health data and trends.
* Ensure Data Accuracy and Integrity: Implement robust data collection, validation, and visualization techniques.

These objectives serve as the foundation for building a comprehensive, data-driven health performance dashboard that empowers users to take charge of their well-being.

---

## PREPARE

### Data Collection & Methodology
This dataset was specifically created for the Lagos Tableau User Group, aiming to provide a structured and insightful representation of health performance metrics. The dataset includes key indicators necessary for tracking and analyzing health trends effectively.

### Dataset Overview
The dataset consists of 730 rows and 15 key columns, capturing essential health metrics for performance tracking and analysis. Below is a brief description of each column:

* Date: The recorded date of the health metrics, enabling trend analysis over time.
* Weight (kg): The individual’s body weight in kilograms, crucial for monitoring weight fluctuations and health progress.
* Height (cm): The individual’s height in centimeters, used to calculate BMI and assess overall body composition.
* BMI (Body Mass Index): A derived metric indicating body fat levels, calculated as weight (kg) / (height (m)²), helping assess whether a person is underweight, normal weight, overweight, or obese.
* Calories Intake: The total number of calories consumed per day, essential for tracking diet and energy balance.
* Calories Burned: The number of calories burned through physical activity and metabolic functions, aiding in understanding energy expenditure.
* Sleep Duration (hours): The total hours of sleep per night, crucial for analyzing sleep patterns and overall well-being.
* Steps Count: The total number of steps taken in a day, providing insights into physical activity levels.
* Heart Rate (bpm): The average heart rate in beats per minute (bpm), a key indicator of cardiovascular health.
* Mood Score: A subjective rating (e.g., on a scale of 1–10) indicating the individual’s emotional state and well-being.
* Water Intake (liters): The amount of water consumed in liters, essential for hydration tracking and overall health.
* Blood Pressure Systolic (mmHg): The upper number in a blood pressure reading, measuring the force of blood against artery walls during heartbeats.
* Blood Pressure Diastolic (mmHg): The lower number in a blood pressure reading, measuring the force of blood against artery walls between heartbeats.
* Date Period: The specific time frame (e.g., daily, weekly, monthly) used for aggregation and trend analysis.

These columns collectively provide a comprehensive overview of an individual’s health, supporting data-driven insights for improved well-being and lifestyle adjustments.

---

## PROCESS

### Data Transformation
To prepare the dataset for analysis, I utilized Microsoft Excel for an initial data review and cleaning, ensuring accuracy and consistency. Afterward, I imported the dataset into Tableau for visualization and further transformation.

### Key Data Processing Steps

#### 1. Data Review & Cleaning (Excel)
Checked for missing values and inconsistencies.
Ensured all numerical data were formatted correctly.
Verified that the Date column was in the correct format for time-based analysis.
#### 2. Data Import & Organization (Tableau)
Loaded the cleaned dataset into Tableau.
Organized fields into appropriate folders for easier navigation.
#### 3. Calculated Fields in Tableau: 
Created custom calculations to enhance analysis and insights. These fields were grouped into the following Categories:

* Date Calculation — Used for time-based comparisons (e.g., current vs. prior period).
* Latest Metric — Extracted the most recent value for each health metric.
* Negative Difference — Highlighted when a metric decreased compared to the previous period.
* No Difference — Indicated when there was no change in a metric from the prior period.
* Positive Difference — Showed when a metric increased compared to the previous period.
* Prior Metrics — Stored values from the previous period for comparison.

#### Date Calculation Folder
* Latest Date: { MAX([Date])}
* Latest Day: DATETRUNC(‘day’,[Date]) = DATEADD(‘day’, -1, DATETRUNC(‘day’, { MAX([Date])} +1))
* Latest Month: DATETRUNC(‘month’, [Date]) = DATEADD(‘month’, -1, DATETRUNC(‘month’, { MAX([Date])} + 1))
* Latest Week: DATETRUNC(‘week’, [Date]) = DATEADD(‘week’, -1, DATETRUNC(‘week’, { MAX([Date])} + 1))
* Latest Year: DATETRUNC(‘year’, [Date]) = DATEADD(‘year’, -1, DATETRUNC(‘year’, { MAX([Date])} + 1))
* Prior Month: DATEADD(‘month’, -1, {MAX([Date])})
* Prior Week : DATEADD(‘week’, -1, {MAX([Date])})
* Prior year: DATEADD(‘year’, -1, {MAX([Date])})
* Date Period Selected: CASE [Parameters].[Date Period]
WHEN ‘Last Week’ THEN DATENAME(‘day’, [Date])
WHEN ‘Last Month’ THEN DATENAME(‘day’, [Date])
WHEN ‘Last Year’ THEN DATENAME(‘month’, [Date])
END
* Date Period: CASE [Parameters].[Date Period]
WHEN ‘Last Week’ THEN [Latest Week]
WHEN ‘Last Month’ THEN [Latest Month]
WHEN ‘Last Year’ THEN [Latest Year]
END.
* Date Color: same formula as Date Period

#### Latest Metrics Folder
* Latest BMI: AVG(IF [Date] = [Latest Date]
THEN [BMI]
END)
* Latest BP Diastolic: AVG(IF [Date] = [Latest Date]
THEN [Blood Pressure Diastolic (mmHg)]
END)
* Latest BP Systolic: AVG(IF [Date] = [Latest Date]
THEN [Blood Pressure Systolic (mmHg)]
END)
* Latest Calories Burned: AVG(IF [Date] = [Latest Date]
THEN [Calories Burned)]
END)
* Latest Calories Intake: AVG(IF [Date] = [Latest Date]
THEN [Calories Intake]
END)
* Latest HR bpm: AVG(IF [Date] = [Latest Date]
THEN [Heart Rate (bpm)]
END)
* Latest Mood Score: AVG(IF [Date] = [Latest Date]
THEN [Mood Score (1–10)]
END)
* Latest Sleep Duration: AVG(IF [Date] = [Latest Date]
THEN [Sleep Duration (hours)]
END)
* Latest Steps Count: AVG(IF [Date] = [Latest Date]
THEN [Steps Count]
END)
* Latest Water Intake: AVG(IF [Date] = [Latest Date]
THEN [Water Intake (liters)]
END).

#### Prior Metrics Folder
* Prior Calories Burned: AVG(CASE [Parameters].[Date Period]
WHEN ‘Last Week’ THEN IF [Date] = [Prior Week] THEN [Calories Burned] END
WHEN ‘Last Month’ THEN IF [Date] = [Prior Month] THEN [Calories Burned] END
WHEN ‘Last Year’ THEN IF [Date] = [Prior Year] THEN [Calories Burned] END
END)
* Prior Calories Intake: AVG(CASE [Parameters].[Date Period]
WHEN ‘Last Week’ THEN IF [Date] = [Prior Week] THEN [Calories Intake] END
WHEN ‘Last Month’ THEN IF [Date] = [Prior Month] THEN [Calories Intake] END
WHEN ‘Last Year’ THEN IF [Date] = [Prior Year] THEN [Calories Intake] END
END)
* Prior Mood Score: AVG(CASE [Parameters].[Date Period]
WHEN ‘Last Week’ THEN IF [Date] = [Prior Week] THEN [Mood Score (1–10)] END
WHEN ‘Last Month’ THEN IF [Date] = [Prior Month] THEN [Mood Score (1–10)] END
WHEN ‘Last Year’ THEN IF [Date] = [Prior Year] THEN [Mood Score (1–10)] END
END)
* Prior Sleep Durations: AVG(CASE [Parameters].[Date Period]
WHEN ‘Last Week’ THEN IF [Date] = [Prior Week] THEN [Sleep Duration (hours)] END
WHEN ‘Last Month’ THEN IF [Date] = [Prior Month] THEN [Sleep Duration (hours)] END
WHEN ‘Last Year’ THEN IF [Date] = [Prior Year] THEN [Sleep Duration (hours)] END
END)
* Prior Steps Count: AVG(CASE [Parameters].[Date Period]
WHEN ‘Last Week’ THEN IF [Date] = [Prior Week] THEN [Steps Count] END
WHEN ‘Last Month’ THEN IF [Date] = [Prior Month] THEN [Steps Count] END
WHEN ‘Last Year’ THEN IF [Date] = [Prior Year] THEN [Steps Count] END
END)
* Prior Water Intake:
AVG(CASE [Parameters].[Date Period]
WHEN ‘Last Week’ THEN IF [Date] = [Prior Week] THEN [Water Intake (liters)] END
WHEN ‘Last Month’ THEN IF [Date] = [Prior Month] THEN [Water Intake (liters)] END
WHEN ‘Last Year’ THEN IF [Date] = [Prior Year] THEN [Water Intake (liters)] END
END)

#### Negative Difference Folder
* Calories Burn: IF [Latest Calories Burn] < [Prior Calories Burn]
THEN [Latest Calories Burn] — [Prior Calories Burn]
END
* Calories Intake: IF [Latest Calories Intake] < [Prior Calories Intake]
THEN [Latest Calories Intake] — [Prior Calories Intake]
END
* Mood Score: IF [Latest Mood Score] < [Prior Mood Score]
THEN [Latest Mood Score] — [Prior Mood Score]
END
* Sleep Duration: IF [Latest Sleep Duration] < [Prior Sleep Duration]
THEN [Latest Sleep Duration] — [Prior Sleep Duration]
END
* Steps Count: IF [Latest Steps Count] < [Prior Steps Count]
THEN [Latest Steps Count] — [Prior Steps Count]
END
* Water Intake: IF [Latest Water Intake] < [Prior Water Intake]
THEN [Latest Water Intake] — [Prior Water Intake]
END

#### Positive Difference Folder
* Calories Burn: IF [Latest Calories Burn] > [Prior Calories Burn]
THEN [Latest Calories Burn] — [Prior Calories Burn]
END
* Calories Intake: IF [Latest Calories Intake] > [Prior Calories Intake]
THEN [Latest Calories Intake] — [Prior Calories Intake]
END
* Mood Score: IF [Latest Mood Score] > [Prior Mood Score]
THEN [Latest Mood Score] — [Prior Mood Score]
END
* Sleep Duration: IF [Latest Sleep Duration] > [Prior Sleep Duration]
THEN [Latest Sleep Duration] — [Prior Sleep Duration]
END
* Steps Count: IF [Latest Steps Count] > [Prior Steps Count]
THEN [Latest Steps Count] — [Prior Steps Count]
END
* Water Intake: IF [Latest Water Intake] > [Prior Water Intake]
THEN [Latest Water Intake] — [Prior Water Intake]
END

#### No Difference Folder
* Calories Burn: IF [Latest Calories Burn] = [Prior Calories Burn]
THEN [Latest Calories Burn] — [Prior Calories Burn]
END
* Calories Intake: IF [Latest Calories Intake] = [Prior Calories Burn]
THEN [Latest Calories Intake] — [Prior Calories Burn]
END
* Mood Score: IF [Latest Mood Score] = [Prior Mood Score]
THEN [Latest Mood Score] — [Prior Mood Score]
END
* Sleep Duration: IF [Latest Sleep Duration] = [Prior Sleep Duration]
THEN [Latest Sleep Duration] — [Prior Sleep Duration]
END
* Steps Count: IF [Latest Steps Count] = [Prior Steps Count]
THEN [Latest Steps Count] — [Prior Steps Count]
END
* Water Intake: IF [Latest Water Intake] = [Prior Water Intake]
THEN [Latest Water Intake] — [Prior Water Intake]
END

These transformations allowed for better structuring and analysis of key performance indicators.

---

## ANALYZE

### Key Insights & Analysis
The Health Tracker Performance Dashboard provides a clear and insightful summary of key health metrics, enabling users to monitor their well-being effectively. Here are some key insights based on the dashboard visualization:

#### 1. Blood Pressure (BP)
* Today’s Reading: 101 / 86 mmHg (Stage 1 Hypertension)
* Average BP: 119 / 78 mmHg

#### Analysis:

* The systolic reading (101) is significantly lower than the average (119), indicating a drop in pressure, while the diastolic (86) is slightly above the average (78).
* This suggests a potential improvement in blood pressure management but requires monitoring to ensure it remains stable.

![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/BP.PNG)

#### 2. Heart Rate (HR)

* Today’s Reading: 77 bpm (Normal)
* Average HR: 69.33 bpm

#### Analysis:

* The current heart rate is higher than the average, which could indicate increased physical activity or stress.
  However, since it’s within a normal range, there’s no immediate concern.

![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/HR.PNG)

#### 3. Body Mass Index (BMI)

* Today’s BMI: 22.87 (Normal Weight)
* Average BMI: 23.10

#### Analysis:

* Slightly below the average BMI, suggesting weight has been maintained or slightly reduced. This could indicate a balanced diet and activity level.

![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/BMI.PNG)

#### 4. Calories Burned

* Today’s Calories Burned: 289.4 cal
* Average Calories Burned: 477.43 cal
* Change from Last Year: -180.5 cal

#### Analysis:

* Calories burned today are significantly lower than the average. This indicates reduced physical activity, which might require an adjustment in workout routines.

![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/Calories%20Burned.PNG)

#### 5. Calories Intake

* Today’s Intake: 1,424 cal
* Average Intake: 2,154.7 cal
* Change from Last Year: -747.4 cal

#### Analysis:

The calorie intake today is below the average, which might indicate a calorie deficit.
If intentional (e.g., weight loss goal), this is positive, but prolonged deficits could impact energy levels.

![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/Calories%20Intake.PNG)

#### 6. Steps Count

* Today’s Step Count: 13,690 steps
* Average Step Count: 10,726 steps
* Change from Last Year: +1,263 steps

#### Analysis:

* Steps taken today exceed the average, showing increased movement and improved physical activity. Positive progress in maintaining an active lifestyle.

![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/Total%20Steps.PNG)

#### 7. Water Intake

* Today’s Intake: 2.050 liters
* Average Intake: 2.2919 liters
* Change from Last Year: -0.7000 liters

#### Analysis:

* Below the average intake, indicating the need to slightly increase water consumption to stay hydrated.

![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/Water%20Intake.PNG)

#### 8. Sleep Duration

* Today’s Sleep: 5.150 hrs
* Average Sleep Duration: 7.6506 hrs
* Change from Last Year: -3.830 hrs

#### Analysis:

* Significant drop in sleep duration compared to the average. This suggests potential sleep deprivation, which could affect overall health and energy levels.

![](https://public.tableau.com/views/HealthProject_17409261794760/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

#### 9. Mood Score

* Today’s Mood Score: 6.540
* Average Mood Score: 6.024
* Change from Last Year: +1.330
* 
#### Analysis:

* The mood score is higher than the average, indicating an improvement in overall well-being and mental state.

![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/Mood%20Score.PNG)

---

## SHARE
#### Communicating Insights from the Dashboard Development

I designed a Tableau Health Tracker Performance Dashboard to provide a comprehensive overview of key health metrics. This dashboard integrates:

* A dynamic date selector that allows users to analyze data for different time periods.
* Bar charts displaying average values for each health metric, serving as a benchmark for comparison.
* Well-structured layouts using Tableau containers and padding, ensuring a clean and organized presentation.
* Effective formatting to enhance readability, making the dashboard intuitive and user-friendly.

#### Data Storytelling & Insights

 To make the dashboard engaging and insightful for stakeholders, I incorporated:

* Comparative Analysis: Each metric compares today’s values with both the average benchmark and last year’s data to highlight trends.
* Color-coded Indicators: Positive changes are highlighted in green, while declines are marked in red, ensuring quick visual interpretation.
* Concise Text Summaries: Each section includes brief insights on whether the user’s health metrics are within normal ranges or require attention.
* Icons & Visual Cues: Health-related icons enhance user engagement and make navigation more intuitive.

![](https://github.com/judoski366/Health-Performance-Dashboard-For-Smarter-Decision/blob/main/Dashboard%201.png)

The Health Tracker Performance Dashboard provides an intuitive way to monitor daily health trends, identify deviations from healthy benchmarks, and track progress over time. These insights enable users to make data-driven health improvements by adjusting diet, sleep, exercise, and hydration habits accordingly

---

## ACT

#### Key Recommendations

Based on the insights derived from the dashboard, here are actionable recommendations to improve overall health and well-being:

#### 1. Blood Pressure Management

* Since blood pressure (101/86 mmHg) falls within Stage 1 Hypertension, it is advisable to Reduce sodium intake and consume more potassium-rich foods (bananas, spinach).
Engage in regular physical activity (e.g., brisk walking, yoga). Monitor stress levels and practice relaxation techniques like meditation.

#### 2. Optimize Heart Health

* With a heart rate of 77 bpm, slightly above the average 69.33 bpm, maintaining cardiovascular health is key: Incorporate aerobic exercises like jogging or cycling.
Maintain a balanced diet rich in omega-3 fatty acids (salmon, flaxseeds). Ensure adequate hydration and sleep to support heart function.

#### 3. Maintain a Healthy BMI

* With a BMI of 22.87, which is within the normal range, focus on sustaining this balance: Continue engaging in regular physical activity to maintain weight.
Consume nutrient-dense foods rather than processed foods. Monitor calorie intake to prevent fluctuations.

#### 4. Increase Calorie Expenditure

* With 289.4 calories burned today, significantly lower than the average 477.43 calories, it is beneficial to: Increase daily physical activity (e.g., strength training, HIIT workouts).
Set a daily movement goal to avoid prolonged inactivity.
Track workouts using a fitness app or smartwatch to stay accountable.

#### 5. Improve Caloric Intake

* Since calorie intake is 1,424 calories, below the average 2,154.7 calories, focus on: Eating more whole foods, proteins, and healthy fats to meet energy needs.
Incorporating healthy snacks between meals to prevent calorie deficits. Ensuring meals are well-balanced with carbs, proteins, and fiber.

#### 6. Maintain High Step Count

* With 13,690 steps today, surpassing the average 10,726 steps, maintain this positive trend by: Setting a daily target of at least 10,000 steps.
Incorporating more outdoor activities like hiking or cycling. Using a standing desk or taking breaks to walk during work hours.

#### 7. Increase Hydration Levels

* With 2.05 liters of water intake, slightly below the average 2.29 liters, it is essential to: Set reminders to drink water at regular intervals.
Consume water-rich foods like watermelon, cucumber, and oranges. Carry a reusable water bottle to track daily intake.

#### 8. Improve Sleep Quality

Sleep duration is 5.15 hours, significantly below the average 7.65 hours, which may impact overall health: Establish a consistent sleep schedule (sleep/wake at the same time daily).
Reduce screen time before bedtime to improve sleep quality. Create a relaxing bedtime routine with meditation or reading.

#### 9. Maintain Positive Mental Well-being

* With a mood score of 6.54, above the average 6.02, it is important to: Continue engaging in stress-relieving activities (exercise, socializing).
Practice gratitude and mindfulness techniques for mental resilience. Ensure work-life balance to prevent burnout.

#### Overall Summary
The Health Tracker Performance Dashboard highlights areas of strength (step count, mood score, BMI) and areas needing improvement (sleep, calorie balance, blood pressure). By following these recommendations, users can enhance their physical health, emotional well-being, and long-term fitness goals.

Thank you for taking the time to read my analysis! I truly appreciate your interest and support. If you’d like to stay connected and explore more insights or collaborate, feel free to connect with me on my Profile.


 ---
## Additional Resources
**_To interact with the report, click[here](https://public.tableau.com/views/HealthProject_17409261794760/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)_**








