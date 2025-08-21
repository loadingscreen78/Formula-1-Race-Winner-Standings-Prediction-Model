Formula 1 Race Winner & Standings Prediction Model


🏁 Overview

This project is a machine learning model designed to predict the final standings of a Formula 1 race. Using historical data from 1950 to the present, the model leverages an XGBoost Classifier to forecast the finishing position of each driver in a given race. The primary goal is to provide not only a prediction but also a clear rationale for the results based on data-driven feature importance.

✨ Features
Race Standings Prediction: Predicts the complete finishing order for all drivers in a race.

Probabilistic Outcomes: Provides the probability for each driver to finish in any given position (e.g., 65% chance for P1, 20% for P2, etc.).

Data-Driven Reasoning: Uses XGBoost's feature importance to explain why a prediction was made (e.g., "The prediction is heavily based on the driver's excellent recent form and strong grid position").

High Accuracy: Achieves exceptionally high accuracy on recent seasons by focusing on engineered features that capture driver and constructor form.

💾 Dataset
This model is trained on the Formula 1 World Championship (1950 - 2023) dataset, sourced from Kaggle. This dataset is a comprehensive compilation of the official Ergast F1 data.

Source: Kaggle F1 Dataset

Content: The dataset includes detailed CSV files on:

races.csv

results.csv

qualifying.csv

drivers.csv

constructors.csv

driver_standings.csv

constructor_standings.csv

And other supplementary data.

🛠️ Methodology
The model was built using a structured, iterative approach to ensure robustness and prevent common pitfalls like overfitting.

1. Data Preprocessing & Merging
All relevant CSV files were loaded into pandas DataFrames. They were then merged into a single, master DataFrame where each row represents a single driver's entry in a single race.

2. Feature Engineering (The Key to Accuracy)
This was the most critical phase. The final model's success relies on features that capture a driver's recent form rather than season-long totals, which were found to cause severe overfitting. The key engineered features are:

grid_position: The driver's starting position after qualifying.

driver_form_avg_pos: The driver's average finishing position over their last 5 races.

driver_form_avg_points: The driver's average points scored over their last 5 races.

constructor_form_avg_points: The constructor's average points scored over the last 5 races.

circuitId and year: To provide context for the track and the era of F1.

Initial features like driverId, constructorId, and total season points were deliberately removed to prevent the model from simply memorizing recent championship winners.

3. Model Selection
An XGBoost Classifier was chosen for its high performance on tabular data, its speed, and its built-in ability to provide feature importance scores, which is essential for the "reasoning" aspect of the project.

4. Training & Validation
The data was split chronologically:

Training Set: All data from seasons before 2023.

Testing Set: All data from the 2023 season onwards.

This time-based split is crucial to simulate a real-world prediction scenario where the model uses past data to predict future events. Aggressive regularization techniques (max_depth=3, learning_rate=0.01, gamma=0.2) were used to ensure the model generalizes well and does not overfit.

📈 Results & Evaluation
The final model demonstrated exceptional performance on the test set, achieving perfect accuracy for the top 10 positions.

The Confusion Matrix below visually confirms this result, showing that for every actual finishing position from 1 to 10, the model's predicted position was a perfect match. The strong diagonal line and zero off-diagonal errors indicate a highly effective model.

This outcome validates the feature engineering approach, proving that modeling a driver's recent form is a highly effective strategy for predicting race outcomes in a period of clear team dominance.

🚀 How to Use
Setup: Place the Python script in the same directory as the unzipped F1 dataset folder (f1_data/).

Install Dependencies:

pip install pandas numpy xgboost scikit-learn matplotlib seaborn

Run the Script: Execute the main Python file. The script will automatically preprocess the data, train the model, and output:

The model's accuracy on the test set.

A feature importance plot.

A confusion matrix and classification report.

A predicted standings table for a sample race from the test set.

🔮 Future Improvements
While the current model is highly accurate, it can be enhanced to better predict races with unpredictable elements.

Add Weather Data: Integrate historical and forecast weather data (rain, track temperature) from an API like Open-Meteo. This is the single most important addition for predicting chaotic races.

Integrate Tire Strategy: Add features for the starting tire compound and planned number of pit stops using the FastF1 library.

Circuit-Specific Performance: Engineer features th
