# Problem 1

# Exploring the Central Limit Theorem through Simulations

---

## 1. Introduction

The **Central Limit Theorem (CLT)** is one of the most powerful results in probability theory and statistics. It asserts that, under fairly general conditions, the distribution of the sample mean of a large number of independent and identically distributed (i.i.d.) random variables approaches a **normal distribution**, regardless of the original population’s distribution. Formally, if \( X_1, X_2, \dots, X_n \) are i.i.d. random variables with mean \( \mu \) and finite variance \( \sigma^2 \), then:

$$
\sqrt{n}\left( \frac{\bar{X}_n - \mu}{\sigma} \right) \xrightarrow{d} \mathcal{N}(0,1) \quad \text{as} \quad n \to \infty
$$

where \( \bar{X}_n = \frac{1}{n} \sum_{i=1}^{n} X_i \) is the sample mean.

The CLT underpins many statistical procedures, including hypothesis testing, confidence interval construction, and regression analysis. Despite its theoretical elegance, an intuitive understanding of the CLT is best achieved through **empirical simulation**.

---

## 2. Objectives

This project aims to:
- **Empirically demonstrate** the Central Limit Theorem through simulations.
- **Explore** different population distributions: uniform, exponential, and binomial.
- **Investigate** the effect of sample size and population characteristics (e.g., variance, skewness) on convergence to normality.
- **Discuss** practical applications of the CLT in real-world settings.

---

## 3. Methodology

We proceed through the following stages:
- **Population Generation**: Simulate large populations from specified distributions.
- **Sampling**: Randomly sample data and compute sample means.
- **Visualization**: Plot histograms and kernel density estimates (KDE) of sampling distributions.
- **Analysis**: Explore convergence behavior and practical implications.

### 3.1 Libraries and Environment Setup

```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import norm, skew, kurtosis

# Ensure reproducibility
np.random.seed(42)

# Plotting style
sns.set(style="whitegrid")
```

---

## 4. Population Distributions

We examine the CLT using the following population distributions:

| Distribution        | Characteristics                                |
|----------------------|------------------------------------------------|
| Uniform(0,1)         | Symmetric, bounded, finite variance            |
| Exponential(λ=1)     | Highly skewed, infinite support, finite variance |
| Binomial(n=10, p=0.5)| Discrete, symmetric if \(p=0.5\), finite variance |

### 4.1 Population Generation

```python
# Generate large populations (size = 100,000)
population_size = 100_000

population_uniform = np.random.uniform(0, 1, population_size)
population_exponential = np.random.exponential(1, population_size)
population_binomial = np.random.binomial(n=10, p=0.5, size=population_size)
```

---

## 5. Sampling and Simulation

To observe the CLT, we sample from each population:
- **Sample Sizes**: \( n = 5, 10, 30, 50, 100 \)
- **Repetitions**: 5000 times per sample size.

### 5.1 Sampling Function

```python
def simulate_sample_means(population, sample_sizes, num_samples=5000):
    """
    Simulates the distribution of sample means for a given population.
    
    Args:
    - population (np.array): The full population to sample from.
    - sample_sizes (list of int): Different sample sizes to test.
    - num_samples (int): Number of repetitions per sample size.
    
    Returns:
    - dict: Keys are sample sizes; values are arrays of sample means.
    """
    results = {}
    for size in sample_sizes:
        means = [np.mean(np.random.choice(population, size, replace=False)) for _ in range(num_samples)]
        results[size] = np.array(means)
    return results

sample_sizes = [5, 10, 30, 50, 100]

sampling_uniform = simulate_sample_means(population_uniform, sample_sizes)
sampling_exponential = simulate_sample_means(population_exponential, sample_sizes)
sampling_binomial = simulate_sample_means(population_binomial, sample_sizes)
```

---

## 6. Visualization

### 6.1 Plotting Function

```python
def plot_distributions(sampling_results, population_name):
    """
    Plots histograms and KDEs for different sample sizes.
    
    Args:
    - sampling_results (dict): Sample means organized by sample size.
    - population_name (str): Title for plots.
    """
    fig, axes = plt.subplots(1, len(sampling_results), figsize=(24, 4))
    
    for ax, (size, means) in zip(axes, sampling_results.items()):
        sns.histplot(means, kde=True, stat="density", ax=ax, bins=30, color='skyblue', edgecolor='black')
        ax.set_title(f'Sample Size = {size}')
        ax.set_xlabel('Sample Mean')
        ax.set_ylabel('Density')
        
        # Overlay normal distribution for comparison
        mu, std = np.mean(means), np.std(means)
        x = np.linspace(mu - 4*std, mu + 4*std, 100)
        ax.plot(x, norm.pdf(x, mu, std), 'r--', label="Normal PDF")
        ax.legend()
        
    plt.suptitle(f'Sampling Distributions from {population_name}', fontsize=18)
    plt.tight_layout()
    plt.show()

# Plot results
plot_distributions(sampling_uniform, "Uniform(0,1)")
plot_distributions(sampling_exponential, "Exponential(λ=1)")
plot_distributions(sampling_binomial, "Binomial(n=10, p=0.5)")
```

---

## 7. Analytical Discussion

### 7.1 Convergence Behavior

- **Uniform Distribution**:  
  Being symmetric and bounded, convergence is very rapid. Even for small samples (\(n=5\)), the sampling distribution appears approximately normal.

- **Exponential Distribution**:  
  Strongly right-skewed; convergence is slower. Noticeable skewness persists at small sample sizes but diminishes as \(n\) increases.

- **Binomial Distribution**:  
  Since \(n=10\) and \(p=0.5\), the binomial distribution is already fairly symmetric, leading to relatively fast convergence.

### 7.2 Quantitative Analysis: Skewness and Kurtosis

We compute skewness and kurtosis to quantify convergence:

```python
def compute_statistics(sampling_results):
    stats = []
    for size, means in sampling_results.items():
        stats.append({
            "Sample Size": size,
            "Mean": np.mean(means),
            "Variance": np.var(means),
            "Skewness": skew(means),
            "Kurtosis": kurtosis(means)
        })
    return stats

import pandas as pd

# Display results
df_uniform = pd.DataFrame(compute_statistics(sampling_uniform))
df_exponential = pd.DataFrame(compute_statistics(sampling_exponential))
df_binomial = pd.DataFrame(compute_statistics(sampling_binomial))

print("Uniform Distribution Sampling Statistics:\n", df_uniform, "\n")
print("Exponential Distribution Sampling Statistics:\n", df_exponential, "\n")
print("Binomial Distribution Sampling Statistics:\n", df_binomial)
```

- **Skewness** measures asymmetry; CLT suggests skewness should decrease with sample size.
- **Kurtosis** measures "tailedness"; convergence implies kurtosis approaches that of the normal distribution (kurtosis ≈ 0 after adjustment).

---

## 8. Practical Applications

The CLT underlies numerous real-world methodologies:

| Application Area             | Example                                                              |
|-------------------------------|----------------------------------------------------------------------|
| Estimation of Parameters      | Estimating average height of a population from a sample             |
| Quality Control               | Monitoring average defect rates in manufacturing processes         |
| Finance and Risk Management   | Modeling average returns of stock portfolios                       |
| Medical Research              | Analyzing average treatment effects across clinical trial samples  |
| Machine Learning              | Cross-validation averaging across folds assumes approximate normality |

**Example 1**:  
In a factory, engineers monitor the **average diameter** of manufactured bolts. Although individual bolt diameters may not be normally distributed, the average diameter across multiple samples follows a normal distribution, enabling **control charts** and **process capability analysis**.

**Example 2**:  
In finance, analysts model the **mean returns** of assets. Even though individual returns may be heavy-tailed, the average return over many days can be treated as normal for purposes like **Value-at-Risk (VaR)** computation.

---

## 9. Conclusion

Through extensive simulations, we have verified the fundamental predictions of the **Central Limit Theorem**:
- Regardless of the underlying distribution, the sample mean tends toward a normal distribution as sample size increases.
- Heavily skewed distributions (e.g., exponential) require larger samples for normality to emerge.
- The variance of the sampling distribution decreases with sample size, following \( \sigma_{\bar{X}}^2 = \sigma^2 / n \).

These results affirm the practical value of the CLT in statistics, data science, finance, manufacturing, medicine, and numerous other fields where inference from sample data is necessary.

---

# References
- Casella, G., & Berger, R. L. (2002). *Statistical Inference* (2nd ed.). Duxbury Press.
- Wasserman, L. (2004). *All of Statistics: A Concise Course in Statistical Inference*. Springer.
- Rice, J. A. (2006). *Mathematical Statistics and Data Analysis* (3rd ed.). Cengage Learning.

---

Would you like me also to prepare:
- 📘 A **ready-to-use Jupyter Notebook** (.ipynb)?
- 📈 A **PDF export** of the full Markdown + output?
- 🎥 An **animated visualization** (GIF/video) showing how distributions evolve as sample size grows?

Let me know! 🚀