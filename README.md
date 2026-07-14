# Public Health Forecasting: Predictive Modeling for Regional Stunting Risk in Pakistan

### Author: Harris Awan
**Academic Track**: Machine Learning & Data Science  
**Data Credit**: *Built on the FlyRank ML Internship dataset* ([flyrank.ai](https://flyrank.ai))

---

## Abstract
This study addresses the critical public health challenge of childhood stunting in Pakistan by developing a predictive model to identify high-risk households using the 2017-18 Demographic and Health Survey (DHS) dataset. We analyze key socioeconomic and geographical indicators—primarily wealth index metrics and urban/rural categorization—to forecast vulnerability. We compare a heuristic-based baseline model with a validated machine learning classifier, finding that incorporating multi-dimensional household data significantly reduces false-negative rates in aid delivery. Our final model achieves a classification accuracy improvements of over 15% relative to the rule-based baseline, providing actionable priority rankings for regional resource dispatch.

---

## 1. Introduction / Problem Statement
Childhood stunting (chronic malnutrition resulting in a low height-for-age ratio) is a critical developmental bottleneck in Pakistan, driven by multi-layered socioeconomic factors. Traditional resource allocation relies on broad regional averages, which often fail to capture micro-level household disparities, leading to high rates of resource misallocation (false positives) and missed vulnerable families (false negatives). 

This research aims to build an actionable decision-support tool. By modeling stunting risk as a function of household assets and demographic markers, public health officials can prioritize targeted nutritional interventions, sanitation infrastructure, and medical support directly to the families in greatest need.

---

## 2. Data Profile & Methodology

### Data Description
The analysis utilizes the Pakistan Demographic and Health Survey (DHS) 2017-18 release. The data profile spans multiple provinces with cluster-level (`hv001`) and household-level (`hv002`) observations.
* **Key Exclusions**: Households with completely missing anthropometric measurements (stunting targets) or unresolved geographical coordinates were excluded to prevent data corruption.
* **Key Features**: 
  * `hv270`: Household wealth index (1 = Poorest to 5 = Richest)
  * `hv025`: Type of place of residence (1 = Urban, 2 = Rural)

### Modeling & Validation Strategy
To prevent data leakage, the dataset was cleanly split into a 70% training set and a 30% test set using stratified sampling. We evaluated two core approaches:
1. **Rule-Based Baseline Heuristic**: Built on a strict heuristic scoring model where lowest wealth status (`hv270 == 1`) and rural status (`hv025 == 2`) are assigned the highest priority scores.
2. **Machine Learning Classifier**: Built on an ensemble model incorporating multi-feature non-linear interactions (maternal education, asset counts, water source types).

---

## 3. Results & Evaluation
The comparative performance on the holdout test set clearly demonstrates the superiority of the machine learning approach:

| Metric | Heuristic Baseline Model | Machine Learning Classifier (w05/w06) |
| :--- | :---: | :---: |
| **Accuracy** | 71.2% | **86.5%** |
| **Sensitivity (Recall)** | 62.1% | **89.3%** |
| **Precision** | 58.4% | **81.2%** |
| **False-Negative Rate** | 37.9% | **10.7%** |

The ensemble machine learning classifier successfully captured non-linear relationships between marginal wealth shifts and local infrastructure quality. This reduction in the false-negative rate (from 37.9% down to 10.7%) directly translates to thousands of high-risk children being proactively captured by intervention programs who would have otherwise been missed by basic rule-based sorting.

---

## 4. Limitations & Honest Framing
While the predictive pipeline is highly performant, users must be aware of its structural limitations:
* **Asset Index Lag**: The wealth index is calculated based on static assets (e.g., household floor material, electronic ownership). It does not capture sudden agricultural economic shocks, localized droughts, or rapid inflation in real time.
* **Geographic Latency**: High-risk areas experiencing temporary migration or security instability may suffer from survey data latency, potentially leading to misassigned priority scores.

---

## 5. Content Action Playbook (Recommendations)
The final model outputs a prioritized queue ranking households from highest predicted risk to lowest, mapping them directly to standardized actions:

1. **Category: CRITICAL_DIRECT_AID** (Risk score $\ge$ 0.75)
   * *Reason Code*: `LOW_WEALTH_HIGH_ISOLATION`
   * *Action*: Immediate dispatch of nutritional supplements and household water sanitation filtration units.
2. **Category: COMMUNITY_MONITORING** (Risk score 0.50 - 0.74)
   * *Reason Code*: `MODERATE_MULTIDIMENSIONAL_RISK`
   * *Action*: Direct enrollment in localized community healthcare tracking and monthly child height-for-age audits.
3. **Category: ROUTINE_OBSERVATION** (Risk score < 0.50)
   * *Reason Code*: `LOW_RISK_BASELINE`
   * *Action*: Standard administrative dispatch of basic hygiene educational pamphlets during seasonal public health drives.

### What Should NOT Be Automated
* **Medical overrides**: Low-risk model predictions must never be used to deny clinical treatment or immediate nutrition packets if a physical child audit shows signs of developmental delay.
* **Entitlement removal**: The model's low-risk classification must never automatically strip historical subsidies or food rations from vulnerable sub-populations.

---

## 6. Reproducibility & Code References
To inspect, rerun, or verify the pipeline, refer to the following documented notebooks in this repository:
* [Week 2: Machine Learning Task Framing](./work/notebooks/w02_ml_task_framing.ipynb)
* [Week 3: Data Profiling & Quality Contract](./work/notebooks/w03_data_contract.ipynb)
* [Week 4: Baseline Heuristic Generation](./work/notebooks/w04_baseline_score.ipynb)
* [Week 5: Core Predictive Machine Learning Model](./work/notebooks/w05_model.ipynb)
* [Week 6: Model Validation and Metrics Audit](./work/notebooks/w06_validation_audit.ipynb)
* [Week 7: Action Playbook Optimization](./work/notebooks/w07_action_playbook.ipynb)

---

## Acknowledgments & Data Credit
This modeling work and the associated research pipeline are built on the **FlyRank ML Internship dataset** ([flyrank.ai](https://flyrank.ai)). We thank the DHS program and FlyRank's research coordination team for providing clean, high-dimensional regional datasets enabling practical educational research.