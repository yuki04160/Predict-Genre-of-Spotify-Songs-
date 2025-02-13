# Predicting Genre of Spotify Songs
To predict the genre of Spotify songs, I built a Multiclass Logistic Regression, KNN, Decision Tree, Random Forest, and XGBoost in R using Kaggle dataset - [Dataset of songs in Spotify](https://www.kaggle.com/mrmorj/dataset-of-songs-in-spotify).
## Project Background
Spotify is a digital music service that gives customers access to millions of songs. To provide better customer services, Spotify provides different genre-based playlists for the customers to discover. Thus, this project aims to see if we can correctly predict the music genre of a song and which audio features are important when forecasting.
## Exploratory Data Analysis
   - Variable identification
   - Univariate analysis
   - Bi-variate analysis
   - Missing value treatment
   - Outliers treatment
## Data Preprocessing
   - Feature Scaling
     - Since predictors have varying scales and KNN is a distance-based algorithm, I standardized data using scale function.
   - Split into training (0.8) and test (0.2)
   - Balance training data
     - I used SMOTE function to undersample a majority class and oversample a minority class.
## Modeling: Supervised Learning
1. Multiclass logistic regression
   - I used For loop to build 15 logistic regression models, one per genre.
   - I used the Softmax function to transform unrelated probabilities into a probability distribution over 15 genres.
   - The predicted genre will be the one associated with the maximum probability.
2. K-nearest neighbors
   - I used Euclidean & Manhattan distance.
   - To find optimal K, I used For loop and plotted accuracy plots.
3. Decision tree
4. Random forest (bagging)
   - To tune hyperparameters ntree, I plotted the trees & Error.
   - To tune hyperparameters mtry, I used the tuneRF function.
5. XGBoost (boosting)
   - To find the best iteration, I used xgb.cv function to perform cross-validation.
## Multiclass Classification Model Evaluation
   - Feature importance
   - Overall accuracy
   - True Positive Rate of each genre
   - F1 score of each genre
## Conclusion
Overall, I found that when predicting genre, “tempo” is the most important audio feature. Also, I found that XGBoost model performed better.

**Model**|Logistic Regression|KNN (Euclidean)|KNN (Manhattan)|Decision Tree|Random Forest|XGBoosting
-----|-----|-----|-----|-----|-----|-----
**Accuracy**|0.53|0.53|0.56|0.48|0.65|0.66

<strong>TPR and F1 score from XGBoost model</strong>

**Genre**|Dark Trap|dnb|Emo|hardstyle|Hiphop|Pop|psytrance|Rap|RnB|techhouse|techno|trance|trap|Trap Metal|Underground Rap
-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----
**TPR**|0.40|0.99|0.70|0.93|0.43|0.23|0.91|0.52|0.47|0.88|0.87|0.87|0.86|0.50|0.29
**F1 score**|0.47|0.99|0.69|0.90|0.44|0.19|0.92|0.41|0.42|0.88|0.86|0.83|0.86|0.39|0.35

In terms of TPRs of XGBoost model, among 15 genres, 7 of them have rates higher than 85%. However, genres such as "Pop" and "Underground Rap" have TPR lower than 30%. Similar situations happened in the case of the F1 score. That is to say, the model can only highly correctly predict some of the genres. Thus, in the future, to improve the model, I can try the following things:
1. Add more data: since "Pop" has the least number of observations in the dataset, I can add more Pop songs' data to increase its TPR.
2. Deal with the remaining outliers: since there are still some outliers that haven't been treated yet, I can try:
   - Binning 
   - Subsetting
   - Feature transformation
     - Right skewed data: log transformation
     - Left skewed data: square transformation
4. Apply feature selection: based on feature importance results, I can reduce the number of input variables.
