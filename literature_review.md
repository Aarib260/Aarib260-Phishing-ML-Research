# ML-Based Phishing URL Detection

## 1. Research Problem

### What is phishing URL detection?

Phishing URL detection can be formulated as a binary classification problem. A URL is represented using measurable features and classified as either **phishing (malicious)** or **legitimate (benign)**.

### Why is automated detection important?

The large and constantly changing number of URLs makes manual identification impractical. Attackers can rapidly create new phishing websites, including previously unseen threats that may not yet appear in security blacklists.

Automated detection can help identify suspicious URLs using patterns learned from previously observed examples.

### Limitations of traditional approaches

Traditional list-based approaches, such as blacklists and whitelists, can be highly effective for known threats but are primarily reactive.

A newly created phishing URL may remain undetected until it is identified, reported, and added to a security database.

Machine-learning approaches provide an alternative by attempting to identify patterns associated with phishing URLs, including previously unseen examples.

---

## 2. Existing Approaches

### Blacklists

Blacklists maintain databases of known malicious URLs.

**Advantages:**
- Fast
- Effective for known threats
- Simple to implement

**Limitations:**
- Struggle with newly created URLs
- Depend on previously identified threats

### Heuristics

Heuristic systems use predefined rules or indicators to identify suspicious URLs, such as unusual URL structures, excessive subdomains, or suspicious characters.

**Advantages:**
- Can identify some previously unseen threats
- Relatively fast

**Limitations:**
- Can produce false positives
- Attackers can adapt to predefined rules

### Machine Learning

Machine-learning approaches learn statistical patterns from labelled examples of phishing and legitimate URLs.

They can use structural, lexical, domain, or other measurable features to classify previously unseen URLs.

### Deep Learning

Deep-learning models, including convolutional and recurrent neural networks, can learn representations directly from URL characters or other input data.

**Advantages:**
- Can learn complex patterns
- Can reduce manual feature engineering

**Limitations:**
- Greater computational requirements
- More difficult to interpret
- Performance can depend heavily on dataset quality and size

---

## 3. Feature Engineering

The project focuses primarily on features that can be extracted from URLs without directly interacting with potentially malicious websites.

### URL / Lexical Features

Examples include:

- URL length
- Token count
- Entropy
- Number of special characters
- Number of dots
- Number of subdomains
- Top-level domain characteristics

**Advantages:**
- Fast to extract
- Relatively safe
- Does not require visiting the website

**Limitations:**
- Attackers can manipulate URL structures
- Some phishing URLs can closely resemble legitimate URLs

### Domain / Host Features

Examples include:

- Domain age
- IP address
- Registrar information
- TLD characteristics

These features can provide useful contextual information but may require external databases or services.

### HTML / Content Features

Examples include:

- JavaScript characteristics
- Hidden elements
- Iframes
- Forms
- Page structure

These features can provide additional information but require accessing the webpage, increasing computational cost and introducing potential security risks.

### Behavioral Features

Examples include:

- Redirect chains
- Network behavior
- Website interactions

These can provide valuable information but are more difficult to collect consistently.

---

## 4. Machine-Learning Models

The project will initially investigate several traditional machine-learning approaches.

### Logistic Regression

Used as a simple and interpretable baseline classifier.

### Decision Tree

Provides an interpretable model capable of learning nonlinear decision boundaries.

### Random Forest

Random Forest is widely used for tabular cybersecurity classification because it can model nonlinear relationships and interactions between features.

It can also provide feature-importance estimates that help investigate which characteristics contribute to classification.

### Neural Networks

Neural networks can learn complex relationships from sufficiently large datasets, but their greater complexity can make interpretation more difficult.

> **Important:** High accuracy on one dataset does not necessarily demonstrate strong real-world performance. Dataset composition, feature selection, evaluation methodology, and dataset-specific patterns must also be considered.

---

## 5. Datasets

### PhiUSIIL

**Size:** 235,795 instances

**Class distribution:**

- 134,850 legitimate
- 100,945 phishing

**Features:** 54

**Labels:**

- `1` = legitimate
- `0` = phishing

#### Why use it?

PhiUSIIL provides a large dataset with a diverse set of features, making it useful for developing and evaluating machine-learning models.

#### Potential limitation

Its large feature set may introduce unnecessary complexity. Some features may also be difficult to reproduce consistently across an independent dataset.

---

### LegitPhish

**Size:** 101,219 labelled URLs

**Class distribution:**

- 63,678 phishing
- 37,540 legitimate

**Features:** 17 structural and lexical features

#### Why use it?

LegitPhish provides a more recent dataset with documented data provenance and verification procedures.

Its focused feature set is useful for investigating whether URL characteristics alone can provide effective classification.

#### Potential limitation

Its smaller feature set may not capture information available through HTML, webpage content, or other contextual features.

---

## 6. Dataset Bias

A broader issue in phishing-detection research is the use of different sources for phishing and legitimate URLs.

For example, phishing URLs may be collected from one security database while legitimate URLs may be obtained from popular-site lists.

If these sources have systematic differences, a model may learn characteristics associated with the **data sources** rather than genuine phishing behavior.

This creates a potential **dataset bias** problem.

Cross-dataset evaluation can help investigate whether a model has learned general phishing characteristics or has become dependent on patterns specific to its training dataset.

---

## 7. Research Gap

Existing studies frequently report high classification performance, sometimes above 98–99%, when models are evaluated using random train/test splits from the same dataset.

However:

> **High within-dataset performance does not necessarily mean that a model will perform equally well on independently collected data.**

Important unresolved challenges include:

- **Generalizability** — Does a model trained on one dataset work effectively on another?
- **Dataset bias** — Is the model learning phishing characteristics or dataset-specific patterns?
- **Robustness** — Does performance remain stable when the data distribution changes?
- **Feature dependence** — Which URL characteristics actually contribute to classification?
- **Explainability** — Can we understand why a model classifies a URL as phishing?

---

## 8. Research Question

> **How well do machine-learning models trained on one phishing URL dataset generalize to an independent dataset, and which URL features contribute most to their performance?**

---

## 9. Hypotheses

### H1 — Generalization

Machine-learning models will achieve strong performance on an internal test set but experience a measurable decrease in performance when evaluated on an independent dataset.

### H2 — URL Features

Lexical and structural URL features can provide useful phishing-detection performance without requiring direct interaction with webpage content.

### H3 — Feature Importance

The importance of individual URL features will differ between datasets, suggesting that dataset composition can influence which characteristics models rely on.

---

## 10. Proposed Methodology

The study will first investigate the compatibility of features between PhiUSIIL and LegitPhish rather than assuming that similarly named features are calculated identically.

If comparable features are available:

1. Prepare the datasets.
2. Select a common feature set.
3. Train Logistic Regression, Decision Tree, and Random Forest models.
4. Evaluate performance using an internal test set.
5. Evaluate the trained models on an independent dataset.
6. Compare the results.
7. Analyze feature importance.
8. Investigate changes in performance between datasets.

### Evaluation Metrics

The models will be compared using:

- Accuracy
- Precision
- Recall
- F1-score
- False-positive rate
- Computational efficiency

If the features in the datasets are not directly comparable, a common set of lexical and structural features will be recalculated directly from the raw URLs.

---

## 11. Expected Contribution

Rather than focusing only on achieving the highest possible accuracy, this research investigates whether apparently strong phishing-detection models **generalize beyond the dataset on which they were developed**.

The project aims to demonstrate the importance of:

- Independent evaluation
- Feature selection
- Dataset bias
- Model robustness
- Feature interpretability

in machine-learning-based phishing URL detection.

---

## Research Status

**Current Stage:** Literature Review

**Next Stage:** Dataset Investigation

### Datasets Under Consideration

- PhiUSIIL
- LegitPhish

### Models Under Consideration

- Logistic Regression
- Decision Tree
- Random Forest

### Research Focus

**Cross-dataset generalizability and feature importance**
