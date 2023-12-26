![Chicago](https://interactive.wttw.com/sites/default/files/explore-chicago-from-the-air-hero_02.jpg)


# Project Name: Unveiling Chicago's Mortality Insights

## Introduction

In the realm of public health governance in Cook County, the Office of the Medical Examiner plays a crucial role in providing empirical evidence for the justice system. This project proposes a tool to enhance the validity and accuracy of findings, addressing evolving challenges in public health.

The objective is to develop a method for efficiently directing resources to investigate non-natural deaths in the county with undetermined or pending manners of death. Additionally, we aim to identify commonly preventable patterns of unintentional deaths and propose interventions to prevent accidents or educate the public, thereby increasing overall safety in the county.

Our focus extends beyond Chicago to the entire Cook County region, aligning with the commitment of the Cook County Commissioner to rectify disparities and injustices post-COVID-19. The project utilizes a Neural Net to expedite the processing of primary and secondary causes of death, including clustering preventable deaths. This innovative approach provides culturally relevant educational information, contributing to broader public health initiatives.

### Background on Chicago

Chicago, often dubbed the "City of Big Shoulders," is the third-largest city in the United States, celebrated for its cultural diversity, economic prominence, and contributions to art and music. As we delve into the data from the Cook County Medical Examiner's Office, our analysis aims to address the specific needs of the entire county, going beyond the boundaries of any single city. However, it faces unique public health challenges and demographic disparities.

## Problem Statement 

Within the evolving landscape of public health governance in Cook County, the Office of the Medical Examiner remains a cornerstone, providing crucial empirical evidence for the justice system. While acknowledging the qualifications of the office's staff, our proposal aims to introduce a tool enhancing the validity and accuracy of findings, aligning with the ever-changing challenges in public health.

   **How can we establish a method to efficiently direct resources for investigating non-natural deaths in the county which have undetermined or pending manners of death? Can we identify commonly preventable patterns of unintentional deaths and direct interventions aimed at preventing accidents or educating the public to increase overall safety of the county?**

Our focus extends to addressing the prevalence of accidental deaths, especially in the post-COVID-19 era, aligning with the Cook County Commissioner's commitment to rectifying disparities and injustices.

### Relevance of the Project to Chicago:

This dataset's exclusive focus on Chicago provides a regional context for our analysis, addressing issues that directly impact Chicagoans. It is significant for:

- **Community Health:** Chicago's diverse neighborhoods present unique health challenges. Analyzing death causes and spatial patterns informs tailored community health initiatives.
- **Resource Allocation:** Understanding the relationship between death causes and zip codes guides resource allocation to areas with the greatest needs.
- **Policy Development:** Identifying correlations between geographic locations and death causes empowers data-driven policymaking to enhance public health and safety in Chicago.

In summary, our project leverages Chicago's unique dynamics and health challenges, exploring the causes of death in connection with specific zip codes to contribute to the well-being of its residents.

## Datasets

**Cook County Medical Examiner's Office Case data:** [Dataset Link](https://datacatalog.cookcountyil.gov/Public-Safety/Medical-Examiner-Case-Archive/cjeq-bs86)

**Zip code data:** [Dataset Link](https://www.unitedstateszipcodes.org/zip-code-database/)

### Data Dictionary 

| Column Name            | Description                                        |
|------------------------|----------------------------------------------------|
| date_of_incident       | Date and time of the incident.                    |
| date_of_death          | Date and time of the death.                       |
| age                    | Age of the deceased.                               |
| gender                 | Gender of the deceased.                            |
| race                   | Race of the deceased.                              |
| latino                 | Binary indicator (0 or 1) for Latino ethnicity.    |
| manner_of_death        | Manner of death (e.g., accident, natural causes).  |
| primary_cause          | Primary cause of death.                            |
| primary_cause_line_a   | Detailed description of the primary cause.         |
| primary_cause_line_b   | Additional information on the primary cause.      |
| primary_cause_line_c   | Further details on the primary cause.             |
| secondary_cause        | Secondary cause of death.                         |
| gun_related            | Binary indicator for deaths related to firearms.  |
| opioid_related         | Binary indicator for deaths related to opioids.   |
| cold_related           | Binary indicator for deaths related to cold conditions. |
| heat_related           | Binary indicator for deaths related to heat conditions. |
| commissioner_district  | District of the commissioner.                     |
| incident_city          | City where the incident occurred.                 |
| incident_zip_code      | Zip code of the incident location.                |
| longitude and latitude | Geographic coordinates of the incident location.  |
| residence_city         | City of residence of the deceased.                |
| residence_zip          | Zip code of the residence of the deceased.        |
| chicago_community_area | Community area in Chicago related to the incident.|
| covid_related          | Binary indicator for deaths related to COVID-19.  |
| age_range              | Categorized age range.                            |
| death_date             | Date of death.                                    |
| death_time             | Time of death.                                    |
| death_day              | Day of the week of death.                         |
| inc_date               | Date of the incident.                             |
| inc_time               | Time of the incident.                             |
| inc_day                | Day of the week of the incident.                  |
| long_topic             | Text data related to topics.                      |
| best_topic_num         | The best-fit topic number.                        |
| best_topic_name        | Name of the best-fit topic.                       |
| best_topic_perc        | Percentage relevance to the best-fit topic.       |

## Data Cleaning
Data cleaning is a crucial step in the data analysis process. In this project, we meticulously prepared and cleaned the dataset to ensure its quality and reliability. This involved handling missing data, removing duplicates, correcting inconsistencies, and transforming the data into a format suitable for analysis. By conducting thorough data cleaning, we laid a solid foundation for accurate and meaningful insights.

- Many Columns were dropped as they were not very relevant which are Case Number, Incident Address, Location, ObjectID, Chicago, Community Ward. 
- Many Columns were added to simplify things which are Age range, Death Date, Time and Day, Incident Date, Time and Date
- Empty Data boxes were filled with NaN, or 0 or dropped accordingly 
- True/False or Yes/No values were changed into 0 or 1

#### Additional Data Cleaning
**Topic Modeling Analysis: Full Dataset**
In our exploration of the full dataset, we employed Gensim's Latent Dirichlet Allocation (LDA) model to extract five distinct topics. The text used for this analysis was derived from the 'primary cause' column, which underwent preprocessing involving stemming and the creation of bigrams.

**Topic Modeling Analysis: Accidental Deaths**
For cases categorized under the 'ACCIDENTAL' manner of death, and specifically those not falling into the 'opioid-related,' 'gun-related,' 'heat-related,' or 'cold-related' categories provided in the dataset, we conducted topic modeling. Utilizing the Gensim LDA model, we identified three pertinent topics within the 'primary cause' column after applying preprocessing techniques such as stemming and bigram creation. 


## Models

#### RNN Model 
**Information Source:** 'Primary Cause' Column

**Technique:** Utilizing GloVe as a fixed, untrainable pre-trained text-embedding layer, augmented with a bidirectional layer, 0.2 dropout, and an output layer.

**Reason for Choosing RNN:** Acknowledging the significance of word order, the RNN model inherently considers the sequence of words, an essential aspect in our data's 'primary cause' column.

**Reason for Choosing Pre-trained Model:** Given the concise, repetitive, and convention-bound nature of the words in our 'primary cause' data, opting for a pre-trained model like GloVe is deemed more suitable than building a self-training model.

***Accuracy rate: 0.9749 precision: 97.9% Recall:98.6%***

**Conclusion:** The model has a relative high accuracy, and well balanced between type I and type II error

#### NLP Models 
For the modeling process, the primary focus was on creating a solid NLP (Natural Language Processing) model to use as a starting point. Multiple NLP models were created using a combination of text extractors (CountVectorizer and TfidfVectorizer) and types of models (Multinomial Naive Bayes and Logistic Regression). The first models centered on the text column “primary_cause,” which states the coroner’s final primary cause of death. The goal of these models is to predict whether a death is accidental or not based solely on the primary cause of death. The results of those models are as follows:

|Text Extractor|Type of Model|Accuracy|
|---|---|---|
|CountVectorizer| Multinomial Naive Bayes | 97.13% |
|CountVectorizer| Logistic Regression | **97.58%** |
|TfidfVectorizer | Multinomial Naive Bayes | 97.42% |
|TfidfVectorizer| Logistic Regression | 97.42% |

Next, the same process was applied to a column that included the ‘primary cause of death’ as well as the ‘secondary cause of death.’ Again, the combination of text extractors and model types were used, and the combination of CountVectorizer and Logistic Regression produced the best accuracy score:

|Text Extractor|Type of Model|Accuracy|
|---|---|---|
|CountVectorizer| Logistic Regression | **97.71%** |

However, there were many data points that had missing information regarding ‘secondary cause’ that were filled with ‘no_text’ in the cleaning process. So, while the accuracy score for the combination of primary and secondary causes of death is higher than the primary by itself, it was a model that was created based off of a vast amount of missing information. 

Being that our data points provided extended information about a death outside of the primary and secondary causes, models were created to include such data. The goal was to see if the NLP models that were created could be improved by including other information. The column ‘primary_cause’ clearly holds powerful information that should be included in a final model. To do this,  the ‘primary’ cause column needed to become binary. The solution to this was to break down the primary causes into the following categories:

|Category Number|Primary Causes|
|---|---|
|0| one_gunshot_wound | 
|1| gunshot_wounds_fall | 
|2| vehicle_collision | 
|3| drug_overdose | 
|4| miscellaneous | 

The dataset includes information regarding the time and date of the incident and time and date of death, as well as location information such as zip code and city of the incident and the residence of the deceased. Curiosity piqued interest into whether or not those dates/times/location were pertinent to building the best model possible. A multitude of models were created to test that, and the results are as follows:

| Date/Time/Locations Included? |Type of Model|Accuracy|
|---|---|---|
|No| Logistic Regression | 89.83% |
|No| K-Nearest Neighbors | 89.83% |
|No| Decision Tree | 90.62% |
|No| Bagged Decision Tree | **90.70%** |
|No| Random Forest | 90.69% |
|No| Ada Boost | 89.92% |
|Yes| Logistic Regression | 82.20% |
|Yes| K-Nearest Neighbors | 62.38% |
|Yes| Decision Tree | 89.50% |
|Yes| Bagged Decision Tree | 90.41% |
|Yes| Random Forest | 90.93% |
|Yes| Ada Boost | 89.91% |

As can be seen, the model with the best accuracy did not include date/time/location information. In fact, all of the models that did include that data ended up being severely overfit and performed worse than those models without. 

## Conclusions 

After extensive data analysis and model evaluation, we have reached several key conclusions. We've identified patterns and relationships between causes of death and geographic locations, shedding light on important insights relevant to public health and safety in Chicago. Our findings have the potential to inform data-driven policies and resource allocation decisions, contributing to the well-being of Cook County residents. The model predicting 'manner of death' may have utility as an a tool to bolster the professionals' confidence in their conclusions and provide justification for further allocation of county resources.


## Future Recommendations

While our analysis has provided valuable insights, there are opportunities for further exploration and improvement. In the future, we recommend:

- Conducting more in-depth analyses to uncover additional correlations and factors influencing causes of death in specific zip codes.
- Exploring additional data sources to enrich the analysis and gain a more comprehensive understanding of mortality factors.
- Collaborating with local authorities and healthcare organizations to implement data-driven strategies for community health and resource allocation.
- Continuously updating and refining the models to improve their predictive accuracy and adapt to evolving trends and challenges.

By pursuing these recommendations, we can enhance the impact of our analysis and contribute to ongoing efforts to improve public health in Chicago and Cook County as a whole.
