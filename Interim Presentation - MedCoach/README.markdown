# MedCoach EDA & Baseline

## Notebook Overview

The Notebook focuses on:
1. **Exploratory Data Analysis (EDA)**: Analyzing a dataset of diseases and symptoms to understand distributions and patterns.
2. **Patient Case Generation**: Using the Ollama framework with `medllama2` to generate realistic patient cases based on disease symptoms.
3. **Baseline Model Evaluation**: Training and evaluating a PubMedBERT model (`microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract`) on generated patient cases to predict diseases at different symptom coverage levels (50%, 80%, and 100%).


## Dataset - [Diseases and their Symptoms](https://www.kaggle.com/datasets/shobhit043/diseases-and-their-symptoms)

The input dataset (`df`) is expected to be a DataFrame with:
- Columns for symptoms (binary indicators, e.g., `symptom_fever`, `symptom_cough`).
- A `prognosis` column indicating the disease label.

The notebook samples 100 random cases for processing (`df_sample`).

## Code Structure**

### EDA
- Removed duplicate rows and constant columns.
- Added a `ones_count` column indicating the number of symptoms per case.
- Grouped data by disease (`prognosis`) to assess sample distribution.
- Filtered to retain cases with ≥ 4 symptoms.
- Removed columns with a single unique value

  ### Baseline
  
  - Random Sampling: Selected 100 random examples from the filtered dataset.

- **Patient Case Generation**:
  Used the **MedLLaMA2** model via **Ollama** to generate 3 case variants for each patient case.
  - `install_ollama()`: Installs Ollama and pulls the `medllama2` model (falls back to `llama3.2:3b` if needed).
  - `call_ollama()`: Generates patient cases for a given disease and symptom list, returning full, 80%, and 50% symptom cases.
  - `process_dataset()`: Extracts diseases and symptoms from the DataFrame.
  - `generate_patient_cases()`: Orchestrates case generation and saves results to a DataFrame.

- **Baseline Evaluation**:
  Used PubMedBERT for sequence classification.
  - `prepare_dataset()`: Splits data into training and validation sets.
  - `tokenize()`: Tokenizes text inputs for PubMedBERT.
  - `train_on()`: Trains and evaluates the model for each symptom coverage stage.
  - Training configuration uses Hugging Face `Trainer` with 3 epochs, a learning rate of 2e-5, and accuracy as the evaluation metric.

### Results

The baseline evaluation yields the following accuracies:

| Case Completeness | Accuracy (approx.) |
|-------------------|--------------------|
| 50%               | 0.1820             |
| 80%               | 0.4932             |
| 100%              | 0.7867             |

These results indicate that PubMedBERT performs better with more complete symptom information, as expected.

## Outputs:
   - `Generated patient cases.csv`: Contains generated patient cases with columns `Disease`, `Full_Case`, `80_Percent_Case`, and `50_Percent_Case`.
| Column          | Column Description          |
|----------------|------------------------------|
| `Disease`    | Disease name |
| `Full_case` | Patient case with all symptoms associated with the disease    |
| `80_Percent_Case`  | The patient case with approximately 80% of the symptoms|
| `50_Percent_Case`   | The patient case with approximately 50% of the symptoms |
   - PubMedBERT evaluation results printed in the notebook, showing accuracy for each stage.


## Future Improvements




