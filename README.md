# Lyrics Generation Using Recurrent Neural Networks

![image](https://github.com/user-attachments/assets/f42a7e17-dd04-4a76-8117-944618c60440)


This project explores the development of a Recurrent Neural Network (RNN) for generating song lyrics based on given melodies. The primary objective is to integrate lyrics and MIDI data into a cohesive model that can predict lyrics harmonizing with the provided melodies.

## Table of Contents

1. [Introduction](#introduction)
2. [Data Exploration and Preprocessing](#data-exploration-and-preprocessing)
3. [MIDI Features Extraction](#midi-features-extraction)
4. [Model Architecture](#model-architecture)
5. [Setup and Experiments](#setup-and-experiments)
6. [Summary](#summary)


## Introduction

This project involves creating an LSTM-based RNN to generate lyrics corresponding to a given melody. The training data consists of song lyrics and corresponding MIDI files, which contain various musical elements like notes, tempo, and instruments. The goal is to integrate this musical data with the lyrics to create a model that can produce coherent and musically relevant lyrics.


## Data Exploration and Preprocessing

The dataset includes two CSV files with lyrics and a collection of MIDI files for the corresponding songs. The lyrics data was cleaned and preprocessed to ensure consistency, including handling missing data and tokenizing the lyrics. The MIDI files were analyzed for any corruptions, and only valid files were included in the final dataset.

![image](https://github.com/user-attachments/assets/21c387ef-0521-47c4-a43a-759095299444)


### Preprocessing Steps:

- Unzipping and organizing the data.
- Cleaning the lyrics and removing non-alphanumeric characters.
- Tokenizing the lyrics and normalizing contractions (e.g., "we'll" to "we will").
- Creating a validation set by splitting the training data (95% training, 5% validation).



### Data Exploration and Visualization:

![image](https://github.com/user-attachments/assets/d0f7b30d-7065-4b34-8ef1-be6fba1a29cf)

![image](https://github.com/user-attachments/assets/f76ed2b5-caab-4c2c-ae46-a33e3c4be0ab)

![image](https://github.com/user-attachments/assets/8c432f87-9e92-46ef-90be-96c4b7adeb70)

![image](https://github.com/user-attachments/assets/79419122-f194-4dc7-b75d-fa8d3e833379)

![image](https://github.com/user-attachments/assets/f37556fc-3c8d-470e-99d9-e1ca6f2d22f3)
![image](https://github.com/user-attachments/assets/2c4b0d3c-6c1b-4a97-89ac-bab815463d6f)


## MIDI Features Extraction

To incorporate melody information, we implemented two approaches:

### First Approach: "Melody per Song"

In this approach, we extracted general musical features for each song, including:
- **Total Velocity**: Overall intensity of the song.
- **Tempo**: Speed of the song.
- **Tempo Changes**: Variations in tempo.
- **Piano Roll Value**: Distribution of notes.
- **Count of Total Notes**: Complexity of the song.
- **Count of Pitch Bends**: Instances of pitch modulation.
- **Count of Control Changes**: Variations in instrument parameters.

These features were then concatenated into a single feature vector representing the song's musical characteristics.

![image](https://github.com/user-attachments/assets/12e3b0b4-cb45-431d-bee1-908ae92eb88c)


### Second Approach: "Melody per Word"

This approach involved extracting features for each word in the lyrics, using a sliding window to capture the temporal context of the MIDI features associated with each word. This method allowed for a more fine-grained representation of the melody in relation to the lyrics.

![image](https://github.com/user-attachments/assets/f0f6fe7b-fc3a-46d2-9f42-39ff4b184977)


## Model Architecture

The model is based on an LSTM network with two input layers:
- **MIDI Features Input**: Accepts a feature vector for the song or word.
- **Word Embedding Input**: Accepts a word embedding vector.

These inputs are concatenated and passed through LSTM layers, followed by dense layers and a dropout layer to prevent overfitting. The output layer uses a softmax activation function to predict the next word in the lyrics.

![image](https://github.com/user-attachments/assets/7dcec6a1-f666-4eb0-94a9-4651f7cec173)
![image](https://github.com/user-attachments/assets/36ed7212-e8bc-416b-a1aa-66d34fda564a)


## Setup and Experiments

Two main models were trained:

### Model 1: Melody per Song
- **Epochs**: 20
- **Batch Size**: 32
- **Optimizer**: Adam
- **Learning Rate**: 0.01
- **Loss Function**: Categorical Crossentropy
- **Metrics**: MSE, Cosine Similarity


![image](https://github.com/user-attachments/assets/087332d2-5f62-4f84-861a-f6b5c8b9db28)
![image](https://github.com/user-attachments/assets/f66cbe80-854b-4849-b685-530dba731123)

![image](https://github.com/user-attachments/assets/f8ba65d0-d303-4ba8-ba09-e8857e535d5b)

![image](https://github.com/user-attachments/assets/567c0545-243a-4192-bd54-9584e5ef0740)


### Model 2: Melody per Word
- **Epochs**: 20
- **Batch Size**: 32
- **Optimizer**: Adam
- **Learning Rate**: 0.01
- **Loss Function**: Categorical Crossentropy
- **Metrics**: MSE, Cosine Similarity

Both models showed promising results during training but encountered overfitting issues when evaluated on the test dataset.

![image](https://github.com/user-attachments/assets/d53eb5df-968a-4189-8e10-e58d63d0aaae)
![image](https://github.com/user-attachments/assets/11de95fb-d743-48d3-9802-5c1ccc16dd8b)
![image](https://github.com/user-attachments/assets/e95eb012-e2e6-46b0-959b-dc65f9926a07)
![image](https://github.com/user-attachments/assets/c00ae35e-9a3b-4ce8-8262-080cf55980fd)



## Summary

This project was a challenging yet rewarding exploration into the integration of RNNs with musical data. We gained valuable experience in feature extraction from MIDI files and deepened our understanding of LSTM networks. Despite the challenges, the project provided insights into the complexities of merging lyrical and musical data and opened new possibilities for further exploration in the field of NLP and music generation.
