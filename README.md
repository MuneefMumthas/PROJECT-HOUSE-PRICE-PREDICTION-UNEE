### Research Question  
**Under What Conditions Can Structural Attributes Alone Accurately Predict House Prices, and When Are Location Attributes Essential?**

#### Evaluation  
This research was aimed to determine the conditions under which house prices could be accurately predicted based solely on structural attributes. The raw housing dataset posed initial challenges typical of real-world data, including missing values, outliers, and inconsistencies. These were addressed through a rigorous preprocessing phase, which included:

- Dropping entries where the price was 0.  
- Converting the “date” column to extract house age and years since renovation.  
- Handling outliers using the Interquartile Range (IQR) method for higher accuracy.  
- Encoding categorical variables with high cardinality, specifically street names, using M-Estimate Encoding, a technique that prevents overfitting by balancing category means with the global mean (McGinnis, 2022).

Additionally, Exploratory Data Analysis (EDA) revealed Seattle as the dominant city, prompting the creation of both a multi-city dataset (12 cities, 100 entries each) and a Seattle-specific dataset (1461 entries) for a location-specific comparison. The “street” attribute had high cardinality, so to assess the impact on model performance, six different approaches were used:

1. Housing data of multiple cities with location attributes.  
2. Housing data of multiple cities with location attributes, except Street.  
3. Housing data of multiple cities without location attributes (only structural attributes).  
4. Housing data of one city with location attributes.  
5. Housing data of one city with location attributes, except Street.  
6. Housing data of one city without location attributes (only structural attributes).  

#### Methodology  
To compare which algorithm would perform better in each dataset, four machine learning algorithms were used: linear regression, support vector regression (SVR), decision tree, and random forest, each offering unique advantages and potential drawbacks for predicting house prices:

- **Linear Regression:** Chosen for its simplicity, interpretability, and widespread use in real estate price prediction.  
- **Support Vector Regression (SVR):** Selected to explore a different approach based on finding the optimal hyperplane that maximises the margin between data points.  
- **Decision Tree Regression:** Included to assess the performance of a non-parametric model that divides data into different regions based on feature values.  
- **Random Forest Regression:** Chosen as an ensemble method that combines multiple decision trees to improve predictive accuracy and reduce overfitting.  

#### Model Performance and Insights  
Linear regression and random forest were the top performers. Specifically, in models incorporating all location attributes, both linear regression and random forest had similar R² scores (0.99), but linear regression had a lower RMSE (1548.10 – multi, 7760.14 – Seattle) compared to the random forest model (7197.78 – multi, 10532.34 – Seattle). However, when location attributes were excluded, random forest outperformed linear regression, highlighting its ability to influence complex relations between structural features to achieve a respectable R² score of 0.497 for the multi-city dataset and 0.529 for the Seattle city dataset.

Furthermore, decision trees exhibited a significant difference in performance between models with and without location attributes. The R² score for the multi-city dataset with location attributes was 0.99, but it dropped drastically to 0.10 without location attributes. This highlights the sensitivity of decision trees to the presence of location information. Interestingly, Support Vector Regression (SVR), while generally slower, surprisingly outperformed decision trees in models without location attributes, suggesting its potential use in situations where location data is unavailable.

In addition to that, the visualised runtimes illustrate the computational efficiency of each algorithm, with Linear Regression and Decision Tree being the fastest, and SVR being the slowest in both training and prediction. Despite its slower speed, SVR did not consistently outperform other models in terms of accuracy.

Despite high cardinality, the “street” attribute improved all models’ performance across datasets with location details, after being encoded using M-Estimate encoding to address potential overfitting concerns. This suggests that the “street” attribute captures unique street-level features relevant to price variation, and the improvement in performance wasn’t due to overfitting to specific street names. The consistent decrease in performance across all models and algorithms when “street” was removed further strengthens this conclusion.

Moreover, the comparison of models without location attributes revealed an intriguing relationship between location granularity and predictive accuracy. The Seattle-specific dataset consistently outperformed the multi-city dataset in all four algorithms, even without any location features. In the multi-city dataset, the relevant location attributes were city, state zip, and street, while for Seattle, only state zip and street were applicable. This suggests that as location becomes more specific, the predictive power of structural attributes alone increases, and explicit location attributes may become unnecessary, similar to how the “country” attribute was dropped during preprocessing as the data was based solely in the USA.

#### Future Directions  
Future research could refine these models by incorporating additional structural features or exploring more complex algorithms, such as a multi-layered neural network to capture intricate relationships between features. Moreover, datasets with a higher density of listings within specific streets or neighbourhoods would facilitate more robust testing of the finding that location attributes become less essential as location granularity increases. This would require either obtaining such a dataset or generating synthetic data that realistically reflects real-world conditions.

#### Conclusion  
This study demonstrates the potential of predicting house prices using structural attributes alone, particularly in well-defined, localised contexts. However, it underscores the complex relationship between location and structure, highlighting the varying importance of location information based on its granularity. For broader, multi-city analyses, including location attributes is essential for accurate prediction. In contrast, in highly specific locations, the structural attributes alone can offer reasonable predictive power. This finding has significant implications for real estate professionals and data scientists, as it suggests that the optimal approach to house price prediction depends heavily on the specific context and the level of location detail available.
