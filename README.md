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
## 5. Models and Experiments

The project explored multiple machine learning and transformer-based approaches for political framing classification.

### Traditional Machine Learning

The following traditional machine learning models were evaluated as baseline approaches:

- **Random Forest**
- **Support Vector Machine (SVM)**

These models provided useful baseline comparisons against the transformer-based approaches.

### Transformer Models

The research also experimented with transformer architectures using **TensorFlow/Keras** before moving to **PyTorch-based fine-tuning**.

The primary transformer model used in the later experiments was:

**Microsoft DeBERTa-v3-base**

DeBERTa was selected because transformer architectures can capture contextual relationships between words, providing a stronger foundation for understanding complex language patterns in news content.

---

## 6. DeBERTa-v3-base

The final transformer experiments were conducted using:

- **Model:** `microsoft/deberta-v3-base`
- **Task:** Three-class classification
- **Framework:** PyTorch
- **Library:** Hugging Face Transformers
- **Optimizer:** AdamW
- **Learning-rate scheduling:** Linear learning-rate scheduler with warm-up
- **Weight decay:** `0.01`
- **Gradient clipping:** Maximum gradient norm of `1.0`
- **Loss function:** Class-weighted Cross Entropy Loss

### Class Weighting

Class weighting was introduced to account for differences in the number of training examples across the three political-framing classes.

This helps reduce the tendency of the model to favor classes with more training examples.

---

## 7. Evaluation Metrics

Because the dataset contains different numbers of examples across the three classes, **accuracy alone is not sufficient** for evaluating the model.

The project therefore evaluates the model using:

### Accuracy

Accuracy is the proportion of all predictions that the model classified correctly.

### Precision

Precision measures the proportion of articles predicted as a particular class that actually belong to that class.

In other words:

> When the model predicts a class, how often is it correct?

### Recall

Recall measures the proportion of articles that actually belong to a particular class that the model successfully identifies.

In other words:

> Of all the articles that truly belong to a class, how many did the model find?

### F1-Score

F1-score is the harmonic mean of precision and recall.

It provides a balance between the model's ability to make correct predictions and its ability to identify relevant examples.

### Macro F1

Macro F1 calculates the F1-score independently for each class and then takes the average, giving **equal importance to Left, Center, and Right**.

Macro F1 is particularly important for this project because strong performance on the larger **Center** class should not hide weaker performance on the **Left** or **Right** classes.

---

## 8. Current DeBERTa Results

One of the DeBERTa evaluation runs produced the following test results:

| Metric | Test Result |
|---|---:|
| Test Loss | 1.0051 |
| Accuracy | 48.46% |
| Precision | 49.24% |
| Recall | 51.12% |
| Macro F1 | 47.90% |

The results indicate that the three political-framing categories remain difficult for the model to distinguish consistently.

Therefore, this result is treated as a **research baseline**, rather than a claim of production-level accuracy.

The results also motivate further experimentation, model improvement, and error analysis.

---

## 9. Class-Level Performance

A more detailed evaluation was conducted to understand how the model performed on each political-framing class.

| Class | Precision | Recall | F1-Score |
|---|---:|---:|---:|
| **Left** | 33.21% | **64.71%** | 43.89% |
| **Center** | **62.94%** | 45.43% | **52.77%** |
| **Right** | 51.57% | 43.21% | 47.02% |

### Key Findings

The class-level results reveal several important patterns.

- **Left:** The model achieves relatively high recall (`64.71%`), meaning it identifies many of the actual Left articles. However, its low precision (`33.21%`) indicates that many articles predicted as Left actually belong to another class.

- **Center:** Center has the strongest precision (`62.94%`). This means that when the model predicts Center, it is comparatively more likely to be correct. However, its recall (`45.43%`) shows that the model still misses many actual Center articles.

- **Right:** The model achieves moderate performance on the Right class, but both recall (`43.21%`) and F1-score (`47.02%`) indicate that distinguishing Right articles from the other classes remains challenging.

These class-level differences demonstrate why **overall accuracy alone does not adequately describe model behavior**.

---

## 10. Traditional Machine Learning Comparison

Traditional machine learning models were also evaluated as baseline approaches.

The experiments included:

- **Random Forest**
- **Support Vector Machine (SVM)**

The baseline models produced different precision, recall, and F1-score profiles across the three political-framing classes.

These experiments provide a reference point for evaluating whether the additional complexity of transformer architectures provides meaningful benefits for political-framing classification.

The comparison also helps identify the strengths and weaknesses of different modeling approaches.

---

## 11. Research Challenges

Political-framing detection is inherently challenging because political framing can depend heavily on context and presentation.

Some of the major challenges observed during the research include:

- **Class imbalance**
- **Overlap between political categories**
- **Context-dependent language**
- **Difficulty distinguishing political framing from emotional language**
- **Similar vocabulary across different political perspectives**
- **False predictions between neighboring classes**
- **Generalization to articles from unseen news sources**

These challenges demonstrate that political-framing classification is more complex than simply identifying keywords or emotional sentiment.

The current results indicate that further research is required before the model can be considered sufficiently reliable for real-world deployment.

---

## 12. Future Work

The research is ongoing, with several areas identified for future improvement.

Planned improvements include:

- Systematic hyperparameter tuning
- Improved text preprocessing
- Further transformer experiments
- Class-specific error analysis
- Better handling of class imbalance
- Testing additional transformer architectures
- Evaluation on unseen news sources
- Robustness testing
- Threshold and calibration experiments
- Improved model interpretability

### FastAPI Deployment

A major next step is to convert the trained model into a **FastAPI application**.

This will allow the research system to be tested interactively by submitting new news articles and observing the model's predictions.

The API will provide a foundation for a future user-facing demonstration of the research.

---

## 13. Potential Application

The long-term goal is to develop an accessible **AI-assisted media-literacy and research tool** that can help users explore political framing in news content.

A potential workflow would allow a user to:

1. **Submit a news article or text.**
2. **Analyze the content using the trained NLP model.**
3. **Receive a predicted political-framing category.**
4. **Explore the model's confidence and known limitations.**
5. **Compare perspectives across different news sources.**

The system is intended to function as an **assistive research and media-literacy tool**, rather than an authority that determines whether a news article is objectively biased.

Model predictions should therefore be interpreted as **AI-generated classifications based on learned patterns**, not as definitive judgments about the political intent or truthfulness of an article.
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