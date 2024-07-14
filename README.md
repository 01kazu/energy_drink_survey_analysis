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

# Data Analysis

## Primary Analysis
There are various questions provided by the marketing team that we are expected to answer:
* 1\. Demographic Insights
  
   * 1.a\. Who prefers energy drinks more? (male/female/non-binary)
       ![gender-group](assets/images/1_1.png)
     
       Looking into gender, 60% of the respondents are Male, about 35% are female and 5% are non-binary. More than half of our respondents are male. Therefore it seems            that males prefer energy drinks. This corresponds with information found [here]([https://typeset.io/questions/is-there-difference-in-energy-drink-consumption-and-gender-2d3ls3206u#:~:text=Energy%20drink%20consumption%20differs%20by,times%20more%20than%20women%201.](https://www.ingentaconnect.com/contentone/psp/hbpr/2022/00000009/00000003/art00006)), that more male take energy drinks than female. It also adds that males buy in more          quantity than females.
     
   * 1.b\. What age group prefers energy drinks more?
       ![age-group](assets/images/1_2.png)
     
       **19-30** age group purchases our product the most. They account for 55% of the dataset. Followed by the **31-45** age group which is 24% and **15-18** age group           which is 15%. It seems the **65+** age group purchased our product the least. It has to be taken into           
       consideration that the **15-18** age group has smaller bins than the other age ranges. According to the [NIC](https://www.nccih.nih.gov/health/energy-drinks#:~:text=Next%20to%20multivitamins%2C%20energy%20drinks,kinds%20of%20energy%20drink%20products.), Men of the **18-34** age group consume the most energy                     drinks, and almost one-third of teens between **12-17** age group drink them regularly.
     
   * 1.c\. Which type of marketing reaches the most Youth (15-30)? 
       ![15-30-group](assets/images/1_3.png)
     
       The top marketing channel for the 19-30 age range is **Online ads** which account for 48% of the respondents. The next marketing channel is **TV Commercial** which accounts for 25%. The bottom marketing channel is  **Print Media** which accounts for 6%.

* 2\. Consumer Preferences
    * 2.a\. 
    * 2.b\. 
       
     
   
