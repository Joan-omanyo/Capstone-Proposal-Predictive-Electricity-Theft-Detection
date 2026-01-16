![ Predictive-Electricity-Theft-Detection (%)](https://github.com/Sesery/Capstone-Proposal-Predictive-Electricity-Theft-Detection/blob/main/ElectricityTheftDetection.png)

# Capstone-Proposal-Predictive-Electricity-Theft-Detection

## 📋 Project Overview

This is an end-to-end machine learning system for detecting electricity theft using smart meter data. The project implements a supervised learning approach to identify fraudulent consumption patterns based on real-world theft behaviors. This is based on Institute of Electrical and Electronics Engineers (IEEE) research, the world's largest technical professional organization dedicated to advancing technology for the benefit of humanity.

## Business Objective

The primary business objective of this project is to develop a machine learning-driven system capable of detecting electricity theft with high precision and recall, directly enabling utility companies to reduce revenue losses stemming from non-technical losses. By accurately identifying fraudulent consumption patterns, the system allows for the efficient prioritization of field inspections, ensuring that investigative resources are allocated to the highest-risk cases. This facilitates proactive fraud detection, shifting from reactive investigations to preventative monitoring and timely intervention. Ultimately, the implementation of this solution enhances grid security and operational efficiency, safeguarding revenue, ensuring equitable billing, and contributing to a more stable and reliable electricity distribution infrastructure.

## 📊 Dataset understanding

* Source: UCI ElectricityLoadDiagrams2011-2014.
* Description: 370 smart meters with 15-minute interval readings from 2011-2014.
* Original Size: 370 columns × 140,256 time points (~4 years of data).
* Processed: Aggregated to daily consumption per meter (540,940 records)in kilowatt-hours.

![Global distribution of consumption (%)](https://github.com/Sesery/Capstone-Proposal-Predictive-Electricity-Theft-Detection/blob/main/global%20consumption.png)

## 🏗️ System Architecture

The system architecture is designed as a robust, end-to-end machine learning pipeline specifically tailored for electricity theft detection. It begins with a comprehensive data processing pipeline that transforms raw 15-minute interval smart meter data into insightful daily consumption profiles. This stage involves sophisticated feature engineering, generating over 30 distinct features that capture critical behavioral patterns. These features quantify statistical properties, rolling temporal statistics across 7, 30, and 90-day windows, pattern consistency through autocorrelation and seasonality, anomaly indicators like sudden drops, and fraud-specific signals such as Benford's Law violations.

To enable supervised learning on a dataset lacking real fraud labels, a realistic theft injection mechanism was implemented, grounded in IEEE research. This mechanism synthetically creates five distinct fraud types with controlled prevalence: Meter Tampering (35%), involving systematic under-recording; Cable Bypass (25%), representing complete meter circumvention; Partial Bypass (20%), for partial load shunting; Time-Based Theft (15%), occurring during specific low-inspection periods; and Gradual Theft (5%), featuring slowly increasing manipulation. These patterns are injected into 5% of the customer base, creating a labeled, imbalanced dataset that mirrors real-world theft distributions.

The model architecture employs a strategic ensemble approach to maximize detection performance. The model stack incorporates a Logistic Regression baseline for interpretability and linear pattern capture, a Random Forest classifier to leverage feature importance and non-linear interactions, and an optimized XGBoost model fine-tuned with early stopping for superior gradient-boosting performance. These diverse algorithms are combined into a final Voting Classifier utilizing weighted soft voting, which synthesizes their individual strengths to produce a more robust and accurate prediction than any single model could achieve alone.

Finally, a multi-faceted evaluation framework ensures the solution meets both technical and business requirements. The primary metric is the F2-Score, which deliberately emphasizes recall to minimize missed theft cases—a critical business imperative. Complementary business metrics include Precision@10%, which measures how effectively the model prioritizes the highest-risk customers for field inspections. This is supplemented by comprehensive standard metrics like accuracy, precision, recall, and PR-AUC, providing a holistic view of model performance across all operational dimensions relevant to utility company deployment.

![End-to-end data processing workflow (%)](https://github.com/Joan-omanyo/Capstone-Proposal-Predictive-Electricity-Theft-Detection/blob/main/End-to-end%20data%20processing%20workflow.png){:width="600px"}

## 📈 Key Results

<details> <summary><b>📊 Detailed Performance Table</b></summary><div align="center">
Model	F2-Score	Precision@10%	PR AUC	Precision	Recall	Accuracy
XGBoost	0.8572	0.6471	0.7680	0.6667	0.8824	0.9831
Random Forest	0.8478	0.6471	0.7639	0.6667	0.8824	0.9831
Ensemble	0.8197	0.7059	0.7349	0.7059	0.7059	0.9828
Logistic Regression	0.7901	0.5882	0.6839	0.5882	0.8824	0.9797
</div> <p><em>🥇 Best metric in column is bolded. Ensemble provides optimal Precision@10% for real-world deployment.</em></p> </details>

## Top Features for Detection

    1. z_score_90d: Long-term deviation from normal pattern.

    2. cum_dev_last: Recent deviation from historical mean.

    3. benford_violation: Irregular digit distribution.

    4. autocorr_weekly: Disruption in weekly patterns.

    5. sudden_drop_count: Frequency of abrupt consumption drops.


## 🛠️ Technical Implementation

### Feature Engineering Highlights

* Benford's Law Analysis: Detects unnatural consumption distributions.

* Rolling Statistics: Customer-specific anomaly detection.

* Pattern Consistency: Autocorrelation for habitual behavior.

* Entropy Measures: Consumption randomness quantification.

### Model Optimization

* Class Imbalance: SMOTE oversampling + class weighting.

* Hyperparameter Tuning: Grid search for optimal parameters.

* Early Stopping: Prevents overfitting in XGBoost.

* Feature Scaling: StandardScaler for numerical stability.


## 📊 Business Impact
### Operational Benefits
Inspection Efficiency: Top 10% predictions capture 70% of theft cases.

False Positive Reduction: Ensemble approach balances precision/recall.

Scalability: Handles 370+ meters with 4 years of historical data.

Interpretability: Feature importance guides investigation priorities.

### Financial Implications

Assuming:

Average theft: €500/month per customer.

Detection rate: 88% (model recall).

370 customers, 5% theft prevalence.

Annual Savings Potential: €97,680.
Inspection Efficiency Gain: 70% reduction in false inspections.

## 🔮 Future Enhancements

Timeframe	Key Enhancements
Short-term (0–3 months)	Real-time streaming pipeline, customer segmentation, explainable AI dashboard
Medium-term (3–12 months)	Billing system integration, weather/calendar feature enrichment, transfer learning
Long-term (12+ months)	Deep learning for temporal patterns, federated learning, blockchain audit logging

## 📚 References
UCI Machine Learning Repository - ElectricityLoadDiagrams.

IEEE Papers on Electricity Theft Detection.

Portuguese Energy Regulatory Authority Reports.

Industry Best Practices for Non-Technical Loss Detection.

## 👥 Team & Contact
Project Lead: [Your Name/Team Name]
Organization: [Your Organization]
Email: [Contact Email]
GitHub: [Repository Link]











