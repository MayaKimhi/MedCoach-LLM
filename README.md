# MedCoach-LLM
MedCoach is an AI-powered learning tool that simulates interactive patient cases to help medical students sharpen their clinical reasoning and diagnostic decision-making skills.

Medical students often face theory-heavy training with limited hands-on diagnostic practice.  
**MedCoach** offers a solution by simulating realistic patient encounters using large language models (LLMs) to:
- Generate synthetic patient cases.
- Simulate diagnostic dialogues between doctors, students, and virtual patients.
- Evaluate students based on their reasoning and similarity to expert clinicians.

## Pipeline Overview

### Input Data
- **Source:** [Diseases and their Symptoms dataset](https://www.kaggle.com/datasets/shobhit043/diseases-and-their-symptoms)
- **Size:** 2564 rows | 400 symptoms | 133 unique diseases
- Diseases and their Symptoms dataset provides a comprehensive collection of disease names and their associated symptoms, encoded in a one-hot manner.
 Each row in the dataset represents a single instance, such as a patient or case study, while each column represents a symptom or disease.

### Preprocessing
- Duplicate removal
- Removal of unused symptoms
- Filtering cases with ≥4 symptoms

### Patient Case Generation
   - Model: `MedLlama2`
   - Output: Full / 80% / 50% symptom cases per disease
     
### Doctor Simulation
   - Model: `Me-LLaMA 13B`
   - Task: Generate diagnostic Q&A
     
### Student Simulation
   - Model: `DeepSeek-R1`
   - Task: Generate student Q&A
     
### Evaluation
   - Metrics: Accuracy, AUC, cosine similarity to expert answers
   - Model-based evaluation: `PubMedBERT`
     
---

## Models
| Model          | Role                         |
|----------------|------------------------------|
| `MedLlama2`    | Case generation & dialogue   |
| `Me-LLaMA 13B` | Doctor role simulation       |
| `DeepSeek-R1`  | Student role simulation      |
| `PubMedBERT`   | Case generation evaluator         |

---
## Generated patient cases
| Model          | Role                         |
|----------------|------------------------------|
| `Disease`    | Disease name |
| `Full_case` | Patient case with all symptoms associated with the disease       |
| `80_Percent_Case`  | The patient case with approximately 80% of the symptoms      |
| `50_Percent_Case`   | The patient case with approximately 50% of the symptoms         |
---

#### Created by Maya Kimhi & Mai Werthaim as part of the “Introduction to Natural Language Processing” course

---
