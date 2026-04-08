# Project README: Data Acquisition and Labeling for Safety/Sensitivity Classification

This notebook focuses on acquiring, processing, and merging various datasets to create a comprehensive collection of prompts categorized by their safety and sensitivity levels. The resulting datasets can be used for training and evaluating models for content moderation, safety classification, or detecting harmful content.

## Data Sources
The following datasets are acquired and processed within this notebook:

*   **ALERT Dataset (`Babelscape/ALERT`)**: Contains adversarial prompts and benign prompts, categorized by attack type and general content.
    *   `alert_adversarial` split: Processed to extract prompts and remove instruction prefixes.
    *   `alert` split: Processed to extract prompts and remove instruction prefixes.
*   **ActorAttack Dataset**: Obtained from a GitHub repository, containing prompts related to harmful goals.
    *   `circuit_breaker_train.csv`: Prompts are extracted from the 'Goal' column.
    *   `harmbench.csv`: Prompts are extracted from the 'Goal' column.
*   **SG-Bench Dataset**: Obtained from a GitHub repository, containing various types of prompts.
    *   `judge_test.json`: Prompts are extracted from the 'query' column.
*   **SaladBench Dataset**: Obtained from a GitHub repository, featuring multiple choice and attack-enhanced prompts.
    *   `mcq_set.json`: Prompts are extracted from the 'query' column.
    *   `attack_enhanced_set.json`: Prompts are extracted from the 'query' column.
    *   `base_set.json`: Prompts are extracted from the 'query' column.

## Data Preparation

The notebook performs the following key data preparation steps:

1.  **Data Loading**: Datasets are loaded from their respective sources (Hugging Face datasets, CSV files from cloned GitHub repositories).
2.  **Text Extraction and Cleaning**: Relevant prompt text is extracted from each dataset. Instruction prefixes (e.g., `### Instruction:`, `### Response:`) are removed to isolate the core prompt content.
3.  **Labeling**: The `safe_dataset` is explicitly labeled 'safe', `unsafe_dataset` is labeled 'unsafe', and `sensitive_dataset` is labeled 'sensitive'. Numeric labels (0, 1, 2) are also assigned for model training.
4.  **Merging Datasets**: All processed datasets are concatenated into a single DataFrame (`merged_df`).
5.  **Sampling (for `the300_dataset.csv`)**: A smaller, balanced dataset (`the300_dataset.csv`) is created by sampling 100 entries each from `safe`, `unsafe`, and `sensitive` categories.

## Output Files

The notebook generates the following CSV files:

*   `the_dataset.csv`: A merged dataset containing prompts from all sources with their categorical labels ('safe', 'unsafe', 'sensitive').
*   `the88K_dataset.csv`: Similar to `the_dataset.csv` but includes a numeric `label_number` column.
*   `the300_dataset.csv`: A smaller, balanced dataset containing 100 samples from 'safe', 'unsafe', and 'sensitive' categories, with both categorical and numeric labels.