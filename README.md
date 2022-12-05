# Genre selection and song duration analysis - Spotify

<ins>*Introduction:*</ins>

Last week Spotify sent out its yearly Spotify Wrapped feature. I noticed most of my songs were under 3 minutes. So using data from [Kaggle](https://www.kaggle.com/datasets/mrmorj/dataset-of-songs-in-spotify?resource=download), I built a classification tree model to analyze genre selection. Just like a decision tree, a classification tree model maps the binary decisions that lead to a specific class. This machine learning model takes input in both numerical and categorical formats e.g. tempo, loudness and tries to make a prediction of a categorical variable e.g. genre. Lastly, using excel, I analyzed the average duration of songs over the last five years.


<ins>*Managing the dataset:*</ins>

After importing different libraries (rpart.plot, gmodels and rpart) I loaded the data set to R-Studio. Libraries are a collection of R functions and code that bring more functionality. Think of it as a toolbox that has different tools once could choose from to fix something. I then deleted some columns such as id, analysis_url and Unnamed..0 because they offered little significance to the model and predictions. Lastly, I checked for missing values in the dataset using the is.na function. Fortunately, the dataset had none.

<ins>*Partitioning the data:*</ins>

Before building the model, I split the data into two sets. 60% of it was used for training the model, and 40% was reserved for testing the model. The training portion is used to train the model to predict correctly while the testing portion is used to evaluate the predictions made by the model. 

<ins>*Buidling a classfication tree model:*</ins>

Using the data from the training portion, I created a model that would predict the genre type relative to all other variables in the dataset, such as tempo, danceability, and energy. Using the rpart.plot function, I got the plot below


<p align="center">
  <img width="600" height="200" src="https://github.com/jackfrost68/Spotify_Analysis/blob/4b98262fd22c00cc82829c9136b4e80f45d6a7d7/Tree%201%20Clearer.png">
</p>

Below is a zoomed in version;

<p align="center">
  <img width="600" height="200" src="https://github.com/jackfrost68/Spotify_Analysis/blob/bdbed1041c626096ffcb66055773f56f04291f41/Zoomed%20in%20tree.png">
</p>

According to the plot above, based on the model, the most important attribute of selecting all genres is the duration_ms, followed by energy and tempo.

<ins>*Evaluating model performance and controlling overfitting:*</ins>

To assess model performance, I calculated the benchmark error rate, which came to 86%. This error rate is similar to blindly guessing the main attributes that would affect genre selection.

Stopping rules are like barriers that prevent the tree from creating more splits/branches. So I created another tree with stopping rules of 2000, 1000, and 0 for the minbucket, minsplit, and cp values respectively. In machine learning, overfitting occurs when a statistical model predicts exactly against the training data i.e. models the training dataset too well. If a model is overfit, it cannot predict against out-of-the-norm data. To control for overfitting, I used the EasyPrune function to "prune" the tree and got the plot below.


<p align="center">
  <img width="600" height="200" src="https://github.com/jackfrost68/Spotify_Analysis/blob/c7b32960c90e1d7637ac9015d4568e49243c630d/Tree%202%20Clearer.png">
</p>

Even after pruning, duration, tempo, and energy remain important attributes for genre selection. Additionally, pruning reduced the error rate from 86% to 51%.

To investigate further, I reduced the dataset to one that only had RnB and HipHop genres. After running the model, I got the plot below;

<p align="center">
  <img width="600" height="200" src="https://github.com/jackfrost68/Spotify_Analysis/blob/57f678bb30e428f3ee9d3c40a774d4d956048328/HipHop%20&%20RnB%20tree.jpeg">
</p>

In this case, speechiness, followed by duration, were the defining attributes for RnB and HipHop genres. Speechiness is defined as the presence of spoken words in a track, according to Spotify's data dictionary.

Lastly, using Excel, I analyzed the average duration of songs over the years. In the dataset, the duration is in milliseconds. So I converted each row to minutes and plotted it against the last five years, and got the plot below.

<p align="center">
  <img width="600" height="200" src="https://github.com/jackfrost68/Spotify_Analysis/blob/e1d554d1aeb205d79feb4d00499808b25c021caf/Avg%20Duration%20of%20songs%20over%20the%20years.png">
</p>

<ins>*Conclusion:*</ins>

According to the dataset and model, duration is a key attribute when selecting genres, even for HipHop & RnB. Over the last five years, the average of a song has steadily decreased. This trend could be attributed to the prolonged exposure to shorter forms of media from platforms like TikTok, Snapchat and Instagram. Producers and artists can leverage this insight to accurately time their songs that suit today's listener's shorter attention spans. 

Severally, I found myself annoyed at the short songs from some of my favorite artists. I'm not naming anyone but, * cough * [Sir](https://www.youtube.com/@sirvevo2080) * cough * , Please make longer songs, thank you!

One drawback to this dataset is the subjective nature of some of the variables. How Spotify measures the danceability and loudness of a song can differ from person to person, either by age, gender, or nationality. For example, some people would prefer upbeat love songs, while others opt for more melodic ones.


Shoutout to [Jewel Ham](https://www.linkedin.com/in/jeweleham0501/) for being the genius behind Spotify Wrapped! 🙌🏾 Read more of her story [here](https://www.yahoo.com/now/intern-created-spotify-wrapped-feature-195344023.html)
