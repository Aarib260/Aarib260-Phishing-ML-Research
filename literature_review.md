# Literature Review: Machine Learning-Based Phishing URL Detection

## 1. Introduction

Phishing is a form of cyberattack in which attackers attempt to deceive users into interacting with malicious websites or providing sensitive information. Because phishing URLs can be created rapidly and changed frequently, automated detection has become an important cybersecurity research problem.

Phishing URL detection can be formulated as a binary classification problem. A URL is represented using measurable characteristics and classified as either **phishing (malicious)** or **legitimate (benign)**.

Traditional security systems, particularly blacklists, are effective at identifying previously reported malicious URLs. However, they are primarily reactive: a newly created phishing URL may not be detected until it has been identified and added to a security database. This limitation has motivated research into machine-learning methods that can identify patterns associated with previously unseen phishing URLs.

---

## 2. Existing Approaches to Phishing Detection

### 2.1 Blacklist-Based Detection

Blacklist-based systems compare URLs against databases of previously identified malicious websites. These systems are generally fast and effective for known threats.

However, their main limitation is their dependence on previously identified URLs. Newly created phishing URLs may remain undetected until they are reported and added to the blacklist.

### 2.2 Heuristic Detection

Heuristic approaches use predefined rules or indicators to identify suspicious URLs. Examples include unusual URL structures, excessive subdomains, suspicious characters, or abnormal domain characteristics.

Although heuristics can detect some previously unseen threats, attackers can adapt their techniques to avoid known rules. Heuristic systems can also produce false positives when legitimate URLs happen to match suspicious patterns.

### 2.3 Machine Learning

Machine-learning approaches attempt to learn statistical patterns from labelled phishing and legitimate URLs.

Instead of relying entirely on predefined rules, a model can learn relationships between URL characteristics and their corresponding labels. Commonly investigated algorithms include:

- Logistic Regression
- Support Vector Machines
- Decision Trees
- Random Forest
- Gradient Boosting
- Neural Networks

Machine learning therefore provides a potential approach for identifying phishing URLs that have not previously appeared in security databases.

### 2.4 Deep Learning

Deep-learning approaches can learn complex representations from URL characters, webpage information, or other features. Convolutional and recurrent neural networks have been investigated for this purpose.

Deep learning can reduce reliance on manually engineered features, but it generally requires greater computational resources and can be more difficult to interpret.

---

## 3. Feature Engineering in Phishing Detection

Feature engineering is an important part of traditional machine-learning approaches to phishing detection. Researchers have investigated several categories of features.

### 3.1 Lexical and URL-Based Features

Lexical features are extracted directly from the URL string.

Examples include:

- URL length
- Number of characters
- Number of dots
- Number of subdomains
- Number of special characters
- Token count
- Entropy
- Presence of suspicious terms
- Top-level domain characteristics

A major advantage of lexical features is that they can be extracted without directly visiting the website. This makes them relatively fast and reduces the risk associated with interacting with potentially malicious content.

However, attackers can manipulate the structure of URLs, meaning that lexical characteristics alone may not always provide sufficient information.

### 3.2 Domain and Host-Based Features

Domain-based features can include:

- Domain age
- IP address
- Registrar information
- DNS characteristics
- Top-level domain

These features can provide additional contextual information about the website.

However, obtaining some domain characteristics may require external services or databases, which can introduce additional latency and availability issues.

### 3.3 HTML and Content Features

Researchers have also investigated features obtained from webpage content.

Examples include:

- JavaScript characteristics
- Forms
- Iframes
- Hidden elements
- Page structure
- External resources

These features can provide additional information about the behavior and structure of phishing websites. However, obtaining them generally requires accessing the website, increasing computational requirements and introducing potential security risks.

### 3.4 Behavioral Features

Behavioral features can include:

- Redirect chains
- Network behavior
- Website interactions
- Popularity information

These features can provide valuable information but can be more difficult to collect consistently because they depend on dynamic website behavior.

---

## 4. Machine-Learning Models in Previous Research

### 4.1 Logistic Regression

Logistic Regression provides a relatively simple baseline for binary classification. Its simplicity and interpretability make it useful for establishing baseline performance.

### 4.2 Decision Trees

Decision Trees can model nonlinear relationships between features and provide relatively interpretable classification rules.

### 4.3 Random Forest

Random Forest has been frequently investigated for phishing detection, particularly when working with tabular feature data.

Its ability to model nonlinear relationships and interactions between features makes it useful for cybersecurity classification. It can also provide feature-importance estimates, which can help researchers investigate which characteristics influence predictions.

However, Random Forest is not immune to overfitting. Its performance depends on factors including dataset composition, feature selection, and model configuration.

### 4.4 Neural Networks

Neural networks can learn complex relationships from sufficiently large datasets and have achieved strong performance in various phishing-detection studies.

However, reported performance can vary substantially depending on the dataset and evaluation methodology. Neural networks can also be more difficult to interpret than traditional models.

Therefore, high accuracy alone should not be treated as evidence of strong real-world generalization.

---

## 5. Datasets Used in Phishing Detection Research

The quality and composition of a dataset can strongly influence the results of a machine-learning study.

### 5.1 PhiUSIIL

The PhiUSIIL dataset contains **235,795 instances**, consisting of:

- 134,850 legitimate URLs
- 100,945 phishing URLs

The dataset contains **54 features** covering different characteristics of URLs and associated webpages.

The large number of examples makes PhiUSIIL useful for developing machine-learning models.

However, its relatively large feature set also raises an important research question: whether all available features are necessary and whether the same features can be reproduced consistently on an independent dataset.

### 5.2 LegitPhish

LegitPhish contains **101,219 labelled URLs**, consisting of:

- 63,678 phishing URLs
- 37,540 legitimate URLs

The dataset focuses on **17 structural and lexical features**.

Its more focused feature set makes it particularly relevant to research investigating whether URL characteristics alone can provide effective phishing detection.

At the same time, its smaller feature set means that it does not contain the same breadth of webpage and content information available in some larger datasets.

---

## 6. Dataset Bias and Generalization

An important issue identified throughout phishing-detection research is **dataset bias**.

Different datasets may obtain phishing and legitimate URLs from different sources. For example, phishing URLs may be collected from security databases while legitimate URLs may be obtained from lists of popular websites.

If the two groups have systematic differences caused by their sources, machine-learning models may learn characteristics associated with the datasets rather than genuine phishing behavior.

This creates a major concern when interpreting very high classification results.

A model that achieves 99% accuracy on a random test split from the same dataset used for training may not necessarily achieve 99% accuracy when presented with independently collected URLs.

Therefore, **cross-dataset evaluation** provides an important way of investigating model generalization.

---

## 7. Research Gap

The literature demonstrates that machine-learning approaches can achieve strong performance in phishing URL classification. However, several challenges remain.

### Generalizability

It is unclear whether models that perform well on one dataset will maintain their performance on independently collected data.

### Dataset Bias

Models may learn patterns specific to the sources or collection methods used to construct a dataset.

### Robustness

Changes in URL structures, attacker behavior, or dataset composition may affect model performance.

### Feature Dependence

A model may achieve high performance because of a small number of highly predictive features. Understanding which features contribute most to classification is therefore important.

### Explainability

Understanding why a model identifies a URL as phishing can provide insight into whether it has learned meaningful cybersecurity characteristics.

These challenges motivate further investigation into cross-dataset performance rather than relying exclusively on within-dataset accuracy.

---

## 8. Proposed Research Direction

Based on the gaps identified in the literature, this project will investigate the following research question:

> **How well do machine-learning models trained on one phishing URL dataset generalize to an independent dataset, and which URL features contribute most to their performance?**

### Hypotheses

**H1 — Generalization**

Machine-learning models will achieve strong performance on an internal test set but experience a measurable decrease in performance when evaluated on an independent dataset.

**H2 — URL Features**

Lexical and structural URL features can provide useful phishing-detection performance without requiring direct interaction with webpage content.

**H3 — Feature Importance**

The importance of individual URL features will differ between datasets, suggesting that dataset composition can influence which characteristics models rely on.

---

## 9. Proposed Methodology

The first stage of the research will investigate whether the features available in PhiUSIIL and LegitPhish are directly comparable.

This is important because features with similar names may not necessarily be calculated using identical definitions or methods.

If a common feature set can be established, several traditional machine-learning models will be evaluated, including:

- Logistic Regression
- Decision Tree
- Random Forest

The models will be evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- False-positive rate
- Computational efficiency

The study will compare:

1. Performance on an internal test set.
2. Performance on an independent dataset.
3. Differences in feature importance.
4. Changes in performance between datasets.

If the features cannot be directly compared, a common set of lexical and structural features will be recalculated from the raw URLs where possible.

---

## 10. Expected Contribution

The purpose of this research is not simply to build a phishing classifier with the highest possible accuracy.

Instead, the study aims to investigate whether apparently strong machine-learning models **generalize beyond the dataset on which they were developed**.

The research will therefore focus on:

- Cross-dataset generalization
- Dataset bias
- Feature importance
- Model robustness
- Independent evaluation

This approach may provide a more realistic assessment of phishing URL detection than relying solely on random train/test splits within a single dataset.

---

## 11. Conclusion

Previous research demonstrates that machine learning can be effective for phishing URL detection. However, reported performance must be interpreted carefully because dataset composition, feature selection, and evaluation methodology can substantially influence results.

The central focus of this research is therefore **generalization**: determining whether models that perform well on one dataset can maintain their performance when tested on independently collected data.

The next stage of the project will involve detailed investigation of the selected datasets, including their features, labels, class distributions, missing values, duplicates, and feature compatibility.
