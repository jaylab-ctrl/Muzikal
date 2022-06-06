
![Logo](https://www.incimages.com/uploaded_files/image/1920x1080/getty_626660256_2000108620009280158_388846.jpg)





![Python Version](https://img.shields.io/badge/python%20version-3.7.13-lightgrey)

![Type of ML](https://img.shields.io/badge/Type%20of%20ML-Binary%20Classification-red)

[![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/tterb/atomic-design-ui/blob/master/LICENSE)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/16-QZNfE4-xsz0Ckxr38yN6xWx8Mg_pQ4)

Badges source: [shields.io](https://shields.io/)
# Muzikal

The is an end-to-end project about Classifying Music Genres, "Rock" and "Hiphop", from the given decomposed audio data, from a survey data.
## Authors for this project

- [@jaylab-ctrl](https://www.github.com/jaylab-ctrl)
- [@Jaanvi20](https://github.com/Jaanvi20)
- [@Palakjain012](https://github.com/Palakjain012) 



## Table of Contents

  - [Business problem](#business-problem)
  - [Data source](#data-source)
  - [Dataset Attributes](#dataset-attributes)
  - [Methods](#methods)
  - [Tech Stack](#tech-stack)
  - [Results](#results)
  - [Lessons learned](#lessons-learned)
  - [Limitation and what can be improved](#limitation-and-what-can-be-improved)
  - [Notebook](#notebook)
  - [Model Deployment on Streamlit](#model-deployment-on-streamlit)
  - [Contribution](#contribution)

## Business Problem 
This app predicts whether music genre is 'Rock' or 'Hip-hop accordinf to the user's input of decompsed music data.

## Data source
The data was collected from DataCamp Projects.

## Dataset Attributes
|Attribute| Description 	|
|-------------------|------------------	|
|Track_id|The track of the song|
|Acousticness|A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic|
|Danceability|Describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable|
|Energy|A measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity|
|Instrumentalness|Predicts whether a track contains no vocals. The closer the instrumentalness value is to 1.0, the greater likelihood the track contains no vocal content. Values above 0.5 are intended to represent instrumental tracks, but confidence is higher as the value approaches 1.0|
|Liveness|Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that the track was performed live. A value above 0.8 provides strong likelihood that the track is live|
|Speechiness|Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66 describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. Values below 0.33 most likely represent music and other non-speech-like tracks|
|Tempo|The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration|
|Valence|A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive, while tracks with low valence sound more negative|
|Genre_top|The genre of the song|

## Methods Used 
- Exploratory Data Analysis
- Machine Learning
- Model Deployment

## Tech Stack

- Python (for EDA and ML)
   - numpy: 1.21.6
   - pandas: 1.3.5
   - matpltlib: 3.2.2
   - seaborn: 0.11.2
   - statsmodels: 0.10.2
   - scikit-learn: 1.0.2
   - imbalanced-learn: 0.8.1
   - scipy: 1.4.1
   - catboost: 1.0.6
   - streamlit: 1.10.0

- Streamlit (for deployment of the ML Model)

## Results

1. Target variable in a pie plot.

![Pie Plot](https://cdn.discordapp.com/attachments/808978547296567316/983349213989568622/unknown.png)

**We need to balance the target variable to reduce the biasness of the majority target varaible during training.**


2. Correlation among the features.

![Correlation Mat](https://cdn.discordapp.com/attachments/808978547296567316/983349359557095456/unknown.png)

**The variables are not highly correlated between each other so no need of Feature Selection.**
But will confirm Feature Selection using Variance Inflation Factor later in the project.


3. Learning different attributes using genres.

![Groupby](https://media.discordapp.net/attachments/415118867258671104/983323011824373800/unknown.png)

**Here we see that:**
 - **Both of these genres have seemingly fair Acousticness**. So there are chances that some songs in these both genres use electonic means.
 - **Hip-hop genre is highly danceable than rock**. So, hip-hop music uses a combination of musical elements, where rock uses less combination.
 - **Both of these generes have good energy**. Energy is the measure of high instensity and acitivity. So, these tracks are mainly fast paced and have loud elements to it.
 - **Rock genre has higher instrumentalness than hip-hop**. Values above 0.5 are intended to represent instrumental tracks. So clearly, we can see that rock music generally has no vocal content. 
 - **Both of these genres have low liveness**. Low liveness values represent an probability that the track was not performed live. So, here we can see that theses tracks are not performed live in front of the audience.
 - **Both of these genres have a low spechiness level**. The values below 0.33 most likely represent music and other non-speech-like tracks. So, these genres mainly do not use speech.
 - **Both of these genres have relatively high tempo**. This means that the tracks of the genres have higher Beats Per Minute (BPM).
 - **The valence factor of hip-hop is higher than rock**. This concludes that hip-hop genres are more positive. Positive music has help a person reduce stress.

4. Plotting the target variable balancing.

![Pie Plot](https://cdn.discordapp.com/attachments/808978547296567316/983349771018338304/unknown.png)

5. The Models.

The best model that was used was Voting Classifier (Ensembled model).

Classification Report

![Class Report](https://cdn.discordapp.com/attachments/415118867258671104/983337654806519908/unknown.png)

Confusion Matrix

![Confusion Mat](https://cdn.discordapp.com/attachments/808978547296567316/983349841109348362/unknown.png)

For the models, the metric used was *Accuracy*.

We used Accuracy as measure because we do not want the model to wrongfully classify the genre, which when can cause problems while building recommendations systems.

| Model  | Accuracy|
|-------------------|------------------	|
| K-Nearest Neighbors|92.40%|
| Random Forest|94.35%|
| CatBoost|94.23%|
| CatBoost with Hyperparamter Tuning|94.51%|
|Voting Classifier (Ensembled Learning)|94.86%|

We used the best model (in terms of Accuracy) for inputing some values.

## Lessons learnt
- Based on the analysis of the project, we learnt how different the genres have some similairities and dissimilarities between them. 
- We also found that danceability and valaence are the most predictive features to determine whether the song is 'Rock' or 'Hip-hop'.
- This project can be mainly used as a building block for developing recommendation systems for music.

## Limitation and what can be improved
- If the dataset had more instances and genres then it would be more beneficial to analyse more genres together.
- Used RandomizedSearch to save time but GridSearch would have yield better results.


## Notebook
The notebook for this project can be found [here](https://colab.research.google.com/drive/16-QZNfE4-xsz0Ckxr38yN6xWx8Mg_pQ4#scrollTo=52TK0jbohlYB).
Application for the Streamlit interface is in the notebook.

## Model Deployment on Streamlit
To run the Streamlit interface in Google Colab, here are the following steps:
- Install  localtunnel
```bash
!npm install -g localtunnel
```
- Then run in the app.py cell in the notebook.
- Later run the Streamlit file thorugh localtunnel.
```bash
!streamlit run app.py & npx localtunnel --port 8501
```
## Contribution
Everyone is open to contribute. I'll gladly welcome the pull requests!
