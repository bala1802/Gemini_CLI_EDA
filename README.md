# Gemini CLI EDA Workflow – Amazon Product Dataset

This guide shows how to use Gemini CLI—Google’s open-source AI agent for the terminal—for rapid, interactive exploratory data analysis (EDA) on an Amazon-style product review dataset.

With Gemini CLI, you can:

- Summarize, analyze, and visualize your data—all from the command line
- Automate repetitive EDA steps using natural language or custom commands
- Generate, save, and run Python scripts for your own analysis

## Getting Started

- MacOS / Linux / Windows (WSL)
- Node.js v18 or higher
- Python (version suitable for pandas, matplotlib, seaborn)
- (Recommended) A venv or conda virtual environment for Python packages

### 1. Install Node.js (if needed)

Download and install from [nodejs.org](https://nodejs.org/en)

Check version:

```
node -v
```

### 2. Install Gemini CLI

Option A: Using npm
```
npm install -g @google/gemini-cli
```

Option B: Homebrew (macOS)
```
brew install gemini-cli
```

Option C: Run Once with npx
```
npx https://github.com/google-gemini/gemini-cli
```

### 3. Verify Installation
```
gemini
```

You should see something similar

<img width="1512" height="861" alt="image" src="https://github.com/user-attachments/assets/c6298c62-51e6-4237-b5bc-593b36e7231d" />

### 4. Create and Activate Your Python Virtual Environment

Inside your project directory:

```
python3 -m venv venv
source venv/bin/activate
pip install pandas matplotlib seaborn  # and any other packages needed
```

### 5. Load Your Dataset

For this usecase, I used [Amazon Dataset](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset) from Kaggle

Ensure your Amazon product dataset is present, e.g.:

```
products.csv
```

Example schema:

```
product_id, product_name, category, discounted_price, actual_price, discount_percentage, rating, rating_count, about_product, user_id, user_name, review_id, review_title, review_content, img_link, product_link
```

## Using Gemini CLI for EDA

### 1. Launch Gemini CLI with Your Virtual Environment Active

```
source venv/bin/activate        # (if not already active)
gemini
```

### 2. Example EDA Prompts

Start EDA by directly typing prompts in Gemini CLI.

Example prompts:

#### Example-1: Summarize Columns and Main Features

```
Summarize the columns and datatypes in products.csv. What are the main features of this dataset?
```
File: .gemini/commands/eda-summary-columns.toml

```
name = "/eda-summary-columns"
description = "Summarize products.csv columns and the main features of the dataset."
prompt = """
Read products.csv in the current directory.
- List all columns and their data types.
- Describe briefly what each column represents.
- Provide an overview of the dataset's structure and its main features.
"""
```

#### Example-2: Summary Statistics for Numerical Columns

```
For products.csv, give summary statistics for numerical columns like price, discount, rating, rating_count.
```
File: .gemini/commands/eda-numeric-stats.toml

```
name = "/eda-numeric-stats"
description = "Generate summary statistics for numerical columns like price, discount, rating, and rating_count."
prompt = """
Read products.csv in the current directory.
For the columns actual_price, discounted_price, discount_percentage, rating, and rating_count:
- Calculate and report mean, median, min, max, and standard deviation.
- Present all results in a clear table.
"""
```

#### Example-3: List Unique Categories and Their Counts
```
List all unique categories and count the number of products in each category.
```

File: .gemini/commands/eda-category-counts.toml

```
name = "/eda-category-counts"
description = "List unique product categories and count products in each."
prompt = """
Read products.csv in the current directory.
- List all unique categories found in the category column.
- Count how many products are in each category.
- Present the results as a table.
"""
```

#### Example-4: Identify Products with Missing or Suspicious Values
```
Identify products with missing or suspicious values.
```

File: .gemini/commands/eda-missing-anomalies.toml

```
name = "/eda-missing-anomalies"
description = "Identify products with missing or suspicious values."
prompt = """
Examine products.csv in the current directory.
- Identify all rows with missing values in any column.
- Flag suspicious values (such as negative prices or ratings out of range 0-5 or 0-100 for percentages).
- Summarize findings in a list or table.
"""
```

#### Example-5: Plot Histogram of Discount Percentage
```
Generate Python code to plot histogram of discount_percentage, and save it as ./scripts/discount_hist.py.
```

File: .gemini/commands/eda-discount-histogram.toml

```
name = "/eda-discount-histogram"
description = "Generate Python code to plot a discount percentage histogram and save it."
prompt = """
Create a Python script using pandas and matplotlib/seaborn to:
- Read products.csv in the current directory.
- Plot a histogram of the discount_percentage column with proper axis labels and a title.
- Save the script as ./scripts/discount_hist.py (create the scripts folder if it doesn’t exist).
- Include comments in the code explaining each step.
"""
```

#### Example-6: Analyze Review Content for Frequent Keywords
```
Analyze review_content for frequent positive and negative keywords. Save the summary as review_topics.txt.
```

File: .gemini/commands/eda-review-keywords.toml

```
name = "/eda-review-keywords"
description = "Analyze review_content for frequent positive and negative keywords."
prompt = """
Analyze the review_content column in products.csv.
- Identify and list the most frequent positive and negative keywords or topics.
- Summarize the findings as a short report.
- Save the summary as review_topics.txt in the current directory.
"""
```

### Instructions for use:

- Create the .gemini/commands/ folder if it does not exist:

```
mkdir -p .gemini/commands scripts
```

- Save each TOML as a separate file as shown above.
- Run the commands inside Gemini CLI:
```
/eda-summary-columns
/eda-numeric-stats
/eda-category-counts
/eda-missing-anomalies
/eda-discount-histogram
/eda-review-keywords
```

### 3. Save Outputs and Results

You can instruct Gemini CLI to save code, figures, or summary reports:

1. “Save this code as ./scripts/eda_category_overview.py”
2. “Save this analysis as summary.txt”

### 4. Tips & Best Practices

- Always specify explicit file paths when saving generated code or reports.
- Keep your EDA scripts organized in a /scripts directory for reproducibility.
- Activate your Python virtual environment before launching Gemini CLI to ensure all code runs with correct dependencies.
- For repetitive tasks, use .toml-based custom commands for speed and consistency.








