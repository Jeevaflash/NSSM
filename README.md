# Neural State Space Models for Multivariate Time-Series Forecasting
This project predicts future time-series values using past data.
The entire program works as a backend pipeline: data → model → training → prediction → evaluation.

What Happens Inside the Code (Step-by-Step)
1. Data Creation

The code first generates synthetic multivariate time-series data.
Each feature contains:

Repeating patterns (seasonality)

A slow trend

Random noise

Sudden changes (structural breaks)

This avoids using external datasets and makes the program fully self-contained.

2. Data Windowing

Time-series data is converted into learning samples.

For each sample:

Input (x) = past values (example: 96 time steps)

Output (y) = future values to predict (example: next 24 time steps)

This is handled using a custom Dataset class.

3. Data Scaling

Before training:

Mean and standard deviation are computed from training data

All data is normalized using these values

This helps models train faster and more stably.

4. Neural State Space Model (NSSM)

The NSSM has three main internal parts:

Encoder
Converts the last observed data point into a hidden state

Transition Network
Updates the hidden state at each future step

Observation Network
Converts the hidden state into predicted output values

The model predicts future steps one by one in a loop.

5. LSTM Baseline Model

A standard LSTM model is implemented for comparison.
It:

Reads past data

Uses its internal memory

Predicts future values step by step

This helps compare NSSM performance against a common deep-learning approach.

6. Training Process

For each training epoch:

Load a batch of data

Run the model forward

Compute prediction error (MSE loss)

Backpropagate gradients

Update model weights

Clip gradients to avoid instability

Early stopping is used to stop training when validation performance stops improving.

7. Evaluation

After training:

Models are tested on unseen data

Predictions are converted back to original scale

Errors are calculated using RMSE, WAPE, and MASE

8. Sensitivity Testing

The code runs the experiment using different hidden-state sizes.
This checks how model performance changes with model complexity.

Output

Printed training and validation loss

Printed test error metrics

Saved prediction results in a .npz file

Summary

This code shows:

How raw time-series data is prepared

How neural models process sequences internally

How training and evaluation loops work

How to compare two forecasting models fairly
