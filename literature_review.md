# Literature Review: ML-Based Phishing URL Detection

## 1. Research Problem
*   **What is phishing URL detection?** 
*   **Why is automated detection important?** 
*   **What are the limitations of traditional approaches?**
*   Traditional detection relies heavily on "List-based" approaches (blacklisting known malicious URLs or whitelisting safe ones). The paper highlights that while lists are highly accurate for known threats, they fail entirely against "zero-day" (newly created) phishing websites because a URL must first be reported and verified before it is blacklisted 

## 2. Existing Approaches
*   **Blacklists:** 
*   **Heuristics:** 
*   **Machine learning:** 
*   **Deep learning:** 

## 3. Feature Engineering
*   **URL/lexical:** 
*   **Domain:** 
*   **HTML/content:** 
*   **Behavioral:** 

## 4. Machine Learning Models
*   **Logistic Regression:** 
*   **Decision Tree:** 
*   **Random Forest:** 
*   **SVM:** 
*   **Neural Networks:** 

## 5. Datasets

### Dataset 1: PhiUSIIL
*   **Size:** 235,795 instances (134,850 legitimate / 100,945 phishing)
*   **Features:** 54 features
*   **Source:** 
*   **Labels:** 1 = legitimate, 0 = phishing
*   **Advantages:** 
*   **Limitations:** 

### Dataset 2: LegitPhish
*   **Size:** 101,219 instances (63,678 phishing / 37,540 legitimate)
*   **Features:** 17 structural/lexical features
*   **Source:** 
*   **Labels:** 
*   **Advantages:** 
*   **Limitations:** 

## 6. Research Gaps
*   *Note: Focus on generalizability, robustness, dataset limitations, and explainability.*

## 7. Relevance to My Research
*   **Proposed Investigation:** Do ML models that perform well on one phishing URL dataset maintain their performance when evaluated on a completely independent dataset?
