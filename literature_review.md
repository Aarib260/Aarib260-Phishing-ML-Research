# Literature Review: ML-Based Phishing URL Detection

## 1. Research Problem
*   **What is phishing URL detection?** It is formulated as a binary classification problem where a raw URL string is mapped to a feature vector and classified as either malicious (phishing) or benign (legitimate).
*   **Why is automated detection important?** Millions of new URLs are generated daily. Attackers constantly create "zero-day" phishing sites that traditional security measures cannot catch in time.
*   **What are the limitations of traditional approaches?** Traditional "List-based" approaches (blacklists/whitelists) are highly accurate for known threats but are entirely reactive. A phishing site must be reported and verified before it is blocked, leaving early victims vulnerable.

## 2. Existing Approaches
*   **Blacklists:** Fast and reliable for known malicious URLs, but fail against zero-day attacks.
*   **Heuristics:** Use predefined expert rules (e.g., "flag URLs with >5 subdomains"). They can catch some new threats but are easily bypassed as attackers adapt their techniques.
*   **Machine learning:** Proactive approach that extracts behavioral and structural features from URLs to train models capable of identifying previously unseen phishing attempts.
*   **Deep learning:** Uses neural networks (e.g., CNNs, LSTMs) to automatically learn feature representations directly from URL characters (Representation Learning), bypassing manual feature engineering, though at a high computational cost.

## 3. Feature Engineering
*   **URL/lexical:** Extracted directly from the URL string (e.g., length, token count, entropy, special characters). *Advantage:* Extremely fast and safe to extract without interacting with a malicious server. *Limitation:* Attackers can manipulate lexical structures to mimic legitimate sites.
*   **Domain/Host:** Extracted from server data (e.g., WHOIS registration date, IP address, registrar). *Advantage:* Provides historical and contextual trust. *Limitation:* Requires querying external APIs, which adds latency.
*   **HTML/content:** Extracted by downloading the webpage (e.g., hidden IFrames, JavaScript, brand logos). *Advantage:* Highly informative. *Limitation:* Computationally expensive and potentially dangerous.
*   **Behavioral:** Extracted from network interactions (e.g., redirect chains, popularity rankings). *Limitation:* Dynamic and highly difficult to collect consistently.

## 4. Machine Learning Models
*   **Logistic Regression / SVM / Decision Tree:** Serve as standard baseline batch-learning algorithms. They are computationally efficient and highly explainable.
*   **Random Forest:** Identified in systematic reviews as the most frequently used traditional ML classifier, highly effective at handling tabular feature data without overfitting.
*   **Neural Networks:** Frequently report the highest detection accuracies (up to 99.98%), but require massive datasets and lack explainability (the "black box" problem).

## 5. Datasets

### Dataset 1: PhiUSIIL
*   **Size:** 235,795 instances (134,850 legitimate / 100,945 phishing).
*   **Features:** 54 diverse features.
*   **Labels:** 1 = legitimate, 0 = phishing.
*   **Advantages:** Large scale and highly diverse feature profile.
*   **Limitations:** Models trained on 54 features may suffer from high dimensionality and latency; it requires investigation to see if all features are actually necessary.

### Dataset 2: LegitPhish
*   **Size:** 101,219 instances (63,678 phishing / 37,540 legitimate).
*   **Features:** 17 strictly structural/lexical features (e.g., length, entropy, TLD).
*   **Advantages:** A newer dataset with strong documentation on data provenance and verification, avoiding the pitfalls of unverified web scraping.
*   **Limitations:** Relies on a smaller subset of features compared to PhiUSIIL (no HTML/content features).

### Dataset 3: The "PhishTank/Alexa" Problem (General Literature)
*   **Limitation identified in reviews:** The majority of existing research relies on scraping PhishTank for malicious URLs and the Alexa Top list for legitimate ones. Models often learn the distinct differences between these two specific sources rather than learning generalized phishing behaviors.

## 6. Research Gaps
*   While recent studies frequently report high classification accuracy (98-99%), these metrics are usually achieved by testing the model on a holdout split of its *own* training dataset. 
*   Literature identifies **generalizability, robustness, dataset bias, and explainability** as the primary unresolved challenges. Models tend to overfit to the quirks of specific datasets (like PhishTank/Alexa collections).

## 7. Relevance to My Research
*   **Proposed Investigation:** Do ML models that perform well on one phishing URL dataset maintain their high performance when evaluated on a completely independent dataset? 
*   **Methodology Idea:** Train traditional ML models (like Random Forest) on Dataset A (e.g., PhiUSIIL) using only the 17 lexical features present in Dataset B (LegitPhish). Then, test those models on Dataset B to measure true cross-dataset generalizability and real-world robustness.
