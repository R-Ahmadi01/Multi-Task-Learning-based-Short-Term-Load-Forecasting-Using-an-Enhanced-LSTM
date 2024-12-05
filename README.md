# Multi-Task-Learning-based-Short-Term-Load-Forecasting-Using-an-Enhanced-LSTM

---

## Authors
- **Ali Forootani**  
  [Ali.forootani1@ucalgary.ca](mailto:Ali.forootani1@ucalgary.ca)  
- **Reza Ahmadi**  
  [Reza.ahmadi3@ucalgary.ca](mailto:Reza.ahmadi3@ucalgary.ca)  

---

## Abstract
This project presents a novel multi-task learning approach to enhance the performance of load forecasting models using a combination of an autoencoder and LSTM. The framework forecasts future load values while reconstructing historical load patterns. By transferring the encoder’s hidden and cell states to the forecasting decoder, the model achieves significant improvements in accuracy compared to traditional models.

---

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Dataset](#Dataset) 
4. [Data Preprocessing](#Data_Preprocessing)
5. [Model Architecture](#model-architecture)
6. [Results](#results)
7. [Contributing](#contributing)
8. [License](#license)
9. [Contact](#contact)

---

# Introduction
Accurate electrical load forecasting is critical for utility companies to reduce operational costs and manage power grids effectively. This project leverages advances in deep learning to develop a robust multi-task learning model. The approach forecasts electricity loads while reconstructing historical data, offering better predictive accuracy and temporal pattern understanding.

---
# Installation
To replicate this project:

1. Clone this repository:
   ```bash
   git clone https://github.com/R-Ahmadi01/Multi-Task-Learning-based-Short-Term-Load-Forecasting-Using-an-Enhanced-LSTM.git
---

# Dataset 
The dataset used in this project is the **PJM hourly load dataset**, a publicly available resource. PJM is a regional transmission organization (RTO) that coordinates the movement of wholesale electricity across multiple states in the United States and the District of Columbia.

---
## Key Features
### Time-Based Features
- **Hour of the day**: Captures intraday variations in load demand.
- **Day of the week**: Differentiates weekdays from weekends to account for weekly patterns.
- **Month**: Accounts for seasonal variations in electricity demand.

### Temperature Predictors
- **Maximum temperature**: Highest temperature recorded within the network for a specific hour.
- **Minimum temperature**: Lowest temperature recorded within the network for a specific hour.
- **Lagged temperature variables**: Includes temperature values from the previous hour to capture trends.

### Engineered Features
- **Next maximum temperature**: Projected maximum temperature for the next hour.
- **Lagged load variables**: Previous load values to capture temporal dependencies.
- **Day type**: Encodes whether the day is a weekday or weekend.

---
# Data Preprocessing
Data preprocessing is a critical step in ensuring the dataset is clean, consistent, and structured for effective model training and evaluation. This process involves feature extraction, handling missing data, and transforming the dataset into a supervised learning format.

## Preprocessing Steps
1. **Parsing and Feature Extraction**:
   - Convert time columns into a datetime format.
   - Extract features such as hour, day, and month.
   
2. **Handling Missing Values**:
   - Remove rows with missing data to maintain dataset consistency.

3. **Feature Engineering**:
   - Create lagged variables and next-step predictors to improve model performance.
   
4. **Normalization**:
   - Apply MinMax scaling to normalize all feature values to a range of [0, 1].

5. **Supervised Learning Format**:
   - Transform the time-series data into a supervised learning format using lagged data for historical inputs and the next 24-hour horizon for targets.

---

## Notes
- The dataset includes hourly load data, making it ideal for short-term forecasting.
- Temperature predictors and time-based features significantly enhance the model's ability to capture seasonal and diurnal patterns.
---
