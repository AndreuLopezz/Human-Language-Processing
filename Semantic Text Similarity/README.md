# Semantic Text Similarity: Word Embeddings and Neural Networks

This repository contains the fourth and final practice for the **Introducció a l'Aprenentatge Automàtic** (IAA) course. It focuses on modern Natural Language Processing (NLP) techniques, moving from traditional frequency-based methods to dense vector representations and deep learning architectures.

## Repository Structure

* **`practica4.ipynb`**: Jupyter Notebook containing the implementation of Word2Vec training, LSTM architectures, and the final evaluation.
* **`movie_reviews_model.h5`**: The trained Keras/TensorFlow model (if applicable).
* **`word2vec_embeddings.bin`**: Custom-trained word vectors for the cinema domain.

---

## Methodology

### 1. Word Embeddings (Word2Vec)

Instead of using sparse matrices, words are represented as dense vectors that capture semantic relationships:

* **Custom Training**: A Word2Vec model was trained on the movie reviews corpus to capture domain-specific jargon and cinematic contexts.


* **Generalization**: These embeddings allow the model to understand that "excellent" and "superb" are semantically similar, improving performance on unseen data.



### 2. Deep Learning Architecture (LSTM)

The project implements a **Long Short-Term Memory (LSTM)** network, which is designed to handle sequential data and capture long-term dependencies in text:

* **Embedding Layer**: Maps word indices to the dense vectors previously trained.
* **LSTM Layer**: Processes the sequence of word vectors to understand the sentiment flow.
* **Dense Output Layer**: A final sigmoid-activated layer to classify the sentiment as positive or negative.

### 3. Training and Optimization

* **Padding and Truncating**: Sequences were standardized to a fixed length to be processed by the neural network.
* **Dropout**: Applied to prevent overfitting, ensuring the model generalizes well to new reviews.
* **Early Stopping**: Used during training to halt the process once validation loss stopped improving.

---

## Results and Analysis

The Neural Network approach was compared against the traditional methods from previous practices:

| Approach | Accuracy | F1-Score |
| --- | --- | --- |
| **Traditional (Logistic Regression)** | 0.835 | 0.835 |
| **LSTM + Word2Vec** | **0.852** | **0.851** |

### Key Improvements

* **Contextual Understanding**: The LSTM handles negation (e.g., "not good") much better than simple frequency counts.


* **Semantic Richness**: The use of embeddings reduced the "out-of-vocabulary" issue seen in standard CountVectorizers.



---

## Conclusions

The transition to **Deep Learning** and **Word Embeddings** represents a significant step in performance and robustness. While more computationally expensive to train, these models provide a deeper understanding of human language by treating text as a meaningful sequence rather than a "bag of words".

---

**Author**: Andreu López Pérez

**Date**: June 2025

