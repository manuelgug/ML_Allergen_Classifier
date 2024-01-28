#  ML Allergen Classifier

## Objective
Build a machine learning model to identify protein allergens from amino acid sequences. The purpose is to use annotated genomes to identify organisms likely to contain many allergens, helping individuals, especially the immunocompromised or immunodepressed, make informed decisions about what to eat.

## Building the Allergens and Non-Allergens Sequence Datasets

1. **Gather Allergen Amino Acid Sequences:**
   - Scrape NCBI for amino acid sequences of proteins with the terms "allergen" or "allergenic."

2. **Remove Redundant and Ambiguous Sequences:**
   - Calculate min and max allergen length.
   - Use min and max allergen length to gather non-allergen amino acid sequences from NCBI's protein database.
   - Remove redundant and ambiguous sequences.

3. **Data Mining (Allergens):**
   - Scrape NCBI for amino acid sequences of proteins with the terms "allergen" or "allergenic."

4. **Data Cleaning (Allergens):**
   - Filter out proteins that are not explicitly allergens based on their header.
   - Visually examine the sequence headers.
   - Keep proteins that contain "allergen" or "allergenic" in their header and remove those with the word "precursor."
   - Remove identical proteins with cd-hit.
   - Filter out sequences that contain ambiguities (X, B, Z, J, or O) or Selenocysteine (U).
   - Remove outliers by length.

5. **Data Mining (Non-Allergens):**
   - Scrape NCBI for amino acid sequences (lengths 11 to 460) of complete proteins from SwissProt without "allergen," "allergenic," "partial," or "precursor."

6. **Data Cleaning (Non-Allergens):**
   - Filter out sequences that contain ambiguities (X, B, Z, J, or O) and Selenocysteine (U).

## Feature Extraction
- Sequence length.
- Physicochemical properties.
- Amino acid proportions.

## Exploratory Data Analysis
- Sources of allergens
- Check Occurrences of Each Category
- Analysis by sequence length
- Amino Acid Profile/Abundance of Each Dataset
![organisms](https://github.com/manuelgug/ML_Allergen_Classifier/blob/main/some_images/allergens_organisms.png)
![amino_acids](https://github.com/manuelgug/ML_Allergen_Classifier/blob/main/some_images/seq_composition.png)


## Cleaning
- Importance of Features
- Remove Correlated Features
- Plot PCA of the Final Variables
![corrplot](https://github.com/manuelgug/ML_Allergen_Classifier/blob/main/some_images/corrplot_filtered.png)
![pca](https://github.com/manuelgug/ML_Allergen_Classifier/blob/main/some_images/pca_features.png)

## Model Building
- Preprocessing
- Model Training
- Optimizing for AUC, F1, and Recall

## Model Comparison
![model_comparison](https://github.com/manuelgug/ML_Allergen_Classifier/blob/main/some_images/model_comparison.png)

# Conclusion
- **model_knn & tuned_AUC_model_xgboost perform the best.**
- Since the objective is to identify allergens in genomes to make decisions on what not to eat, higher recall (tuned_AUC_model_xgboost) may be preferred over higher precision (model_knn). Also, tuned_AUC_model_xgboost has a slightly higher AUC, which is to take into account in unbalanced data.

# To Do
1. Test the best models on out-of-sample sequences.
2. Collect genomes from foods and use the models on them.
3. Come up with an "allergen index" for each genome.
