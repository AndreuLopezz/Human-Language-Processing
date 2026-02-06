# Sentiment Analysis on Movie Reviews: Supervised vs. Lexicon-based

This repository contains the second practice for the **Introduccio a l'Aprenentatge Automatic** (IAA) course. The project is split into two distinct approaches to solve the sentiment analysis problem on the NLTK `movie_reviews` dataset: a supervised machine learning approach and a semi-supervised lexicon-based approach.

## Repository Structure

* **`pract2.ipynb`**: Implementation of supervised models (Naive Bayes, SVM, Logistic Regression).
* **`pract2b.ipynb`**: Implementation of a sentiment classifier using WordNet, SentiWordNet, and VADER.
* **`REPORT.pdf`**: Technical documentation including hyperparameter studies and error analysis.

---

## Part A: Supervised Learning

### 1. Preprocessing and Splitting

* **Data Source**: NLTK `movie_reviews` (2,000 documents).
* **Cleaning**: Lowercasing, removal of non-alphabetic characters, and stop-word filtering using NLTK.
* **Splitting**: 70% Training / 30% Test, stratified to maintain class balance.

### 2. Hyperparameter Optimization

We utilized `GridSearchCV` with 5-fold Cross-Validation to optimize both the `CountVectorizer` and the classifiers:

* **Multinomial Naive Bayes**: Optimized smoothing parameter `alpha`.
* **Support Vector Machine (SVM)**: Optimized `C`, `kernel` (rbf), and `gamma`.
* **Logistic Regression**: Optimized regularization `C` and `penalty`.

### 3. Performance Comparison

| Model | Accuracy (Test) | F1-Score (Weighted) |
| --- | --- | --- |
| **MultinomialNB** | 0.8167 | 0.8163 |
| **SVM** | 0.8117 | 0.8116 |
| **Logistic Regression** | **0.8350** | **0.8349** |

### 4. Top Feature Analysis

Using Logistic Regression coefficients, we identified the most discriminative words. Positive weights correlate with "pos" reviews, while negative weights correlate with "neg" reviews.

---

## Part B: Lexicon-based Sentiment Analysis

### 1. Methodology

This approach does not "train" on labels but uses linguistic resources:

* **Lemmatization**: Words are normalized based on their POS (Part-of-Speech) tags.
* **Word Sense Disambiguation**: The **Lesk algorithm** and **Wu-Palmer Similarity** are used to find the most accurate `synset` for a word given its context.
* **SentiWordNet**: Extracts positivity and negativity scores for each synset.
* **VADER Fallback**: If SentiWordNet lacks data for a specific term, the system falls back to VADER polarity scores.

### 2. Optimization with Optuna

We used the **Optuna** framework to find the best:

* **Category Weights**: Importance of Adjectives vs. Verbs vs. Nouns.
* **Scoring Biases**: Adjusting `peso_pos` and `peso_neg` to handle model subjectivity.
* **Best Accuracy**: Achieved **62.67%** using a specific combination of Adjectives, Adverbs, and Verbs.

### 3. Error Analysis

We analyzed the most common words and bigrams in misclassified reviews:

* **False Positives**: Often caused by sarcastic text or "good" words describing bad movie elements.
* **False Negatives**: Often caused by reviews describing "dark" or "violent" plots using negative-weighted words, even if the review is positive.

---

## Installation and Requirements

To run these notebooks, you need the following libraries:

```bash
pip install nltk numpy pandas scikit-learn seaborn matplotlib optuna

```

And the following NLTK resources:

* `movie_reviews`
* `stopwords`
* `wordnet`
* `sentiwordnet`
* `vader_lexicon`
* `averaged_perceptron_tagger`

---

**Author**: Andreu Lopez Perez
**Date**: December 2024