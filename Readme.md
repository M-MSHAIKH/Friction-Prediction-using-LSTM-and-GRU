# Friction Prediction Using LSTM and GRU

This project uses a Long Short-Term Memory (LSTM) and Gated Recurrent Unit (GRU) neural network to predict the friction coefficient of a vehicle based on vehicle lateral dynamics only.

## 📘 Overview

The model is trained on sequences of vehicle dynamics data including:
- Steering angle left/right
- Steering rate left/right
- Steering torque left/right

The goal is to predict the tire-road friction coefficient in real time using time-series inputs.

## 📊 Input/Output

- **Input:** 6 features per time step (time-series window of length 10)
- **Output:** 1 or 2 friction coefficient predictions (depending on configuration)
- Labelled output calculated using a **physical tire brush model**

## 🛠️ Libraries

- Python 3.10+
- PyTorch
- NumPy
- scikit-learn
- Matplotlib

## 🧠 Model Architectures
Below are the detailed architectures of the models used for friction prediction:

📘 LSTM Model
'''text
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
FrictionLSTM                             [64, 2]                   --
├─LSTM: 1-1                              [64, 10, 64]              51,712
├─Linear: 1-2                            [64, 2]                   130
==========================================================================================
Total params: 51,842
Trainable params: 51,842
Non-trainable params: 0
Total mult-adds (M): 33.10
==========================================================================================
Input size (MB): 0.02
Forward/backward pass size (MB): 0.33
Params size (MB): 0.21
Estimated Total Size (MB): 0.55
==========================================================================================
'''

📗 GRU Model
'''text
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
FrictionGRU                              [64, 2]                   --
├─GRU: 1-1                               [64, 10, 64]              38,784
├─Linear: 1-2                            [64, 2]                   130
==========================================================================================
Total params: 38,914
Trainable params: 38,914
Non-trainable params: 0
Total mult-adds (M): 24.83
==========================================================================================
Input size (MB): 0.02
Forward/backward pass size (MB): 0.33
Params size (MB): 0.16
Estimated Total Size (MB): 0.50
==========================================================================================
'''

## 🚀 How to Run

1. Clone this repo:
    ```bash
    git clone https://github.com/your-username/friction-lstm.git
    cd friction-lstm
    ```

2. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

After installing all required dependencies you can run the jupyter notebook or can run as python file.

## 📁 Dataset

The dataset used in this project was obtained from [P1 Garage @ Bucknell University](https://www.projects.bucknell.edu/Beal_Automotive/).  
It contains time-series vehicle dynamics data collected from test drives on different surfaces (e.g., dry and wet asphalt).

Features include:
- Steering angle (left/right)
- Steering rate (left/right)
- Steering torque etc

The data was preprocessed using windowed sequences for training the LSTM model.


## 📈 Results

- RMSE with LSTM: **0.0129**
- RMSE with GRU: **0.0101**

## 💾 Model Saving

Model is saved as:
```python
torch.save(model.state_dict(), "friction_lstm_model.pth")
