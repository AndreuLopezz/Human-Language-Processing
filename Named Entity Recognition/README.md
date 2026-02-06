# Named Entity Recognition using CRF

This project focuses on the development of a **Named Entity Recognition (NER)** system using **Conditional Random Fields (CRF)**. The study evaluates how various feature engineering strategies, semantic embeddings, and label encoding schemes impact the performance of sequential models in Spanish and Dutch.

## Repository Structure

* **`NER_sense_features.ipynb`**: Baseline implementation using default CRF settings without additional features.


* **`NER_amb_features_1/2/3/4.ipynb`**: Iterative models incorporating morphological features, context, and word embeddings.


* **`NER_grid_search_amb_codificacions.ipynb`**: Systematic optimization of hyperparameters and comparison of encoding schemes.


* **`PRACTICA 3 - EXTRACCIÓ D'ENTITATS ANOMENADES.pdf`**: The full technical report detailing methodology and results.



---

## Methodology and Progression

The system was developed through several phases to identify the most effective characteristics for entity detection:

1. **Baseline Model**: A simple sequence-based model without morphological or contextual information.


2. **Feature Extraction**: Added characteristics such as capitalization, digit presence, punctuation, and local context (previous and next words).


3. **Semantic Embeddings**: Integrated **Word2Vec** vectors (ID 39 for Dutch, ID 68 for Spanish) to capture latent semantic relationships between words.


4. **Dimensionality Reduction**: Explored **K-means clustering** on embeddings to improve computational efficiency by using cluster IDs as features.


5. **Grid Search Optimization**: Automated selection of the best feature combinations and comparison of label encodings.



---

## Results and Comparison

Performance was measured using the **weighted F1-Score** across the CoNLL-2002 corpus.

| Model Version | Spanish F1-Score | Dutch F1-Score |
| --- | --- | --- |
| Model Base (No features) | 70.38% | 63.11% |
| Model with Basic Features | 76.41% | - |
| Model with Expanded Features | 76.83% | - |
| Model with Embeddings | 77.99% | 72.85% |

| **Optimized Model (BIO)** | <br>**78.03%** | <br>**73.22%** |

### Label Encoding Analysis

The study compared various schemes to represent entity boundaries:

* **BIO and IO**: Achieved the highest performance (0.780 F1).


* **BIOW and BIOES**: Showed slightly lower performance, suggesting that increased complexity does not always improve generalization in these models.



---

## Extra: Medical NER (CADEC Corpus)

As an extension, the system was applied to the **CADEC corpus** to detect biomedical entities in social media text.

* **Preprocessing**: A custom parser was implemented to transform `.conll` files into (word, label) tuples compatible with `CRFTagger`.


* **Features**: Included medical-specific suffixes (e.g., *-itis*, *-oma*) and expanded context windows.


* **Outcome**: Achieved a weighted F1-Score of **55.01%**. Performance was significantly hindered by severe data imbalance among minority categories like `B-S` or `I-Di`.



---

**Authors**: Andreu López Pérez

**Date**: May 2025