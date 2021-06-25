# YELP REVIEWS TO UNLOCK BUSINESS GROWTH OPPORTUNITIES
Valentina Rizzati <br/>
June 24, 2021 <br/>
Metis: Natural Language Processing <br/>

---

How to navigate this repo:
- proposal_yelp.pdf: my initial proposal for a classification project 
- mvp_yelp.pdf: mvp presented two days before the final project submission
- data folder: data I used for modeling, both in json and csv format
- images: images I used in my presentation
- final: all files used for the final submission
  1. 1_yelp_extract_reviews.ipynb : notebook corresponding to the first phase of data extraction through MongoDB and initial data cleaning
  2. 2_yelp_unsupervised_modeling.ipynb : notebook corresponding to the second phase of topic modeling
  3. 3_yelp_supervised_modeling.ipynb : notebook corresponding to the third phase of classification
  4. pickle files for use across notebooks
  5. yelp_cafe_review_optimizer.pdf : final presentation

---

## ABSTRACT
As a Data Scientist on the Business team at Yelp, I have been tasked with building a tool enabling business owners to extract useful information from Yelp reviews to optimize their performance. For my prototype, I have decided to focus on cafés because their relative low variance in pricing and customer preferences across regions will likely make the insights more applicable on a national scale. 

My impact hypothesis is that by providing café owners with visibility on the elements that customers care about the most (i.e. topics that are discussed more often in Yelp reviews), they will be able to optimize their café’s most critical features and progressively expand their customer base. In fact, the more a café owner will address the topics that boost customer satisfaction, the more positive sentiment reviews they will drive which, in itself, will attract more customers to the café. Therefore, the objective of this project is to build the engine to nurture this positive feedback loop. 

After consolidating all data on Portland cafés and related reviews, I started by conducting toping modeling with a combination of TF-IDF vectorizer and NMF topic modeler. Once I extracted the 9 main topics characterizing the Yelp reviews on cafés, I passed them in a classification model scheme presenting topics as features and positive sentiment as target. Through cross-validation, I was able to select Random Forest as my model of choice with a F1 score of 0.93.

## DATA

I have collected data on Yelp reviews and businesses from the [Yelp dataset](https://www.yelp.com/dataset). 
Then, I have created a MongoDB database containing 5 collections presenting Yelp data about various businesses across the US. For the purpose of this project, I focused on the *business* and *review* collections. 

I have chosen Portland as the test market for this model because ~16% of café-related reviews presented in the Yelp dataset were about coffee establishments in Portland, which is not surprising knowing the strong coffee culture characterizing this city. Therefore, the fact that reviews on Portland cafés alone represent such a significant size of the available cafés reviews on Yelp and the fact that Portland is definitely a representative market for coffee, enhanced my confidence in the generalizability potential of choosing Portland as the test market for my prototype model.

I filtered the resulting dataframes for Portland as the location of interest and *Cafes*, *Coffee & Tea*, and *Coffee Roasteries* as the three café-related business categories. So, I ended up with a business-related dataframe containing information about ca. 1,200 cafés in Portland, and a review-related dataframe containing information about ca. 120,000 reviews about cafés in Portland.

For the purpose of this analysis a review is considered positive if its associated number of stars is greater than 3, and negative if lower than 3. The target of our classification model will be based on this definition of *positive sentiment*.

## DESIGN

As reflected in the three jupyter notebooks included in the final folder of this repo, this project is designed around three main components:
1. **Data Extraction, Cleaning & EDA** : prepare data for modeling
2. **Unsupervised Learning Model** : define the 9 most important topics characterizing Yelp reviews on cafés
3. **Supervised Learning Model** : build a classification model to interpret the importance of the 9 topics in driving a positive sentiment review 

As a last step, in light of the results from my analysis, I have generated a few business insights and ideas for product development and marketing campaigns for the Yelp team. These are summarized in the final presentation. 

## ALGORITHM

As a first step, I have extracted, cleaned and explored the data using MongoDB, pandas, numpy, seaborn and matplotlib.

Next, in the **unsupervised learning** phase, I fist used TF-IDF and NMF to built a topic modeling baseline, which generated fairly well-defined and separable topics. After tuning the TF-IDF and NMF hyperparameters, I ended up with my optimal model that delivered 9 main topics about Yelp reviews on Portland cafés. 
To further explore trends by sentiment, I tested my topic modeling algorithm on positive sentiment and negative sentiment reviews separately. Similarly, I built wordclouds and scattertext visualizations to better understand my corpus by sentiment type.  

Finally, as part of the **supervised learning** phase, I defined the 9 review topics as my features and *positive sentiment* as my target variable. Then, I chose F1 score as my metric of choice because of the importance to balance recall and precision. After a first baseline with a Logistic Regression model, I run a cross-validation pipeline comparing F1 scores across two Logistic Regression models, one Random Forest, one XGBoost and one Bernoulli Naive Bayes model. 
I finally selected Random Forest as my model of choice given its superior F1 score of 0.93. The related feature importance plot was very useful in interpreting the topics that are most important in generating a positive sentiment review. 

## TOOLS

- MongoDB to store Yelp data contained in five json files
- Pandas and numpy for data manipulation
- spaCy and NLTK for NLP preprocessing
- wordcloud, stylecloud and scattertext for NLP-related visualizations
- Seaborn and matplotlib for other data visualization
- Scikit-learn for classification data modeling

## COMMUNICATION

A slide deck is included in this repo. 

In addition, see below a few visualizations related to both topic modeling and classification phases of this project.

----

### Topic Modeling
#### 1. Wordcloud | Positive Sentiment Reviews
![wordcloud_pos](https://user-images.githubusercontent.com/68084582/123345871-09366c80-d525-11eb-9feb-61674554dba8.png)

#### 2. Wordcloud | Negative Sentiment Reviews
![wordcloud_neg](https://user-images.githubusercontent.com/68084582/123345888-0f2c4d80-d525-11eb-8211-b4f338a8b932.png)

#### 3. Scattertext | All Reviews
<img width="1196" alt="scattertext_img" src="https://user-images.githubusercontent.com/68084582/123345905-17848880-d525-11eb-9830-bcc08cca8f17.png">

----

### Classification
#### 1. Confusion Matrix
![confusion](https://user-images.githubusercontent.com/68084582/123345960-3551ed80-d525-11eb-800e-ad3a883daab7.png)

#### 2. Feature Importance Plot
![importances](https://user-images.githubusercontent.com/68084582/123345973-3daa2880-d525-11eb-8a91-ca291e73caef.png)
