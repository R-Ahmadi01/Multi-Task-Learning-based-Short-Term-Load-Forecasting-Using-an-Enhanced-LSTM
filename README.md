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
4. [Data Preprocessing](#Data-Preprocessing)
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
## Architecture Components

### 1. **Encoder**
- **Purpose**: Captures temporal dependencies in the historical load data.
- **Implementation**: 
  - Built using Long Short-Term Memory (LSTM) layers.
  - Processes input sequences over a specified historical time window.
  - Outputs:
    - **Hidden state (`state_h`)**: Encodes learned temporal features.
    - **Cell state (`state_c`)**: Stores long-term dependencies.

### 2. **Decoders**
#### a. **Forecasting Decoder**
- **Purpose**: Predicts load values for the next 24 hours.
- **Implementation**:
  - LSTM layers initialized with the encoder's hidden and cell states.
  - Fully connected layers to map LSTM outputs to the forecast horizon.

#### b. **Reconstruction Decoder**
- **Purpose**: Reconstructs the historical load patterns.
- **Implementation**:
  - Shares the encoder's final hidden and cell states.
  - LSTM layers generate reconstructed sequences from the encoded features.

---

## Key Features
1. **State Transfer**:
   - The encoder's hidden (`state_h`) and cell (`state_c`) states are transferred to both decoders.
   - This ensures that both tasks share a rich representation of historical temporal dependencies.

2. **Shared Learning**:
   - The encoder serves as a shared component, facilitating knowledge transfer between tasks.
   - The dual-task design enhances model performance compared to single-task models.

3. **Custom Loss Function**:
   - A custom loss function scales the mean squared error (MSE) to emphasize forecasting accuracy while maintaining reconstruction quality.

4. **Loss Weighting**:
   - Forecasting Task: Weight = 2.0 (Primary focus).
   - Reconstruction Task: Weight = 1.0 (Secondary task).

---

## High-Level Architecture
```plaintext
Input → Encoder (LSTM) → Shared States → Forecasting Decoder (LSTM + Dense) → Predicted Load
                                ↓
                                → Reconstruction Decoder (LSTM) → Reconstructed Sequence
```
<p align="center">
 <img src="(https://github.com/R-Ahmadi01/Multi-Task-Learning-based-Short-Term-Load-Forecasting-Using-an-Enhanced-LSTM/blob/main/proposed%20deep%20model.png)" alt="Model Structure" width="720"/>
</p>
<p align="center">
 <img src="(https://github.com/R-Ahmadi01/Multi-Task-Learning-based-Short-Term-Load-Forecasting-Using-an-Enhanced-LSTM/blob/main/Multi-task%20learning%20high%20level%20demonstration.png(" alt="Model Structure" width="720"/>
</p>
<p align="center">
 <img src="(https://github.com/R-Ahmadi01/Multi-Task-Learning-based-Short-Term-Load-Forecasting-Using-an-Enhanced-LSTM/blob/main/LSTM%20associated%20with%20its%20parameters.png)" alt="Model Structure" width="720"/>
</p>


---
## Notes
- The dataset includes hourly load data, making it ideal for short-term forecasting.
- Temperature predictors and time-based features significantly enhance the model's ability to capture seasonal and diurnal patterns.

