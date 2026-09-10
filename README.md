# Material_info_final_project

Project files
data_generation.ipynb

This notebook contains the data-generation and cleaning workflow. 
It is as follows:

Loads the Cu and Cu–Pt structures from the original database.
Processes the supplied Pt structures.
Runs the atomate2 elastic workflow using the MatterSim potential.
Extracts k_reuss, k_voigt and k_vrh.
Clear dataset as asked and produces the cleaned database used for machine learning.

Initially, the Alexandria OPTIMADE service did not return the required Pt structures. Therefore, the supplied omitted_20Pt_structures.json file was used as the source of the 20 Pt structures. Although the Alexandria query worked later, the supplied Pt dataset was retained to maintain consistency throughout the project.

Model.ipynb

This notebook contains the featurization, model training and evaluation. It:

Generates compositional and structural descriptors using matminer.
Adds custom ChemEnv local-environment features.
Trains Random Forest and Gradient Boosting regressors.
Applies Mutual Information and model-based feature selection.
Evaluates the four model configurations using nested 5-fold outer and 5-fold inner cross-validation.
Stores model metrics, optimal hyperparameters, selected features, feature importances and outer-fold predictions.
Compares the model performance and feature-selection methods.