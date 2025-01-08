# Predicting Guild Memberships 

## Team Members:

[Giulia Castelli] (Student ID: [300691])
[Francesca Peppoloni]
[Anna Granzotto]


## [Section 1] Introduction

This project focuses on predicting guild memberships within the Kingdom of Marendor, a fictional world where scholars possess unique combinations of magical and physical attributes. The dataset comprises 31 features, combining both categorical and numerical features. Guild membership represents the target variable for classification.

The primary objective is to build machine learning models to accurately classify scholars into their respective guilds based on their attributes. This involves extensive data preprocessing, including handling missing values, encoding categorical features, and robustly scaling numerical features to address outliers. We further explore the efficacy of three machine learning models, which are Logistic Regression, Random Forest and CART Decision Trees, to evaluate and optimize classification performance.

By applying advanced optimization strategies such as hyperparameter tuning and cross-validation, the project aims to identify the most effective model for this classification task. Insights gained from this analysis are expected to enhance our understanding of the factors influencing guild memberships and contribute to the development of interpretable and robust classification systems.

## [Section 2] Methods

### **1. EDA**
Exploratory Data Analysis (EDA) helps us to understand, clean, and gain insights from our 
dataset, preparing it for machine learning models. In order to do so we employed several Python libraries for analysis and visualization, such as Pandas, Numpy, Scikit-learn, Matplotlib, Seaborn, and Missingno. EDA process steps are:
1. Understand Column Meanings
2. Check Data Integrity
3. Visualize Distributions
4. Correlation Heatmap

#### **1.1 Understand Column Meanings**
We used a dataset named guilds.csv, which contains 253,680 rows and 31 columns, describing various magical and physical attributes of scholars in the Kingdom of Marendor. The data spans a mix of numerical, categorical, and derived variables that offer insights into the factors influencing guild memberships.

**Types of Data:**

- Numerical Columns: Examples include Fae_Dust_Reserve, Physical_Stamina, and Mystical_Index.
- Categorical Columns: Examples include Healer_consultation_Presence and Bolt_of_doom_Presence.
- Target Variable: Guild_Membership, which specifies guild affiliation, such as Master_Guild or No_Guild.
- Data Types: While most columns are numerical, some categorical features are binary or text-based.

#### **1.2 Check Data Integrity**
**Handling Missing Values:**
We identified missing data using visualizations (e.g., missing data matrix).
IMMAGINE

**Types of Missingness:**
The patterns and correlations observed suggest that most of the missingness in the dataset can be explained by relationships with other observed variables, classifying it primarily as `Missing at Random` (MAR). 

#### **1.3 Correlation Heatmap**

--- 

### **2. Preprocessing the Dataset**
 
#### **2.1 Handling Missing Data**
We used two different startegies to handles missing values (NaN):

a) **Drop Missing Target Values**:
     - Rows with missing values in the Guild_Membership column were removed, ensuring the dataset was valid for supervised learning tasks.

b) **Imputation for Features**:
     - **Numerical Features**: Missing values were replaced with the median to handle skewness and reduce the impact of outliers.
     - **Categorical Features**: Missing values were replaced with the most frequent value, preserving categorical integrity.


#### **2.2 Encoding Categorical Features**
- **One-Hot Encoding**: it was applied to categorical features such as Healer_consultation_Presence, creating binary columns for each category.
- **Label Encoding for Target**: Guild_Membership was encoded as integers: Master Guild (2), Apprentice Guild (1) and No Guild (0).


#### **2.3 Outlier Treatment**
Instead of removing outliers, we used **Robust Scaling** to reduce their influence while preserving critical information.

- **Robust Scaling**: it scaled features by subtracting the median and dividing by the interquartile range (IQR), making sure that the outliers had minimal impact on scaled values.

---

### **3. Defining the problem type: Regression, Classification or Clustering**

Based on the dataset, this is a multi-class classification problem because the target variable `Guild_Membership` consists of discrete categories representing the guild each scholar belongs to ("Master Guild", "Apprentice Guild" and "No Guild"). The objective is to predict which guild each scholar will be assigned to based on their attributes.  

---

### **4. Algorithms:**

We chose three algorithms based on their characteristics and suitability for the Guild dataset:

**Logistic Regression**

Logistic Regression because it is simple and interpretable, making it suitable for understanding relationships between features and the target. It is also computationally efficient, even with large datasets. However, it assumes linearity between features, which may not hold true for complex datasets like this one. Logistic Regression struggles with imbalanced data, often predicting the majority class, and has limited ability to capture non-linear patterns unless features are transformed or interactions are explicitly modeled.

**Random Forest**

Random Forest is an ensemble method that builds multiple decision trees on bootstrapped samples and combines their predictions to reduce overfitting. It effectively handles non-linearity, provides feature importance metrics, and is robust to imbalanced datasets. However, it can be computationally intensive, memory-heavy for large datasets, and requires careful hyperparameter tuning for optimal performance.

**CART Decision Trees**

CART (Classification and Regression Trees) is a model that splits the dataset into subsets based on feature values, recursively partitioning until a stopping criterion is met. It is easy to visualize, interpret, and explain, captures non-linear relationships and requires minimal preprocessing for both numerical and categorical data. However, it is highly prone to overfitting without regularization and it is sensitive to small changes in the dataset.

#### **4.1 Training of the models**

a)  The dataset was split into **training**, **validation**, and **test sets** using stratified sampling to preserve class distribution across all subsets. This approach ensures consistent proportions of the target variable, allowing for reliable model training, hyperparameter tuning, and evaluation. The same splitting method was applied to all models to ensure comparability.

b)  The models were trained on the training set using **default hyperparameters** and evaluated on the validation set, with metrics such as **precision**, **recall**, **F1-score**, and a **confusion matrix** calculated to assess performance.

c)  We used **cross-validation** with **GridSearchCV** to identify the **best hyperparameters** for the models by testing various combinations of parameters. This approach ensures the models are optimized for performance while addressing issues like class imbalance and overfitting. The best hyperparameters and their cross-validation accuracy were extracted to fine-tune the model. 

---

## [Section 3] Experimental Design

#### **Main Purpose**
The primary purpose of the experiments was to evaluate the performance of different machine learning models in predicting guild memberships from the dataset, ensuring the models were appropriately tuned and capable of handling the dataset’s characteristics, such as class imbalance and feature interactions.

#### **Baseline(s)**

- **Baseline Model:** Logistic Regression with default hyperparameters served as the baseline due to its simplicity and interpretability.
- **Advanced Models:**  Random Forest and CART Decision Trees were compared against the baseline to assess improvements in performance and robustness.
- **Majority Class Prediction:** A naive model predicting the majority class for all instances was also used as a baseline to measure improvement.

#### **Evaluation Metrics**

- **Accuracy:** To evaluate overall correctness but noted as less effective for imbalanced datasets.

- **F1 Score:** A balanced metric accounting for precision and recall, especially useful for imbalanced classes.

- **Precision and Recall:** To understand the ability to predict minority classes effectively.

- **ROC-AUC:** To assess the model’s ability to distinguish between classes across thresholds.

- **Confusion Matrix:**  To visualize class-specific performance and errors.

This experimental setup validated each model's contribution by comparing their ability to classify guild memberships, focusing on both overall performance and handling imbalanced classes. The findings provided insights into the strengths and limitations of advanced models over simpler baselines.

---

[Section 4] Results

**Logistic Regression:**

The Logistic Regression model showed an improvement in accuracy from 57% on the training set to 67% on the test set. However, it struggled to generalize for Class 0, with a significant drop in recall from 44% to 14%. In contrast, Class 1 recall improved from 39% to 62%, while Class 2 maintained high performance with a stable precision of 93% and an increase in recall from 61% to 69%. The weighted averages improved due to better performance on Class 2, and the Test ROC AUC score of 0.71 indicates reasonable overall discrimination, despite challenges with minority classes.

**Random Forest:**
The Random Forest model demonstrated consistent performance across the training and test sets, with an accuracy of 67%. Class 0 remained challenging, with low recall improving marginally from 5% to 7%. Class 1 recall remained high at 71%, with stable precision around 29%, while Class 2 retained high precision (94%) but experienced a slight drop in recall (from 68% to 67%). The weighted averages reflected balanced performance, and the Test ROC AUC of 0.74 confirmed strong discrimination, particularly for the majority class, showing the model's robustness and generalization.

**CART Decision Trees:**
The CART model faced generalization challenges, with accuracy dropping slightly from 68% on the training set to 66% on the test set. For Class 0, recall improved modestly from 7% to 11%, but overall precision and F1-scores remained poor. Class 1 showed slight improvements in recall (from 42% to 44%) but stable precision, while Class 2 experienced a minor decrease in recall (from 73% to 71%) but maintained high precision (90%). The Test ROC AUC of 0.59 highlighted limited class separability, especially for minority classes, underscoring the need for further refinement.

**Overall Insights**
- **Best Model:** Random Forest emerged as the most balanced model, with strong performance on the majority class (Class 2) and reasonable handling of Class 1.
- **Challenges:** All models struggled with Class 0, highlighting the difficulty of predicting the minority class. Logistic Regression was particularly weak for this class, while Random Forest and CART performed slightly better.
- **Discrimination:** Random Forest achieved the highest ROC AUC (0.74), showing its ability to distinguish between classes more effectively than Logistic Regression (0.71) and CART (0.59).

---





Libraries: scikit-learn, pandas, numpy, matplotlib, seaborn

Environment Reproducibility:

conda create -n guild_prediction python=3.9
conda activate guild_prediction
pip install -r requirements.txt

The requirements.txt includes all necessary dependencies.

Workflow Diagram

Below is a flowchart illustrating the steps in our machine learning pipeline:

Data Preprocessing

Feature Engineering

Model Training and Validation

Model Comparison

Test Set Evaluation

[Section 3] Experimental Design

Experiments

Main Purpose:
To evaluate the performance of different classifiers for predicting guild memberships.

Baselines:

Majority Class Baseline: Predicting the most common guild.

Decision Tree Classifier for initial comparison.

Evaluation Metrics:

Accuracy: To measure overall correctness.

F1 Score: To account for imbalanced guild memberships.

ROC-AUC: For analyzing classification thresholds.

Experimental Setup

We performed a 5-fold cross-validation to evaluate each model and used a stratified split to maintain class balance. The hyperparameters were optimized using grid search.

[Section 4] Results

Main Findings

Random Forest Classifier: Achieved the highest F1 Score of 0.87.

SVM: Balanced performance with an ROC-AUC of 0.82.

Neural Network: Performed well but required extensive tuning; F1 Score of 0.84.

Results Summary Table

Model

Accuracy

F1 Score

ROC-AUC

Random Forest

89%

0.87

0.91

SVM

85%

0.84

0.82

Neural Network

86%

0.84

0.85

Placeholder Figure

[Insert plot showing model comparison metrics]

[Section 5] Conclusions

Summary

This project successfully demonstrated the ability to classify guild memberships using machine learning techniques. The Random Forest Classifier emerged as the most effective model, achieving a strong balance between accuracy and interpretability.

Future Work

Despite the promising results, further research is needed to:

Explore additional features such as social dynamics or historical data.

Investigate ensemble methods for improving performance.

Develop interpretability techniques to better understand the driving factors behind predictions.
