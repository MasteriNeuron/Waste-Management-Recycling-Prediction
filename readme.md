♻️ Waste Management and Recycling Prediction Project
📋 Overview
This project builds a machine learning model to predict the Recycling Rate (%) for waste management in Indian cities using the Waste Management and Recycling in India dataset (2019–2023). The dataset includes features like Waste Generated (Tons/Day), Population Density, City/District, Waste Type, and Disposal Method. The goal is to optimize waste management and reduce landfill dependency through accurate predictions, served via a Flask web app with a user-friendly interface. 🚀
🎯 Objectives

Predict Recycling Rates: Use regression models to forecast Recycling Rate (%) based on waste management features. 📈
Enhance Model Performance: Achieve high R² scores (target ≥ 0.80) using advanced feature engineering and ensemble methods. 🧠
Deploy a Web Interface: Provide a Flask-based interface for users to input data and get predictions. 🌐
Ensure Reproducibility: Serialize models and preprocessing artifacts for consistent training and prediction. 💾

🗂️ Project Structure
├── 📂 datasets/
│   ├── 📂 raw/
│   │   └── Waste_Management_and_Recycling_India.csv
│   ├── 📂 processed/
│   │   ├── target_encodings.pkl
│   │   ├── trained_model.pkl
│   │   ├── scaler.pkl
│   │   ├── selector.pkl
│   │   ├── model_name.pkl
│   │   └── hybrid_model_results.csv
├── 📂 src/
│   ├── 📂 config/
│   │   └── config.yaml
│   ├── 📂 data_processing/
│   │   ├── __init__.py
│   │   └── preprocess.py
│   ├── 📂 pipelines/
│   │   ├── __init__.py
│   │   ├── training_pipelines.py
│   │   ├── prediction_pipelines.py
│   ├── 📂 utils/
│   │   ├── __init__.py
│   │   └── helper.py
│   ├── 📂 logger/
│   │   ├── __init__.py
│   │   └── logs.py
├── 📂 static/
│   └── style.css
├── 📂 templates/
│   ├── index.html
│   ├── result.html
│   ├── error.html
├── 📂 logs/
│   └── pipeline.log
├── app.py
├── requirements.txt

🚀 Getting Started
Prerequisites

Python 3.8+ 🐍
Virtual environment (recommended)
Dependencies listed in requirements.txt

Installation

Clone the repository:git clone <repository-url>
cd waste-management-prediction


Set up a virtual environment:python -m venv venv
.\venv\Scripts\activate  # Windows
source venv/bin/activate  # Linux/Mac


Install dependencies:pip install -r requirements.txt


Place the dataset:
Ensure Waste_Management_and_Recycling_India.csv is in datasets/raw/.



Running the Project

Train the Model:

Run the Flask app and train via the web interface:python app.py


Open http://localhost:5000 and click "Train Model".


Or run the training pipeline standalone:python src/pipelines/training_pipelines.py


Check logs/pipeline.log for training logs and verify artifacts in datasets/processed/:
target_encodings.pkl 🗝️
trained_model.pkl 🤖
scaler.pkl 📏
selector.pkl 🔍
model_name.pkl 🏷️
hybrid_model_results.csv 📊




Make Predictions:

With the Flask app running, go to http://localhost:5000.
Enter values for features (e.g., Waste Generated (Tons/Day), City/District).
Submit to get the predicted Recycling Rate (%). ✅
Check logs/pipeline.log for prediction logs.



🔧 Key Components
1. Data Preprocessing (preprocess.py) 🛠️

Feature Engineering: Creates 37 features from 9 input columns, including:
Coordinate parsing (Landfill_Lat, Landfill_Long)
Ratios (Waste_Per_Capita, Cost_Efficiency)
Target encoding for categorical columns (City/District, Waste Type, Disposal Method)
City/waste type statistics
Log transformations and polynomial features


Data Augmentation: Uses SMOTE-like techniques and noise addition to increase dataset size (from 850 to ~3400 rows).
Artifacts: Saves target_encodings.pkl, scaler.pkl, and selector.pkl for consistent prediction.

2. Training Pipeline (training_pipelines.py) 🏋️

Models: Trains a Stacking Ensemble (RandomForest, ExtraTrees, GradientBoosting, LightGBM, XGBoost with LinearRegression meta-model) and a Deep XGBoost model.
Feature Selection: Uses SelectKBest with mutual_info_regression to select top features.
Outcome: Selects the best model based on R² (e.g., Stacking Ensemble: 0.9725, Deep XGBoost: ~0.7225).
Artifacts: Saves trained_model.pkl, model_name.pkl, and others.

3. Prediction Pipeline (prediction_pipelines.py) 🔮

Process: Applies the same feature engineering as training, scales with scaler.pkl, selects features with selector.pkl, and predicts using the best model.
Fixes: Ensures identical feature set (37 features) and shape as training by using saved artifacts.

4. Flask Web App (app.py, templates/, static/) 🌐

Interface: Uses Tailwind CSS and Bootstrap for a dark-themed, user-friendly form (index.html).
Endpoints:
/: Form to input features.
/train: Triggers training and saves artifacts.
/predict: Returns predicted Recycling Rate (%) in result.html.


Error Handling: Displays errors in error.html if artifacts are missing.

🛑 Challenges and Solutions


Low R² Scores 📉

Issue: Initial models had low performance (e.g., -12% R²).
Solution: Implemented advanced feature engineering, data augmentation, and ensemble models, achieving R² up to 0.9725.



📊 Outcomes

Model Performance:
Stacking Ensemble: R² = 0.9725, high accuracy for complex patterns.
Deep XGBoost: R² ≈ 0.7225, robust fallback.
Dataset Size: Augmented from 850 to ~3400 rows.
Features Used: 37 engineered features, reduced to top features via SelectKBest.


Artifacts: All required files (target_encodings.pkl, trained_model.pkl, etc.) are saved in datasets/processed/.
Web Interface: Fully functional Flask app with a dark-themed, responsive UI for predictions. 🌟
Logs: Detailed logging in logs/pipeline.log for debugging and monitoring. 📜

🔮 Future Improvements

Add Confidence Intervals: Display prediction confidence in result.html. 📈
Feature Importance: Visualize key features in the web interface. 📊
More Data: Incorporate external features (e.g., weather, policies) to boost performance. 🌍
Neural Networks: Explore deep learning for complex interactions. 🧠
CI/CD Integration: Automate model retraining and deployment with MLflow. 🚀

🐛 Debugging Tips

Check Logs: Review logs/pipeline.log for errors in training or prediction.
Verify Artifacts: Ensure datasets/processed/ contains all .pkl files after training.
Clear Cache: Remove .pyc files to avoid outdated code:del src\*.pyc /s

 ** Special Thanks to Mr.Shubham Chaudhary" for contribution in this project.**


📧 Contact
For questions or contributions, reach out via the repository or email(shubham.chaudhary@pw.live). Let’s make waste management smarter! ♻️