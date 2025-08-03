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

