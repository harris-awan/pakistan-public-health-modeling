# Capstone Project Framing: Socio-Economic Determinants of Child Health in Pakistan

## 1. Provisional Lane Choice
* **Selected Lane:** Classification / Scoring (Advanced Track / Mentor-Gated)
* **Domain Focus:** Public health demographics, epidemiological risk profiling, and resource allocation.

## 2. Core Research Question & Unit of Analysis
* **Research Question:** Can maternal socioeconomic indicators, household asset wealth indices, and localized geographic parameters be modeled to estimate the probability of severe health deficits (such as stunting or acute malnutrition indicators) in children under the age of five?
* **Unit of Analysis:** An individual child record extracted from regional health survey microdata.

## 3. The Business Logic: Decision, Action, & Output
* **Model Output:** A predicted probability risk score ($p \in [0, 1]$) indicating a household's vulnerability to critical child health milestones.
* **The Decision:** Determining the distribution priority of localized healthcare interventions, vitamin programs, and community wellness workers across sparse regions.
* **The Action:** Public health teams or field NGOs deploy physical aid infrastructure directly to the specific community clusters flagged with elevated risk probabilities.

## 4. Risk Mitigation: The Cost of a Wrong Recommendation
* **False Positive (Type I Error) & Cost:** The model flags a low-risk household as critical. **Cost:** Misallocation of finite medical supplies and worker hours to stable areas, adding administrative overhead and leaving fewer assets for critical zones.
* **False Negative (Type II Error) & Cost:** The model misclassifies a high-risk child as safe. **Cost:** Severe ethical consequences where vulnerable individuals fail to receive preventive clinical screening, resulting in preventable illness or nutritional regression.

## 5. Why This is an ML Problem (Not Just "Train a Model")
* **High-Dimensional Interaction:** Socioeconomic determinants of health do not scale linearly. The layered effects of structural poverty, sanitation access, and parental literacy form non-linear patterns that simple static filters or averages cannot capture.
* **Role of Cautious Modeling:** This system does not act as an automated execution or diagnostic agent. It functions purely as a probabilistic screening tool meant to assist human decision-makers, and all model insights must be interpreted as directional risk indicators subject to manual validation.