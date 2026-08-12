# AI News Bias Detector

An NLP-based research project for detecting political framing in news articles and classifying them into three categories:

- **Left**
- **Center**
- **Right**

The project investigates whether modern Natural Language Processing (NLP) and transformer-based models can identify political framing from the language, context, emphasis, and presentation of news content.

> **Important:** This is not a conventional sentiment-analysis system. The goal is to study political framing and bias, which can exist independently of whether an article expresses positive, negative, or neutral emotion.

---

## 1. Research Motivation

People consume news from many different sources every day. Although different outlets may report the same event, they can emphasize different facts, use different descriptions, and present the same issue from different perspectives.

These differences are not always obvious to readers.

Manually comparing large numbers of articles to identify political framing is also difficult and time-consuming.

This project explores whether NLP can provide a data-driven approach for identifying these patterns at scale.

---

## 2. Why Sentiment Analysis Is Not Enough

Sentiment analysis primarily focuses on the emotional orientation of text, such as whether a piece of writing is positive, negative, or neutral.

Political framing is different.

A news article can describe a tragic, emotional, or controversial event without necessarily being politically Left or Right.

Political framing can instead appear through:

- Word choice
- Description of people or events
- What information is emphasized
- What information is omitted
- Context surrounding an event
- Quotes and sources selected
- Tone and presentation
- How political issues are positioned within the article

For this reason, the project focuses on **contextual political framing rather than sentiment alone**.

---

## 3. Research Objective

The primary objective is to develop and evaluate NLP models capable of classifying news articles into:

| Class | Description |
|---|---|
| Left | News content classified as having a Left political framing |
| Center | News content classified as having a Center political framing |
| Right | News content classified as having a Right political framing |

The research also compares transformer-based approaches with traditional machine-learning baselines.

---

## 4. Methodology

The project followed an experimental NLP workflow:

```text
News Dataset
     ↓
Data Exploration & Analysis
     ↓
Text Preprocessing
     ↓
Train / Validation / Test Split
     ↓
Traditional ML Baselines
     ↓
Transformer Experiments
     ↓
DeBERTa-v3-base Fine-Tuning
     ↓
Evaluation
     ↓
Error & Class-Level Analysis
     ↓
Future API Deployment
```
5. Models and Experiments

The project explored multiple approaches, including:

Traditional Machine Learning
Random Forest
Support Vector Machine (SVM)

These models provided useful baseline comparisons against transformer-based approaches.

Transformer Models

The research also experimented with transformer architectures using TensorFlow/Keras before moving to PyTorch-based fine-tuning.

The primary transformer model used for the later experiments was:

Microsoft DeBERTa-v3-base

DeBERTa was selected because transformer architectures can capture contextual relationships between words and provide a stronger foundation for understanding complex language patterns.

6. DeBERTa-v3-base

The final transformer experiments used:

microsoft/deberta-v3-base
Three classification labels
PyTorch
Hugging Face Transformers
AdamW optimization
Learning-rate scheduling
Weight decay
Gradient clipping
Class-weighted Cross Entropy Loss

Class weighting was introduced to account for differences in the number of examples across the three classes.

7. Evaluation Metrics

Because the dataset contains different numbers of examples across classes, accuracy alone is not sufficient for evaluating the model.

The project therefore evaluates:

Accuracy

The proportion of all predictions that were correct.

Precision

The proportion of articles predicted as a particular class that actually belonged to that class.

Recall

The proportion of articles belonging to a particular class that the model successfully identified.

F1-score

The harmonic mean of precision and recall.

Macro F1

The average F1-score across all classes, giving each class equal importance.

Macro F1 is particularly important in this project because strong performance on the larger Center class should not hide weak performance on the Left or Right classes.

8. Current DeBERTa Results

One of the evaluation runs produced:

Metric	Test Result
Test Loss	1.0051
Accuracy	48.46%
Precision	49.24%
Recall	51.12%
Macro F1	47.90%

The model's class-level performance showed that the three political categories remain difficult to distinguish consistently.

This result is therefore treated as a research baseline rather than a claim of production-level accuracy.

9. Class-Level Performance

A detailed evaluation showed:

Class	Precision	Recall	F1
Left	33.21%	64.71%	43.89%
Center	62.94%	45.43%	52.77%
Right	51.57%	43.21%	47.02%

The results reveal an important research finding:

The model identifies many actual Left articles, but its low Left precision means it also incorrectly predicts Left for many other articles.
Center has the strongest precision, meaning Center predictions are comparatively reliable when the model makes them.
Right shows moderate performance but remains difficult to distinguish from the other political categories.

These class-level differences demonstrate why overall accuracy alone does not adequately describe the behavior of the model.

10. Traditional ML Comparison

Traditional machine-learning models were also evaluated as baselines.

The experiments included:

Random Forest
Support Vector Machine (SVM)

The baseline experiments produced different precision, recall, and F1 profiles across the three classes.

This comparison helps establish whether the additional complexity of transformer architectures provides meaningful benefits for political framing classification.

11. Research Challenges

Political bias detection is inherently challenging because political framing can be subtle and context-dependent.

Some of the major challenges observed include:

Class imbalance
Overlap between political categories
Context-dependent language
Difficulty distinguishing framing from emotional language
Similar vocabulary across different political perspectives
False predictions between neighboring classes
Generalization to articles from unseen sources

The current results show that further research is required before the model can be considered sufficiently reliable for real-world deployment.

12. Future Work

The research is ongoing.

Planned improvements include:

Systematic hyperparameter tuning
Improved text preprocessing
Further transformer experiments
Class-specific error analysis
Better handling of class imbalance
Testing additional transformer architectures
Evaluation on unseen news sources
Robustness testing
Threshold and calibration experiments
Improved model interpretability

A major next step is to turn the trained model into a FastAPI application so that the system can be tested interactively with new articles.

13. Potential Application

The long-term goal is to develop an accessible AI-assisted tool that can help users:

Submit a news article or text.
Analyze the content using the trained NLP model.
Receive a predicted political-framing category.
Explore the model's confidence and evaluation limitations.
Compare perspectives across different news sources.

The system is intended as an assistive research and media-literacy tool, not as an authority that determines whether a news article is objectively biased.

14. Project Structure

```bash

AI-News-Bias-Detector/
│
├── notebooks/
│   ├── 01_AI_News_Bias_Detector_Modeling.ipynb
│   └── 02_AI_News_Bias_Detector_Modeling_Continuation.ipynb
│
├── README.md
├── LICENSE
└── .gitignore

```