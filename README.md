# 🍔 FoodHub Order (EDA) Project

## 📌 Project Overview

This project performs an Exploratory Data Analysis (EDA) on the `foodhub_order.csv` dataset using Python. The analysis focuses on understanding customer ordering behavior, restaurant popularity, cuisine trends, ratings, preparation time, delivery performance, and sales insights.

The notebook used in this project is:

* `foodhub_order.ipynb`

The project highlights important data analysis workflows and business-oriented analytical techniques, including:

* 📥 Data loading and inspection
* 🧹 Data cleaning and preprocessing
* ❓ Handling missing values
* 🔍 Exploratory Data Analysis (EDA)
* 📊 Data visualization and trend analysis
* 📈 Statistical summaries
* 💡 Business insight generation

---

# 📂 Dataset Information

## 🗂️ Dataset Name

`foodhub_order.csv`

## 📝 Dataset Description

The dataset contains food delivery order information from different restaurants. It includes customer ratings, cuisine types, order costs, preparation time, delivery time, and day-wise ordering information.

---

# 🛠️ Technologies Used

The following technologies and libraries are used in this project:

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Jupyter Notebook

---

# 📁 Project Structure

```bash
FoodHub-Order-Analysis/
│
├── foodhub_order.ipynb              # Main Jupyter Notebook
├── foodhub_order.csv                # Dataset file
├── EDA Report of FoodHub Order.pdf  # Project documentation
```

---

# ⚙️ Installation Guide

## 1️⃣ Install Python

Download and install Python from:

* 🐍 ❖Python Official Website❖[https://www.python.org/downloads/](https://www.python.org/downloads/)❖

Make sure Python is added to PATH during installation.

---

## 2️⃣ Install Required Libraries

Open terminal or command prompt and run:

```bash
pip install numpy pandas matplotlib seaborn notebook
```

---

## 3️⃣ Open Jupyter Notebook

Run the following command:

```bash
jupyter notebook
```

Then open:

```bash
foodhub_order.ipynb
```

---

# ▶️ How to Run the Project

## 📥 Clone the Repository

```bash
git clone https://github.com/jesh-rijal/FoodHub-Orders-EDA.git
```

## 📂 Move into Project Folder

```bash
cd FoodHub-Orders-EDA
```

## 🚀 Run the Notebook

```bash
jupyter notebook
```

Open the notebook and run all cells sequentially.

---

# 📖 Detailed Notebook Explanation

# 1️⃣ Importing Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

## 📘 Explanation

### 🔢 NumPy

Used for numerical operations and array handling.

### 🐼 Pandas

Used for data manipulation and analysis.

### 📊 Matplotlib

Used for creating visualizations and charts.

### 🎨 Seaborn

Used for advanced statistical visualizations.

---

# 2️⃣ Loading the Dataset

```python
dataset = pd.read_csv('foodhub_order.csv')
dataset.head()
```

## 📘 Explanation

* `pd.read_csv()` loads the CSV dataset.
* `dataset.head()` displays the first 5 rows.

Purpose:

* Verify dataset loading.
* Understand dataset structure.
* Check column names and sample values.

---

# 3️⃣ Viewing Dataset Information

## 📄 Display Last Rows

```python
dataset.tail()
```

Shows the last 5 rows of the dataset.

---

## 🎲 Random Sample Rows

```python
dataset.sample(5)
```

Displays 5 random rows from the dataset.

Purpose:

* Understand data variability.
* Verify randomness in records.

---

## 📏 Dataset Shape

```python
dataset.shape
```

Returns:

```python
(rows, columns)
```

Purpose:

* Understand dataset size.
* Check total records and features.

---

## 🧾 Column Names

```python
dataset.columns
```

Displays all column names.

Purpose:

* Identify features.
* Understand available variables.

---

## ℹ️ Dataset Information

```python
dataset.info()
```

Displays:

* Data types
* Non-null counts
* Memory usage

Purpose:

* Detect missing values.
* Understand feature types.
* Identify cleaning requirements.

---

## 📈 Statistical Summary

```python
dataset.describe()
```

Provides:

* Mean
* Standard deviation
* Minimum values
* Maximum values
* Quartiles

Purpose:

* Understand numerical feature distribution.
* Detect unusual values.

---

# 4️⃣ Data Cleaning

## 🗑️ Dropping Unnecessary Column

```python
dataset = dataset.drop(columns=['order_id'])
```

## 📘 Explanation

`order_id` is removed because it acts only as a unique identifier and does not contribute to meaningful analysis.

---

# 5️⃣ Restaurant Name Cleaning

## 🔍 Checking Unique Restaurant Names

```python
dataset['restaurant_name'].unique()
```

Purpose:

* Inspect inconsistent text values.
* Detect unwanted characters.

---

## ✨ Removing Special Characters

```python
dataset['restaurant_name'].str.replace(r"[a-zA-Z.]", "", regex=True).unique()
```

Purpose:

* Identify unusual symbols and noisy text.

---

## 🧹 Cleaning Restaurant Names

```python
dataset['restaurant_name'] = (
    dataset['restaurant_name']
    .astype(str)
    .str.replace(r"[\x8c_¤¾Ñ¼']", "", regex=True)
)
```

## 📘 Explanation

This step removes corrupted or unreadable characters from restaurant names.

Purpose:

* Improve text quality.
* Standardize restaurant names.
* Ensure clean analysis.

---

# 6️⃣ Exploring Categorical Features

## 🍜 Cuisine Types

```python
dataset['cuisine_type'].unique()
```

Purpose:

* Identify all cuisine categories.

---

## 📅 Day of the Week

```python
dataset['day_of_the_week'].unique()
```

Purpose:

* Check available day categories.

---

## ⭐ Ratings

```python
dataset['rating'].unique()
```

Purpose:

* Inspect rating values.
* Detect invalid or missing values.

---

# 7️⃣ Handling Missing Ratings

## 🔢 Count Rating Values

```python
dataset['rating'].value_counts()
```

Purpose:

* Understand rating frequency.

---

## 🔄 Convert Ratings to Numeric

```python
dataset['rating'] = pd.to_numeric(dataset['rating'], errors='coerce')
```

## 📘 Explanation

* Converts rating column into numeric type.
* Invalid values become `NaN`.

`errors='coerce'` prevents program errors and safely handles invalid values.

---

## 📍 Finding Mode

```python
dataset['rating'].mode()[0]
```

## 📘 Explanation

Returns the most common rating value.

Purpose:

* Use mode for missing value replacement.

---

## 🩹 Filling Missing Ratings

```python
dataset['rating'] = dataset['rating'].fillna(dataset['rating'].mode()[0])
```

## 📘 Explanation

Missing ratings are replaced using the most frequent rating value.

Purpose:

* Preserve dataset size.
* Maintain realistic rating distribution.

---

## 🔢 Convert Ratings to Integer

```python
dataset['rating'] = dataset['rating'].astype(int)
```

Purpose:

* Ensure consistent numeric formatting.

---

# 8️⃣ Checking Numeric Features

## ⏱️ Food Preparation Time

```python
dataset['food_preparation_time'].unique()
```

Purpose:

* Inspect preparation duration values.

---

## 🚚 Delivery Time

```python
dataset['delivery_time'].unique()
```

Purpose:

* Inspect delivery duration values.

---

# 9️⃣ Missing Values and Duplicate Check

## ❓ Missing Values

```python
dataset.isnull().sum()
```

Purpose:

* Verify whether null values remain.

---

## 📑 Duplicate Values

```python
dataset.duplicated().sum()
```

Purpose:

* Detect duplicate rows.
* Maintain data quality.

---

# 🔍 10. Exploratory Data Analysis (EDA)

# 🍽️ Most Ordered Restaurants

```python
most_ordered_resturant = dataset['restaurant_name'].value_counts()
```

## Purpose

* Identify popular restaurants.
* Analyze customer preferences.

---

# 🍕 Most Ordered Cuisine Types

```python
most_order_cuisine_type = dataset['cuisine_type'].value_counts()
```

## Purpose

* Identify most preferred cuisines.
* Understand market demand.

---

# 💰 Most Frequent Order Amounts

```python
often_order_amount = dataset['cost_of_the_order'].value_counts()
```

## Purpose

* Analyze customer spending behavior.
* Detect common pricing ranges.

---

# 📈 Highest Order Amount

```python
highest_order_amount = dataset['cost_of_the_order'].max()
```

## Purpose

* Identify highest-value order.
* Detect premium transactions.

---

# 📉 Lowest Order Amount

```python
lowest_order = dataset['cost_of_the_order'].min()
```

## Purpose

* Identify minimum order value.
* Analyze low-cost transactions.

---

# 📊 11. Data Visualization

# 📅 Orders by Day of the Week

```python
plt.figure(figsize=(7,6))
day_of_the_week.plot(kind='pie', autopct='%1.1f%%')
plt.title('Orders by Day of the Week')
plt.show()
```

## Visualization Purpose

* Compare order distribution.
* Identify busiest days.
* Analyze weekly customer activity.

---

# ⭐ Customer Ratings Distribution

```python
plt.figure(figsize=(7,6))
customers_rating.plot(kind='bar')
plt.title('Customer Ratings')
plt.show()
```

## Visualization Purpose

* Analyze customer satisfaction.
* Detect common rating trends.

---

# ⏳ Food Preparation Time Analysis

```python
max_preparation_time = dataset['food_preparation_time'].max()
min_preparation_time = dataset['food_preparation_time'].min()
```

## Purpose

* Measure kitchen efficiency.
* Detect preparation delays.

---

# 🚴 Delivery Time Analysis

```python
max_delivery_time = dataset['delivery_time'].max()
min_delivery_time = dataset['delivery_time'].min()
```

## Purpose

* Measure delivery performance.
* Identify slow delivery cases.

---

# 🍱 Ratings by Cuisine Type

```python
total_rating_by_cuisine_type = dataset.groupby('cuisine_type')['rating'].sum()
```

## Purpose

* Compare cuisine popularity through ratings.
* Identify highly rated cuisine categories.

---

# 📆 Total Sales by Day

```python
total_sales = dataset.groupby('day_of_the_week')['cost_of_the_order'].sum()
```

## Purpose

* Analyze daily revenue trends.
* Identify highest sales days.

---

# 💵 Total Sales by Cuisine Type

```python
total_sales_by_cuisine_type = dataset.groupby('cuisine_type')['cost_of_the_order'].sum()
```

## Purpose

* Compare cuisine-based revenue.
* Identify profitable cuisine categories.

---

# 💡 Key Insights from the Analysis

## 👥 Customer Behavior Insights

* Some restaurants receive significantly more orders than others.
* Certain cuisines are highly preferred by customers.
* Customer ratings are mostly concentrated around common rating values.
* Order activity differs across weekdays and weekends.

---

## 🏢 Business Insights

* High-performing cuisines can be prioritized for marketing.
* Restaurants with slow preparation or delivery times may require operational improvements.
* Popular order days can help optimize staffing and delivery resources.
* High-sales cuisine categories contribute major revenue.

---

# 🎓 Learning Outcomes

## 🎓 Learning Outcomes

This project provides practical exposure to:

* Data preprocessing
* Missing value handling
* Feature exploration
* Data visualization
* Business insight generation
* Real-world EDA workflows
* Python data analysis libraries

---

# 🚀 Future Improvements

Possible future enhancements:

* Build a recommendation system.
* Predict delivery time using machine learning.
* Create an interactive dashboard.
* Deploy the project as a web application.

---

# 🧰 Recommended Tools

## 💻 IDEs

* ❖url❖Visual Studio Code❖[https://code.visualstudio.com/❖](https://code.visualstudio.com/❖)
* ❖url❖Jupyter Notebook❖[https://jupyter.org/❖](https://jupyter.org/❖)

---

# ✅ Conclusion

This project demonstrates a complete Exploratory Data Analysis (EDA) workflow using a food delivery dataset. It covers data loading, cleaning, preprocessing, visualization, and business insight extraction to showcase how real-world datasets are analyzed using Python.

---

# 👨‍💻 Author

```text
Name: Jesh Rijal
GitHub: [My GitHub Profile](https://github.com/jesh-rijal)
```

---

# 📜 License

This project is open-source and available for educational and learning purposes.
