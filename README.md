# Prodigy InfoTech Data Science Internship — Task 01

**Submitted by:** Sudip Mitra  
**Track:** Data Science  
**Task:** 01 — Population Data Visualization


## Population Data Visualization

This project was created as part of the Prodigy InfoTech Data Science
Internship, Task 01.

The purpose of this project is to take a large population dataset and
turn the data into visual charts that are easier to understand.

The project uses World Development Indicators population data and
focuses on population values for the year 2024.

## Project Objective

The main objective is to visualize the distribution of population data
using a histogram and identify the entries with the highest population
values using a bar chart.

Instead of reading hundreds of population values from a table,
visualization makes it easier to see the overall distribution and
compare large population values.

## Dataset

The dataset contains World Development Indicators data for the
population indicator:

``` text
Indicator Name: Population, total
Indicator Code: SP.POP.TOTL
```

The dataset contains population data from 1960 to 2024.

Important columns used in this project include:

-   `Country Name`
-   `Country Code`
-   `Indicator Name`
-   `Indicator Code`
-   `2024`

The dataset also contains World Bank aggregate entries such as `World`,
`High income`, `IBRD only`, and regional groups.

Dataset source:

https://github.com/Prodigy-InfoTech/data-science-datasets/tree/main/Task%201

## Technologies Used

-   Python
-   Pandas
-   Matplotlib
-   Seaborn
-   Google Colab or Jupyter Notebook

## Project Workflow

The notebook follows this workflow:

``` text
Load Libraries
      ↓
Load CSV Dataset
      ↓
Skip Metadata Rows
      ↓
Inspect Dataset
      ↓
Check Missing Values
      ↓
Select 2024 Population Data
      ↓
Convert Population Values to Numeric
      ↓
Remove Missing Values
      ↓
Create Histogram
      ↓
Find Top 10 Population Values
      ↓
Create Bar Chart
```

## 1. Importing Libraries

The project starts by importing the required Python libraries:

``` python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

Pandas handles the dataset, while Matplotlib is used to create the
visualizations. Seaborn is also imported for possible data visualization
use.

## 2. Loading the Dataset

The CSV file contains four metadata rows before the actual table
headers.

Therefore, the notebook uses:

``` python
df = pd.read_csv("data.csv", skiprows=4)
```

The `skiprows=4` parameter tells Pandas to ignore the first four rows
and start reading the actual dataset from the fifth row.

The notebook then checks the data using:

``` python
print(df.head())
print(df.shape)
print(df.columns.tolist())
```

The loaded dataset contains 266 rows and 70 columns, including the year
columns from 1960 to 2024 and an empty `Unnamed: 69` column.

## 3. Inspecting Missing Values

The project checks the size of the dataset and missing values:

``` python
print("Rows:", df.shape[0])
print("Columns:", df.shape[1])

print("\nColumn names:")
print(df.columns.tolist())

print("\nMissing values:")
print(df.isnull().sum())
```

This helps understand the structure and quality of the data before
visualization.

The `Unnamed: 69` column contains missing values for all 266 rows. The
notebook does not explicitly remove this column because it is not used
in the visualization.

## 4. Selecting 2024 Population Data

The project focuses on population values for 2024.

The values are converted into numeric format:

``` python
population_2024 = pd.to_numeric(df["2024"], errors="coerce")
```

Invalid values are converted to missing values using `errors="coerce"`.

The missing values are then removed:

``` python
population_2024 = population_2024.dropna()
```

The resulting series contains 265 population observations.

## 5. Histogram

The first visualization is a histogram:

``` python
plt.figure(figsize=(10, 6))

plt.hist(population_2024, bins=20)

plt.title("Distribution of Population Across Countries in 2024")
plt.xlabel("Population (in million)")
plt.ylabel("Number of Countries")

plt.tight_layout()
plt.show()
```

The histogram divides the population values into 20 groups, called bins.

This makes it easier to see how the population values are distributed
instead of looking at individual numbers.

### What the histogram helps us understand

The histogram can be used to identify:

-   How population values are distributed.
-   How many observations fall into different population ranges.
-   Whether most observations have relatively small or large population
    values.
-   Whether a few very large population values affect the overall
    distribution.

## 6. Finding the Top 10 Population Values

The notebook then converts the 2024 column to numeric format:

``` python
df["2024"] = pd.to_numeric(df["2024"], errors="coerce")
```

It selects the ten largest values using:

``` python
top_10 = df.nlargest(10, "2024")
```

The selected values are displayed with:

``` python
print(top_10[["Country Name", "2024"]])
```

## 7. Bar Chart

The selected values are visualized using a bar chart:

``` python
plt.figure(figsize=(12, 6))

plt.bar(top_10["Country Name"], top_10["2024"])

plt.title("Top 10 Countries by Population in 2024")
plt.xlabel("Country")
plt.ylabel("Population")

plt.xticks(rotation=45, ha="right")

plt.tight_layout()
plt.show()
```

The height of each bar represents the population value.

This makes it easy to compare the largest population values visually.

## Important Dataset Detail

The current notebook selects the ten largest population values from the
complete dataset.

Because the World Development Indicators dataset contains both countries
and World Bank aggregate groups, the current top 10 result includes
entries such as:

``` text
World
IDA & IBRD total
Low & middle income
Middle income
IBRD only
Early-demographic dividend
Lower middle income
Upper middle income
East Asia & Pacific
Late-demographic dividend
```

These are World Bank aggregates or groups, not individual countries.

Therefore, the current bar chart demonstrates how to find and visualize
the largest population entries in the dataset. If the goal is
specifically to show the top 10 individual countries, an additional
filtering step should be added before `nlargest()`.

## How This Project Makes Data Easier to Understand

The original dataset contains hundreds of rows and many years of
population values.

Reading the numbers directly from the CSV makes it difficult to identify
patterns.

The project converts those numbers into visual information.

For example:

``` text
Large population dataset
          ↓
Select useful data
          ↓
Create histogram
          ↓
Understand distribution
```

And:

``` text
Population values
       ↓
Find largest values
       ↓
Create bar chart
       ↓
Compare visually
```

A graph allows a person to understand differences and patterns much
faster than manually comparing hundreds of numerical values.

## How to Run the Project

### 1. Clone the repository

Open Command Prompt or Terminal:

``` bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
```

Replace `YOUR-USERNAME` and `YOUR-REPOSITORY` with the actual GitHub
username and repository name.

Move into the project folder:

``` bash
cd YOUR-REPOSITORY
```

### 2. Install the required libraries

``` bash
pip install pandas matplotlib seaborn
```

### 3. Add the dataset

Place the dataset file named:

``` text
data.csv
```

in the same directory as the notebook.

The project expects this file because the notebook uses:

``` python
df = pd.read_csv("data.csv", skiprows=4)
```

### 4. Open the notebook

Using Jupyter:

``` bash
jupyter notebook
```

Then open:

``` text
prodigy_datascience_01.ipynb
```

You can also open the notebook directly in Google Colab.

### 5. Run the cells

Run the cells from top to bottom.

The notebook will:

1.  Import the libraries.
2.  Load the dataset.
3.  Inspect the dataset.
4.  Check missing values.
5.  Extract 2024 population data.
6.  Create the histogram.
7.  Find the top 10 population values.
8.  Create the bar chart.

## Using This Project With Your Own Dataset

You can use the same basic workflow with another CSV dataset.

### Step 1: Replace the dataset

Put your CSV file in the project directory.

For example:

``` text
my_data.csv
```

### Step 2: Change the file name

Replace:

``` python
df = pd.read_csv("data.csv", skiprows=4)
```

with:

``` python
df = pd.read_csv("my_data.csv")
```

If your dataset has metadata rows before the column headings, use the
appropriate `skiprows` value.

For example:

``` python
df = pd.read_csv("my_data.csv", skiprows=3)
```

### Step 3: Inspect your dataset

Use:

``` python
print(df.head())
print(df.shape)
print(df.columns.tolist())
print(df.isnull().sum())
```

This helps you understand which columns are available.

### Step 4: Select a numerical column

For example:

``` python
values = pd.to_numeric(df["Age"], errors="coerce")
values = values.dropna()
```

### Step 5: Create a histogram

``` python
plt.figure(figsize=(10, 6))

plt.hist(values, bins=20)

plt.title("Distribution of Age")
plt.xlabel("Age")
plt.ylabel("Frequency")

plt.tight_layout()
plt.show()
```

### Step 6: Create a bar chart

If you have a numerical column that you want to rank:

``` python
top_10 = df.nlargest(10, "Age")
```

Then:

``` python
plt.figure(figsize=(12, 6))

plt.bar(top_10["Name"], top_10["Age"])

plt.title("Top 10 Entries")
plt.xlabel("Name")
plt.ylabel("Age")

plt.xticks(rotation=45, ha="right")

plt.tight_layout()
plt.show()
```

The column names must be changed to match your own dataset.

## Project Structure

A simple GitHub repository can look like this:

``` text
Task-01/
│
├── data.csv
├── prodigy_datascience_01.ipynb
├── README.md
└── requirements.txt
```

Example `requirements.txt`:

``` text
pandas
matplotlib
seaborn
```

Install the dependencies with:

``` bash
pip install -r requirements.txt
```

## Learning Outcomes

This project demonstrates practical skills in:

-   Loading CSV data with Pandas.
-   Handling metadata rows.
-   Inspecting dataset structure.
-   Checking missing values.
-   Converting data to numeric format.
-   Removing missing observations.
-   Selecting values from a dataset.
-   Finding the largest values with `nlargest()`.
-   Creating histograms.
-   Creating bar charts.
-   Understanding data through visualization.
-   Preparing a Python data analysis project for GitHub.

## Motivation

The motivation behind this project is to demonstrate how raw numerical
data can be transformed into information that is easier for people to
understand.

A dataset may contain hundreds of rows and many years of information.
Visualization provides a simple way to identify patterns, distributions,
and comparisons without manually reading every value.

This project provides a basic foundation for exploratory data analysis
and can be adapted to other datasets and real-world data analysis
problems.

## Conclusion

This project uses Python, Pandas, and Matplotlib to analyze population
data from the World Development Indicators dataset.

The notebook loads and inspects the dataset, extracts population data
for 2024, creates a histogram to visualize the distribution, and creates
a bar chart for the ten largest population entries.

The workflow can be reused with other datasets by changing the input
file and selecting the appropriate columns.
