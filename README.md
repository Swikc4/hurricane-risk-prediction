<a id="readme-top"></a>

<br />
<div align="center">
  <h3 align="center">Hurricane Risk Prediction</h3>
  <p align="center">
    ZIP-level hurricane damage analysis for Miami-Dade County with a Random Forest model - a Data Science and Machine Learning Club project at Baruch College
    <br />
    <a href="https://github.com/Swikc4/hurricane-risk-prediction"><strong>Explore the repo »</strong></a>
  </p>
</div>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a>
      <ul><li><a href="#built-with">Built With</a></li></ul>
    </li>
    <li><a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#results-and-what-they-mean">Results and What They Mean</a></li>
    <li><a href="#known-issues-to-fix-before-rerunning">Known Issues to Fix Before Rerunning</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

## About The Project

I worked on this project with the Data Science and Machine Learning Club at Baruch College in November and December 2025. We looked at recorded hurricane damage in Miami-Dade County, Florida. My part included cleaning the data, analyzing ZIP codes, and working with a Random Forest model.

We used OpenFEMA housing-assistance records and kept the ZIP code, disaster number, and damage amount. After removing missing values, we grouped the records by ZIP code. I looked at the 10 ZIP codes with the highest total recorded damage and made a bar chart.

For the model, ZIP codes in the top 25% of recorded damage were labeled high risk. We used average damage, record count, and a mock exposure feature as inputs. The data was split into 153 training ZIP codes and 39 test ZIP codes. The repo has one model: Random Forest, built with scikit-learn.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

* ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
* ![pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
* ![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
* ![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
* ![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge)
* ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Getting Started

The notebooks were written in Google Colab and use manual file uploads, so they run most easily in Colab. They also run locally in Jupyter with small path changes.

### Prerequisites

* Python 3 with pandas, NumPy, scikit-learn, and Matplotlib
  ```sh
  pip install pandas numpy scikit-learn matplotlib
  ```

### Installation

1. Clone the repo
   ```sh
   git clone https://github.com/Swikc4/hurricane-risk-prediction.git
   ```
2. Open the notebooks in Google Colab or Jupyter and run them in order: Week 1, then Week 2, then Week 3.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

The project runs in three notebooks:

1. **Week 1: Hurricane Damage Data Gathering** - pulls Miami-Dade housing-assistance records from the live OpenFEMA API, keeps ZIP code, disaster number, and damage amount, drops missing values, and plots a damage-distribution histogram and a top-10 ZIP bar chart. The saved output (`dataWeek1_clean.csv`, 1,000 rows) is included in the repo. The API call returns only the first page of results, so this file is not a complete damage history.
2. **Week 2: FeatureEngineering** - groups the cleaned records by ZIP code (192 ZIPs), builds the average-damage, record-count, and mock-exposure features, labels the top 25% of ZIPs by total recorded damage as high risk, and saves the 80/20 train/test split (`X_train`, `X_test`, `y_train`, `y_test` - all included).
3. **Week 3: RandomForest** - loads the four saved CSVs, trains a Random Forest classifier (200 trees, max depth 5, balanced class weights), and prints a model report card with accuracy and ROC-AUC plus a feature-importance chart.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Results and What They Mean

The saved notebook reports 89.7% accuracy. A rerun using the saved CSV files also got 35 of the 39 test ZIP codes right (89.7% accuracy, ROC-AUC 0.972).

That score needs context. The exposure feature is made from random numbers, not real exposure measurements. The high-risk label is also based on the same damage records used for the inputs. Average damage multiplied by record count gives the total damage used to create the label, so the model already has much of the answer in its inputs. In the rerun, average damage and record count carried about 95% of the feature importance, and the random exposure feature about 5%.

This was a learning project, not a reliable forecast of future hurricane damage. The test set is small. The top-10 chart shows past recorded damage, not a prediction of which areas will be hit next. The data request also does not collect every page of FEMA results, so this file is not a complete damage history. I would not use it for emergency planning or insurance decisions.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Known Issues to Fix Before Rerunning

Before rerunning Week 3, change `Y_test` to `y_test` in the evaluation cell and use the same variable name for importance in the feature chart (`importance` vs `importances`). In Week 1, remove the extra dot at the end of the top-10 chart's `ticklabel_format` line. The chart labels dollars as millions without dividing the values, so that axis also needs correcting. Set a NumPy random seed if you regenerate the mock exposure feature.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Acknowledgments

* [OpenFEMA Housing Assistance Owners dataset](https://www.fema.gov/about/openfema/data-sets)
* Data Science and Machine Learning Club at Baruch College
