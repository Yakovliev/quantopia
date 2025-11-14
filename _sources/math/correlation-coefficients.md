# Correlation Coefficients

Correlation coefficients are statistical measures that quantify the extent to which two variables are related. They transform covariance into a standardized, interpretable value, typically ranging from -1 to +1. This standardization allows us to compare the strength of relationships across different datasets and variable types.

## Pearson Correlation Coefficient

The Pearson Product-Moment Correlation Coefficient, often denoted as $r$ for a sample and $\rho$ (rho) for a population, is the most widely used measure of correlation. It quantifies the **strength** and **direction** of a **linear relationship** between two continuous variables.

### Definition and Purpose

Pearson's correlation coefficient is a standardized version of the covariance. By dividing the covariance by the product of the standard deviations of the two variables, we normalize the measure, removing the influence of their scales and units. This results in a dimensionless value that always falls between -1 and +1.

Let's recall the definitions of covariance and standard deviation that we covered [previously](variance-covariance.md).

*   **Population Covariance:** $\text{Cov}(X, Y) = \sigma_{XY} = \frac{\sum_{i=1}^{N} (x_i - \mu_X)(y_i - \mu_Y)}{N}$
*   **Population Standard Deviation for X:** $\sigma_X = \sqrt{\frac{\sum_{i=1}^{N} (x_i - \mu_X)^2}{N}}$
*   **Population Standard Deviation for Y:** $\sigma_Y = \sqrt{\frac{\sum_{i=1}^{N} (y_i - \mu_Y)^2}{N}}$

Similarly, for a sample:

*   **Sample Covariance:** $s_{XY} = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{n-1}$
*   **Sample Standard Deviation for X:** $s_X = \sqrt{\frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n-1}}$
*   **Sample Standard Deviation for Y:** $s_Y = \sqrt{\frac{\sum_{i=1}^{n} (y_i - \bar{y})^2}{n-1}}$

### Formulas for Pearson's Correlation Coefficient

#### Population Pearson Correlation Coefficient ($\rho_{XY}$)

The population Pearson correlation coefficient is given by:

$$\rho_{XY} = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y}$$

Substituting the formulas for population covariance and standard deviations, we get:

$$\rho_{XY} = \frac{\frac{1}{N} \sum_{i=1}^{N} (x_i - \mu_X)(y_i - \mu_Y)}{\sqrt{\frac{1}{N} \sum_{i=1}^{N} (x_i - \mu_X)^2} \sqrt{\frac{1}{N} \sum_{i=1}^{N} (y_i - \mu_Y)^2}}$$

Simplifying the $N$ terms in the denominator and numerator:

$$\rho_{XY} = \frac{\sum_{i=1}^{N} (x_i - \mu_X)(y_i - \mu_Y)}{\sqrt{\sum_{i=1}^{N} (x_i - \mu_X)^2} \sqrt{\sum_{i=1}^{N} (y_i - \mu_Y)^2}}$$

#### Sample Pearson Correlation Coefficient ($r_{XY}$)

The sample Pearson correlation coefficient is given by:

$$r_{XY} = \frac{s_{XY}}{s_X s_Y}$$

Substituting the formulas for sample covariance and standard deviations, and remembering Bessel's correction $(n-1)$ for sample estimates:

$$r_{XY} = \frac{\frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})^2} \sqrt{\frac{1}{n-1} \sum_{i=1}^{n} (y_i - \bar{y})^2}}$$

Simplifying the $(n-1)$ terms in the numerator and denominator:

$$r_{XY} = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n} (x_i - \bar{x})^2} \sqrt{\sum_{i=1}^{n} (y_i - \bar{y})^2}}$$

It is important to note that while Bessel's correction (dividing by $n-1$) is crucial for making $s_X^2$, $s_Y^2$, and $s_{XY}$ *unbiased estimators* of their population counterparts, the $n-1$ terms cancel out in the calculation of $r_{XY}$. This means that the sample Pearson correlation coefficient $r_{XY}$ itself is generally **not an unbiased estimator** of the population correlation coefficient $\rho_{XY}$, especially for small sample sizes. However, it remains a consistent estimator, meaning it converges to the true population value as the sample size increases.

### Derivation of Standardization: Why Pearson's $r$ is bounded between -1 and +1

The property that Pearson's correlation coefficient always lies between -1 and +1 is not arbitrary; it stems directly from a fundamental mathematical inequality known as the **Cauchy-Schwarz Inequality**. This inequality provides the rigorous mathematical basis for the standardization.

The Cauchy-Schwarz Inequality states that for any real numbers $a_1, \ldots, a_n$ and $b_1, \ldots, b_n$:

$$ \left( \sum_{i=1}^n a_i b_i \right)^2 \le \left( \sum_{i=1}^n a_i^2 \right) \left( \sum_{i=1}^n b_i^2 \right) $$

Let's apply this to the components of our Pearson correlation coefficient.
For the sample Pearson correlation coefficient, let:
*   $a_i = (x_i - \bar{x})$ (the deviation of each $x$ value from its mean)
*   $b_i = (y_i - \bar{y})$ (the deviation of each $y$ value from its mean)

Substituting these into the Cauchy-Schwarz inequality, we get:

$$ \left( \sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y}) \right)^2 \le \left( \sum_{i=1}^n (x_i - \bar{x})^2 \right) \left( \sum_{i=1}^n (y_i - \bar{y})^2 \right) $$

Now, take the square root of both sides. Remember that $\sqrt{A^2} = |A|$:

$$ \left| \sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y}) \right| \le \sqrt{\sum_{i=1}^n (x_i - \bar{x})^2} \sqrt{\sum_{i=1}^n (y_i - \bar{y})^2} $$

Finally, divide both sides by the term on the right (which is always non-negative, assuming not all $x_i$ or all $y_i$ are identical, which would lead to zero standard deviation):

$$ \left| \frac{\sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^n (x_i - \bar{x})^2} \sqrt{\sum_{i=1}^n (y_i - \bar{y})^2}} \right| \le 1 $$

The expression inside the absolute value is precisely the formula for the sample Pearson correlation coefficient, $r_{XY}$. Therefore, we have:

$$ |r_{XY}| \le 1 $$

This inequality mathematically demonstrates that the absolute value of Pearson's $r_{XY}$ (and similarly for $\rho_{XY}$) must be less than or equal to 1. This means $r_{XY}$ must lie in the range $[-1, +1]$.

The equality $|r_{XY}| = 1$ holds if and only if there is a perfect linear relationship between the deviations, i.e., $(y_i - \bar{y}) = k(x_i - \bar{x})$ for some non-zero constant $k$. If $k > 0$, $r_{XY} = +1$; if $k < 0$, $r_{XY} = -1$. Geometrically, this means the two mean-centered data vectors are perfectly collinear.

### Derivation of the Raw-Score Computational Formula for Sample Pearson Correlation Coefficient

While the definitional formula is clear, for practical computation, especially before the widespread use of statistical software, a raw-score formula was often preferred to minimize intermediate calculations and rounding errors. Let's derive this form.

We start with the definitional formula for the sample Pearson correlation coefficient:

$$r_{XY} = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n} (x_i - \bar{x})^2 \sum_{i=1}^{n} (y_i - \bar{y})^2}}$$

We will expand the numerator and each term in the denominator separately using the computational formulas for sum of products of deviations and sum of squared deviations.

**1. Expanding the Numerator:**

Recall the alternative form for the sum of products of deviations (we derived a similar equation [here](variance-covariance.md) during the derivation of the alternative form of sample covariance formula):

$$ \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y}) = \sum_{i=1}^{n} x_i y_i - n\bar{x}\bar{y} $$

Now, substitute the definitions of the sample means $\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n}$ and $\bar{y} = \frac{\sum_{i=1}^{n} y_i}{n}$:

$$ \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y}) = \sum_{i=1}^{n} x_i y_i - n \left( \frac{\sum_{i=1}^{n} x_i}{n} \right) \left( \frac{\sum_{i=1}^{n} y_i}{n} \right) $$

$$ = \sum_{i=1}^{n} x_i y_i - \frac{(\sum_{i=1}^{n} x_i)(\sum_{i=1}^{n} y_i)}{n} $$

To combine these terms, we can find a common denominator:

$$ \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y}) = \frac{n \sum_{i=1}^{n} x_i y_i - (\sum_{i=1}^{n} x_i)(\sum_{i=1}^{n} y_i)}{n} $$

**2. Expanding the Denominator Terms:**

Recall the alternative form for the sum of squared deviations for variable $X$ (we derived a similar equation [here](variance-covariance.md) during the derivation of the alternative form of sample variance formula):

$$ \sum_{i=1}^{n} (x_i - \bar{x})^2 = \sum_{i=1}^{n} x_i^2 - n\bar{x}^2 $$

Substitute $\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n}$:

$$ \sum_{i=1}^{n} (x_i - \bar{x})^2 = \sum_{i=1}^{n} x_i^2 - n \left( \frac{\sum_{i=1}^{n} x_i}{n} \right)^2 $$

$$ = \sum_{i=1}^{n} x_i^2 - n \frac{(\sum_{i=1}^{n} x_i)^2}{n^2} $$

$$ = \sum_{i=1}^{n} x_i^2 - \frac{(\sum_{i=1}^{n} x_i)^2}{n} $$

Combining with a common denominator:

$$ = \frac{n \sum_{i=1}^{n} x_i^2 - (\sum_{i=1}^{n} x_i)^2}{n} $$

Similarly, for variable $Y$:

$$ \sum_{i=1}^{n} (y_i - \bar{y})^2 = \frac{n \sum_{i=1}^{n} y_i^2 - (\sum_{i=1}^{n} y_i)^2}{n} $$

**3. Substituting into the Full Formula:**
Now, substitute these expanded forms back into the formula for $r_{XY}$:

$$r_{XY} = \frac{\frac{n \sum_{i=1}^{n} x_i y_i - \sum_{i=1}^{n} x_i \sum_{i=1}^{n} y_i}{n}}{\sqrt{\left( \frac{n \sum_{i=1}^{n} x_i^2 - (\sum_{i=1}^{n} x_i)^2}{n} \right) \left( \frac{n \sum_{i=1}^{n} y_i^2 - (\sum_{i=1}^{n} y_i)^2}{n} \right)}}$$

Let's simplify the denominator. The $\frac{1}{n}$ terms under the square root can be pulled out:
$$ \sqrt{\frac{1}{n^2} \left( n \sum_{i=1}^{n} x_i^2 - (\sum_{i=1}^{n} x_i)^2 \right) \left( n \sum_{i=1}^{n} y_i^2 - (\sum_{i=1}^{n} y_i)^2 \right)} $$
$$ = \frac{1}{n} \sqrt{\left( n \sum_{i=1}^{n} x_i^2 - (\sum_{i=1}^{n} x_i)^2 \right) \left( n \sum_{i=1}^{n} y_i^2 - (\sum_{i=1}^{n} y_i)^2 \right)} $$

So, the full expression becomes:

$$r_{XY} = \frac{\frac{n \sum_{i=1}^{n} x_i y_i - \sum_{i=1}^{n} x_i \sum_{i=1}^{n} y_i}{n}}{\frac{1}{n} \sqrt{\left( n \sum_{i=1}^{n} x_i^2 - \left( \sum_{i=1}^{n} x_i \right)^2 \right) \left( n \sum_{i=1}^{n} y_i^2 - \left( \sum_{i=1}^{n} y_i \right)^2 \right)}}$$

The $\frac{1}{n}$ terms in the main numerator and denominator cancel out, leaving us with the raw-score computational formula for Pearson's $r$:

$$r_{XY} = \frac{n \sum_{i=1}^{n} x_i y_i - \sum_{i=1}^{n} x_i \sum_{i=1}^{n} y_i}{\sqrt{\left( n \sum_{i=1}^{n} x_i^2 - \left( \sum_{i=1}^{n} x_i \right)^2 \right) \left( n \sum_{i=1}^{n} y_i^2 - \left( \sum_{i=1}^{n} y_i \right)^2 \right)}}$$

This form is particularly useful for calculations when raw sums of $x_i$, $y_i$, $x_i^2$, $y_i^2$, and $x_i y_i$ are readily available or easier to compute directly. We can also write this form:

$$r_{XY} = \frac{\sum_{i=1}^{n} x_i y_i - n\bar{x}\bar{y}}{\sqrt{\left( \sum_{i=1}^{n} x_i^2 - n\bar{x}^2 \right) \left( \sum_{i=1}^{n} y_i^2 - n\bar{y}^2 \right)}}$$

This is another common and useful computational form for Pearson's $r$, often preferred for manual calculation as it avoids intermediate calculation of individual deviations.

### Interpretation

The value of Pearson's $r$ (or $\rho$) tells us two things about the linear relationship between $X$ and $Y$:

*   **Direction:**
    *   **Positive values ($r > 0$):** Indicate a positive linear relationship. As $X$ increases, $Y$ tends to increase.
    *   **Negative values ($r < 0$):** Indicate a negative linear relationship. As $X$ increases, $Y$ tends to decrease.
    *   **Zero value ($r = 0$):** Indicates no linear relationship.
*   **Strength (magnitude of the absolute value):**
    *   **$|r| = 1$:** Perfect linear relationship. All data points fall exactly on a straight line.
    *   **$0.7 \le |r| < 1$:** Strong linear relationship.
    *   **$0.3 \le |r| < 0.7$:** Moderate linear relationship.
    *   **$0 < |r| < 0.3$:** Weak linear relationship.
    *   **$|r| = 0$:** No linear relationship.

<p><img src="https://upload.wikimedia.org/wikipedia/commons/d/d4/Correlation_examples2.svg" alt="Correlation examples2.svg" height="300" width="656.7">
<br>
Fig. Several sets of (x, y) points, with the Pearson correlation coefficient of x and y for each set. The correlation reflects the strength and direction of a linear relationship (top row), but not the slope of that relationship (middle row), nor many aspects of nonlinear relationships (bottom row). N.B.: the figure in the center has a slope of 0 but in that case the correlation coefficient is undefined because the variance of Y is zero.
By <a href="https://commons.wikimedia.org/w/index.php?title=User:DenisBoigelot&amp;action=edit&amp;redlink=1" class="new" title="User:DenisBoigelot (page does not exist)">DenisBoigelot</a>, <a href="https://creativecommons.org/publicdomain/zero/1.0/deed.en" title="Creative Commons Zero, Public Domain Dedication">CC0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=15165296">Link</a>. <a href="https://en.wikipedia.org/wiki/Pearson_correlation_coefficient">Wikipedia</a></p>

### Assumptions and Limitations

For Pearson's correlation coefficient to be an appropriate and reliable measure, we typically assume:

1.  **Linearity:** The relationship between the two variables must be linear. If the relationship is non-linear (e.g., U-shaped, exponential), Pearson's $r$ will underestimate the true strength of the association or even suggest no relationship. It's crucial to visualize the data (e.g., with a scatter plot) to confirm linearity before relying on Pearson's $r$. Sometimes, non-linear transformations (like logarithmic or square root) can linearize a relationship, making Pearson's $r$ applicable to the transformed variables.
2.  **Continuous Variables:** Both variables $X$ and $Y$ should be measured on an interval or ratio scale (i.e., continuous).
3.  **No Significant Outliers:** Pearson's $r$ is highly sensitive to outliers. A single extreme data point can significantly inflate or deflate the coefficient, potentially misrepresenting the overall relationship for the majority of data points. While outliers can be problematic (e.g., data entry errors), sometimes they represent crucial, high-impact events that should not be simply dismissed. A "robust" measure might overlook these critical data points, so understanding the nature of outliers is key.
4.  **Homoscedasticity (for inferential statistics)**: For each value of $X$, the variance of $Y$ should be constant, and vice versa. This is more relevant for linear regression assumptions but contributes to the validity of statistical inferences about correlation.
5.  **Bivariate Normality (for inferential statistics)**: If we want to perform hypothesis testing or construct confidence intervals for Pearson's $r$, the data should ideally come from a bivariate normal distribution. This means that for any given value of $X$, the corresponding values of $Y$ are normally distributed, and vice-versa. For descriptive purposes, this assumption is less critical.

---

## Spearman's Rank Correlation Coefficient

Spearman's rank correlation coefficient, often denoted as $r_s$ or $\rho_s$, is a non-parametric measure of the strength and direction of a **monotonic relationship** between two ranked variables. It is particularly useful when:

*   The data are ordinal (ranks, ratings).
*   The data are continuous but do not meet the normality assumption for Pearson's $r$.
*   The relationship is monotonic but not necessarily linear (e.g., an exponential curve).
*   The data contain outliers that would disproportionately influence Pearson's $r$.

### Concept of Ranks

The core idea behind Spearman's correlation is to transform the original data into ranks and then calculate Pearson's correlation coefficient on these ranks. By using ranks, we focus on the *relative order* of data points rather than the raw magnitudes of differences, making it robust to non-linear monotonic transformations and outliers.

For each variable $X$ and $Y$:

1.  **Assign ranks to $X$ values:** The smallest $X$ value gets rank 1, the next smallest gets rank 2, and so on, up to $n$ for the largest value.
2.  **Assign ranks to $Y$ values:** Similarly, the smallest $Y$ value gets rank 1, the next smallest gets rank 2, etc.
3.  **Handle Ties:** If two or more values are identical (a "tie"), we assign them the average of the ranks they would have received. For example, if two values are tied for the 3rd and 4th position, they both get a rank of $(3+4)/2 = 3.5$.

### Formula

Spearman's $r_s$ can be calculated in two ways:

1.  **Using Pearson's formula on ranks:** This is the fundamental definition. If $R_X$ and $R_Y$ are the ranks of the variables $X$ and $Y$, then:

    $$r_s = \frac{\text{Cov}(R_X, R_Y)}{s_{R_X} s_{R_Y}}$$

    This means we apply the Pearson correlation formula directly to the ranked data.

2.  **Simplified Formula (for no ties):** When there are no tied ranks in either variable, a simpler computational formula can be used:

    $$r_s = 1 - \frac{6 \sum d_i^2}{n(n^2 - 1)}$$

    where:
    *   $d_i = R_{X_i} - R_{Y_i}$ is the difference between the ranks of each observation $i$.
    *   $n$ is the number of observations.

#### Derivation of the Simplified Formula (for no ties)

Let's derive the simplified formula for Spearman's $r_s$ when there are no ties. We start with Pearson's formula applied to ranks:

$$r_s = \frac{\sum_{i=1}^{n} (R_{X_i} - \overline{R_X})(R_{Y_i} - \overline{R_Y})}{\sqrt{\sum_{i=1}^{n} (R_{X_i} - \overline{R_X})^2} \sqrt{\sum_{i=1}^{n} (R_{Y_i} - \overline{R_Y})^2}}$$

When we have $n$ distinct ranks (from 1 to $n$), the sum of ranks is $\sum_{i=1}^n i = \frac{n(n+1)}{2}$.

The mean of these ranks is $\overline{R_X} = \overline{R_Y} = \frac{\sum_{i=1}^n i}{n} = \frac{n(n+1)/2}{n} = \frac{n+1}{2}$.

Now, let's consider the sum of squared deviations for ranks. The sum of squares of the first $n$ integers is $\sum_{i=1}^n i^2 = \frac{n(n+1)(2n+1)}{6}$.

The sum of squared deviations from the mean for ranks is:

$$\sum_{i=1}^n (R_i - \overline{R})^2 = \sum_{i=1}^n R_i^2 - n(\overline{R})^2$$

$$= \frac{n(n+1)(2n+1)}{6} - n\left(\frac{n+1}{2}\right)^2$$

$$= \frac{n(n+1)(2n+1)}{6} - \frac{n(n+1)^2}{4}$$

To simplify, we find a common denominator (12) and factor out common terms:

$$= \frac{2n(n+1)(2n+1) - 3n(n+1)^2}{12}$$

$$= \frac{n(n+1) [2(2n+1) - 3(n+1)]}{12}$$

$$= \frac{n(n+1) [4n+2 - 3n-3]}{12}$$

$$= \frac{n(n+1)(n-1)}{12}$$

$$= \frac{n(n^2-1)}{12}$$

So, for both $X$ and $Y$ ranks (assuming no ties), we have:

$$\sum_{i=1}^{n} (R_{X_i} - \overline{R_X})^2 = \frac{n(n^2-1)}{12}$$

$$\sum_{i=1}^{n} (R_{Y_i} - \overline{R_Y})^2 = \frac{n(n^2-1)}{12}$$

Now, let $d_i = R_{X_i} - R_{Y_i}$. We know that $\sum d_i = \sum (R_{X_i} - R_{Y_i}) = \sum R_{X_i} - \sum R_{Y_i} = n\overline{R_X} - n\overline{R_Y} = 0$.

Consider the sum of squared differences:

$\sum d_i^2 = \sum (R_{X_i} - R_{Y_i})^2 =$

We can rewrite this using the property $(a-b)^2 = a^2 - 2ab + b^2$:

$= \sum [(R_{X_i} - \overline{R_X}) - (R_{Y_i} - \overline{R_Y})]^2$ (since $\overline{R_X} = \overline{R_Y}$)
$= \sum (R_{X_i} - \overline{R_X})^2 - 2 \sum (R_{X_i} - \overline{R_X})(R_{Y_i} - \overline{R_Y}) + \sum (R_{Y_i} - \overline{R_Y})^2 = \sum d_i^2$

We can rearrange this equation to solve for the numerator of Pearson's formula on ranks:

$$2 \sum (R_{X_i} - \overline{R_X})(R_{Y_i} - \overline{R_Y}) = \sum (R_{X_i} - \overline{R_X})^2 + \sum (R_{Y_i} - \overline{R_Y})^2 - \sum d_i^2$$

Substitute the sum of squared deviations for ranks:

$$2 \sum (R_{X_i} - \overline{R_X})(R_{Y_i} - \overline{R_Y}) = \frac{n(n^2-1)}{12} + \frac{n(n^2-1)}{12} - \sum d_i^2$$

$$2 \sum (R_{X_i} - \overline{R_X})(R_{Y_i} - \overline{R_Y}) = \frac{2n(n^2-1)}{12} - \sum d_i^2$$

$$\sum (R_{X_i} - \overline{R_X})(R_{Y_i} - \overline{R_Y}) = \frac{n(n^2-1)}{12} - \frac{1}{2} \sum d_i^2$$

Now substitute this back into the Pearson's formula for ranks, where the denominator is $\sqrt{\frac{n(n^2-1)}{12} \cdot \frac{n(n^2-1)}{12}} = \frac{n(n^2-1)}{12}$:

$$r_s = \frac{\frac{n(n^2-1)}{12} - \frac{1}{2} \sum d_i^2}{\frac{n(n^2-1)}{12}}$$
$$r_s = 1 - \frac{\frac{1}{2} \sum d_i^2}{\frac{n(n^2-1)}{12}}$$
$$r_s = 1 - \frac{6 \sum d_i^2}{n(n^2-1)}$$

This completes the derivation of the simplified formula for Spearman's $r_s$ when there are no ties. If ties are present, the formula using Pearson's coefficient on the ranks (with average ranks for ties) should be used, as the simplified formula can become inaccurate.

### Interpretation

Spearman's $r_s$ also ranges from -1 to +1, with interpretations similar to Pearson's $r$, but specifically for **monotonic relationships**:

*   **+1:** Perfect positive monotonic relationship. As one variable increases, the other also consistently increases (not necessarily at a constant rate or linearly).
*   **-1:** Perfect negative monotonic relationship. As one variable increases, the other consistently decreases.
*   **0:** No monotonic relationship.

### Assumptions and Limitations

*   **Monotonicity:** The relationship between the variables should be monotonic (consistently increasing or consistently decreasing). If the relationship is non-monotonic (e.g., U-shaped), Spearman's $r_s$ will be close to zero, just like Pearson's $r$.
*   **Ordinal Data or Ranked Continuous Data:** Suitable for ordinal variables or when continuous variables are converted to ranks. By using ranks, we lose information about the *magnitude* of differences between values. For example, a large difference in raw scores might result in the same rank difference as a small difference, which can sometimes obscure important distinctions.
*   **Robust to Outliers:** Because it uses ranks, it is less sensitive to outliers than Pearson's $r$. An outlier might change its rank by only a small amount, rather than disproportionately affecting the squared differences. This can be beneficial, but if outliers represent critical information, this robustness might hide their impact.
*   **Less Powerful than Pearson's $r$ for Linear Relationships:** If the relationship is truly linear and the data meet Pearson's assumptions, Pearson's $r$ is generally more powerful (i.e., more likely to detect a significant relationship and provide a more precise estimate).
*   **Sensitivity to Tied Ranks:** While tie-handling rules (average ranks) exist, a large number of ties can still affect the accuracy and interpretation of Spearman's $r_s$. With very small sample sizes, achieving perfect (+1 or -1) Spearman correlations is more likely by chance than with Pearson's $r$, potentially leading to spurious conclusions.

---

## Kendall Rank Correlation Coefficient (Kendall's Tau)

Kendall's Tau ($\tau$) is another non-parametric measure of the strength and direction of association between two ranked variables. It is an alternative to Spearman's $r_s$ and is particularly useful for assessing monotonic relationships with ordinal data. While Spearman's $r_s$ is based on the differences in ranks, Kendall's Tau is based on the number of **concordant and discordant pairs** of observations. Kendall's Tau is often considered more robust than Spearman's $\rho_S$ in the presence of ties and for smaller sample sizes.

### Concept of Concordant and Discordant Pairs

To understand Kendall's Tau, we need to consider pairs of observations. For any two distinct observations $i$ and $j$ from our dataset, we compare their values on both variables, $(x_i, y_i)$ and $(x_j, y_j)$.

For simplicity in counting, we typically sort the data based on $X$ in ascending order. If $X_i = X_j$, we then sort by $Y$. Then for any pair of observations $(x_i, y_i)$ and $(x_j, y_j)$ with $x_i < x_j$:

*   **Concordant Pair ($N_c$):** If $y_i < y_j$, the ranks for both variables move in the same direction (both increase). This pair contributes +1 to $N_c$.
*   **Discordant Pair ($N_d$):** If $y_i > y_j$, the ranks for the variables move in opposite directions (X increases, Y decreases). This pair contributes +1 to $N_d$.
*   **Tied Pair:** If $x_i = x_j$ (tie in X) or $y_i = y_j$ (tie in Y), the pair is considered a tie. Tied pairs are handled differently depending on the specific Tau variant.

Kendall's Tau essentially measures the "probability of concordance minus the probability of discordance."

### Formulas for Kendall's Tau

There are several versions of Kendall's Tau (Tau-a, Tau-b, Tau-c), primarily differing in how they handle ties. **Kendall's Tau-b ($\tau_b$)** is the most commonly used version when ties are present.

#### Kendall's Tau-a (no ties)

For data without any ties:

$$\tau_a = \frac{N_c - N_d}{\frac{n(n-1)}{2}}$$

where $N_c$ is the number of concordant pairs, $N_d$ is the number of discordant pairs, and $\frac{n(n-1)}{2}$ is the total number of distinct pairs possible from $n$ observations.

#### Derivation of Kendall's Tau-a

Let's derive the formula for Kendall's Tau-a.

The total number of unique pairs of observations we can form from $n$ data points is given by the combination formula "n choose 2":

$$ \text{Total Pairs} = \binom{n}{2} = \frac{n(n-1)}{2} $$

Each of these pairs can be classified as either concordant, discordant, or tied. For Kendall's Tau-a, we assume no ties, so every pair is either concordant or discordant.

Thus, the total number of pairs is simply the sum of concordant and discordant pairs:
$$ \text{Total Pairs} = N_c + N_d $$
Therefore,
$$ N_c + N_d = \frac{n(n-1)}{2} $$

Kendall's Tau-a is defined as the difference between the number of concordant pairs and the number of discordant pairs, normalized by the total number of possible pairs. This normalization ensures the value falls between -1 and +1.

$$ \tau_a = \frac{N_c - N_d}{\text{Total Pairs}} $$

Substituting the expression for the total number of pairs:

$$ \tau_a = \frac{N_c - N_d}{\frac{n(n-1)}{2}} $$

This derivation clearly shows how the formula for Kendall's Tau-a is constructed directly from the counts of concordant and discordant pairs and the total number of possible comparisons.

#### Kendall's Tau-b (with ties)

When ties are present, we adjust the denominator to account for them. Tied pairs cannot be definitively classified as concordant or discordant in the same way.

$$\tau_b = \frac{N_c - N_d}{\sqrt{\left(\frac{n(n-1)}{2} - N_x\right)\left(\frac{n(n-1)}{2} - N_y\right)}}$$

where:
*   $N_c$ is the number of concordant pairs.
*   $N_d$ is the number of discordant pairs.
*   $\frac{n(n-1)}{2}$ is the total number of possible pairs of observations (combinations of $n$ items taken 2 at a time)
*   $N_x = \sum_{j=1}^{g_x} \frac{t_j(t_j-1)}{2}$ is a correction for ties in variable $X$. Here, $g_x$ is the **number of groups** of tied ranks in $X$, and $t_j$ is the number of tied observations within the **$j$-th group**. This sum represents the number of pairs that are tied on $X$ but not necessarily on $Y$. These pairs are excluded from the denominator's calculation of "comparable" pairs because their relationship cannot be determined solely by $X$.
*   $N_y = \sum_{k=1}^{g_y} \frac{u_k(u_k-1)}{2}$ is a similar correction for ties in variable $Y$. $g_y$ is the **number of groups** of tied ranks in $Y$, and $u_k$ is the number of tied observations in the **$k$-th group**. This sum represents the number of pairs that are tied on $Y$ but not necessarily on $X$. These pairs are also excluded from the denominator's "comparable" pairs for similar reasons.

The denominator in $\tau_b$ effectively removes pairs that are tied on either $X$ or $Y$ from the total pool of comparable pairs, ensuring that the denominator only includes pairs that are truly comparable for evaluating concordance or discordance.

### Interpretation

Kendall's Tau also ranges from -1 to +1:

*   **+1:** Perfect positive monotonic association.
*   **-1:** Perfect negative monotonic association.
*   **0:** No monotonic association.

The interpretation of the magnitude of Kendall's Tau is often less intuitive than Pearson's $r$ or Spearman's $r_s$. It can be thought of as the difference between the probability that two randomly chosen observations will be in the same order (concordant) and the probability that they will be in a different order (discordant). Values of Kendall's Tau tend to be smaller in magnitude than Spearman's $r_s$ for the same data, even though both measure monotonic relationships. This is because they quantify different aspects of rank agreement.

### Assumptions and Limitations

*   **Monotonicity:** The relationship between the variables should be monotonic.
*   **Ordinal Data:** The variables can be measured on an ordinal scale, or their values can be meaningfully ranked.
*   **Robust to Outliers:** Like Spearman's $r_s$, Kendall's $\tau$ is less sensitive to outliers than Pearson's $r$ due to its reliance on ranks and pair comparisons.
*   **Computational Complexity:** For large datasets, counting all pairs can be computationally intensive, as it generally involves $O(n^2)$ comparisons (though optimized algorithms exist).
*   **Nuance of Tie Handling:** While $\tau_b$ accounts for ties, different methods of handling ties (e.g., using Kendall's Tau-c) exist, and the choice can subtly influence the result, highlighting that there's no single perfect way to deal with ambiguity arising from ties.

---

## Other Methods to Investigate Correlation

While Pearson, Spearman, and Kendall are widely used, they don't cover all types of relationships or data types. Here, we'll briefly explore a few other methods that are valuable in specific contexts, moving beyond strictly linear or monotonic relationships to more general forms of dependency.

### 1. Point-Biserial Correlation Coefficient ($r_{pb}$)

*   **Purpose**: Measures the strength and direction of the linear association between two variables when one is a **continuous (interval or ratio) variable** and the other is a **dichotomous nominal variable** (a categorical variable with exactly two categories, typically coded as 0 and 1).
*   **Conceptual Basis**: The point-biserial correlation coefficient is mathematically equivalent to Pearson's $r$ where one variable is dichotomous. It can also be understood as a way to quantify the standardized difference between the means of the continuous variable for the two groups defined by the dichotomous variable.
*   **Formula**:
    $$r_{pb} = \frac{\bar{X}_1 - \bar{X}_0}{s_X} \sqrt{\frac{n_1 n_0}{n^2}}$$
    where $\bar{X}_1$ and $\bar{X}_0$ are the means of the continuous variable for category 1 and 0 respectively, $s_X$ is the pooled standard deviation of the continuous variable, $n_1$ and $n_0$ are the number of observations in each category, and $n$ is the total number of observations.
*   **Interpretation**: Ranges from -1 to +1. A positive value implies higher values of the continuous variable are associated with one category, and negative with the other.
*   **Example**: Correlation between "exam score" (continuous) and "passed/failed a prerequisite course" (dichotomous: 0=failed, 1=passed).

### 2. Phi Coefficient ($\phi$)

*   **Purpose**: Measures the association between **two dichotomous nominal variables**. It is typically used for data presented in a $2 \times 2$ contingency table.
*   **Conceptual Basis**: Similar to the point-biserial correlation, the phi coefficient is also a special case of Pearson's $r$ applied to two dichotomous variables. It is also closely related to the chi-squared statistic.
*   **Formula**: For a $2 \times 2$ table with cell counts $a, b, c, d$:
    |       | $Y_1$ | $Y_2$ | Total |
    | :---- | :---- | :---- | :---- |
    | $X_1$ | $a$   | $b$   | $a+b$ |
    | $X_2$ | $c$   | $d$   | $c+d$ |
    | Total | $a+c$ | $b+d$ | $n$   |
    $$\phi = \frac{ad - bc}{\sqrt{(a+b)(c+d)(a+c)(b+d)}}$$
*   **Interpretation**: Ranges from -1 to +1. A positive value indicates a positive association, a negative value indicates a negative association, and 0 indicates no association.
*   **Example:** Correlation between "pass/fail status" on Exam A (pass/fail) and "pass/fail status" on Exam B (pass/fail). For sparse contingency tables (many zero counts), $\phi$ can be unstable.

### 3. Cramer's V

*   **Purpose**: Measures the association between **two nominal variables** when at least one of the variables has more than two categories (i.e., for $r \times c$ contingency tables where $r$ or $c$ is greater than 2).
*   **Conceptual Basis**: Cramer's V is a chi-square based measure of association, adjusting the chi-square statistic to range from 0 to 1, making it suitable for comparing associations across tables of different sizes.
*   **Formula**:
    $$V = \sqrt{\frac{\chi^2}{n \cdot \min(k-1, r-1)}}$$
    where $\chi^2$ is the Pearson chi-squared statistic, $n$ is the total number of observations, $k$ is the number of columns, and $r$ is the number of rows.
*   **Interpretation**: Ranges from 0 to +1. 0 indicates no association, and 1 indicates a perfect association. It does not provide information about the direction of the relationship, only its strength.
*   **Example**: Association between "favorite color" (red, blue, green) and "city of residence" (City A, City B, City C).

### 4. Distance Correlation

*   **Purpose:** Measures the strength of dependence between two random variables or two random vectors of arbitrary dimension. A key advantage is that **distance correlation is zero if and only if the random vectors are independent**. This is a much stronger property than Pearson's $r$, which only detects linear dependence.
*   **Concept:** It's based on comparing the characteristic functions of the joint distribution and the product of the marginal distributions. Essentially, it quantifies how similar the joint distribution is to what it would be if the variables were independent.
*   **Strengths:** Can detect non-linear and complex dependencies that Pearson's $r$ would miss. For example, if $Y = X^2$ or if $X$ and $Y$ have a circular relationship ($X=\cos(\theta), Y=\sin(\theta)$), Pearson's $r$ would be low or zero, but distance correlation would correctly report a high value, indicating strong dependence.
*   **Limitations:** Computationally more intensive for large datasets. Interpretation of the magnitude (e.g., a value of 0.5) is less intuitive than traditional correlation coefficients, and it can be sensitive to noise, especially in high dimensions.
*   **Example:** Detecting a U-shaped or parabolic relationship that Pearson's $r$ would incorrectly report as weak or non-existent.
*   **Example 2**: Detecting complex dependencies between gene expression levels and disease progression, where the relationship might not be linear or easily visualized.

### 5. Mutual Information

*   **Purpose:** A concept from information theory that quantifies the **amount of information obtained about one random variable by observing another random variable**. It measures general statistical dependence, including non-linear and non-monotonic relationships.
*   **Concept:** It's based on the entropy of the individual variables and their joint entropy. It calculates how much the uncertainty about one variable is reduced when the other variable is known.
*   **Formula (conceptual):** For discrete variables, $I(X;Y) = \sum_{y \in Y} \sum_{x \in X} p(x,y) \log \left(\frac{p(x,y)}{p(x)p(y)}\right)$. For continuous variables, this becomes an integral involving probability density functions. In practice, continuous variables are often discretized into bins or kernel density estimation is used to approximate the distributions, which can introduce sensitivity to bin choices or kernel parameters.
*   **Strengths:** Very powerful for detecting any form of statistical dependency. It is always non-negative, with 0 indicating independence. It doesn't assume any specific type of relationship or data distribution.
*   **Limitations:** The values are not bounded between -1 and +1, making direct comparisons of strength across different variable pairs less straightforward than with correlation coefficients. Requires estimation of probability distributions, which can be challenging for continuous variables.
*   **Example:** Understanding how much information about a person's "political affiliation" can be gained by knowing their "income bracket," even if the relationship is highly complex and non-linear.

### 6. Goodman and Kruskal's Gamma ($\gamma$)

*   **Purpose:** Another non-parametric measure for **ordinal variables**, similar to Kendall's Tau. It is particularly useful when dealing with a large number of ties.
*   **Concept:** It is based purely on the number of concordant and discordant pairs, but unlike Kendall's Tau, it *completely ignores* tied pairs in its denominator.
*   **Formula (conceptual):** $\gamma = \frac{N_c - N_d}{N_c + N_d}$
*   **Interpretation:** Ranges from -1 to +1. It measures the probability that a random pair of observations will have the same rank order on both variables, minus the probability that they will have different rank orders, *among those pairs that are not tied on either variable*. Because it ignores ties, Gamma often produces a higher magnitude correlation estimate than Tau for the same data, which might be misleading if ties are numerous and meaningful.
*   **Example:** Correlation between "satisfaction level" (low, medium, high) and "service quality rating" (poor, average, good, excellent).

### 7. Tetrachoric Correlation

*   **Purpose**: Measures the correlation between **two underlying continuous variables** that have both been artificially dichotomized (reduced to two categories). It estimates what the Pearson correlation would be if we could observe the continuous variables.
*   **Concept**: Assumes the underlying continuous variables are bivariate normally distributed. This is a strong assumption that is often untestable and might not hold in reality, potentially leading to misleading results. It's often estimated using maximum likelihood.
*   **Interpretation**: Ranges from -1 to +1.
*   **Example**: Estimating the correlation between "true mathematical ability" and "true verbal ability" based on pass/fail outcomes on two tests.

### 8. Polychoric Correlation

*   **Purpose**: A generalization of tetrachoric correlation. It measures the correlation between **two underlying continuous variables** that have both been artificially categorized into multiple ordered categories (ordinal variables).
*   **Concept**: Similar to tetrachoric, it assumes underlying bivariate normality and estimates the Pearson correlation from the observed ordinal data. The same strong assumptions about underlying continuous, normally distributed variables apply.
*   **Interpretation**: Ranges from -1 to +1.
*   **Example**: Estimating the correlation between "true job satisfaction" and "true work-life balance" from survey responses on a 5-point Likert scale for both.

### 9. Eta-squared ($\eta^2$) and Partial Eta-squared ($\eta_p^2$)

*   **Purpose**: Primarily used in **ANOVA (Analysis of Variance)** to measure the proportion of variance in a **dependent interval/ratio variable** that is explained by one or more **nominal (categorical) independent variables**. They are measures of effect size.
*   **Interpretation**: Ranges from 0 to 1. A value of 0.01 indicates a small effect, 0.06 a moderate effect, and 0.14 a large effect (Cohen's conventions).
*   **Example**: How much of the variance in "exam scores" (continuous) can be explained by "teaching method" (categorical: Method A, Method B, Method C).

### Maximal Information Coefficient (MIC)

*   **Purpose**: A measure of **general dependence** between two variables, capable of capturing a wide range of functional and non-functional relationships. It is part of the Maximal Information-based Nonparametric Exploration (MINE) family of statistics.
*   **Conceptual Basis**: MIC is based on the concept of mutual information from information theory. It estimates the maximum mutual information over all possible grids that can be drawn on the scatterplot of the data, normalizing it to a value between 0 and 1. Its calculation is computationally intensive, making a full derivation beyond the scope of this lecture.
*   **Interpretation**: Ranges from 0 to 1. A higher value indicates a stronger relationship.
*   **Example**: Identifying complex associations in large biological datasets or social network analysis, where relationships are often intricate and non-linear.

---

## Correlation does not imply causation!

A critical takeaway that we must always remember, regardless of the coefficient used, is the mantra: **"Correlation does not imply causation."** A strong statistical association between two variables indicates that they tend to vary together, but it does not, by itself, tell us that one variable causes the other. The observed relationship might be due to a confounding variable, pure coincidence, or even reverse causation. Establishing causation often requires rigorous experimental design. However, it's important to recognize that in many fields where randomized controlled trials are impractical or unethical, advanced observational causal inference techniques (e.g., instrumental variables, regression discontinuity, propensity score matching) are employed to move closer to causal claims. Furthermore, sometimes correlation *is* sufficient for actionable insights (e.g., "if X and Y correlate, we can use X to predict Y, even if we don't know why"). Correlation coefficients are powerful descriptive and exploratory tools, forming a fundamental part of our data analysis toolkit, and they serve as valuable starting points for generating hypotheses about potential causal links.

---

## Summary

| Coefficient / Concept | Description & Use Case | Formula(s) & Interpretation |
| :--- | :--- | :--- |
| **Pearson Correlation** ($r$, $\rho$) | Measures the strength and direction of a **linear relationship** between two **continuous** variables. It is sensitive to outliers. | **Sample Formula** $r_{XY} = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum (x_i - \bar{x})^2 \sum (y_i - \bar{y})^2}}$ <br> **Computational Formula** $r_{XY} = \frac{n \sum x_i y_i - (\sum x_i)(\sum y_i)}{\sqrt{[n \sum x_i^2 - (\sum x_i)^2][n \sum y_i^2 - (\sum y_i)^2]}}$ <br> **Interpretation:** Ranges from -1 (perfect negative linear) to +1 (perfect positive linear). 0 indicates no linear relationship. |
| **Spearman's Rank Correlation** ($r_s$) | A non-parametric measure of a **monotonic relationship** between two ranked variables. It is robust to outliers and does not assume a linear relationship. | **Definitional Formula** $r_s = \frac{\text{Cov}(R_X, R_Y)}{s_{R_X} s_{R_Y}}$ <br> **Simplified (no ties)** $r_s = 1 - \frac{6 \sum d_i^2}{n(n^2 - 1)}$ <br> **Interpretation:** Ranges from -1 (perfect negative monotonic) to +1 (perfect positive monotonic). 0 indicates no monotonic relationship. |
| **Kendall's Rank Correlation** ($\tau$) | Another non-parametric measure of a **monotonic relationship**. It is based on counting concordant and discordant pairs and is particularly robust with ties and small samples. | **Tau-a (no ties)** $\tau_a = \frac{N_c - N_d}{n(n-1)/2}$ <br> **Tau-b (with ties)** $\tau_b = \frac{N_c - N_d}{\sqrt{(\frac{n(n-1)}{2} - N_x)(\frac{n(n-1)}{2} - N_y)}}$ <br> **Interpretation:** Ranges from -1 to +1. Represents the difference between the probability of concordance and discordance. |
| **Point-Biserial Correlation** ($r_{pb}$) | Measures the association between one **continuous** variable and one **dichotomous** (two-category) variable. | $r_{pb} = \frac{\bar{X}_1 - \bar{X}_0}{s_X} \sqrt{\frac{n_1 n_0}{n^2}}$ <br> **Interpretation:** Ranges from -1 to +1, similar to Pearson's r. |
| **Phi Coefficient** ($\phi$) | Measures the association between **two dichotomous** variables, typically from a 2x2 contingency table. | $\phi = \frac{ad - bc}{\sqrt{(a+b)(c+d)(a+c)(b+d)}}$ <br> **Interpretation:** Ranges from -1 to +1. |
| **Cramer's V** | Measures the strength of association between **two nominal** variables where at least one has more than two categories. | $V = \sqrt{\frac{\chi^2}{n \cdot \min(k-1, r-1)}}$ <br> **Interpretation:** Ranges from 0 (no association) to +1 (perfect association). Does not show direction. |
| **Distance Correlation** | A powerful measure that detects both **linear and non-linear** dependencies between variables. | *Based on characteristic functions; no simple formula.* <br> **Interpretation:** Is 0 if and only if the variables are independent. A value greater than 0 indicates dependence. |
| **Mutual Information** $I(X;Y)$ | A measure from information theory that quantifies any kind of **statistical dependence** by measuring the reduction in uncertainty. | $I(X;Y) = \sum \sum p(x,y) \log (\frac{p(x,y)}{p(x)p(y)})$ <br> **Interpretation:** Is always non-negative. 0 indicates independence. Values are not capped at 1. |
| **Fundamental Principle** | **Correlation does not imply causation.** | A strong statistical relationship between two variables does not prove that one causes the other. The association may be due to coincidence, reverse causation, or a third, confounding variable. |

---

## Additional materials

* https://en.wikipedia.org/wiki/Correlation_does_not_imply_causation
* https://en.wikipedia.org/wiki/Correlation
* https://en.wikipedia.org/wiki/Causality
* https://en.wikipedia.org/wiki/Correlation_coefficient
* https://en.wikipedia.org/wiki/Pearson_correlation_coefficient
* https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient
* https://en.wikipedia.org/wiki/Kendall_rank_correlation_coefficient
* https://en.wikipedia.org/wiki/Ordinal_data
* https://en.wikipedia.org/wiki/Contingency_table
* https://en.wikipedia.org/wiki/Phi_coefficient
* https://en.wikipedia.org/wiki/Distance_correlation
* https://en.wikipedia.org/wiki/Mutual_information
* https://en.wikipedia.org/wiki/Information_theory
