# Variance and Covariance

> In statistics, we often use uppercase letters (e.g., $X$) to denote a **random variable**, which represents the abstract concept or process being measured (like the height of a person). Lowercase letters with an index (e.g., $x_i$) represent the specific **observations** or actual data points collected for that variable (e.g., $x_1 = 175\text{cm}$, $x_2 = 182\text{cm}$, etc.). While this document will primarily use the lowercase notation for calculations, it is helpful to remember this distinction.

## Why Variance and Covariance Matter: A Foundation for Data Understanding

Variance and covariance are more than just statistical formulas; they are fundamental building blocks in statistics, data science, and quantitative analysis, offering profound insights into the nature of data. Mastering these concepts is indispensable for anyone working with data.

*   **Quantifying Uncertainty and Dispersion (Variance & Standard Deviation):**
    Variance, and its more interpretable cousin, standard deviation, quantify the spread, dispersion, or volatility of a single variable. This is critical in diverse fields for:
    *   **Finance:** Measuring the risk or volatility of an investment portfolio.
    *   **Quality Control:** Assessing the consistency and precision of a manufacturing process to ensure product standards.
    *   **Scientific Research:** Understanding the inherent variability within experimental results and the reliability of measurements.
    *   **Sports Analytics:** Evaluating the consistency of athlete performance.
    *   **Machine Learning:** Informing feature scaling, understanding data distribution for model assumptions, and anomaly detection.

*   **Revealing Relationships and Dependencies (Covariance & Correlation):**
    Covariance and its standardized counterpart, the correlation coefficient, quantify how two variables move together. This understanding is vital for:
    *   **Economics:** Analyzing the relationship between economic indicators like interest rates and inflation, or supply and demand.
    *   **Healthcare:** Investigating associations between lifestyle factors (e.g., diet, exercise) and health outcomes (e.g., disease incidence).
    *   **Portfolio Management:** Diversifying investments by selecting assets with low or negative covariance to reduce overall risk.
    *   **Predictive Modeling:** Identifying influential features in regression analysis, understanding multicollinearity, and building more robust predictive models.
    *   **Social Sciences:** Studying how different demographic factors relate to social behaviors or outcomes.

These measures form the bedrock for more advanced statistical concepts, including hypothesis testing, confidence intervals, linear regression, principal component analysis (PCA), factor analysis, and time series modeling. A deep understanding of variance and covariance empowers analysts to make informed decisions, draw valid conclusions, and build effective models from data.

---

## Mean (Average)

Before diving into variance and covariance, we need to understand the concept of the mean, also known as the average. The mean is a measure of central tendency, representing the typical value in a dataset.

For a set of $N$ data points (observations) $x_1, x_2, \ldots, x_N$:

**Population Mean ($\mu$)**: If we have the entire population, the mean is calculated as the sum of all observations divided by the number of observations.

$$\mu = \frac{\sum_{i=1}^{N} x_i}{N}$$

**Sample Mean ($\bar{x}$)**: If we have a sample from a larger population, the sample mean is calculated similarly.

$$\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n}$$

where $n$ is the number of observations in the sample.

### Example: Calculating the Mean

Let's consider a small dataset of daily high temperatures (in Celsius) for a particular week: $x = \{20, 22, 19, 23, 21, 20, 24\}$.

**Calculation Steps:**

1.  **Sum of observations:** $\sum_{i=1}^{7} x_i = 20 + 22 + 19 + 23 + 21 + 20 + 24 = 149$
2.  **Number of observations:** $N = 7$ (if we consider this the entire population of temperatures for *that specific week*) or $n = 7$ (if this is a sample from a larger set of daily temperatures).

**Population Mean ($\mu$):**
If this represents the entire population of interest (e.g., the high temperatures for *that exact week*), the population mean is:
$$\mu = \frac{\sum_{i=1}^{N} x_i}{N} = \frac{149}{7} \approx 21.286 \text{ C}$$

**Sample Mean ($\bar{x}$):**
If we treat these 7 days as a *sample* drawn from a larger population (e.g., temperatures throughout a whole month or season), the sample mean is calculated identically:
$$\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n} = \frac{149}{7} \approx 21.286 \text{ C}$$
In this specific numerical example, the result for population and sample mean is the same because the calculation formula is identical. The distinction lies in the statistical context of whether the data represents the *entire* group or a *subset*.

---

## Variance

Variance is a measure of how spread out a set of data is. It quantifies the average of the squared differences from the mean. A high variance indicates that data points are spread far from the mean and from each other, while a low variance indicates that data points are clustered closely around the mean.

Why squared differences?
* **To avoid cancellation:** If we just summed the deviations $(x_i - \mu)$, positive and negative deviations would cancel out, potentially leading to a sum of zero even for widely dispersed data.
* **To penalize larger deviations more:** Squaring exaggerates larger differences, giving more weight to data points that are further from the mean.

**Units of Variance:**

It's crucial to note that variance is always expressed in **squared units** of the original data. For example, if your data points represent measurements in meters (m), the variance will be in square meters ($m^2$). This squaring often makes variance less intuitive for direct interpretation in the context of the original measurements, which naturally leads us to the standard deviation.

### Standard Deviation

While variance provides a numerical value for data spread, its squared units can be difficult to relate directly to the original data. The **standard deviation** is defined as the **square root of the variance** and is expressed in the **same units** as the original data. This makes it a much more interpretable, intuitive, and widely used measure of data dispersion.

*   A **low standard deviation** indicates that data points tend to be clustered closely around the mean, implying high consistency or low variability.
*   A **high standard deviation** indicates that data points are spread out over a wider range of values, implying greater variability or dispersion.

#### Population Standard Deviation ($\sigma$)

The population standard deviation is the square root of the population variance. It is typically denoted by the lowercase Greek letter sigma ($\sigma$).

$$\sigma = \sqrt{\sigma^2} = \sqrt{\frac{\sum_{i=1}^{N} (x_i - \mu)^2}{N}}$$

#### Sample Standard Deviation ($s$)

The sample standard deviation is the square root of the sample variance. It is typically denoted by the lowercase Latin letter $s$.

$$s = \sqrt{s^2} = \sqrt{\frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n-1}}$$

### Population Variance ($\sigma^2$)

The population variance is the true variance of an entire population. The population variance is the average of the squared differences between each data point and the population mean.

For a population with $N$ data points $x_1, x_2, \ldots, x_N$ and population mean $\mu$:

1.  **Calculate the deviation of each data point from the mean**: $(x_i - \mu)$
2.  **Square each deviation**: $(x_i - \mu)^2$
3.  **Sum all the squared deviations**: $\sum_{i=1}^{N} (x_i - \mu)^2$
4.  **Divide by the total number of data points ($N$) to find the average squared deviation**:

Thus, the formula for population variance is:

$$\sigma^2 = \frac{\sum_{i=1}^{N} (x_i - \mu)^2}{N}$$

**Alternative Form (Computational Formula)**:

So, here is our main formula:

$$\sigma^2 = \frac{\sum_{i=1}^{N} (x_i - \mu)^2}{N}$$

Expand the squared term:

$$\sigma^2 = \frac{1}{N} \sum_{i=1}^{N} (x_i^2 - 2x_i\mu + \mu^2)$$

Distribute the summation:

$$\sigma^2 = \frac{1}{N} \left( \sum_{i=1}^{N} x_i^2 - \sum_{i=1}^{N} 2x_i\mu + \sum_{i=1}^{N} \mu^2 \right)$$

Pull constants out of the summation:

$$\sigma^2 = \frac{1}{N} \left( \sum_{i=1}^{N} x_i^2 - 2\mu \sum_{i=1}^{N} x_i + N\mu^2 \right)$$

Recall that $\mu = \frac{\sum_{i=1}^{N} x_i}{N}$, which means $\sum_{i=1}^{N} x_i = N\mu$. Substitute this into the equation:

$$\sigma^2 = \frac{1}{N} \left( \sum_{i=1}^{N} x_i^2 - 2\mu (N\mu) + N\mu^2 \right)$$

$$\sigma^2 = \frac{1}{N} \left( \sum_{i=1}^{N} x_i^2 - 2N\mu^2 + N\mu^2 \right)$$

$$\sigma^2 = \frac{1}{N} \left( \sum_{i=1}^{N} x_i^2 - N\mu^2 \right)$$

$$\sigma^2 = \frac{\sum_{i=1}^{N} x_i^2}{N} - \mu^2$$

This is a convenient form often used for calculation.

### Sample Variance ($s^2$)

When we work with a sample from a larger population, we use sample variance to estimate the population variance.

The sample variance is an estimate of the population variance, calculated using the squared differences from the sample mean, divided by $n-1$.

**Derivation of the Formula**:

If we were to use $n$ in the denominator for sample variance, like we did for population variance, our estimate would consistently be *underestimated*. This is because the sample mean ($\bar{x}$) is calculated from the sample itself, and it will always be closer to the sample data points than the true population mean ($\mu$) would be. This makes the sum of squared deviations from $\bar{x}$ smaller than the sum of squared deviations from $\mu$.

To correct for this bias and provide an **unbiased estimator** of the population variance, we divide by $n-1$, which is known as **Bessel's correction**. The term $n-1$ represents the **degrees of freedom**. We lose one degree of freedom because we used the sample mean ($\bar{x}$) (which is derived from the sample data) in the calculation.

So, for a sample with $n$ data points $x_1, x_2, \ldots, x_n$ and sample mean $\bar{x}$:

1.  **Calculate the deviation of each data point from the sample mean**: $(x_i - \bar{x})$
2.  **Square each deviation**: $(x_i - \bar{x})^2$
3.  **Sum all the squared deviations**: $\sum_{i=1}^{n} (x_i - \bar{x})^2$
4.  **Divide by $n-1$**:

Thus, the formula for sample variance is:

$$s^2 = \frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n-1}$$

**Alternative Form (Computational Formula)**:

Similar to population variance, we can derive an alternative form:

$$s^2 = \frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n-1}$$

Expand the squared term:

$$s^2 = \frac{1}{n-1} \sum_{i=1}^{n} (x_i^2 - 2x_i\bar{x} + \bar{x}^2)$$

Distribute the summation:

$$s^2 = \frac{1}{n-1} \left( \sum_{i=1}^{n} x_i^2 - 2\bar{x} \sum_{i=1}^{n} x_i + \sum_{i=1}^{n} \bar{x}^2 \right)$$

Recall that $\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n}$, which means $\sum_{i=1}^{n} x_i = n\bar{x}$. Substitute this into the equation:

$$s^2 = \frac{1}{n-1} \left( \sum_{i=1}^{n} x_i^2 - 2\bar{x} (n\bar{x}) + n\bar{x}^2 \right)$$

$$s^2 = \frac{1}{n-1} \left( \sum_{i=1}^{n} x_i^2 - 2n\bar{x}^2 + n\bar{x}^2 \right)$$

$$s^2 = \frac{1}{n-1} \left( \sum_{i=1}^{n} x_i^2 - n\bar{x}^2 \right)$$

This is another common form for calculation.

### Example: Calculating Variance and Standard Deviation

Let's use the same dataset of daily high temperatures (in Celsius) from our mean example: $x = \{20, 22, 19, 23, 21, 20, 24\}$.
We calculated the mean $\mu \approx \bar{x} \approx 21.286 \, ^{\circ}\text{C}$.

#### Step-by-step Calculation using Definitional Formula:

| $x_i$ | $(x_i - \bar{x})$ | $(x_i - \bar{x})^2$ |
| :---- | :---------------- | :------------------ |
| 20    | $20 - 21.286 = -1.286$ | $(-1.286)^2 \approx 1.654$ |
| 22    | $22 - 21.286 = 0.714$  | $(0.714)^2 \approx 0.510$  |
| 19    | $19 - 21.286 = -2.286$ | $(-2.286)^2 \approx 5.226$ |
| 23    | $23 - 21.286 = 1.714$  | $(1.714)^2 \approx 2.938$  |
| 21    | $21 - 21.286 = -0.286$ | $(-0.286)^2 \approx 0.082$ |
| 20    | $20 - 21.286 = -1.286$ | $(-1.286)^2 \approx 1.654$ |
| 24    | $24 - 21.286 = 2.714$  | $(2.714)^2 \approx 7.366$  |
|       | **Sum:** $\approx 0$ | **Sum of Squared Deviations:** $\sum (x_i - \bar{x})^2 \approx 19.43$ |

*Note: Slight difference in sum of squared deviations compared to previous calculation due to carrying more decimal places for the mean.*

#### Population Variance ($\sigma^2$) and Standard Deviation ($\sigma$)

If this dataset represents the entire population ($N=7$):

$$\sigma^2 = \frac{\sum_{i=1}^{N} (x_i - \mu)^2}{N} = \frac{19.43}{7} \approx 2.776 \, ^{\circ}\text{C}^2$$

$$\sigma = \sqrt{2.776} \approx 1.666 \, ^{\circ}\text{C}$$

#### Sample Variance ($s^2$) and Standard Deviation ($s$)

If this dataset is a sample from a larger population ($n=7$):

$$s^2 = \frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n-1} = \frac{19.43}{7-1} = \frac{19.43}{6} \approx 3.283 \, ^{\circ}\text{C}^2$$

$$s = \sqrt{3.283} \approx 1.812 \, ^{\circ}\text{C}$$

Notice that the sample variance and standard deviation are slightly larger than their population counterparts due to Bessel's correction, providing an unbiased estimate.

### Interpretation and Limitations of Variance and Standard Deviation

*   **Interpretation of Magnitude:** A larger variance or standard deviation signifies greater variability or dispersion in the data. For instance, a high standard deviation in daily stock returns implies greater volatility and risk, whereas a low standard deviation in manufactured product weights suggests high precision and consistent quality.
*   **Units and Intuition:** Standard deviation is in the original units, making it directly comparable to the mean. This allows for more intuitive statements like "most data points fall within $\pm 1$ standard deviation of the mean" (especially true for normally distributed data), which is crucial for constructing confidence intervals and understanding data distribution.
*   **Sensitivity to Outliers:** Both variance and standard deviation involve squaring deviations. This mathematical property means they are highly sensitive to outliers. A single extreme value can disproportionately inflate these measures, potentially misrepresenting the spread of the majority of the data.
*   **Comparison:** Standard deviation is generally preferred over variance for describing the spread of data because its units align with the data itself, making it more intuitive and practical for direct interpretation and communication. Variance, however, is mathematically more convenient for certain theoretical derivations and statistical tests (e.g., ANOVA).
*   **Relationship to Moments:** For advanced readers, variance is formally the **second central moment** of a probability distribution, providing a fundamental measure of the distribution's spread around its mean.

<p><img src="https://upload.wikimedia.org/wikipedia/commons/f/f9/Comparison_standard_deviations.svg" alt="Comparison standard deviations.svg" height="453" width="612">
<br>
Fig. Example of samples from two populations with the same mean but different variances. The red population has mean 100 and variance 100 (SD=10) while the blue population has mean 100 and variance 2500 (SD=50) where SD stands for Standard Deviation.
By <a href="https://commons.wikimedia.org/w/index.php?title=User:JRBrown&amp;action=edit&amp;redlink=1" class="new" title="User:JRBrown (page does not exist)">JRBrown</a> - <span class="int-own-work" lang="en">Own work</span>, Public Domain, <a href="https://commons.wikimedia.org/w/index.php?curid=10777712">Link</a>. <a href="https://en.wikipedia.org/wiki/Variance">Wikipedia</a></p>

### Properties of Variance

Understanding the mathematical properties of variance can simplify calculations and provide deeper insight into its behavior.

Let $X$ be a random variable and $a$ and $b$ be constants.

1.  **Variance of a Constant**: The variance of a constant is zero. A constant does not vary, so its spread is zero.

    $$Var(a) = 0$$

2.  **Non-Negativity**: Variance is always non-negative. Since it is an average of squared values, it cannot be negative.

    $$Var(X) \ge 0$$

3.  **Effect of a Constant Multiplier**: If you scale a random variable by a constant $a$, the variance is scaled by $a^2$.

    $$Var(aX) = a^2 Var(X)$$

    *This is because the deviation from the mean $(ax_i - a\mu)$ becomes $a(x_i - \mu)$, and squaring this term gives $a^2(x_i - \mu)^2$.*

4.  **Effect of an Added Constant**: Adding a constant to every data point shifts the mean by that constant, but it does not change the spread of the data. The variance remains unchanged.

    $$Var(X + b) = Var(X)$$

5.  **Variance of a Sum of *Independent* Random Variables**: If two random variables $X$ and $Y$ are independent, the variance of their sum is the sum of their variances.

    $$Var(X + Y) = Var(X) + Var(Y)$$

---

## Covariance

While variance measures the spread of a single variable, **covariance** measures the **joint variability** of two random variables. In other words, it tells us how two variables change together.

* **Positive Covariance**: Indicates that the two variables tend to move in the same direction. If one increases, the other tends to increase; if one decreases, the other tends to decrease.
* **Negative Covariance**: Indicates that the two variables tend to move in opposite directions. If one increases, the other tends to decrease.
* **Covariance close to zero**: Suggests there is no strong linear relationship between the two variables. (Note: Zero covariance does not necessarily mean independence, only that there's no *linear* relationship.)

### Population Covariance ($\text{Cov}(X, Y)$ or $\sigma_{XY}$)

The population covariance is the true covariance between two variables for an entire population.

The population covariance is the average of the products of the deviations of each variable from their respective means.

Let $X = \{x_1, x_2, \ldots, x_N\}$ and $Y = \{y_1, y_2, \ldots, y_N\}$ be two sets of data points for a population, with population means $\mu_X$ and $\mu_Y$ respectively.

1.  **Calculate the deviation of each $x$ data point from its mean**: $(x_i - \mu_X)$
2.  **Calculate the deviation of each $y$ data point from its mean**: $(y_i - \mu_Y)$
3.  **Multiply the corresponding deviations**: $(x_i - \mu_X)(y_i - \mu_Y)$
4.  **Sum all these products**: $\sum_{i=1}^{N} (x_i - \mu_X)(y_i - \mu_Y)$
5.  **Divide by the total number of data points ($N$) to find the average product of deviations**:

Thus, the formula for population covariance is:

$$\text{Cov}(X, Y) = \sigma_{XY} = \frac{\sum_{i=1}^{N} (x_i - \mu_X)(y_i - \mu_Y)}{N}$$

**Alternative Form (Computational Formula)**:

$$\text{Cov}(X, Y) = \frac{1}{N} \sum_{i=1}^{N} (x_i - \mu_X)(y_i - \mu_Y)$$

Expand the product:

$$\text{Cov}(X, Y) = \frac{1}{N} \sum_{i=1}^{N} (x_i y_i - x_i \mu_Y - y_i \mu_X + \mu_X \mu_Y)$$

Distribute the summation:

$$\text{Cov}(X, Y) = \frac{1}{N} \left( \sum_{i=1}^{N} x_i y_i - \sum_{i=1}^{N} x_i \mu_Y - \sum_{i=1}^{N} y_i \mu_X + \sum_{i=1}^{N} \mu_X \mu_Y \right)$$

Pull constants out of the summation:

$$\text{Cov}(X, Y) = \frac{1}{N} \left( \sum_{i=1}^{N} x_i y_i - \mu_Y \sum_{i=1}^{N} x_i - \mu_X \sum_{i=1}^{N} y_i + N\mu_X \mu_Y \right)$$

Recall that $\sum_{i=1}^{N} x_i = N\mu_X$ and $\sum_{i=1}^{N} y_i = N\mu_Y$. Substitute these:

$$\text{Cov}(X, Y) = \frac{1}{N} \left( \sum_{i=1}^{N} x_i y_i - \mu_Y (N\mu_X) - \mu_X (N\mu_Y) + N\mu_X \mu_Y \right)$$

$$\text{Cov}(X, Y) = \frac{1}{N} \left( \sum_{i=1}^{N} x_i y_i - N\mu_X \mu_Y - N\mu_X \mu_Y + N\mu_X \mu_Y \right)$$

$$\text{Cov}(X, Y) = \frac{1}{N} \left( \sum_{i=1}^{N} x_i y_i - N\mu_X \mu_Y \right)$$

$$\text{Cov}(X, Y) = \frac{\sum_{i=1}^{N} x_i y_i}{N} - \mu_X \mu_Y$$

<p><img src="https://upload.wikimedia.org/wikipedia/commons/a/a0/Covariance_trends.svg" alt="Covariance trends.svg" height="800" width="266.7">
<br>
Fig. The sign of the covariance of two random variables X and Y.
By <a href="https://commons.wikimedia.org/wiki/User:Cmglee" title="User:Cmglee">Cmglee</a>, <a href="https://creativecommons.org/licenses/by-sa/4.0" title="Creative Commons Attribution-Share Alike 4.0">CC BY-SA 4.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=90452334">Link</a>. <a href="https://en.wikipedia.org/wiki/Covariance">Wikipedia</a></p>

### Sample Covariance ($s_{XY}$)

When working with a sample from a larger population, we use sample covariance to estimate the population covariance.

The sample covariance is an estimate of the population covariance, calculated using the products of the deviations from the sample means, divided by $n-1$.

Similar to sample variance, we use $n-1$ in the denominator to provide an unbiased estimate of the population covariance.

For a sample with $n$ pairs of data points $(x_1, y_1), (x_2, y_2), \ldots, (x_n, y_n)$, and sample means $\bar{x}$ and $\bar{y}$:

1.  **Calculate the deviation of each $x$ data point from its sample mean**: $(x_i - \bar{x})$
2.  **Calculate the deviation of each $y$ data point from its sample mean**: $(y_i - \bar{y})$
3.  **Multiply the corresponding deviations**: $(x_i - \bar{x})(y_i - \bar{y})$
4.  **Sum all these products**: $\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})$
5.  **Divide by $n-1$**:

Thus, the formula for sample covariance is:

$$s_{XY} = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{n-1}$$

**Alternative Form (Computational Formula)**:

$$s_{XY} = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})$$

Expand the product:

$$s_{XY} = \frac{1}{n-1} \sum_{i=1}^{n} (x_i y_i - x_i \bar{y} - y_i \bar{x} + \bar{x}\bar{y})$$

Distribute the summation:

$$s_{XY} = \frac{1}{n-1} \left( \sum_{i=1}^{n} x_i y_i - \sum_{i=1}^{n} x_i \bar{y} - \sum_{i=1}^{n} y_i \bar{x} + \sum_{i=1}^{n} \bar{x}\bar{y} \right)$$

Pull constants out of the summation:

$$s_{XY} = \frac{1}{n-1} \left( \sum_{i=1}^{n} x_i y_i - \bar{y} \sum_{i=1}^{n} x_i - \bar{x} \sum_{i=1}^{n} y_i + n\bar{x}\bar{y} \right)$$

Recall that $\sum_{i=1}^{n} x_i = n\bar{x}$ and $\sum_{i=1}^{n} y_i = n\bar{y}$. Substitute these:

$$s_{XY} = \frac{1}{n-1} \left( \sum_{i=1}^{n} x_i y_i - \bar{y} (n\bar{x}) - \bar{x} (n\bar{y}) + n\bar{x}\bar{y} \right)$$

$$s_{XY} = \frac{1}{n-1} \left( \sum_{i=1}^{n} x_i y_i - n\bar{x}\bar{y} - n\bar{x}\bar{y} + n\bar{x}\bar{y} \right)$$

$$s_{XY} = \frac{1}{n-1} \left( \sum_{i=1}^{n} x_i y_i - n\bar{x}\bar{y} \right)$$

### Correlation Coefficient (Pearson's r)

The units of covariance are the product of the units of the two variables involved. For example, if variable $X$ is measured in kilograms (kg) and variable $Y$ in centimeters (cm), then $\text{Cov}(X,Y)$ will be in $\text{kg} \cdot \text{cm}$. This property makes the *magnitude* of covariance difficult to interpret on its own, as it depends entirely on the scales and units of $X$ and $Y$. It prevents direct comparison of the strength of relationships across different datasets or variable pairs. This limitation leads us to a more standardized measure: the correlation coefficient.

While covariance effectively indicates the *direction* (positive, negative, or none) of a linear relationship between two variables, its unstandardized magnitude makes it difficult to assess the *strength* of that relationship. The **Pearson Correlation Coefficient (or Pearson's r)** is a standardized version of covariance that measures both the **strength** and **direction** of a *linear* relationship between two variables.

The Pearson correlation coefficient always ranges between -1 and +1, making it universally interpretable:

*   **+1:** Indicates a perfect positive linear relationship. As one variable increases, the other increases proportionally.
*   **-1:** Indicates a perfect negative linear relationship. As one variable increases, the other decreases proportionally.
*   **0:** Indicates no linear relationship between the two variables. This is a crucial point: it does not necessarily mean there is *no* relationship at all, just no *linear* one.

Pearson's correlation coefficient is the covariance of the two variables divided by the product of their standard deviations.

#### Population Correlation Coefficient ($\rho$)

The population correlation coefficient, denoted by the lowercase Greek letter rho ($\rho$), is calculated by dividing the population covariance by the product of the population standard deviations of the two variables. This normalization process removes the units and standardizes the measure.

$$\rho_{XY} = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y} = \frac{\sigma_{XY}}{\sigma_X \sigma_Y}$$

#### Sample Correlation Coefficient ($r$)

The sample correlation coefficient, denoted by the lowercase Latin letter $r$, is calculated similarly, using sample covariance and sample standard deviations.

$$r_{XY} = \frac{s_{XY}}{s_X s_Y}$$

We will review Pearson's correlation coefficient and other correlation coefficients in a separate lecture.

<p><img src="https://upload.wikimedia.org/wikipedia/commons/d/d4/Correlation_examples2.svg" alt="Correlation examples2.svg" height="300" width="656.7">
<br>
Fig. Several sets of (x, y) points, with the Pearson correlation coefficient of x and y for each set. The correlation reflects the strength and direction of a linear relationship (top row), but not the slope of that relationship (middle row), nor many aspects of nonlinear relationships (bottom row). N.B.: the figure in the center has a slope of 0 but in that case the correlation coefficient is undefined because the variance of Y is zero.
By <a href="https://commons.wikimedia.org/w/index.php?title=User:DenisBoigelot&amp;action=edit&amp;redlink=1" class="new" title="User:DenisBoigelot (page does not exist)">DenisBoigelot</a>, <a href="https://creativecommons.org/publicdomain/zero/1.0/deed.en" title="Creative Commons Zero, Public Domain Dedication">CC0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=15165296">Link</a>. <a href="https://en.wikipedia.org/wiki/Pearson_correlation_coefficient">Wikipedia</a></p>

### Interpretation and Limitations of Covariance and Correlation

*   **Direction vs. Strength:** Covariance indicates the *direction* of a linear relationship (positive, negative, or none). Correlation, being standardized, indicates both the *direction* and the *strength* of a linear relationship (from -1 to +1). Correlation is generally preferred for assessing strength because its value is bounded and unitless.
*   **Units and Comparability:** Covariance has units that are the product of the units of the two variables, making its magnitude difficult to interpret or compare across different datasets. Correlation is unitless, making it universally comparable and interpretable.
*   **Linear Relationships Only:** Both covariance and Pearson's correlation coefficient only measure the *linear* association between variables. A correlation coefficient close to zero does not imply the absence of *any* relationship, only the absence of a *linear* one. Strong non-linear relationships (e.g., parabolic, exponential, cyclical) will yield low Pearson correlation coefficients. For such cases, other measures like **Spearman's rank correlation** (which measures monotonic relationships) or visualizations are necessary.
*   **Sensitivity to Outliers:** Like variance and standard deviation, both covariance and correlation are sensitive to outliers. A few extreme data points can significantly alter their values, potentially misrepresenting the overall relationship between variables.
*   **Correlation Does Not Imply Causation (A Critical Distinction):** This is arguably the most crucial cautionary point in statistics. A strong correlation between two variables does not automatically mean that one causes the other. The observed relationship might be due to a confounding variable (a third, unobserved factor influencing both), pure coincidence, or even reverse causation. For example, ice cream sales and drowning incidents often increase at the same time, but ice cream doesn't cause drowning; a third variable (temperature) influences both. Always be wary of inferring causation from correlation alone; controlled experiments or advanced causal inference techniques are required to establish causation.
*   **Relationship to Moments:** For advanced readers, covariance is the **second mixed central moment** between two random variables, extending the concept of variance to multivariate settings.

### Properties of Covariance

Covariance also has several important properties. Let $X$, $Y$, and $Z$ be random variables and $a, b, c, d$ be constants.

1.  **Symmetry**: The covariance of $X$ and $Y$ is the same as the covariance of $Y$ and $X$.

    $$Cov(X, Y) = Cov(Y, X)$$

2.  **Covariance with a Constant**: The covariance of a random variable with a constant is zero. A constant has no variability to share.

    $$Cov(X, a) = 0$$

3.  **Covariance with Itself**: The covariance of a random variable with itself is its variance.

    $$Cov(X, X) = Var(X)$$

4.  **Effect of Scaling and Shifting**:

    $$Cov(aX + b, cY + d) = ac \cdot Cov(X, Y)$$

5.  **Distributive Property**:

    $$Cov(X + Y, Z) = Cov(X, Z) + Cov(Y, Z)$$

6.  **Variance of a Sum of *Dependent* Random Variables**: The property for the variance of a sum can be generalized for dependent variables using covariance.

    $$Var(X + Y) = Var(X) + Var(Y) + 2Cov(X, Y)$$

---

## Bessel's Correction

The use of $n-1$ in the denominator for sample variance (and sample covariance) is not just a convention; it's a crucial mathematical adjustment known as **Bessel's Correction**. Its purpose is to ensure that the sample variance is an **unbiased estimator** of the population variance.

Let's break down why this correction is necessary, both intuitively and with a conceptual sketch of the mathematical proof.

### Intuitive Explanation

Imagine you want to estimate the average height of all people in a large city. You take a sample of 100 people and calculate their average height ($\bar{x}$). You then want to estimate the variance of heights in the entire city ($\sigma^2$) using your sample.

1. **The problem of using the sample mean:** When you calculate the variance, you're looking at how much each data point deviates from the "true" mean. If you knew the *population mean* ($\mu$), you would calculate $\frac{\sum (x_i - \mu)^2}{N}$. However, you usually don't know $\mu$. So, you use the *sample mean* ($\bar{x}$) as an estimate for $\mu$.

2. **Sample mean is "closer" to the sample data:** The crucial point is that the sample mean ($\bar{x}$) is calculated *from* the sample data itself. By its very nature, $\bar{x}$ will always be the value that minimizes the sum of squared deviations for *that specific sample*. Think of it this way: if you try to fit a line to a set of points, the line you choose will be the one that minimizes the squared distances to *those specific points*. The sample mean is the "best fit" for your sample data.

3. **Underestimation:** Because $\bar{x}$ is the "best fit" for your sample, the sum of squared deviations from $\bar{x}$ ($\sum (x_i - \bar{x})^2$) will always be *smaller than or equal to* the sum of squared deviations from the true population mean ($\sum (x_i - \mu)^2$). It will only be equal if your sample mean happens to perfectly match the population mean, which is highly unlikely in practice.

    Therefore, if you divide by $n$ (like you would for population variance), your sample variance would systematically *underestimate* the true population variance. It would be a biased estimator, always tending to be a little too small.

4. **The correction ($n-1$):** To counteract this downward bias, we divide by a slightly smaller number, $n-1$. Dividing by a smaller number makes the overall result larger, thereby "inflating" the sample variance just enough to make it an unbiased estimate of the population variance.

### Degrees of Freedom Explanation

Another way to understand $n-1$ is through the concept of **degrees of freedom**.

* When calculating the population variance, you use the population mean ($\mu$), which is a fixed, known value. Each of your $N$ data points $(x_i - \mu)$ provides independent information about the spread. You have $N$ independent pieces of information, so you divide by $N$.

* When calculating sample variance, you first calculate the sample mean ($\bar{x}$) from your $n$ data points. Once you know $\bar{x}$, you "lose" one degree of freedom. This means that if you know $n-1$ of the deviations $(x_i - \bar{x})$ and you know $\bar{x}$, the last deviation is not independent; it's determined by the others because $\sum (x_i - \bar{x}) = 0$.

    For example, if you have a sample of three numbers and their mean is 5:
    * If $x_1 - \bar{x} = 2$
    * If $x_2 - \bar{x} = -3$
    * Then $x_3 - \bar{x}$ *must be* $1$ (because $2 + (-3) + 1 = 0$).

    So, you only have $n-1$ independent pieces of information contributing to the variability around the sample mean. Dividing by $n-1$ accounts for this loss of a degree of freedom.

However, now we can say:
* We have a formula for the population mean $\mu$.
* Thus, the calculation of the population mean should also decrease the number of degrees of freedom. Or not?

The key difference lies in whether the mean we are using in our calculation ($\bar{x}$ or $\mu$) is **estimated from the data itself** or is a **fixed, known value independent of the data**.

Why $\bar{x}$ reduces degrees of freedom by one (for sample variance/covariance)?

When you calculate the **sample variance ($s^2$)** using the formula $s^2 = \frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n-1}$:

1.  **You first calculate $\bar{x}$ from the $n$ data points in our sample.**
2.  **This act of calculating $\bar{x}$ imposes a constraint on the data points.** Specifically, the sum of the deviations from the mean must always be zero: $\sum_{i=1}^{n} (x_i - \bar{x}) = 0$.
3.  Because of this constraint, if you know $n-1$ of the deviations $(x_i - \bar{x})$, the *last* deviation is automatically determined. It's not free to vary independently.
    * For example, if you have three numbers, $x_1, x_2, x_3$, and their mean $\bar{x}$.
    * You calculate $(x_1 - \bar{x})$ and $(x_2 - \bar{x})$.
    * Then, $(x_3 - \bar{x})$ *must be* equal to $-[(x_1 - \bar{x}) + (x_2 - \bar{x})]$.
    * So, only $n-1$ of these deviations are truly independent pieces of information contributing to the variability around $\bar{x}$.

This "loss" of one piece of independent information is precisely why we say you lose one degree of freedom. You've used one piece of information from the sample (the sample mean) to define the center point around which you're measuring variability.

Why $\mu$ does NOT reduce degrees of freedom (for population variance/covariance)

When you calculate the **population variance ($\sigma^2$)** using the formula $\sigma^2 = \frac{\sum_{i=1}^{N} (x_i - \mu)^2}{N}$:

1.  **The population mean ($\mu$) is a constant, a fixed parameter of the entire population.**
2.  **You assume $\mu$ is known.** In theoretical scenarios where you are calculating population variance, you *hypothetically* have access to the true $\mu$.
3.  **No constraint is imposed on the deviations from $\mu$ by the calculation of $\mu$.** Each deviation $(x_i - \mu)$ is an independent piece of information about the spread from this *pre-defined* center point. You haven't used any of the $x_i$ values to determine $\mu$.

> Think of it like this: if you have a target ($\mu$) and you're shooting arrows ($x_i$), and you want to know how spread out our shots are from the true center of the target, you just measure the distance of each shot from the target's center. Each shot provides independent information.

> However, if you don't know the true target center, you fire 10 arrows, estimate the center of the target based on where our 10 arrows landed ($\bar{x}$), and then measure the spread from *that estimated center*. In this second scenario, our estimated center is influenced by the arrows themselves, meaning one of the arrow's positions isn't truly "free" if you know the other 9 and our estimated center.


To find $\mu$, you perform a calculation as well as you perform a calculation to find $\bar{x}$. The distinction regarding degrees of freedom comes down to *when* that mean is known or estimated relative to the variance calculation.

When we discuss the **population variance ($\sigma^2$)** and its formula $\sigma^2 = \frac{\sum_{i=1}^{N} (x_i - \mu)^2}{N}$:

1.  **Hypothetical Knowledge or Definitive Calculation**: In the context of population variance, we *assume* we either already know the true population mean ($\mu$) or we are in a theoretical scenario where we *have* access to the *entire population data* ($N$ observations) to definitively calculate $\mu$.
    * If you have the *entire population* of $N$ data points, then calculating $\mu = \frac{\sum_{i=1}^{N} x_i}{N}$ gives you the *true, definitive* population mean. It's not an estimate; it's the exact value for that population.
    * Once you have this definitive $\mu$, when you then calculate the variance, you are measuring the spread of each $x_i$ from this **fixed, true center** (!!!).

2.  **No Estimation from a Subset**: The crucial part is that when you calculate $\sigma^2$, you are **not estimating $\mu$ from a *subset* of the data that you're simultaneously using to calculate the variance.**
    * Each of the $N$ deviations $(x_i - \mu)$ is indeed an independent piece of information about the spread around that fixed $\mu$. There's no "loss" of information or constraint imposed on these deviations because the $\mu$ is taken as the true center of the entire data set you're working with.

Contrast with Sample Variance:

For **sample variance ($s^2$)**, when you use $\bar{x}$ calculated from a *sample* of $n$ observations:

1.  **Estimation from a Subset**: You are taking a *subset* (the sample) of the larger population. You don't know the true population mean $\mu$.
2.  **Using $\bar{x}$ as an Estimator**: You calculate $\bar{x}$ from *this very sample* of $n$ data points to serve as an estimate of $\mu$.
3.  **Self-Fulfilling Constraint**: Because $\bar{x}$ is derived *from* the $n$ sample points, it automatically minimizes the sum of squared deviations for *that specific sample*. This introduces a statistical dependency: if you know $n-1$ deviations from $\bar{x}$, the last one is fixed. This is why you lose a degree of freedom.

Another analogy:

* **Population Variance**: You have a perfectly calibrated ruler (your true $\mu$) and you measure $N$ items. Each measurement is independent with respect to the fixed ruler.
* **Sample Variance**: You have $n$ items, and you first try to estimate the "average size" using these $n$ items (your $\bar{x}$). Then you measure how much each item deviates from *your own estimate*. Because your estimate ($\bar{x}$) was influenced by the items themselves, there's a slight dependency. One item's deviation isn't completely "free" once you've fixed the average from those $n$ items.

So, while you *do* calculate $\mu$ for the population variance, that calculation uses the *entire* population data. This $\mu$ then serves as the definitive, non-estimated center point from which deviations are measured, allowing all $N$ deviations to contribute independently. For sample variance, $\bar{x}$ is an estimate derived from a subset, which inherently "ties" one degree of freedom.

In summary:

| Feature           | Sample Variance ($s^2$)                                        | Population Variance ($\sigma^2$)                                   |
| :---------------- | :------------------------------------------------------------- | :----------------------------------------------------------------- |
| Mean Used         | $\bar{x}$ (Sample Mean)                                       | $\mu$ (Population Mean)                                            |
| Source of Mean    | Calculated *from* the $n$ data points in the sample.           | A fixed parameter of the population, calculated using all $N$ data points of the entire population. |
| Constraint        | The sum of deviations from $\bar{x}$ is constrained to zero.  | No such constraint on deviations from $\mu$.                       |
| Degrees of Freedom| $n-1$ (one degree lost because $\bar{x}$ was estimated).     | $N$ (all $N$ deviations are independent).                          |
| Purpose           | Unbiased estimate of $\sigma^2$.                               | True variance of the population (if $\mu$ is known).               |

This distinction is fundamental in statistics, as it addresses the bias that arises when using sample statistics to infer properties of a larger population. The $n-1$ in the denominator is Bessel's correction, explicitly designed to create an unbiased estimator for population variance when only a sample is available.

### Mathematical Proof Sketch (for Variance)

The formal proof involves using the concept of **expected value**. An estimator $\hat{\theta}$ for a parameter $\theta$ is unbiased if $E[\hat{\theta}] = \theta$. We want $E[s^2] = \sigma^2$.

Let $X_1, X_2, \ldots, X_n$ be independent and identically distributed (i.i.d.) random variables from a population with mean $\mu$ and variance $\sigma^2$.

We know:
* $E[X_i] = \mu$
* $Var(X_i) = E[(X_i - \mu)^2] = \sigma^2$
* $E[\bar{X}] = \mu$
* $Var(\bar{X}) = E[(\bar{X} - \mu)^2] = \frac{\sigma^2}{n}$

Let's derive this last equation.

We start with the definition of the variance of $\bar{X}$:

$$Var(\bar{X}) = E[(\bar{X} - E[\bar{X}])^2]$$

First, let's find the expected value of the sample mean, $E[\bar{X}]$:

$$E[\bar{X}] = E\left[ \frac{1}{n} \sum_{i=1}^{n} X_i \right]$$

$$E[\bar{X}] = \frac{1}{n} E\left[ \sum_{i=1}^{n} X_i \right]$$

$$E[\bar{X}] = \frac{1}{n} \sum_{i=1}^{n} E[X_i]$$

Since each $X_i$ comes from the same population, $E[X_i] = \mu$ for all $i$:

$$E[\bar{X}] = \frac{1}{n} \sum_{i=1}^{n} \mu$$

$$E[\bar{X}] = \frac{1}{n} (n\mu)$$

$$E[\bar{X}] = \mu$$

So, the expected value of the sample mean is the population mean. This is why $\bar{X}$ is an unbiased estimator of $\mu$.

Now, substitute $E[\bar{X}] = \mu$ back into the variance definition:

$$Var(\bar{X}) = E[(\bar{X} - \mu)^2]$$

Next, substitute the definition of $\bar{X}$:

$$Var(\bar{X}) = Var\left( \frac{1}{n} \sum_{i=1}^{n} X_i \right)$$

Using the property $Var(c Y) = c^2 Var(Y)$, where $c = \frac{1}{n}$:

$$Var(\bar{X}) = \left( \frac{1}{n} \right)^2 Var\left( \sum_{i=1}^{n} X_i \right)$$
$$Var(\bar{X}) = \frac{1}{n^2} Var\left( \sum_{i=1}^{n} X_i \right)$$

Since $X_1, X_2, \ldots, X_n$ are independent (a key assumption for simple random sampling), the variance of their sum is the sum of their variances:

$$Var\left( \sum_{i=1}^{n} X_i \right) = \sum_{i=1}^{n} Var(X_i)$$

Since each $X_i$ comes from the same population, $Var(X_i) = \sigma^2$ for all $i$:
$$\sum_{i=1}^{n} Var(X_i) = \sum_{i=1}^{n} \sigma^2 = n\sigma^2$$

Now, substitute this back into our expression for $Var(\bar{X})$:

$$Var(\bar{X}) = \frac{1}{n^2} (n\sigma^2)$$
$$Var(\bar{X}) = \frac{n\sigma^2}{n^2}$$
$$Var(\bar{X}) = \frac{\sigma^2}{n}$$

This result is incredibly important because it quantifies how the precision of our estimate of the mean improves as we increase our sample size. A larger sample size ($n$) leads to a smaller variance for the sample mean, meaning $\bar{X}$ is more likely to be closer to the true population mean $\mu$. This is the mathematical basis for why larger samples give more reliable estimates.

**Proof for Bessel's Correction:**

Now, let's consider the "biased" sample variance, $s^2_{\text{biased}} = \frac{1}{n} \sum_{i=1}^n (X_i - \bar{X})^2$. We want to find its expected value:

$$E[s^2_{\text{biased}}] = E\left[ \frac{1}{n} \sum_{i=1}^n (X_i - \bar{X})^2 \right] = \frac{1}{n} E\left[ \sum_{i=1}^n (X_i - \bar{X})^2 \right]$$

Let's work with the sum of squares in the numerator: $\sum_{i=1}^n (X_i - \bar{X})^2$.

We can rewrite $(X_i - \bar{X})$ as $(X_i - \mu) - (\bar{X} - \mu)$.

$$\sum_{i=1}^n (X_i - \bar{X})^2 = \sum_{i=1}^n [(X_i - \mu) - (\bar{X} - \mu)]^2$$
$$= \sum_{i=1}^n [(X_i - \mu)^2 - 2(X_i - \mu)(\bar{X} - \mu) + (\bar{X} - \mu)^2]$$
$$= \sum_{i=1}^n (X_i - \mu)^2 - 2(\bar{X} - \mu) \sum_{i=1}^n (X_i - \mu) + \sum_{i=1}^n (\bar{X} - \mu)^2$$

Note that

$$\sum_{i=1}^n (X_i - \mu) = \sum X_i - n\mu = n\bar{X} - n\mu = n(\bar{X} - \mu)$$

$$\sum_{i=1}^n (\bar{X} - \mu)^2 = n(\bar{X} - \mu)^2$$

Substitute these back:

$$\sum_{i=1}^n (X_i - \bar{X})^2 = \sum_{i=1}^n (X_i - \mu)^2 - 2(\bar{X} - \mu) [n(\bar{X} - \mu)] + n(\bar{X} - \mu)^2$$
$$= \sum_{i=1}^n (X_i - \mu)^2 - 2n(\bar{X} - \mu)^2 + n(\bar{X} - \mu)^2$$
$$= \sum_{i=1}^n (X_i - \mu)^2 - n(\bar{X} - \mu)^2$$

Now, take the expectation of this expression:

$$E\left[ \sum_{i=1}^n (X_i - \bar{X})^2 \right] = E\left[ \sum_{i=1}^n (X_i - \mu)^2 - n(\bar{X} - \mu)^2 \right]$$

By linearity of expectation:

$$= \sum_{i=1}^n E[(X_i - \mu)^2] - n E[(\bar{X} - \mu)^2]$$

We know $E[(X_i - \mu)^2] = \sigma^2$ (by definition of population variance) and $E[(\bar{X} - \mu)^2] = Var(\bar{X}) = \frac{\sigma^2}{n}$. Thus

$$E\left[ \sum_{i=1}^n (X_i - \bar{X})^2 \right] = \sum_{i=1}^n \sigma^2 - n \frac{\sigma^2}{n}$$
$$= n\sigma^2 - \sigma^2 = (n-1)\sigma^2$$

Therefore, the expected value of the numerator of the sample variance is $(n-1)\sigma^2$. Therefore,

$$E[s^2_{\text{biased}}] = \frac{1}{n} E\left[ \sum_{i=1}^n (X_i - \bar{X})^2 \right] = \frac{n-1}{n} \sigma^2$$

So, the expected value $E[s^2_{\text{biased}}]$ is not equal to the population variance $\sigma^2$.

Remember that we want $E[s^2] = \sigma^2$. Therefore, we will have for

$$s^2 = \frac{\sum_{i=1}^n (X_i - \bar{X})^2}{n-1}$$

$$E[s^2] = E\left[ \frac{\sum_{i=1}^n (X_i - \bar{X})^2}{n-1} \right] = \frac{1}{n-1} E\left[ \sum_{i=1}^n (X_i - \bar{X})^2 \right]$$
$$= \frac{1}{n-1} (n-1)\sigma^2 = \sigma^2$$

This mathematical derivation shows that by dividing by $n-1$, the sample variance ($s^2$) indeed becomes an unbiased estimator of the population variance ($\sigma^2$). If we had divided by $n$, the expected value would have been $\frac{n-1}{n}\sigma^2$, confirming the downward bias.

---

## Additional Materials

* https://en.wikipedia.org/wiki/Variance
* https://en.wikipedia.org/wiki/Covariance
* https://www.ncl.ac.uk/webtemplate/ask-assets/external/maths-resources/statistics/descriptive-statistics/variance-and-standard-deviation.html
* https://mathsathome.com/variance/
* https://online.stat.psu.edu/stat505/book/export/html/643
* https://online.stat.psu.edu/stat505/book/export/html/653
* https://en.wikipedia.org/wiki/Covariance_matrix
* https://en.wikipedia.org/wiki/Mean
* https://en.wikipedia.org/wiki/Standard_deviation
* https://en.wikipedia.org/wiki/Sample_mean_and_covariance
* https://en.wikipedia.org/wiki/Statistical_population
* https://en.wikipedia.org/wiki/Bessel%27s_correction
* https://en.wikipedia.org/wiki/Degrees_of_freedom_(statistics)
* https://en.wikipedia.org/wiki/Pearson_correlation_coefficient
