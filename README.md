# BikeCast – Bike Rental Demand Prediction

A machine learning project that analyses historical bike rental data and predicts hourly bike rental demand using weather conditions, temperature, time, and seasonal patterns.

## Project Overview

BikeCast is a machine learning project developed to analyse the factors influencing hourly bicycle rental demand and evaluate regression models for demand prediction.

The project explores historical bike-sharing data, performs data preprocessing and exploratory data analysis, builds and evaluates multiple regression models, and includes a Streamlit application for interactive demand prediction.

The name **BikeCast** combines *Bike* and *Forecast*.

## Project Objectives

- Explore historical bike rental demand through Exploratory Data Analysis (EDA).
- Identify relationships between rental demand, weather, and time-related variables.
- Clean and preprocess the dataset for machine learning.
- Build and evaluate multiple regression models.
- Compare model performance using MAE, RMSE, and R².
- Develop a Streamlit application for interactive demand prediction.

## Dataset

The project uses an hourly bike rental demand dataset.

| Dataset detail | Value |
|---|---:|
| Original observations | 17,379 |
| Original features | 14 |
| Processed observations | 16,872 |
| Training observations | 13,497 |
| Testing observations | 3,375 |
| Processed features | 52 |

### Features Used

| Feature | Description |
|---|---|
| season | Season of the year |
| yr | Year |
| mnth | Month |
| hr | Hour of the day |
| holiday | Whether the day is a holiday |
| weekday | Day of the week |
| workingday | Whether the day is a working day |
| weathersit | Weather condition |
| temp | Normalised temperature |
| hum | Humidity |
| windspeed | Wind speed |
| cnt | Total bike rental count (target variable) |

The `atemp` and `registered` columns were removed during preprocessing.

## Exploratory Data Analysis

Exploratory Data Analysis was performed to understand demand distribution and identify patterns in bike rentals.

### Key Findings

- **Peak demand hour:** 5 PM (17:00).
- **Busiest season:** Fall, followed closely by Summer.
- **Peak month:** June.
- **Weather influence:** Clear weather recorded higher rental demand, while rainy and snowy conditions showed lower demand.
- **Hourly pattern:** Demand showed morning and evening peaks, corresponding approximately to commuting hours.
- **Correlation:** Hour and temperature showed positive relationships with rental demand.

These findings highlight the influence of time, season, and weather on bike rental behaviour.

## Data Preprocessing

The following preprocessing steps were performed:

1. Removed duplicate records.
2. Converted season and weather codes into readable categories.
3. Removed unnecessary columns such as `atemp` and `registered`.
4. Treated zero values in humidity as missing values.
5. Imputed missing humidity values using the median grouped by season and weather condition, with an overall median fallback.
6. Applied IQR-based outlier removal to the target variable `cnt`.
7. Performed one-hot encoding on categorical features using `drop_first=True`.
8. Split the dataset into training and testing sets using an 80:20 ratio and `random_state=42`.
9. Applied StandardScaler to numerical features, fitting it on the training data before transforming the test data.

The resulting processed dataset contained 52 features.

## Machine Learning Models

Seven regression models were implemented and evaluated:

1. Multiple Linear Regression
2. Polynomial Regression
3. Recursive Feature Elimination (RFE) with Linear Regression
4. Ridge Regression
5. Lasso Regression
6. ElasticNet Regression
7. Random Forest Regression

RFE was used to select 35 features for its regression model.

### Model Evaluation

The models were evaluated using three performance metrics:

- **MAE (Mean Absolute Error):** Measures the average absolute prediction error.
- **RMSE (Root Mean Squared Error):** Measures prediction error while giving greater weight to larger errors.
- **R² Score:** Measures how well the model explains variation in the target variable.

The original project evaluation reported the following results:

| Model | RMSE | MAE | R² |
|---|---:|---:|---:|
| Polynomial Regression | 45.96 | 32.09 | 0.91 |
| Random Forest Regression | 46.72 | 30.20 | 0.91 |

Random Forest Regression was selected as the final model based on its lower MAE, while Polynomial Regression achieved a lower RMSE.

## Streamlit Application

BikeCast includes a Streamlit application for interactive bike rental demand prediction.

The application allows users to enter relevant information, including:

- Season
- Year
- Month
- Hour
- Weather condition
- Temperature
- Humidity
- Wind speed
- Working-day and holiday information

The Streamlit application code is included in the original Jupyter Notebook and is also provided separately as `src/app.py`.

### Model and Scaler Files

The trained model (`model.pkl`) and scaler (`scaler.pkl`) are generated when the relevant training and model-saving sections of the notebook are executed successfully.

These generated files are not included as separate pre-trained files in this repository. Users must run the notebook to create them.

### Running the Application

There are two ways to work with the application:

**Option 1: Use the application section in the notebook**

1. Open the notebook in Jupyter Notebook, JupyterLab, or VS Code.
2. Run the required preprocessing, training, and model-saving cells.
3. Execute the Streamlit application section included in the notebook using the appropriate Streamlit execution workflow.

**Option 2: Use the separate `app.py` file**

1. Run the notebook's preprocessing, training, and model-saving sections, without relying on its embedded application section.
2. Ensure the generated `model.pkl` and `scaler.pkl` files are available in the `models/` directory expected by `src/app.py`.
3. Run the separate Streamlit application:

```bash
streamlit run src/app.py
```

The separate application requires the generated model and scaler files to be available at the expected paths. Running the notebook and generating these files is therefore necessary before launching the application.

**Note:** The application workflow is included in the project, but local execution and prediction compatibility still require final verification.

## Technologies Used

- **Programming Language:** Python
- **Data Analysis:** Pandas, NumPy
- **Data Visualisation:** Matplotlib, Seaborn
- **Machine Learning:** Scikit-learn
- **Model Persistence:** Joblib
- **Application Development:** Streamlit
- **Development Environment:** Jupyter Notebook / Google Colab / VS Code

## Project Structure

```text
BikeCast-GitHub/
│
├── data/
│   └── Bike Rental Demand.csv
│
├── notebooks/
│   └── GT_Project_2026_final.ipynb
│
├── src/
│   └── app.py
│
├── models/                  # Generated after running the notebook
│   ├── model.pkl
│   └── scaler.pkl
│
├── requirements.txt
│
└── README.md
```

The `models/` directory and its files are generated locally when the relevant notebook cells are executed. They are not supplied as pre-trained model files in this repository.

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/anushreemadhuambika-code/bikecast-bike-rental-demand-prediction.git BikeCast-GitHub
```

### 2. Navigate to the project folder

```bash
cd BikeCast-GitHub
```

### 3. Create a virtual environment (recommended)

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

### 5. Run the notebook

Open `notebooks/GT_Project_2026_final.ipynb` in Jupyter Notebook, JupyterLab, or VS Code.

Run the notebook cells in sequence to perform preprocessing, train the models, and generate the saved model and scaler files.

### 6. Launch the Streamlit application

After generating the required model and scaler files, run:

```bash
streamlit run src/app.py
```

## Project Limitations and Future Improvements

Potential improvements include:

- Testing chronological train/test splitting to evaluate performance on future time periods.
- Comparing additional machine learning and ensemble models.
- Improving feature engineering using date and time-related variables.
- Evaluating model performance on unseen future data.
- Validating the Streamlit application's preprocessing pipeline against the original training pipeline.
- Deploying the application for public access.

## Project Background

BikeCast was originally developed as an academic machine learning project and as a group of 6 members. This repository organises the original notebook, dataset, and application code into a structured GitHub portfolio project.

The reported evaluation metrics are retained from the original project evaluation and have not yet been independently reproduced during this repository preparation.

## Author

**M. Anushree**

BSc Computer Science with Data Analytics  
Rajagiri College of Social Sciences, Kochi

GitHub: [@anushreemadhuambika-code](https://github.com/anushreemadhuambika-code)

---

*BikeCast – Understanding demand. Predicting mobility.*