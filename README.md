# 🏙️ NYC Airbnb Price Analysis & OLS Regression

<div align="center">

## 📊 Understanding the Drivers of Airbnb Listing Prices in New York City

**An interpretable statistical analysis of Airbnb listing prices using Exploratory Data Analysis, Data Preprocessing, Multicollinearity Diagnostics, and Ordinary Least Squares Regression.**

<br>

**🐍 Python**  •  **📊 Pandas**  •  **📈 Matplotlib**  •  **🎨 Seaborn**  •  **📐 Statsmodels**  •  **🧠 Statistical Modeling**

</div>

---

## 🌟 Project Overview

Airbnb has transformed the short-term rental market by enabling property owners to offer accommodations to travelers worldwide. However, listing prices vary substantially depending on **location, room type, availability, reviews, and host-related characteristics**.

This project investigates the factors associated with Airbnb listing prices in **New York City** using an **interpretable statistical modeling framework**.

Rather than focusing only on prediction accuracy, the project emphasizes:

* 🔎 **Exploratory Data Analysis**
* 🧹 **Data Quality & Cleaning**
* 📊 **Distribution & Outlier Analysis**
* 🔤 **Categorical Variable Encoding**
* 📐 **Multicollinearity Diagnostics**
* 🧮 **Ordinary Least Squares (OLS) Regression**
* 📋 **Statistical Significance**
* 💡 **Business-Oriented Interpretation**

The overall workflow follows the **CRISP-DM methodology** and is designed as a professional end-to-end data science analysis.

---

## 🎯 Problem Statement

Airbnb listing prices show considerable variation across New York City.

The central question of this project is:

> **Which listing characteristics and location-related factors are associated with Airbnb prices, and how effectively can an interpretable OLS regression model explain this variation?**

The analysis aims to identify statistically meaningful relationships while also examining whether the assumptions required for reliable OLS inference are satisfied.

---

## 🚀 Objectives

| #     | Objective                                                               |
| ----- | ----------------------------------------------------------------------- |
| 🔹 01 | Perform comprehensive **Exploratory Data Analysis (EDA)**               |
| 🔹 02 | Identify missing values, duplicates, invalid observations, and outliers |
| 🔹 03 | Understand distributions and relationships between variables            |
| 🔹 04 | Prepare numerical and categorical variables for regression              |
| 🔹 05 | Investigate **multicollinearity using VIF**                             |
| 🔹 06 | Develop an **Ordinary Least Squares (OLS)** regression model            |
| 🔹 07 | Evaluate statistical significance of predictors                         |
| 🔹 08 | Examine important OLS assumptions                                       |
| 🔹 09 | Extract meaningful business insights                                    |
| 🔹 10 | Assess the limitations of the fitted statistical model                  |

These objectives are aligned with the project methodology documented in the notebook.

---

## 📦 Dataset

### 🏠 NYC Airbnb Open Data

The analysis uses Airbnb listings from **New York City, USA**.

| Property             |          Value |
| -------------------- | -------------: |
| 📌 Observations      |     **48,895** |
| 📌 Original Features |         **16** |
| 🎯 Target Variable   |    **`price`** |
| 📍 Geography         |  New York City |
| 📐 Modeling Approach | OLS Regression |

The dataset contains information about listings, hosts, locations, room types, prices, reviews, minimum-stay requirements, and availability.

### 🧾 Original Features

```text
id
name
host_id
host_name
neighbourhood_group
neighbourhood
latitude
longitude
room_type
price
minimum_nights
number_of_reviews
last_review
reviews_per_month
calculated_host_listings_count
availability_365
```

---

## 🔍 Analytical Workflow

The project follows a structured **CRISP-DM-inspired workflow**:

```text
🏢 Business Understanding
          ↓
📂 Data Understanding
          ↓
🔎 Exploratory Data Analysis
          ↓
🧹 Data Cleaning
          ↓
⚙️ Feature Preparation
          ↓
🔤 Categorical Encoding
          ↓
📐 Multicollinearity Diagnostics
          ↓
🧮 OLS Regression
          ↓
🧪 Model Diagnostics
          ↓
📊 Statistical Interpretation
          ↓
💡 Business Insights
          ↓
🏁 Conclusion
```

The notebook explicitly organizes the analysis around Business Understanding, Data Understanding, EDA, Data Cleaning, Feature Engineering, Preprocessing, OLS Modeling, Assumption Testing, Model Evaluation, Business Insights, and Conclusion.

---

# 🔎 Exploratory Data Analysis

## 1️⃣ Data Understanding

Initial inspection covers:

* Dataset dimensions
* Column names
* Data types
* Descriptive statistics
* Unique-value analysis
* Missing-value analysis
* Duplicate detection

The original dataset contains **48,895 rows and 16 columns**.

---

## 2️⃣ Data Quality Assessment

### 🧩 Missing Values

Missingness was investigated across all variables.

Notable missing values include:

* `last_review`
* `reviews_per_month`
* `name`
* `host_name`

`reviews_per_month` and `last_review` each contain **10,052 missing observations**, corresponding to approximately **20.56%** of the dataset.

The analysis treats the missingness of review-related variables carefully rather than blindly replacing values during the EDA stage.

---

## 3️⃣ Duplicate & Validity Checks

The notebook checks:

* 🔁 Duplicate rows
* 💰 Zero prices
* ❌ Negative prices
* 📅 Invalid minimum-night values
* 📆 Invalid availability values
* 📊 Potential numerical outliers

No complete duplicate rows were found.

The analysis also identified **11 listings with a price of zero** and **14 observations with minimum nights above 365**.

---

# 📊 Univariate Analysis

The project examines the distributions of key numerical variables including:

* `price`
* `minimum_nights`
* `number_of_reviews`
* `reviews_per_month`
* `calculated_host_listings_count`
* `availability_365`

Several variables exhibit strong right-skewness and potential outliers, motivating further statistical investigation.

### 📌 Outlier Detection

The **IQR method** is used to identify potential outliers.

| Feature                             | Outliers | Outlier % |
| ----------------------------------- | -------: | --------: |
| 💰 `price`                          |    2,972 |     6.08% |
| 🌙 `minimum_nights`                 |    6,607 |    13.51% |
| ⭐ `number_of_reviews`               |    6,021 |    12.31% |
| 📝 `reviews_per_month`              |    3,312 |     6.77% |
| 🏠 `calculated_host_listings_count` |    7,081 |    14.48% |
| 📅 `availability_365`               |        0 |     0.00% |

## The notebook concludes that many extreme observations may represent legitimate business scenarios such as luxury listings, professional hosts, highly reviewed properties, or long-term rentals rather than simple data-entry errors.

# 📈 Bivariate & Multivariate Analysis

The project investigates relationships between:

* 🏠 Room Type
* 📍 Neighbourhood Group
* 🗺️ Neighbourhood
* 🌐 Latitude & Longitude
* ⭐ Reviews
* 📅 Availability
* 🌙 Minimum Nights
* 💰 Price

The analysis indicates that **location and accommodation type are important dimensions of Airbnb pricing**. Spatial analysis also suggests that geographic variables may contribute explanatory information.

---

# 🔤 Data Preprocessing

Categorical predictors are transformed using **one-hot encoding**.

The model preparation includes:

```python
pd.get_dummies(
    X,
    columns=[
        "neighbourhood_group",
        "neighbourhood",
        "room_type"
    ],
    drop_first=True,
    dtype=int
)
```

This produces a high-dimensional design matrix containing numerical predictors and encoded categorical variables.

---

# 📐 Multicollinearity Analysis

One of the most important statistical diagnostics in this project is **Variance Inflation Factor (VIF)**.

The analysis revealed extremely high VIF values, including **infinite VIFs for multiple neighbourhood dummy variables**.

This indicates strong linear dependency among some encoded predictors and highlights a key challenge when applying OLS to high-cardinality categorical variables.

### ⚠️ Why this matters

High multicollinearity can lead to:

* Unstable coefficient estimates
* Inflated standard errors
* Difficult coefficient interpretation
* Singular or near-singular design matrices
* Reduced reliability of statistical inference

The notebook's OLS output also explicitly warns about strong multicollinearity or a singular design matrix.

---

# 🧮 OLS Regression Model

The project uses:

> **Ordinary Least Squares (OLS) Regression**

OLS was selected because the project prioritizes **interpretability and statistical inference**, allowing the analysis to examine:

* Regression coefficients
* Standard errors
* t-statistics
* p-values
* Confidence intervals
* R²
* Adjusted R²
* F-statistic

The data is divided into:

```text
80% → Training Data
20% → Testing Data
```

using `random_state=42`.

---

# 📊 Model Results

### 🏆 OLS Performance Summary

| Metric           |                 Result |
| ---------------- | ---------------------: |
| 🧮 Model         | Ordinary Least Squares |
| 🎯 Target        |                `price` |
| 📊 Observations  |                 39,116 |
| 📈 R²            |              **0.113** |
| 📈 Adjusted R²   |              **0.108** |
| 🧪 F-statistic   |              **21.70** |
| 📌 Model p-value |              **0.000** |

The fitted model is statistically significant overall, but its **R² of 11.3% indicates limited explanatory power for Airbnb price variation**.

---

# 🔬 Important Statistical Findings

Several variables show statistically significant associations with price in the fitted OLS model.

Examples include:

* 📍 `longitude`
* ⭐ `number_of_reviews`
* 📝 `reviews_per_month`
* 🏠 `calculated_host_listings_count`
* 📅 `availability_365`
* 🗺️ Several neighbourhood indicators
* 🏡 `room_type_Private room`
* 🏡 `room_type_Shared room`

For example, the model estimates a positive coefficient for `availability_365` and negative coefficients for several review-related variables and room-type indicators, conditional on the other variables in the model.

> **Important:** Statistical significance should not automatically be interpreted as causation.

---

# 🧪 Model Diagnostics

The project goes beyond simply fitting the regression model and investigates important OLS assumptions.

### Key diagnostic areas

| Diagnostic           | Purpose                                             |
| -------------------- | --------------------------------------------------- |
| 📐 Linearity         | Checks whether linear relationships are appropriate |
| 🔗 Multicollinearity | Evaluates dependency among predictors               |
| 📊 Homoscedasticity  | Checks whether residual variance is constant        |
| 📈 Normality         | Evaluates residual distribution                     |
| 🔄 Independence      | Checks residual dependence                          |

The notebook identifies significant diagnostic limitations, particularly **multicollinearity and non-normal residuals**.

---

# ⚠️ Model Limitations

A professional analysis should report limitations rather than hiding them.

### 1. Low explanatory power

The model achieves:

```text
R² = 0.113
```

meaning that the current predictors explain only a relatively small portion of the observed variation in Airbnb prices.

### 2. Multicollinearity

Several encoded neighbourhood variables show infinite VIF values, indicating perfect or near-perfect linear dependencies within the design matrix.

### 3. Non-normal residuals

The OLS diagnostics indicate extremely strong skewness and kurtosis in the residual distribution, which limits the reliability of standard OLS inference under the classical normality assumption.

### 4. High-dimensional categorical encoding

Encoding hundreds of neighbourhood categories creates a large feature space and increases the risk of unstable estimates and sparse categories.

---

# 💡 Key Business Perspective

The analysis suggests that Airbnb pricing is not determined by a single factor.

Instead, pricing appears to be associated with a combination of:

```text
📍 Location
   +
🏠 Room Type
   +
📅 Availability
   +
⭐ Review Activity
   +
🏙️ Neighbourhood Characteristics
```

This reinforces the importance of considering **both property characteristics and geographic context** when analyzing Airbnb pricing.

However, because the current OLS model has limited explanatory power and notable multicollinearity issues, its coefficients should be interpreted as **associations rather than causal effects**.

---

# 🛠️ Tech Stack

| Category                   | Tools                |
| -------------------------- | -------------------- |
| 🐍 Programming             | Python               |
| 🗃️ Data Manipulation      | Pandas, NumPy        |
| 📊 Visualization           | Matplotlib, Seaborn  |
| 📐 Statistical Modeling    | Statsmodels          |
| 🤖 ML Utilities            | Scikit-learn         |
| 📓 Environment             | Jupyter Notebook     |
| 📈 Statistical Diagnostics | VIF, OLS Diagnostics |

---

# 📂 Project Structure

```text
NYC-Airbnb-OLS-Regression/
│
├── 📓 Airbnb_Price_Analysis.ipynb
│
├── 📁 data/
│   └── AB_NYC_2019.csv
│
├── 📁 images/
│   ├── price_distribution.png
│   ├── correlation_matrix.png
│   ├── neighbourhood_analysis.png
│   └── model_diagnostics.png
│
├── 📄 README.md
│
└── 📜 LICENSE
```

> Rename the notebook/data/image filenames above to match the exact files you keep in your repository.

---

# ▶️ How to Run

### 1️⃣ Clone the repository

```bash
git clone <YOUR-GITHUB-REPOSITORY-URL>
```

### 2️⃣ Navigate to the project

```bash
cd NYC-Airbnb-OLS-Regression
```

### 3️⃣ Install dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels jupyter
```

### 4️⃣ Launch Jupyter Notebook

```bash
jupyter notebook
```

### 5️⃣ Open the notebook

```text
Airbnb_Price_Analysis.ipynb
```

Run the cells sequentially to reproduce the analysis.

---

# 📌 Reproducibility

The project uses a fixed random seed during the train-test split:

```python
random_state = 42
```

This helps maintain consistent train/test partitions across runs.

---

# 🎓 What This Project Demonstrates

This project demonstrates practical understanding of:

```text
✅ Business Problem Formulation
✅ Data Understanding
✅ Exploratory Data Analysis
✅ Missing-Value Analysis
✅ Data Quality Checks
✅ Outlier Detection
✅ Categorical Encoding
✅ Statistical Modeling
✅ OLS Regression
✅ VIF & Multicollinearity
✅ Statistical Significance
✅ Model Diagnostics
✅ Critical Model Evaluation
✅ Business Interpretation
```

---

# 🔮 Future Improvements

The current analysis provides a strong statistical baseline, but several improvements could make the model more robust:

* 🔧 Reduce high-VIF predictors
* 🧹 Remove zero-variance and redundant dummy variables
* 🏘️ Group rare neighbourhood categories
* 📉 Investigate log transformation of `price`
* 📊 Explore robust standard errors
* 🧪 Perform formal heteroscedasticity tests
* 📐 Improve residual diagnostics
* 🤖 Compare OLS with regularized regression
* 🌲 Benchmark against Random Forest / Gradient Boosting
* 🎯 Compare predictive performance using appropriate regression metrics

These improvements are especially relevant because the current model shows limited explanatory power and substantial multicollinearity.

---

# 🏁 Conclusion

This project presents an **interpretable statistical investigation of NYC Airbnb listing prices** using a structured data science workflow.

The analysis demonstrates that Airbnb prices are associated with **location, room type, availability, review activity, and neighbourhood characteristics**. At the same time, the OLS diagnostics reveal important modeling challenges, particularly **high multicollinearity, non-normal residuals, and relatively low explanatory power**.

Rather than treating these limitations as failures, the project uses them as statistical evidence to understand **where the model works, where it struggles, and how it can be improved**.

> **The key takeaway:**
> A professional data science project is not just about achieving a high score — it is about understanding the data, validating assumptions, interpreting results responsibly, and clearly communicating limitations.

---

## 👩‍💻 Author

<div align="center">

### **Aarti Bisht**

**Data Science Intern | Machine Learning Enthusiast | Data Storyteller 📊**

Building practical, interpretable, and business-focused data science solutions.

⭐ If you found this project useful, consider giving the repository a star!

</div>

---

## 📜 License

This project is intended for **educational, analytical, and portfolio purposes**.

Please review the original dataset's terms and licensing conditions before redistributing the dataset itself.

---

<div align="center">

### ⭐ Explore the Analysis • 📊 Understand the Data • 🧠 Question the Model • 🚀 Improve the Solution

**Made with Python 🐍 & Data 📊**

</div>
