## Normalization of Indicators

In the pursuit of aggregating the financial stability index, numerous indicators contribute to the economy's stability. However, the high multidimensionality of these indicators poses a challenge in capturing their collective impact accurately. To address this, a synthetic index must be derived from these basic indicators. Given that each indicator possesses its unique measurement unit, normalization is typically employed prior to aggregation. This README elucidates and validates the mathematical methodologies utilized to address this challenge effectively. 

## Standard Normal Distribution (Z-score):
The first approach is Standard normal distribution (Z-score) which is a common method used to standardize variables to have a mean of 0 and a standard deviation of 1. This transformation is valuable when dealing with variables that have different units or scales, allowing for comparability and facilitating further statistical analysis. 

#### Characteristics:

- **Mean and Standard Deviation**: The mean  $\( \mu \)$ of the standard normal distribution is 0, and the standard deviation $(\( \sigma \))$ is 1.
  
- **Symmetry**: The standard normal distribution is symmetric about its mean, meaning that the probabilities of observing values to the left and right of the mean are equal.

- **Probability Density Function (PDF)**: The probability density function of the standard normal distribution is given by:

 $$\ f(z) = \frac{1}{\sqrt{2\pi}} e^{-\frac{z^2}{2}} \$$

- **Z-Scores**: A Z-score represents the number of standard deviations a data point is from the mean of its distribution. It is calculated as:

$$\ Z = \frac{X - \mu}{\sigma} \$$

  - $\( X \)$: Observed value.
  - $\( \mu \)$: Mean of the distribution.
  - $\( \sigma \)$: Standard deviation of the distribution.
  - $\( Z \)$: Z-score.

The Z-score transformation assumes that the data follow a normal distribution, which may not always be the case. However, even if the data do not strictly adhere to a normal distribution, the Z-score transformation can still provide valuable insights, particularly when the sample size is large due to the Central Limit Theorem.

The Central Limit Theorem (CLT) is a fundamental concept in statistics that states that the sampling distribution of the sample mean approaches a normal distribution as the sample size increases, regardless of the shape of the population distribution.

Let $\( X_1, X_2, ..., X_n \)$ be a sequence of independent and identically distributed $(i.i.d.)$ random variables with mean $\( \mu \)$ and standard deviation $\( \sigma \)$. The sample mean, denoted by $\( \bar{X} \)$, is given by:

$$ \bar{X} = \frac{1}{n} \sum_{i=1}^{n} X_i $$

According to the Central Limit Theorem:

$$ \lim_{n \to \infty} P\left(\frac{\bar{X} - \mu}{\frac{\sigma}{\sqrt{n}}} \leq x\right) = \Phi(x) $$

Where $\( \Phi(x) \)$ is the cumulative distribution function (CDF) of the standard normal distribution. This equation states that as the sample size $\( n \)$ increases, the standardized sample mean converges in distribution to the standard normal distribution.

It's important to assess the distribution of the data before and after transformation to ensure that extreme values or outliers do not unduly influence the results. Robustness checks, such as sensitivity analysis, can help evaluate the impact of outliers on the analysis.

## Empirical Normalization:

Empirical normalization, also known as sample normalization or min-max scaling, is a technique used to scale numeric data within a specific range. Unlike the standard normal distribution (Z-score), which standardizes data based on the mean and standard deviation of a distribution, empirical normalization rescales data based on its observed minimum and maximum values.

#### Characteristics:

For each data point $\( X \)$ in the dataset, apply the following transformation:
   
   $$\ X_{\text{norm}} = \frac{X - X_{\text{min}}}{X_{\text{max}} - X_{\text{min}}} \$$

   Where:
   - $\( X_{\text{norm}} \)$: Normalized value of $\( X \)$.
   - $\( X \)$: Original data point.
   - $\( X_{\text{min}} \)$: Minimum value of the dataset.
   - $\( X_{\text{max}} \)$: Maximum value of the dataset.

   This transformation scales the data to fall within the range [0, 1].

### Difference from Standard Normal Distribution (Z-Score):

- **Mean and Standard Deviation**: Empirical normalization does not involve mean and standard deviation calculations like the standard normal distribution (Z-score). Instead, it relies solely on the observed minimum and maximum values of the data.

- **Range**: Empirical normalization scales data to a specific range (e.g., [0, 1]), while the standard normal distribution (Z-score) standardizes data to have a mean of 0 and a standard deviation of 1.

- **Use Cases**: Empirical normalization is commonly used when the distribution of the data is unknown or does not follow a normal distribution, whereas the standard normal distribution (Z-score) is used when working with normally distributed data.
