# Learning Probability Density Functions using Roll-Number-Parameterized Non-Linear Model

## 📌 Overview

This project demonstrates learning a probability density function (PDF) from real-world environmental data using a roll-number-parameterized non-linear transformation and Maximum Likelihood Estimation (MLE).

The analysis uses **NO₂ (Nitrogen Dioxide)** concentration data from the *India Air Quality Dataset*.

---

## 🎯 Objective

- Apply a roll-number-based non-linear transformation to NO₂ data  
- Estimate Gaussian distribution parameters (μ, σ, λ, c)  
- Fit and validate the probability density function  
- Visualize empirical vs theoretical distribution  

---

## 🔢 Roll Number Parameterization

For roll number **102316130**, the transformation is:

\[
z = x + a_r \sin(b_r x)
\]

Where:

- \( a_r = 0.05 \times (r \bmod 7) = 0.10 \)
- \( b_r = 0.3 \times (r \bmod 5 + 1) = 0.30 \)

This introduces controlled non-linearity into the dataset.

---

## 📊 Statistical Modeling

The transformed data is modeled using a Gaussian distribution:

\[
\hat{p}(z) = c \, e^{-\lambda (z-\mu)^2}
\]

Parameters are estimated using Maximum Likelihood Estimation:

- **μ** → Mean of transformed data  
- **σ** → Standard deviation  
- **λ = 1/(2σ²)**  
- **c = 1/(σ√(2π))**

---

## 📈 Results

- The transformed NO₂ data approximately follows a normal distribution.  
- Maximum Likelihood Estimation successfully fits the Gaussian model.  
- The non-linear transformation slightly alters the distribution while preserving Gaussian characteristics.  
- Histogram and PDF comparison show a reasonable fit.

---

## 🛠 Tools Used

- Python  
- NumPy  
- Pandas  
- Matplotlib  
- KaggleHub  

---

## ✅ Conclusion

This project demonstrates how real-world environmental data can be transformed and modeled using probabilistic techniques.  

Despite introducing roll-number-based non-linearity, the data remains well-approximated by a Gaussian distribution, validating the robustness of statistical modeling using MLE.

---
