# ML-EDA
# GenZ Dating App Dataset

## Overview
This dataset contains information related to user activities, preferences, and interactions on a GenZ-focused dating app. It includes categorical, numerical, and timestamp data, which can be used for user behavior analysis, trend predictions, and recommendation system development.

## Data Dictionary
Below is a table describing the dataset's columns, including their data types and descriptions.

| Column Name        | Data Type  | Description |
|--------------------|-----------|-------------|
| `user_id`         | Integer   | Unique identifier for each user. |
| `age`             | Integer   | Age of the user. |
| `gender`          | Object    | Gender of the user (e.g., Male, Female, Non-binary). |
| `location`        | Object    | User's geographical location. |
| `sign_up_date`    | DateTime  | The date the user registered on the platform. |
| `last_active`     | DateTime  | The last recorded activity timestamp of the user. |
| `subscription`    | Object    | Type of subscription plan (e.g., Free, Premium). |
| `messages_sent`   | Integer   | Total number of messages sent by the user. |
| `matches_count`   | Integer   | Total number of matches made by the user. |
| `profile_complete`| Float     | Percentage of profile completion (0-100). |

## Data Cleaning Steps
The following cleaning steps have been performed:

### 1. Checked for Duplicate Rows
- Used `.duplicated().sum()` to check for duplicate entries.
- If duplicates exist, they can be removed using `data.drop_duplicates(inplace=True)`.

### 2. Identified Inconsistencies in Categorical Data
- Retrieved unique values using `data[column].unique()` to check for spelling variations, case sensitivity, and whitespace inconsistencies.
- Standardized categorical values by converting them to lowercase and stripping extra spaces:  
  ```python
  data['gender'] = data['gender'].str.lower().str.strip()
  ```

### 3. Handled Missing Values
- Checked for missing values using `data.isnull().sum()`.
- Identified columns with more than 50% missing values and dropped them:
  ```python
  threshold = 0.5 * len(data)
  cols_to_drop = data.columns[data.isnull().sum() > threshold]
  data.drop(columns=cols_to_drop, inplace=True)
  ```
- Filled missing categorical values with mode and numerical values with median where appropriate.

### 4. Tracked Dataset Changes Over Time
- Implemented a dataset hash check to track changes:
  ```python
  import hashlib
  def get_data_hash(df):
      return hashlib.md5(pd.util.hash_pandas_object(df, index=True).values).hexdigest()
  ```
- This helps in identifying updates and ensuring version control.

## How to Use This Dataset
1. Clone this repository:
   ```sh
   git clone https://github.com/your-repo/genz-dating-app-data.git
   ```
2. Load the dataset in Python:
   ```python
   import pandas as pd
   data = pd.read_csv("GenZ_DatingApp_Data.csv")
   ```
3. Explore the dataset:
   ```python
   print(data.head())
   print(data.info())
   ```


