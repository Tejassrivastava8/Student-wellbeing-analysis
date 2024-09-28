# Student-wellbeing-analysis

## Overview

The analysis utilizes data from **1,100 students**, assessed through a Likert scale ranging from **0 to 5**. In this scale, higher values represent more severe or stronger conditions. Key areas of focus include:

### Key Areas of Focus:
- **Psychological Factors**: Anxiety levels, self-esteem, depression
- **Physiological Factors**: Sleep quality, frequency of headaches
- **Environmental Factors**: Living conditions, noise levels, unmet basic needs
- **Academic Factors**: Academic performance, study load
- **Social Factors**: Incidence of bullying, participation in extracurricular activities

## Power BI Dashboard Breakdown

The Power BI report is structured into three main pages:

1. **Page 1**:
   Includes correlations between critical factors such as:
     - Anxiety and academic performance
     - Depression and sleep quality
     - Bullying and mental health history

3. **Page 2**: 
   - Presents metrics with DAX measures, offering a clear view of the data collected.

4. **Page 3**: 
   - Features a **Correlation Heatmap** that visually represents the relationships between various variables. 
   - Notable correlations include:
     - **Poor sleep** correlating strongly with **depression** (0.71).
     - **Anxiety** negatively impacting **academic performance** (-0.65).
     - Insights on how bullying is associated with mental health issues.

## DAX Measures
- Academic negative effect = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[academic_performance]<3&&StressLevelDataset[study_load]>3&&StressLevelDataset[teacher_student_relationship]<3&&StressLevelDataset[future_career_concerns]<2))
- Physiological negative effect = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[headache]>3&&StressLevelDataset[blood_pressure]>2&&StressLevelDataset[sleep_quality]<3&&StressLevelDataset[breathing_problem]>3))
- Environmental negative effect = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[noise_level]>3&&StressLevelDataset[living_conditions]<3&&StressLevelDataset[safety]<2&&StressLevelDataset[basic_needs]<3))
- Psycological negative effect = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[anxiety_level]>10&&StressLevelDataset[self_esteem]<15&&StressLevelDataset[mental_health_history]=1&&StressLevelDataset[depression]>15))
- Social negative effect = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[social_support]<1&&StressLevelDataset[peer_pressure]>3&&StressLevelDataset[extracurricular_activities]<3&&StressLevelDataset[bullying]>2))
- Below avg academics = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[academic_performance]<3))
- extracurricular activity = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[extracurricular_activities]>=2))
- Frequent headaches = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[headache]>=5))
- High noise = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[noise_level]>=2))
- Percentage of bullying = DIVIDE(COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[bullying]>=3)),COUNTROWS(StressLevelDataset))*100
- Percentage students with depression = DIVIDE(COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[depression]>10)),COUNTROWS(StressLevelDataset))*100
- Poor sleep = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[sleep_quality]<=2))
- Students with low self esteem = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[self_esteem]<AVERAGE(StressLevelDataset[self_esteem])))
- unmet basic needs = COUNTROWS(FILTER(StressLevelDataset,StressLevelDataset[basic_needs]<=2))

## Python code for Correlation Heatmap
  ```python
   import seaborn as sns
  import matplotlib.pyplot as plt
  sns.heatmap(dataset.corr(), cmap='Purples', annot=True)
  plt.show()
```



**This analysis is for educational purposes only**
