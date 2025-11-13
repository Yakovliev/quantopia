# Variance and Covariance

> In statistics, we often use uppercase letters (e.g., $X$) to denote a **random variable**, which represents the abstract concept or process being measured (like the height of a person). Lowercase letters with an index (e.g., $x_i$) represent the specific **observations** or actual data points collected for that variable (e.g., $x_1 = 175\text{cm}$, $x_2 = 182\text{cm}$, etc.). While this document will primarily use the lowercase notation for calculations, it is helpful to remember this distinction.

## Mean (Average)

Before diving into variance and covariance, we need to understand the concept of the mean, also known as the average. The mean is a measure of central tendency, representing the typical value in a dataset.

For a set of $N$ data points (observations) $x_1, x_2, \ldots, x_N$:

**Population Mean ($\mu$)**: If we have the entire population, the mean is calculated as the sum of all observations divided by the number of observations.

$$\mu = \frac{\sum_{i=1}^{N} x_i}{N}$$

**Sample Mean ($\bar{x}$)**: If we have a sample from a larger population, the sample mean is calculated similarly.

$$\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n}$$

where $n$ is the number of observations in the sample.

## Variance

Variance is a measure of how spread out a set of data is. It quantifies the average of the squared differences from the mean. A high variance indicates that data points are spread far from the mean and from each other, while a low variance indicates that data points are clustered closely around the mean.

Why squared differences?
* **To avoid cancellation:** If we just summed the deviations $(x_i - \mu)$, positive and negative deviations would cancel out, potentially leading to a sum of zero even for widely dispersed data.
* **To penalize larger deviations more:** Squaring exaggerates larger differences, giving more weight to data points that are further from the mean.

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

This form can sometimes simplify calculations.

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

## Additional Materials

* https://www.ncl.ac.uk/webtemplate/ask-assets/external/maths-resources/statistics/descriptive-statistics/variance-and-standard-deviation.html
* https://mathsathome.com/variance/
* https://en.wikipedia.org/wiki/Covariance
* https://online.stat.psu.edu/stat505/book/export/html/643
* https://online.stat.psu.edu/stat505/book/export/html/653
