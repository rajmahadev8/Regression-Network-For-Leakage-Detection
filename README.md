# 💧 Regression Networks for Leakage Detection using Deep Neural Networks and Explainable AI

## Overview

This project develops a deep learning-based regression system for **leak localization** using steady-state mass flow measurements from four vacuum pumps.

The objective is to predict the two-dimensional location of a leak inside a vacuum bag based on sensor measurements collected during the manufacturing process of Carbon Fiber Reinforced Polymer (CFRP) components.

The dataset and experimental setup were provided as part of the course project. The focus of this work was on developing, training, evaluating, and interpreting deep neural network models for accurate leak localization.

The project includes:

- Exploratory Data Analysis (EDA)
- Data preprocessing and feature scaling
- Deep neural network regression
- Learning rate scheduling
- Comparison of preprocessing strategies
- Custom TensorFlow training loops
- Manual implementation of backpropagation
- Explainable AI using Layer-Wise Relevance Propagation (LRP)
- Regression performance analysis

---

# 🏭 Industrial Background

Fiber composite components are manufactured by curing stacked and impregnated materials under heat and pressure. During this process, the structure is vacuum sealed to ensure sufficient pressure throughout curing.

Small leaks in the vacuum bag reduce the applied pressure, negatively affecting product quality. While the presence of a leak can be detected from residual mass flow measurements at the vacuum pumps, identifying its exact location is significantly more challenging and often results in costly production delays.

This project investigates the use of deep learning to automatically estimate leak locations from steady-state sensor measurements, enabling faster and more efficient quality control.

---

# 🎯 Problem Statement

The experimental setup consists of a vacuum table equipped with four vacuum pumps positioned at its corners.

For each experiment:

- A leak was introduced at a random location.
- Residual steady-state mass flow rates from the four vacuum pumps were recorded.
- The corresponding leak coordinates were measured.

Using these measurements, the regression model learns a mapping from:

**Input**

- Mass Flow Controller 1 (MFC1)
- Mass Flow Controller 2 (MFC2)
- Mass Flow Controller 3 (MFC3)
- Mass Flow Controller 4 (MFC4)

↓

**Output**

- Leak x-coordinate
- Leak y-coordinate

The dataset contains **317 experimentally generated samples**, which were provided for model development and evaluation.


The data was analyzed through:

- descriptive statistics
- scatter plots
- feature distributions
- histogram analysis
- train-validation-test splitting

---

# ⚙️ Data Preprocessing

Several preprocessing strategies were investigated to improve model convergence and robustness.

## Standard Min-Max Scaling

Input features were normalized into the range:

- [0,1]

to stabilize optimization.

---

## Robust Preprocessing Pipeline

A second preprocessing pipeline was implemented consisting of:

- Logarithmic transformation
- Winsorization for outlier reduction
- Min-Max Scaling

This preprocessing strategy reduced the influence of extreme sensor values and produced more balanced feature distributions.

The two preprocessing methods were experimentally compared using validation loss to determine the better-performing pipeline.

---

# 🧠 Deep Neural Network Architecture

A fully connected regression network was implemented using TensorFlow and Keras.

## Network Configuration

- 10 hidden layers
- 2048 neurons per hidden layer
- ReLU activation
- Linear output layer
- L2 weight regularization

The architecture was optimized for continuous coordinate prediction rather than classification.

---

# 🚀 Training Strategy

The network was trained using the Adam optimizer together with learning-rate scheduling.

Two learning-rate schedules were investigated:

- Polynomial Decay
- Exponential Decay

The exponential decay schedule produced smoother convergence during optimization.

Training included:

- mini-batch gradient descent
- validation monitoring
- learning-rate scheduling
- regularization

---

# 📈 Model Evaluation

Performance was evaluated using:

- Mean Squared Error (MSE)
- Validation Loss
- Test Loss

Predictions were visualized by comparing:

- Ground Truth leak locations
- Predicted leak locations

using scatter plots and coordinate matching.

---

# 🔄 Custom Training Loop

To better understand TensorFlow's internal optimization process, a custom training loop was implemented.

Instead of relying solely on `model.fit()`, the project used:

- TensorFlow Dataset API
- GradientTape
- Manual optimizer updates
- Batch-wise gradient computation

This provided full control over the optimization process while reproducing the behavior of TensorFlow's built-in training pipeline.

---

# 🧮 Manual Backpropagation

One of the key contributions of this project was implementing the backpropagation algorithm entirely from first principles.

The implementation included:

- Forward propagation
- ReLU activation derivatives
- Gradient computation for every layer
- Weight gradients
- Bias gradients
- Parameter updates

The manually computed gradients were compared against TensorFlow's automatic differentiation.

The numerical error between both approaches was below machine precision, validating the correctness of the implementation.

---

# 🤖 Automatic Differentiation vs Manual Gradients

The project compared two optimization approaches:

### TensorFlow Automatic Differentiation

- GradientTape
- Automatic graph differentiation
- Built-in optimization

### Manual Gradient Computation

- Custom forward pass
- Custom backward propagation
- Explicit gradient derivation
- Manual parameter updates

This comparison provided valuable insight into how deep learning frameworks internally compute gradients.

---

# 🔍 Explainable AI (XAI)

To improve model interpretability, Layer-Wise Relevance Propagation (LRP) was implemented.

LRP attributes prediction relevance back to each sensor input, allowing visualization of how strongly each MFC sensor contributed to the predicted leak location.

The implementation included:

- Positive and negative weight decomposition
- Layer-wise relevance propagation
- Relevance conservation
- Input attribution visualization

This makes the regression model significantly more interpretable than a standard black-box neural network.

---

# 📊 Model Interpretation

For each prediction, relevance scores were computed for all four sensor inputs.

The project visualized:

- Ground-truth leak position
- Predicted leak position
- Individual sensor relevance scores

These explanations provide insight into which sensors contribute most strongly to localization accuracy.

---

# 📌 Key Learning Outcomes

This project demonstrates practical experience with:

- Deep Neural Networks
- Regression using TensorFlow
- Advanced data preprocessing
- Robust feature engineering
- Learning-rate scheduling
- L2 Regularization
- Custom TensorFlow training loops
- Manual backpropagation implementation
- Automatic differentiation
- Explainable AI (Layer-Wise Relevance Propagation)

Rather than treating TensorFlow as a black box, this project explores the mathematical foundations behind neural network optimization and model interpretability.

---

# 🛠️ Technologies Used

- Python
- TensorFlow
- Keras
- NumPy
- Pandas
- Scikit-Learn
- Matplotlib
- Seaborn
- Jupyter Notebook

---

# 📂 Repository Structure

```bash
├── notebooks/
│   └── Regression_Networks_for_Leakage_Detection.ipynb
├── data/
│   └── project_1_data.csv
└── README.md
```

---

# 🔮 Future Improvements

Potential future extensions include:

- Bayesian Neural Networks
- Monte Carlo Dropout for uncertainty estimation
- Physics-informed regression models
- Transformer-based sensor fusion
- Real-time leak localization
- Multi-leak prediction
- Deployment on embedded industrial systems

---

# 📌 Conclusion

This project presents an end-to-end deep learning solution for leak localization using regression networks.

Beyond building an accurate prediction model, the work investigates robust preprocessing techniques, compares automatic and manual gradient computation, and applies Explainable AI through Layer-Wise Relevance Propagation to improve transparency and interpretability.

The project provides both practical implementation experience and a deeper understanding of the mathematical foundations of modern deep learning.

---

# 👨‍💻 Author

**Raj Mahadevwala**

Master's Student – Data Science / AI  
Technical University of Braunschweig

---
