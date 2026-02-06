# Language Identification using Character Trigrams

This project implements a Natural Language Processing (NLP) system designed to identify the language of a given sentence. It uses a character-based **Trigram Model** combined with **Lidstone Smoothing** to classify text into one of six languages: Italian, English, French, German, Dutch, and Spanish.

## Project Structure

* **Corpus**: The dataset is divided into training and testing sets.
* **Training Set**: 30,000 sentences per language.
* **Test Set**: 10,000 sentences per language.


* **Source Files**: The raw text files are located in the `langId/` directory (e.g., `ita_trn.txt`, `eng_tst.txt`).

## Technical Workflow

### 1. Data Preprocessing

The text is cleaned using regular expressions to ensure consistency across the corpus:

* **Digit Removal**: All numbers are stripped from the text.
* **Lowercasing**: Text is converted to lowercase to reduce vocabulary size.
* **Whitespace Normalization**: Multiple spaces are replaced with a single space.
* **Sentence Splitting**: Files are split by line breaks to handle individual samples.
* **Sequence Handling**: Training data is concatenated with double spaces to form a continuous sequence for n-gram extraction.

### 2. Feature Extraction: Character Trigrams

The model identifies patterns using sequences of three characters (trigrams):

* **Trigram Generation**: Created using `nltk.ngrams`.
* **Frequency Filtering**: To eliminate noise and rare character combinations, only trigrams appearing **5 or more times** in the training set are retained.

### 3. Classification Model

The system uses a probabilistic approach to determine the language:

* **Lidstone Smoothing ( )**: Handles the "Zero Frequency Problem" for trigrams that appear in the test set but were not seen during training.
* **Log-Likelihood Calculation**: Instead of multiplying small probabilities (which leads to numerical underflow), the model sums the logarithms of the trigram probabilities:


* **Prediction**: The language that maximizes the total score is selected as the final prediction.

## Performance Evaluation

The model's performance is analyzed using a **Confusion Matrix** and a detailed error report.

### Global Metrics

The script provides a comprehensive summary including:

* **Global Accuracy**: The percentage of correctly classified sentences across all languages.
* **Language-Specific Accuracy**: Detailed breakdown for each language.
* **Error Analysis**: Identification of specific sentences that were misclassified, grouped by the incorrect language predicted (e.g., French sentences mistakenly classified as Italian).

## How to Run

1. Ensure you have `scikit-learn`, `matplotlib`, `seaborn`, and `nltk` installed.
2. Place your language files in a folder named `langId/`.
3. Execute the script to see the Confusion Matrix and accuracy statistics.

---

**Course**: Introducció a l'Aprenentatge Automàtic (IAA)

**Task**: Language Identification Practice