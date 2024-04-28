## Normalization of Indicators

In the pursuit of aggregating a financial stability index, numerous indicators typically contribute to the economy's stability. However, the high multidimensionality of these indicators poses a challenge in capturing their collective impact accurately. To address this, a synthetic index must be derived from these basic indicators. Given that each indicator possesses its unique measurement unit, normalization is typically employed prior to aggregation. This README elucidates and validates the mathematical methodologies utilized to address this challenge effectively. 

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

#### Proof:

1. **Mean Centering**:
   
   Subtracting the mean $\( \mu \)$ from each data point $\( X_i \)$ shifts the distribution so that it is centered around 0.

2. **Scaling by Standard Deviation**:

   Dividing by the standard deviation $\( \sigma \)$ scales the data so that the spread (variability) of the distribution is consistent regardless of the original units of measurement.

3. **Preservation of Relative Distances**:

   - **Proof for Mean**: When $\( X = \mu \)$, $\( Z = \frac{\mu - \mu}{\sigma} = 0 \)$. Thus, the mean is correctly mapped to 0.
   
   - **Proof for Standard Deviation**: The spread of the distribution remains consistent as the standard deviation scales all data points by the same factor.
   
   - **Proof for Intermediate Values**: For any intermediate value $\( X_i \)$, the Z-score places it in terms of standard deviations from the mean, preserving the relative distances between data points.

Therefore, the Z-score transformation centers data around the mean and scales it to have a standard deviation of 1, preserving the relative distances between data points.

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

#### Proof:

Let $\( X_1, X_2, ..., X_n \)$ be a dataset with $\( n \)$ observations.

2. **Preservation of Relative Distances**:

   - **Proof for Minimum Value**: When $\( X = X_{\text{min}} \), \( X_{\text{norm}} = \frac{X_{\text{min}} - X_{\text{min}}}{X_{\text{max}} - X_{\text{min}}} = 0 \)$. Thus, the minimum value is correctly mapped to 0.
   
   - **Proof for Maximum Value**: When $\( X = X_{\text{max}} \), \( X_{\text{norm}} = \frac{X_{\text{max}} - X_{\text{min}}}{X_{\text{max}} - X_{\text{min}}} = 1 \)$. Thus, the maximum value is correctly mapped to 1.
   
   - **Proof for Intermediate Values**: For any intermediate value $\( X_i \), \( 0 \leq X_{\text{norm}} \leq 1 \)$, preserving the relative distances between data points.

Therefore, empirical normalization scales data within the range [0, 1] while preserving the relative distances between data points.


## Difference from Standard Normal Distribution (Z-Score):

- **Mean and Standard Deviation**: Empirical normalization does not involve mean and standard deviation calculations like the standard normal distribution (Z-score). Instead, it relies solely on the observed minimum and maximum values of the data.

- **Range**: Empirical normalization scales data to a specific range (e.g., [0, 1]), while the standard normal distribution (Z-score) standardizes data to have a mean of 0 and a standard deviation of 1.

- **Use Cases**: Empirical normalization is commonly used when the distribution of the data is unknown or does not follow a normal distribution, whereas the standard normal distribution (Z-score) is used when working with normally distributed data.


# Financial Stability Index (FSI) Calculation

With the preprocessing steps highlighted, the Financial Stability Index (FSI) which is a synthetic indicator designed to measure the overall financial stability of a country, can be covered. Per the paper "Financial System Stability Index Indonesia", It is formed by aggregating and weighting normalized sub-indices from three composite indices: Banking Soundness Index (BSI), Financial Vulnerability Index (FVI), and Regional Economic Climate Index (RECI).

## Composite Indices
### 1. Banking Soundness Index (BSI)
The BSI comprises five sub-indices representing various aspects of banking soundness:
- Capital Adequacy Ratio
- Asset Quality of Non-Performing Loans
- Liquidity Loans to Deposits Ratio
- Profitability in terms of Return Equity
- Profitability in terms of Net Interest Margin

### 2. Financial Vulnerability Index (FVI)
The FVI consists of eight sub-indices reflecting financial vulnerability indicators:
- Current Account balance to GDP Ratio
- Ratio of Money Supply to Foreign Reserves
- M2 Multiplier
- Debt to GDP Ratio
- Exchange Rate
- IHSG
- Inflation
- Growth GDP National

### 3. Regional Economic Climate Index (RECI)
The RECI includes two sub-indices indicating the regional economic climate:
- Growth GDP for USA
- Growth GDP for ASEAN Countries

## Calculation Methodology
The FSI is calculated using the following steps:

1. **Normalization**:
   Normalize each sub-index within the BSI, FVI, and RECI using either standard normal distribution (Z-score) or empirical normalization.

2. **Weighting**:
   Assign weights to each normalized sub-index to reflect its relative importance in measuring financial stability.

3. **Aggregation**:
   Combine the normalized and weighted sub-indices from each composite index to form a single composite index for financial stability.

4. **Formulation of the Financial Stability Index (FSI)**:
   Combine the composite indices for BSI, FVI, and RECI to form the FSI using a weighted sum approach. Each sub-index is scaled by the reciprocal of the total number of sub-indices within its respective composite index to ensure appropriate weighting.

The formula for calculating the FSI is as follows:

$$\ FSI = \frac{1}{3} \left( \frac{BSI_1 + BSI_2 + ... + BSI_5}{5} \right) + \frac{1}{3} \left( \frac{FVI_1 + FVI_2 + ... + FVI_8}{8} \right) + \frac{1}{3} \left( \frac{RECI_1 + RECI_2}{2} \right) \$$

If we're assigning equal weights to each composite index (i.e., $\( w_1 = w_2 = w_3 = \frac{1}{3} \)$), the relative contributions of each sub-index to the FSI would indeed vary based on the number of sub-indices within each composite index. the number of sub-indices within each composite index will influence their relative contributions to the overall Financial Stability Index (FSI) when considering the weighting scheme. 


   - Finally, validate the Financial Stability Index to ensure that it effectively captures the concept of financial stability and provides meaningful insights. This may involve comparing the FSI with other measures of financial stability, conducting sensitivity analyses, and seeking feedback from experts in the field.

The specific details of normalization, weighting, and aggregation will depend on your data, research objectives, and the context in which you're analyzing financial stability. It's essential to carefully consider these factors and ensure that your methodology is transparent, robust, and aligned with the concept of financial stability.

Here's a simplified example of how you might combine the normalized and weighted sub-indices:

\[ FSI = w_1 \times BSI + w_2 \times FVI + w_3 \times RECI \]

Where:
- \( BSI \), \( FVI \), and \( RECI \) are the normalized composite indices for Banking Soundness, Financial Vulnerability, and Regional Economic Climate, respectively.
- \( w_1 \), \( w_2 \), and \( w_3 \) are the weights assigned to each composite index.

The specific details of normalization, weighting, and aggregation will depend on your data, research objectives, and the context in which you're analyzing financial stability. It's essential to carefully consider these factors and ensure that your methodology is transparent, robust, and aligned with the concept of financial stability.


In this formulation, each sub-index is divided by the total number of sub-indices within its respective composite index to ensure that the weights are appropriately scaled based on the number of indicators.

This approach ensures that the relative contributions of each sub-index to the FSI are adjusted to account for differences in the number of sub-indices within each composite index. However, it's essential to consider whether equal weighting is appropriate or if different weighting schemes should be used based on the perceived importance or relevance of each composite index to the concept of financial stability.


## Validation
Validate the FSI to ensure that it effectively captures the concept of financial stability and provides meaningful insights. Consider comparing the FSI with other measures of financial stability and conducting sensitivity analyses.

## Conclusion
The FSI provides a comprehensive assessment of financial stability by integrating various indicators from multiple domains. It serves as a valuable tool for policymakers, researchers, and stakeholders in monitoring and managing financial stability risks.
