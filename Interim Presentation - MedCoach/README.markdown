#MedCoach EDA & Baseline with Patient Case Generation

This repository contains a Jupyter Notebook (`EDA_and_Baseline.ipynb`) that performs Exploratory Data Analysis (EDA) and establishes a baseline for disease diagnosis using patient case generation and evaluation with PubMedBERT.

## Project Overview

The project focuses on:
1. **Exploratory Data Analysis (EDA)**: Analyzing a dataset of diseases and symptoms to understand distributions and patterns.
2. **Patient Case Generation**: Using the Ollama framework with `medllama2` (or `llama3.2:3b` as a fallback) to generate realistic patient cases based on disease symptoms.
3. **Baseline Model Evaluation**: Training and evaluating a PubMedBERT model (`microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract`) on generated patient cases to predict diseases at different symptom coverage levels (50%, 80%, and 100%).

## Prerequisites

To run the notebook, ensure you have the following installed:
- Python 3.8+
- Jupyter Notebook or JupyterLab
- Required Python packages (install via `pip`):
  ```bash
  pip install pandas numpy scikit-learn transformers datasets evaluate torch subprocess
  ```
- Ollama framework for local LLM inference:
  ```bash
  curl -fsSL https://ollama.com/install.sh | bash
  ```
- Google Colab (optional, if running in a cloud environment)

## Dataset

The input dataset (`df`) is expected to be a DataFrame with:
- Columns for symptoms (binary indicators, e.g., `symptom_fever`, `symptom_cough`).
- A `prognosis` column indicating the disease label.
- Optional `ones_count` column for symptom counts.

The notebook samples 100 random cases for processing (`df_sample`).

## Usage

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/disease-diagnosis-baseline.git
   cd disease-diagnosis-baseline
   ```

2. **Set Up Environment**:
   - Install dependencies listed in the Prerequisites section.
   - Ensure Ollama is installed and running (`ollama serve`).

3. **Run the Notebook**:
   - Open `EDA_and_Baseline.ipynb` in Jupyter Notebook or JupyterLab.
   - Execute the cells sequentially to:
     - Perform EDA on the dataset.
     - Install and configure Ollama with `medllama2` or `llama3.2:3b`.
     - Generate patient cases for 100 diseases with full, 80%, and 50% symptom coverage.
     - Save the generated cases to `patient_cases.csv`.
     - Train and evaluate PubMedBERT on the generated cases for three stages (50%, 80%, 100% symptom coverage).

4. **Outputs**:
   - `patient_cases.csv`: Contains generated patient cases with columns `Disease`, `Full_Case`, `80_Percent_Case`, and `50_Percent_Case`.
   - PubMedBERT evaluation results printed in the notebook, showing accuracy for each stage.

## Code Structure

- **EDA Section**:
  - Analyzes symptom distributions and disease prevalence in the dataset.
  - Visualizations (e.g., histograms, heatmaps) are included (partially visible in the provided document due to truncation).

- **Patient Case Generation**:
  - `install_ollama()`: Installs Ollama and pulls the `medllama2` model (falls back to `llama3.2:3b` if needed).
  - `call_ollama()`: Generates patient cases for a given disease and symptom list, returning full, 80%, and 50% symptom cases.
  - `process_dataset()`: Extracts diseases and symptoms from the DataFrame.
  - `generate_patient_cases()`: Orchestrates case generation and saves results to a DataFrame.

- **Baseline Evaluation**:
  - Uses PubMedBERT for sequence classification.
  - `prepare_dataset()`: Splits data into training and validation sets.
  - `tokenize()`: Tokenizes text inputs for PubMedBERT.
  - `train_on()`: Trains and evaluates the model for each symptom coverage stage.
  - Training configuration uses Hugging Face `Trainer` with 3 epochs, a learning rate of 2e-5, and accuracy as the evaluation metric.

## Results

The baseline evaluation yields the following accuracies:
- **Stage 1 (50% Symptom Coverage)**: 0.1820
- **Stage 2 (80% Symptom Coverage)**: 0.4932
- **Stage 3 (100% Symptom Coverage)**: 0.7867

These results indicate that PubMedBERT performs better with more complete symptom information, as expected.

## Limitations

- The dataset size (100 samples) may limit model generalization.
- Ollama model availability (`medllama2`) depends on successful installation; fallback to `llama3.2:3b` may affect case quality.
- PubMedBERT training is performed on a small dataset, which may lead to overfitting.

## Future Improvements

- Expand the dataset size for better model training and evaluation.
- Incorporate additional LLMs for case generation to compare quality.
- Fine-tune PubMedBERT hyperparameters or explore other biomedical models (e.g., BioBERT).
- Add cross-validation to ensure robust evaluation.

## Contributing

Contributions are welcome! Please:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit changes (`git commit -m 'Add your feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a Pull Request.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Contact

For questions or issues, please open an issue on GitHub or contact [your-email@example.com].
