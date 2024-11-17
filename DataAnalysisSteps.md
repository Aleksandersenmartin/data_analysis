# Step 1 

## 1. Understand the Dataset 
Before diving into analysis, take time to understand the data's context and structure: 
	- Understand the business context: what is the dataset about? What are the objectives of our analysis? 
	- Understand the Data source: where did the data come from? Is it reliable and complete? 
	- Understand key attributes: identify the key variable and their roles (e.g., target variable, predictors) 

Check list: 
	What question do you need to answer 
	What are the important columns/variables? 
	Are there any relationships between the variables? 
	
## 2. Inspect the data
Stat by exploring the structure and content of the dataset: 
	- Use methods like head(), info(), and describe() in python or R. 
	- Identify column data types, missing values, and unique value counts .

## 3. Check for Missing values
Identify and handle missing data appropriatley: 

	- Stategies: 
		○ Drop /rows/columns if the proportion of missing data is to high 
		○ Impute missing values: 
			§ Mean/median for numerical data. 
			§ Mode for Categorical data. 
			§ Advanced teqhniques (e.g., KNN inputation) for complex scenarios
			
## 4. Check for duplicates
Identify and remove duplicate rows to aboid bias in analysis 
- Check for duplicates
print(df.duplicated().sum())

-Drop duplicate rows
df = df.drop_duplicates()


## 5. Handle outliers 
Detect and adress outliers to prevent them from skewing you analysis: 
	- Use visualization techniques like box plots to identify outliers. 
	- Handle outliers by: 
		○ Removing them (if clearly erroneous)
		○ Capping them (setting them to threshold)
		○ Transforming data 

## 6. Standardize Column Names 
Ensure column names are consistent, readable, and follow a standard convention (e.g., lowercase with underscores :

df.columns = df.columns.str.lower().str.replace(' ', '_')


## 7. Correct Data Types 
Ensure each column has the correct data type: 
	- Convert strings to datetime for time-based data 
	- Convert categorical variables to category 

- Convert to datetime
df['date_column'] = pd.to_datetime(df['date_column'])

- Convert to categorical
df['category_column'] = df['category_column'].astype('category')


## 8. Handle Categorical Variables
	- Encode categorical variables for analysis. 
		○ One-hot encoding for machine learning models. 
		○ Label encoding for ordinal variables. 

- One-hot encoding
df = pd.get_dummies(df, columns=['categorical_column'])

- Label encoding
from sklearn.preprocessing import LabelEncoder
encoder = LabelEncoder()
df['ordinal_column'] = encoder.fit_transform(df['ordinal_column'])

## 9. Scale/standardize Numerical Data 
Standardize or normalize numerical data to improve the performance of models sensitice to scale (e.g., logistic regression, sVM) 

from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
df['scaled_column'] = scaler.fit_transform(df[['numerical_column']])

## 10. Visualize the data 
Use exploratory data analysis (EDA) techniques to understand the dataset better: 
 - Visualize distribution of numerical columns 
	- Plot relationships between variables 
	- Check for correlations. 

## 11. Document your process
Maintain a log of the changes you make to the dataset, including: 
	- Columns dropped or imputed.
	- Values replaced or scaled
	- Assumption made during data cleaning 

## 12. Save the cleaned dataset 
Save the processed dataset for further analysis or modelling 

