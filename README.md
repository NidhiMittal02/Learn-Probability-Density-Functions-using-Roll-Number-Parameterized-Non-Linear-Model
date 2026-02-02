# 📘 Learn Probability Density Functions using Roll-Number-Parameterized Non-Linear Model

---

## 📥 Input Description

### Dataset Input
- **Dataset:** India Air Quality Data  
- **Feature Used:** NO₂ (Nitrogen Dioxide concentration)  
- **Nature of Data:** Continuous-valued environmental measurements  
- **Source:**  
  [India air quality dataset](https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data )

### Roll Number Input
Let **r** be the university roll number.  
The roll number is used to personalize the transformation using modulus operations.

---

## ⚙️ Methodology

The methodology consists of **three main stages**: **Data Transformation → PDF Modeling → Parameter Estimation**.

---

### 🔹 Stage 1: Non-Linear Data Transformation

The raw NO₂ values ($x$) are transformed into a new variable ($z$) using:

$$
z = Tr(x) = x + a_r \sin(b_r x)
$$

Where:

$$
a_r = 0.05 \cdot (r \bmod 7), \quad
b_r = 0.3 \cdot (r \bmod 5 + 1)
$$

**Purpose of the Transformation:**

- Introduces **controlled non-linearity**  
- Ensures **roll-number-based uniqueness**  
- Preserves the **continuous nature** of the data  
- Increases **modeling complexity** for learning  

The transformed variable $z$ remains continuous but exhibits **non-linear variations** compared to $x$.

---

### 🔹 Stage 2: Probability Density Function Modeling

After transformation, the distribution of $z$ is modeled using a Gaussian-based continuous PDF:

$$
\hat{p}(z) = c \cdot e^{-\lambda (z - \mu)^2}
$$

Where:

- $\mu$ → Mean of the distribution  
- $\lambda$ → Precision parameter (inverse of variance)  
- $c$ → Normalization constant  

This is equivalent to a **normal distribution expressed using a precision parameter**.

---

### 🔹 Stage 3: Parameter Estimation (MLE)

The parameters are estimated using **Maximum Likelihood Estimation**:

- **Mean estimation:**  
  μ = (1/N) ∑ z_i

- **Variance estimation:**  
  σ² = (1/N) ∑ (z_i - μ)²

- **Precision parameter:**  
  λ = 1 / (2σ²)

- **Normalization constant (continuous PDF):**  
  c = √(λ / π)


This ensures that the PDF is **properly normalized**, i.e.,

$$
\int_{-\infty}^{\infty} \hat{p}(z) \, dz = 1
$$

Hence, the learned model represents a **valid continuous probabilit**


## 📊 Results

### 🔹 Estimated Parameters

| Parameter | Description | Value |
|---------|------------|-------|
| **μ (mu)** | Mean of transformed data | 22.675341923478776 |
| **λ (lambda)** | Precision parameter | 0.0021294365683539275 |
| **c** | Normalization constant | 0.026034990142274693 |

---

## ✅ Conclusion

This project demonstrates the learning of a **continuous probability density function** from real-world air quality data using a **roll-number-parameterized non-linear transformation**. The parameters learned via **Maximum Likelihood Estimation** successfully define a normalized Gaussian model for the transformed NO₂ feature.

---
