# Combined-Cycle Power Plant Output Prediction

*AI101 mini-project · Team 33*

Predicting net electrical output from the operating conditions of a combined-cycle power plant using linear regression.

*Repository:* [ArinjayGarg/Combined-Cycle-Power-Plant](https://github.com/ArinjayGarg/Combined-Cycle-Power-Plant)<br>
<br>
*Presentation:* [View slides](https://docs.google.com/presentation/d/1i_HJsBoYm9vk3iMOxbR0VByTbUC7At4bo_q7MOe8lqY/edit?usp=sharing)<br>
<br>
*Video:* [Watch video](https://youtu.be/USvFHuFqIu0)

## Project overview

A combined-cycle power plant uses gas and steam turbines to generate electricity. This project uses four measured operating conditions to estimate the plant’s net hourly electrical output (PE). The analysis explores the data, compares linear regression models built with different feature combinations, and evaluates the best-performing combination.

## Dataset

The project uses the [Combined Cycle Power Plant dataset from the UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/294/combined%2Bcycle%2Bpower%2Bplant). It contains 9,568 hourly-average records collected from 2006 to 2011 while the plant operated at full load.

| Column | Meaning | Unit | Model role |
|---|---|---|---|
| AT | Ambient temperature | °C | Input feature |
| V | Exhaust vacuum | cm Hg | Input feature |
| AP | Ambient pressure | mbar | Input feature |
| RH | Relative humidity | % | Input feature |
| PE | Net hourly electrical output | MW | Prediction target |

The notebook reports no missing values and 41 duplicate rows. Those duplicate rows were counted but not removed in the model run.

## Method

1. Load the CSV file and inspect its shape, columns, summary statistics, missing values, and duplicate rows.
2. Explore distributions, potential outliers, and relationships between each input and PE.
3. Split the data into training and test sets using an 80/20 split and random_state=42.
4. Fit linear regression models for all 15 non-empty combinations of AT, V, AP, and RH.
5. Compare models using MAE, MSE, RMSE, and R². Refit the lowest-RMSE feature combination and report five-fold cross-validation results.

The analysis uses Python with NumPy, pandas, scikit-learn, Matplotlib, and Seaborn. Package names are listed in [requirements.txt](requirements.txt).

## Results

The four-feature model (AT + V + AP + RH) had the lowest RMSE among the 15 combinations.

| Evaluation | MAE | MSE | RMSE | R² |
|---|---:|---:|---:|---:|
| Held-out test set (1,914 records) | 3.596 MW | 20.274 MW² | 4.503 MW | 0.930 |
| Five-fold cross-validation on training data | 3.632 MW | — | 4.572 MW | 0.928 |

The feature combination was selected by comparing RMSE on the same held-out test set used for the reported test metrics. This makes the test result useful for this project comparison, but potentially optimistic. A stricter evaluation would select features using training-only validation and reserve a separate final test set.

## Key learnings

- Ambient temperature had the strongest single-feature correlation with PE in the notebook (r = -0.948).
- Using all four inputs gave the lowest RMSE, although its advantage over AT + V + RH was small (4.503 vs. 4.513 MW).
- Five-fold cross-validation and the test-set evaluation were close (R² = 0.928 and 0.930, respectively).

## Project structure

```text
.
├── data/
│   └── dataset.csv
├── Notebooks/
│   ├── main.ipynb
├── plots/
│   ├── EDA/
│   ├── Feature_Selection/
│   └── Model_Evaluation/
├── README.md
└── requirements.txt
```


- Notebooks/main.ipynb contains the feature-name reference.
- plots/EDA/ contains exploratory charts.
- plots/Feature_Selection/ contains feature-comparison results and charts.
- plots/Model_Evaluation/ contains prediction, residual, and coefficient plots plus saved predictions.

## Run the notebook

### Prerequisites

Install [Git](https://git-scm.com/downloads) and [Python 3](https://www.python.org/downloads/) if they are not already installed. Check that they are available in a terminal:

```text
git --version
python --version
```

On Windows, the Python launcher may be named py; if python --version is not recognized, try py --version and use py in place of python below.

### 1. Clone the repository

Run these commands from the parent folder where you want the project directory created:

```bash
git clone https://github.com/ArinjayGarg/Combined-Cycle-Power-Plant.git
cd Combined-Cycle-Power-Plant
```

### 2. Create a virtual environment

Create an isolated Python environment in the project folder:

```bash
python -m venv .venv
```

### 3. Activate the environment

Use the command for your operating system. Run only one of these:

*Windows PowerShell*

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks script activation, open Command Prompt in the project folder and activate with:

```bat
.venv\Scripts\activate.bat
```

*macOS or Linux*

```bash
source .venv/bin/activate
```

When the environment is active, the terminal prompt usually shows (.venv).

### 4. Install the project packages

From the project root, install the packages listed in requirements.txt:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 5. Launch the analysis notebook

Start Jupyter from the Notebooks folder. This matters because the notebook reads the dataset from ../data/dataset.csv and saves results under ../plots/.

```bash
cd Notebooks
jupyter notebook main.ipynb
```

In the browser tab that opens, select *Kernel → Restart Kernel and Run All Cells* (or *Run → Run All Cells*, depending on the Jupyter version). The test.ipynb notebook runs the analysis, compares feature combinations, evaluates the final model, and regenerates the plots and result files under plots/. main.ipynb contains the feature-name reference.

To stop Jupyter, return to the terminal where it is running and press *Ctrl+C*, then confirm if prompted. To leave the virtual environment, run:

```
deactivate
```


### Troubleshooting

- *git or python is not recognized:* install Git or Python, then close and reopen the terminal so its PATH is refreshed. On Windows, try py for Python.
- *jupyter is not recognized:* confirm (.venv) appears in the prompt and repeat python -m pip install -r requirements.txt.
- *The dataset file cannot be found:* stop Jupyter, change to the project’s Notebooks folder, and launch jupyter notebook test.ipynb again. The notebook uses relative paths, so its working directory must be Notebooks.
- *A package import fails:* activate the project environment and install the requirements again. Avoid installing packages into a different Python environment.

## Team 33

| Member | Entry number | Assigned role | Contribution | GitHub |
|---|---|---|---|---|
| Trisha Bansal | 2026eeb1420 | Execution lead | Idea selection and substantial coding | [2026eeb1420-tri](https://github.com/2026eeb1420-tri) |
| Arinjay Garg | 2026mcb1513 | Video lead | Team coordination and idea selection | [ArinjayGarg](https://github.com/ArinjayGarg) |
| Shubham Maurya | 2026aib1081 | Documentation lead | Coding and documentation | [2026aib1081-cyber](https://github.com/2026aib1081-cyber) |
| Jyoti | 2026aib1044 | PPT lead | Project ideas and documentation | [2026aib1044](https://github.com/2026aib1044) |

## AI-use disclosure

The team reports using AI assistance mainly for bug fixing, suggestions to make the code more industry-style, and occasional background research. 

## Dataset citation

Tfekci, P. & Kaya, H. (2014). Combined Cycle Power Plant [Dataset]. UCI Machine Learning Repository. [https://doi.org/10.24432/C5002N](https://doi.org/10.24432/C5002N). The dataset is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).