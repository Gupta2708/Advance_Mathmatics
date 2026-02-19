# Learning Probability Density Functions using Roll-Number-Parameterized Non-Linear Model

A Python implementation for learning probability density function parameters from transformed air quality data using Maximum Likelihood Estimation (MLE).

---

## 📌 Overview

This project implements a **roll-number-parameterized non-linear transformation model** to learn probability density function (PDF) parameters.

The analysis uses **NO₂ (Nitrogen Dioxide)** data from the *India Air Quality Dataset* to demonstrate:

- Non-linear data transformation
- Gaussian parameter estimation
- Maximum likelihood estimation
- Probability density function fitting
- Statistical visualization

---

## 🎯 Objectives

1. **Transform Data**  
   Apply a roll-number-parameterized non-linear transformation to NO₂ measurements.

2. **Parameter Learning**  
   Estimate parameters (λ, μ, c) of a Gaussian probability density function.

3. **Statistical Modeling**  
   Use Maximum Likelihood Estimation (MLE) to fit the distribution.

---

## 📂 Dataset

- **Source:** Kaggle – India Air Quality Data  
- **Feature Used:** `no2` (Nitrogen Dioxide concentration levels)
- **Data Type:** Continuous environmental measurements

---

## ⚙️ Methodology

---

### 🔹 Step 1: Non-Linear Transformation

Each NO₂ value \( x \) is transformed into \( z \) using:

\[
z = T_r(x) = x + a_r \sin(b_r x)
\]

Where:

- \( r \) = University Roll Number (**102316130**)
- \( a_r = 0.05 \times (r \bmod 7) \)
- \( b_r = 0.3 \times (r \bmod 5 + 1) \)

### ✅ Calculated Parameters (for r = 102316130)

- \( r \bmod 7 = 2 \)
- \( r \bmod 5 = 0 \)

Therefore:

- **aᵣ = 0.05 × 2 = 0.10**
- **bᵣ = 0.3 × (0 + 1) = 0.30**

So the transformation becomes:

\[
z = x + 0.10 \sin(0.30x)
\]

---

### 🔹 Step 2: Probability Density Function

We assume the transformed variable \( z \) follows a Gaussian distribution:

\[
\hat{p}(z) = c \, e^{-\lambda (z - \mu)^2}
\]

Where:

- \( \mu \) = Mean of transformed data
- \( \sigma \) = Standard deviation
- \( \lambda = \frac{1}{2\sigma^2} \)
- \( c = \frac{1}{\sigma \sqrt{2\pi}} \)

---

### 🔹 Step 3: Maximum Likelihood Estimation

Using sample statistics:

\[
\mu = \frac{1}{n} \sum z_i
\]

\[
\sigma = \sqrt{\frac{1}{n} \sum (z_i - \mu)^2}
\]

Then:

\[
\lambda = \frac{1}{2\sigma^2}
\]

\[
c = \frac{1}{\sigma\sqrt{2\pi}}
\]

These parameters are estimated directly from transformed NO₂ data.

---

## 📊 Visualization

The notebook includes:

- Histogram of transformed data \( z \)
- Overlaid fitted Gaussian PDF
- Visual comparison of empirical vs theoretical distribution

---

## 🧮 Mathematical Form

The standard Gaussian distribution:

\[
\hat{p}(z) = \frac{1}{\sigma\sqrt{2\pi}} \, e^{-\frac{(z-\mu)^2}{2\sigma^2}}
\]

Reparameterized as:

\[
\hat{p}(z) = c \, e^{-\lambda (z-\mu)^2}
\]

Where:

- \( \lambda = \frac{1}{2\sigma^2} \)
- \( c = \frac{1}{\sigma\sqrt{2\pi}} \)

---

## 🛠 Technologies Used

- Python 3
- NumPy
- Pandas
- Matplotlib
- KaggleHub (for dataset download)
- Google Colab Environment

---

## 🚀 Implementation Code

```python
import pandas as pd
import numpy as np
from matplotlib import pyplot as plt
import kagglehub
import os

# Download dataset
path = kagglehub.dataset_download("shrutibhargava94/india-air-quality-data")
file_path = os.path.join(path, "data.csv")

df = pd.read_csv(file_path, encoding="latin1")

# Roll number
r = 102316130

# Compute parameters
ar = 0.05 * (np.mod(r, 7))
br = 0.3 * (np.mod(r, 5) + 1)

# Extract NO2 values
x = df['no2'].dropna().values

# Non-linear transformation
z_df = x + ar * np.sin(br * x)

# Estimate Gaussian parameters
mu = np.mean(z_df)
sigma = np.std(z_df)
lambda_para = 1 / (2 * np.square(sigma))
const = 1 / (sigma * np.sqrt(2 * np.pi))

# Plot
plt.hist(z_df, bins=50, density=True, label='Transformed Data')
x_vals = np.linspace(z_df.min(), z_df.max(), 1000)
y_vals = const * np.exp(-lambda_para * (x_vals - mu)**2)

plt.plot(x_vals, y_vals, label='Fitted PDF')
plt.legend()
plt.show()
```

---

## 📌 Key Observations

- The transformed NO₂ data approximately follows a normal distribution.
- The roll-number-based transformation slightly modifies the shape.
- Maximum likelihood estimation successfully fits a Gaussian model.
- Visual comparison confirms reasonable approximation.

---

## 🎓 Educational Value

This project demonstrates:

- Working with real-world environmental data
- Applying non-linear mathematical transformations
- Maximum Likelihood Estimation (MLE)
- Gaussian distribution modeling
- Data visualization techniques
- Parameterized modeling based on unique identifiers

---

## ✅ Conclusion

The roll-number-parameterized transformation introduces controlled non-linearity into environmental data.  
Despite the transformation, the resulting distribution remains approximately Gaussian, and its parameters can be successfully estimated using MLE.

This demonstrates the robustness of Gaussian modeling in real-world environmental datasets.

---
