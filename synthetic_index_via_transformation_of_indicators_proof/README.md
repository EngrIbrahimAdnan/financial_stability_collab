## Normalization of Indicators

In the pursuit of aggregating the financial stability index, numerous indicators contribute to the economy's stability. However, the high multidimensionality of these indicators poses a challenge in capturing their collective impact accurately. To address this, a synthetic index must be derived from these basic indicators. Given that each indicator possesses its unique measurement unit, normalization is typically employed prior to aggregation. This README elucidates and validates the mathematical methodologies utilized to address this challenge effectively.

### Central Limit Theorem (CLT) Explanation

The Central Limit Theorem (CLT) is a fundamental concept in statistics that states that the sampling distribution of the sample mean approaches a normal distribution as the sample size increases, regardless of the shape of the population distribution.

#### Mathematical Representation:

Let $\( X_1, X_2, ..., X_n \)$ be a sequence of independent and identically distributed $(i.i.d.)$ random variables with mean $\( \mu \)$ and standard deviation $\( \sigma \)$. The sample mean, denoted by $\( \bar{X} \)$, is given by:

$$ \bar{X} = \frac{1}{n} \sum_{i=1}^{n} X_i $$

According to the Central Limit Theorem:

$$ \lim_{n \to \infty} P\left(\frac{\bar{X} - \mu}{\frac{\sigma}{\sqrt{n}}} \leq x\right) = \Phi(x) $$

Where $\( \Phi(x) \)$ is the cumulative distribution function (CDF) of the standard normal distribution. This equation states that as the sample size $\( n \)$ increases, the standardized sample mean converges in distribution to the standard normal distribution.

#### Examples:

1. **Coin Flipping**: Flipping a fair coin and calculating the average number of heads in each set of flips.
2. **Dice Rolling**: Rolling a fair six-sided die and calculating the average value rolled in each set of rolls.
3. **Height of Students**: Studying the average height of students in a school by taking multiple random samples.

In each case, the Central Limit Theorem applies, showing that the distribution of the sample mean tends towards a normal distribution as the sample size increases.


Got it! Let's include definitions for the parameters used in the Z-score calculation. Here's the updated version:


## Standard Normal Distribution (Z-Score)

The standard normal distribution, often referred to as the Z-distribution or Z-score, is a specific instance of the normal distribution with a mean of 0 and a standard deviation of 1. It serves as a benchmark against which other normal distributions can be compared and standardized.

### Characteristics:

- **Mean and Standard Deviation**: The mean $(\( \mu \))$ of the standard normal distribution is 0, and the standard deviation $(\( \sigma \))$ is 1.
  
- **Symmetry**: The standard normal distribution is symmetric about its mean, meaning that the probabilities of observing values to the left and right of the mean are equal.

- **Probability Density Function (PDF)**: The probability density function of the standard normal distribution is given by:

 $$\[ f(z) = \frac{1}{\sqrt{2\pi}} e^{-\frac{z^2}{2}} \]$$

- **Z-Scores**: A Z-score represents the number of standard deviations a data point is from the mean of its distribution. It is calculated as:

$$\ Z = \frac{X - \mu}{\sigma} \$$

  - $\( X \)$: Observed value.
  - $\( \mu \)$: Mean of the distribution.
  - $\( \sigma \)$: Standard deviation of the distribution.
  - $\( Z \)$: Z-score.

- **Standardization**: Z-scores are used to standardize data from different normal distributions, making them comparable. By converting data points to their respective Z-scores, we can determine how unusual or typical a particular observation is within its distribution.

### Examples:

1. **Example 1: Z-Score Calculation**
   
   Suppose we have a data point $\( X = 68 \)$ from a normal distribution with $\( \mu = 65 \)$ and $\( \sigma = 3 \)$. To calculate the Z-score for this data point:
   
   $$\ Z = \frac{68 - 65}{3} = 1 \$$
   
   So, the Z-score for the data point 68 is 1 standard deviation above the mean.

2. **Example 2: Probability Calculation**
   
   Using a Z-table, we can find the probability of observing a Z-score less than 1.96 (rounded to two decimal places). Consulting the table, we find that the probability is approximately 0.975.

### Z-Table Example:

| Z-Score | Probability (P(Z < z)) |
|---------|------------------------|
| -3.00   | 0.0013                 |
| -2.00   | 0.0228                 |
| -1.96   | 0.0250                 |
| -1.64   | 0.0500                 |
| -1.28   | 0.1003                 |
| -1.00   | 0.1587                 |
|  0.00   | 0.5000                 |
|  1.00   | 0.8413                 |
|  1.28   | 0.8997                 |
|  1.64   | 0.9500                 |
|  1.96   | 0.9750                 |
|  2.00   | 0.9772                 |
|  3.00   | 0.9987                 |

This table shows probabilities associated with various Z-scores under the standard normal distribution.
