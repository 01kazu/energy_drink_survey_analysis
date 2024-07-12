# CodeX Energy drink survey analysis

# Table of Contents

- [Introduction](#introduction)
- [Objective](#objective)
  - [Tools](#tools)
- [Data Exploration](#data-exploration)
- [Data Cleaning](#data-cleaning)



# Introduction
CodeX is a German beverage company that is aiming to make its mark in the Indian market. A few months ago, they launched their energy drink in 10 cities in India.
Their Marketing team is responsible for increasing brand awareness, market share, and product development. They conducted a [survey](assets/docs/Survey_Questions_and_Response_Options.pdf) in those 10 cities and received results from 10,000 respondents. 

# Objective

- What is the key pain point?

  The Chief Marketing Officer wants to know what meaningful insights can be found in the survey collected and how they can help his team make decisive actions.

- What is the solution?
  
  - I have to answer [questions](assets/docs/Primary_Secondary_Insights.pdf) based on the data given.
  
  - To create a dashboard that provides insights about the survey questions' responses. I will be focusing on:
    1. Marketing channels
    2. Purchase locations
    3. Typical consumption situations
    4. Expected price range of energy drink
    5. Time preferred to consume energy drinks
    6. Number of times energy drinks are consumed


    ## Tools
  
    | Tool | Purpose |
    | --- | --- |
    | Python | Exploring, cleaning, analyzing the data |
    | Power BI | Visualizing the data via interactive dashboards |
    | GitHub | Hosting the project documentation and version control |

# Data Exploration
- These are my initial observations on the datasets given:
  1. There are no missing data points in all three datasets.
  2. The column **Tried_before** of the [fact_survey_responses.csv](assets/datasets/fact_survey_responses.csv) dataset indicates if the respondants have tried our product or not. There is another column **Taste_experience** that allows respondants to give a rating on our product if they have tried it. It seems some respondants responded No to **Tried_before** while still giving a rating. So that has to be corrected.
  3. The column **Reasons_preventing_trying** of the [fact_survey_responses.csv](assets/datasets/fact_survey_responses.csv) dataset indicates why respondents who answered No to the **Tried_before** column did not try our product. Respondents who answered Yes to the **Tried_before** column should not have responded to the **Reasons_preventing_trying** column. So that has to be corrected.
  4. The column **Brand_perception** of the [fact_survey_responses.csv](assets/datasets/fact_survey_responses.csv) dataset indicates what respondents who answered Yes to the **heard_before** column think of our product. Respondents who answered No to the **Heard_before** column should not have any response in the **Brand_perception** column. This has to be corrected.

# Data Cleaning
- The pandas and the numpy packages in the python programming language will be used to change values of the columns to expected Null values. These are the conditions:
  
| Condition | Column Name | Expected Value |
| --- | --- | --- |
| **Tried_before** = No | **Taste_experience** | NULL |
| **Tried_before** = Yes | **Reasons_preventing_trying** | NULL |
| **Heard_before** = No | **Brand_perception** | NULL |

Below are the codes used to execute the cleaning of data:

```python
not_tried_before = fact_survey_responses['Tried_before'] == 'No'
fact_survey_responses.loc[not_tried_before, 'Taste_experience'] = np.nan
```
```python
tried_before = fact_survey_responses['Tried_before'] == 'Yes'
fact_survey_responses.loc[tried_before, 'Reasons_preventing_trying'] = np.nan
```
```python
heard_before = fact_survey_responses['Heard_before'] == 'No'
fact_survey_responses.loc[heard_before, 'Brand_perception'] = np.nan
```
