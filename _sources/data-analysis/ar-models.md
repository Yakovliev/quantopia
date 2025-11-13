# Autoregressive (AR) Models

Imagine we are tracking the daily temperature in a specific city. We intuitively know that today's temperature is probably influenced by yesterday's temperature, and perhaps even the day before that. It's unlikely that the temperature will suddenly jump from freezing to boiling hot without any prior indication. This idea - that a value in a sequence is dependent on its preceding values - is at the heart of time series analysis.

A **time series** is simply a sequence of data points indexed in time order. Examples include stock prices, monthly sales figures, daily rainfall, or even your heart rate over time. When we model a time series based on its *own past values*, we are engaging in a form of **autoregression**. The prefix "auto-" means "self," so we are essentially regressing the series on itself. Also, we assume that data points are equally spaced points in time.

This approach is incredibly useful because it allows us to capture the inherent temporal dependencies within the data. Instead of looking for external factors (like economic indicators affecting stock prices), we first try to understand the internal dynamics of the series itself.

The Autoregressive (AR) model is one of the simplest yet most effective tools for modeling time series data that exhibits autocorrelation, meaning that past values have a linear influence on current values. The Autoregressive (AR) model is a foundational approach that assumes the current value of the series, $Y_t$, can be explained as a linear function of its own past values, or "lags".

Think of an echo in a canyon. The sound we hear now is, in part, an echo of the sound produced moments ago. The strength of that echo diminishes over time. Similarly, in an AR model, the current value of a time series is a "noisy echo" of its past values.

Consider a simple scenario: predicting your mood tomorrow. Your mood today might be a significant factor. If you're happy today, you're more likely to be happy tomorrow. However, your mood from two days ago might have less direct influence, and your mood from a month ago probably has very little direct influence. The AR model formalizes this idea of decaying influence from past observations.

## The AR(1) Model: Our Starting Point

Let's begin with the simplest form of the Autoregressive model, known as AR(1). The '1' indicates that the current value of the time series depends only on its immediately preceding value.

We define the AR(1) model as:

$$Y_t = c + \phi_1 Y_{t-1} + \epsilon_t$$

where:
*   $Y_t$ is the value of the time series at time $t$.
*   $Y_{t-1}$ is the value of the time series at the previous time step, $t-1$.
*   $c$ is a constant term, representing the intercept or the baseline level of the series if all past influences were zero.
*   $\phi_1$ (phi-one) is the autoregressive coefficient. It quantifies the linear influence of the previous value $Y_{t-1}$ on the current value $Y_t$.
*   $\epsilon_t$ (epsilon-t) is the error term, also known as the white noise term. It represents the random shock or unpredictable component at time $t$ that cannot be explained by past values.

## The General AR(p) Model

The AR(1) model can be extended to an AR(p) model, where `p` denotes the order of the model. An AR(p) model means that the current value $Y_t$ depends on its past $p$ values ($Y_{t-1}, Y_{t-2}, ..., Y_{t-p}$).

We define the general AR(p) model as:

$$Y_t = c + \phi_1 Y_{t-1} + \phi_2 Y_{t-2} + \dots + \phi_p Y_{t-p} + \epsilon_t$$

This can be written more compactly using summation notation:

$$Y_t = c + \sum_{i=1}^{p} \phi_i Y_{t-i} + \epsilon_t$$

Here:
*   $p$ is the order of the AR model, representing how many past values influence the current value. It's a dimensionless integer.
*   $\phi_i$ are the autoregressive coefficients for lag $i$. These are dimensionless quantities.

---

## Underlying Mathematical Assumptions: The Foundation of AR Models

For the AR model to be valid and for its parameters to be reliably estimated, we rely on several key mathematical assumptions.

### Stationarity of the Time Series ($Y_t$)

*   **What it means**: A time series is considered **stationary** if its statistical properties (like mean, variance, and autocorrelation) do not change over time. Imagine taking a "snapshot" of the series at different points in time; the statistical characteristics should look roughly the same.
*   **Why it's important**: Stationarity is crucial because it allows us to make inferences about future values based on past observations. If the underlying statistical process is changing, then past relationships might not hold true in the future.
*   **Types of Stationarity**:
    *   **Strict Stationarity**: The joint probability distribution of any set of observations $(Y_{t_1}, ..., Y_{t_k})$ is the same as $(Y_{t_1+h}, ..., Y_{t_k+h})$ for any time shift $h$. This is a very strong condition.
    *   **Weak (or Covariance) Stationarity**: This is a more commonly used and less restrictive assumption. A time series is weakly stationary if:
        1.  The mean is constant: $E[Y_t] = \mu$ for all $t$.
        2.  The variance is constant: $Var(Y_t) = E[(Y_t - \mu)^2] = \sigma_Y^2$ for all $t$.
        3.  The autocovariance depends only on the lag, not on the time $t$: $Cov(Y_t, Y_{t-k}) = E[(Y_t - \mu)(Y_{t-k} - \mu)] = \gamma_k$ for all $t$ and any lag $k$.

### White Noise Error Term ($\epsilon_t$)

The error term $\epsilon_t$ is assumed to be a **white noise process**. This means it is a sequence of uncorrelated random variables with constant mean and variance.
Specifically, for $\epsilon_t$:

1.  **Zero Mean**: The expected value of the error at any time point is zero.

    $$E[\epsilon_t] = 0$$
    
    for all $t$.
2.  **Constant Variance**: The variance of the error is constant over time. This property is called **homoscedasticity**.

    $$Var(\epsilon_t) = \sigma_\epsilon^2$$
3.  **No Autocorrelation**: The errors are uncorrelated with each other across time. The error at one point in time gives no information about the error at another point. This is crucial because it means that the errors themselves are unpredictable and do not contain any systematic information that could be used to improve the model. If errors were correlated, it would imply that our model hasn't captured all the temporal dependencies.

    $$\text{Cov}(\epsilon_t, \epsilon_s) = 0 \quad \text{for} \quad t \neq s$$
    
4.  **Independence (often implied or assumed for inference)**: While not strictly necessary for estimation methods like OLS, for statistical inference (e.g., hypothesis testing, confidence intervals), it is often assumed that $\epsilon_t$ is independently and identically distributed (i.i.d.).
5.  **Often (but not always) Normal Distribution**: For statistical inference, it is often assumed that $\epsilon_t \sim N(0, \sigma_\epsilon^2)$.

These assumptions ensure that our model is well-behaved, that we can accurately estimate its parameters, and that our forecasts are statistically sound.

## Derivation of Stationarity Condition for AR(1)

Let's derive the condition for stationarity for an AR(1) model.

Our AR(1) model is $Y_t = c + \phi_1 Y_{t-1} + \epsilon_t$.

**1. Constant Mean ($E[Y_t] = \mu$)**:

If the series is stationary, then $E[Y_t] = E[Y_{t-1}] = \mu$. We also assume the error term $\epsilon_t$ has a mean of zero, i.e., $E[\epsilon_t] = 0$.

Taking the expectation of the AR(1) equation:

$$E[Y_t] = E[c + \phi_1 Y_{t-1} + \epsilon_t]$$

Using the linearity of expectation:

$$E[Y_t] = E[c] + E[\phi_1 Y_{t-1}] + E[\epsilon_t]$$

$$\mu = c + \phi_1 E[Y_{t-1}] + 0$$

Since $E[Y_{t-1}] = \mu$ for a stationary series:

$$\mu = c + \phi_1 \mu$$

Now, we can solve for $\mu$:

$$\mu - \phi_1 \mu = c$$

$$\mu (1 - \phi_1) = c$$

$$\mu = \frac{c}{1 - \phi_1}$$

For $\mu$ to be well-defined and finite, we must have $1 - \phi_1 \neq 0$, which means $\phi_1 \neq 1$.

**2. Constant Variance ($Var(Y_t) = \sigma_Y^2$)**:

For a stationary series, the variance $Var(Y_t)$ must also be constant over time, let's denote it as $\sigma_Y^2$. We also assume $\epsilon_t$ is white noise with variance $Var(\epsilon_t) = \sigma_\epsilon^2$.

First, let's express $Y_t$ in terms of deviations from its mean, $Y_t - \mu$:

$$Y_t - \mu = c + \phi_1 Y_{t-1} + \epsilon_t - \mu$$

Substitute $c = \mu(1 - \phi_1)$ (from the mean derivation):

$$Y_t - \mu = \mu(1 - \phi_1) + \phi_1 Y_{t-1} + \epsilon_t - \mu$$

$$Y_t - \mu = \mu - \phi_1 \mu + \phi_1 Y_{t-1} + \epsilon_t - \mu$$

$$Y_t - \mu = \phi_1 (Y_{t-1} - \mu) + \epsilon_t$$

Let's denote $y'_t = Y_t - \mu$. Then:

$$y'_t = \phi_1 y'_{t-1} + \epsilon_t$$

Now, we can find the variance $Var(y'_t) = \sigma_Y^2$:

$$Var(y'_t) = Var(\phi_1 y'_{t-1} + \epsilon_t)$$

Since $\epsilon_t$ is independent of $y'_{t-1}$ (as $\epsilon_t$ is a shock at time $t$ and $y'_{t-1}$ depends on past shocks), we can write:

$$Var(y'_t) = Var(\phi_1 y'_{t-1}) + Var(\epsilon_t)$$

$$\sigma_Y^2 = \phi_1^2 Var(y'_{t-1}) + \sigma_\epsilon^2$$

For a stationary series, $Var(y'_t) = Var(y'_{t-1}) = \sigma_Y^2$:

$$\sigma_Y^2 = \phi_1^2 \sigma_Y^2 + \sigma_\epsilon^2$$

$$\sigma_Y^2 (1 - \phi_1^2) = \sigma_\epsilon^2$$

$$\sigma_Y^2 = \frac{\sigma_\epsilon^2}{1 - \phi_1^2}$$

For the variance $\sigma_Y^2$ to be positive and finite, we must have $1 - \phi_1^2 > 0$.
This implies $\phi_1^2 < 1$, which means $-1 < \phi_1 < 1$.

So, the condition for an AR(1) process to be weakly stationary is that the absolute value of its autoregressive coefficient $\phi_1$ must be less than 1:

$$|\phi_1| < 1$$

If $|\phi_1| \ge 1$, the series will exhibit explosive behavior (grow indefinitely) or persist indefinitely, and its variance will not be constant.

## Condition for Stationarity in AR(p): The Characteristic Polynomial

For an AR(p) process to be weakly stationary, the condition is a generalization of the $|\phi_1| < 1$ requirement. It involves the roots of its characteristic polynomial.

The original model is:

$$Y_t = c + \phi_1 Y_{t-1} + \phi_2 Y_{t-2} + \dots + \phi_p Y_{t-p} + \epsilon_t$$

Or, using summation notation:

$$Y_t = c + \sum_{i=1}^{p} \phi_i Y_{t-i} + \epsilon_t$$

Just like in the AR(1) case, we assume the process is **stationary**. A key property of a stationary process is that its mean is constant over time. Let's call this mean $\mu$.

*   $E[Y_t] = \mu$
*   $E[Y_{t-1}] = \mu$
*   ...
*   $E[Y_{t-p}] = \mu$

We also know that the error term $\epsilon_t$ is white noise with a mean of zero:
*   $E[\epsilon_t] = 0$

Now, let's take the expectation (the "mean") of both sides of the AR(p) equation:

$$E[Y_t] = E[c + \sum_{i=1}^{p} \phi_i Y_{t-i} + \epsilon_t]$$

Using the rules of expectation (it's a linear operator):

$$\mu = E[c] + \sum_{i=1}^{p} \phi_i E[Y_{t-i}] + E[\epsilon_t]$$

Substitute the known mean values:

$$\mu = c + \sum_{i=1}^{p} \phi_i \mu + 0$$

Now we have an expression relating the constant $c$ to the mean $\mu$.

Our goal is to substitute $c$ out of the original equation. Let's rearrange the equation to solve for $c$:

$$\mu - \sum_{i=1}^{p} \phi_i \mu = c$$

Factor out $\mu$ from the left side:

$$c = \mu \left( 1 - \sum_{i=1}^{p} \phi_i \right)$$

This equation tells us that the constant term $c$ is directly related to the mean of the series ($\mu$) and the sum of the autoregressive coefficients ($\phi_i$).

Now, take the original AR(p) model and replace $c$ with the expression we just derived:

$$Y_t = \underbrace{\mu \left( 1 - \sum_{i=1}^{p} \phi_i \right)}_{c} + \sum_{i=1}^{p} \phi_i Y_{t-i} + \epsilon_t$$

This is where the algebra comes in. We want to group terms that involve $\mu$ with terms that involve $Y$.

First, move the $\mu$ term from the right side to the left side:

$$Y_t - \mu = -\mu \sum_{i=1}^{p} \phi_i + \sum_{i=1}^{p} \phi_i Y_{t-i} + \epsilon_t$$

Now, we can combine the two summations because they both run from $i=1$ to $p$:

$$Y_t - \mu = \sum_{i=1}^{p} (\phi_i Y_{t-i} - \phi_i \mu) + \epsilon_t$$

Factor out the $\phi_i$ term inside the summation:

$$Y_t - \mu = \sum_{i=1}^{p} \phi_i (Y_{t-i} - \mu) + \epsilon_t$$

The term $(Y_t - \mu)$ represents the deviation of the series from its mean at time $t$. The term $(Y_{t-i} - \mu)$ is the deviation from the mean at time $(t-i)$.

Let's define a new variable, $y'_t$, to represent this deviation:

$$y'_t = Y_t - \mu$$

Now, substitute this new variable into our rearranged equation:

$$y'_t = \sum_{i=1}^{p} \phi_i y'_{t-i} + \epsilon_t$$

If we expand the summation, we get the following expression:

$$y'_t = \phi_1 y'_{t-1} + \phi_2 y'_{t-2} + \dots + \phi_p y'_{t-p} + \epsilon_t$$

This is the **mean-centered** or **de-meaned** form of the AR(p) model. We've shown that an AR(p) process with a constant $c$ is equivalent to an AR(p) process with no constant, but applied to the series after its mean has been subtracted out.

This simplified form is much easier to work with when analyzing theoretical properties like stationarity using tools like the characteristic polynomial, as it removes the constant $c$.

Let's introduce the **lag operator** $L$, where $L Y_t = Y_{t-1}$, $L^2 Y_t = Y_{t-2}$, and so on.

So, we have:

$$y'_t = \phi_1 y'_{t-1} + \phi_2 y'_{t-2} + \dots + \phi_p y'_{t-p} + \epsilon_t$$

Now, apply the lag operator:

$$y'_t = \phi_1 L y'_t + \phi_2 L^2 y'_t + \dots + \phi_p L^p y'_t + \epsilon_t$$

Rearranging the terms to group $y'_t$:

$$y'_t - \phi_1 L y'_t - \phi_2 L^2 y'_t - \dots - \phi_p L^p y'_t = \epsilon_t$$

$$(1 - \phi_1 L - \phi_2 L^2 - \dots - \phi_p L^p) y'_t = \epsilon_t$$

The polynomial in $L$ is called the **autoregressive polynomial**:

$$\Phi(L) = 1 - \phi_1 L - \phi_2 L^2 - \dots - \phi_p L^p$$

So the AR($p$) model can be written as:

$$\Phi(L) y'_t = \epsilon_t$$

The **characteristic equation** is obtained by setting the autoregressive polynomial to zero and replacing the lag operator $L$ with a complex variable (often $z$ or $x$):

$$1 - \phi_1 z - \phi_2 z^2 - \dots - \phi_p z^p = 0$$

The condition for an AR($p$) process to be stationary is that **all the roots of the characteristic equation must lie outside the unit circle** in the complex plane. This means that the absolute value (modulus) of each root must be greater than 1. If any root lies inside or on the unit circle, the process is non-stationary and requires differencing (leading to ARIMA models) or other transformations.

### Additional Notes about Characteristic Polynomial

We rearranged our AR(p) model into a compact form using the lag operator $L$:

$$(1 - \phi_1 L - \phi_2 L^2 - \dots - \phi_p L^p) y'_t = \epsilon_t$$

Or more simply:

$$\Phi(L) y'_t = \epsilon_t$$

Then, we stated that to check for stationarity, we must analyze the roots of the **characteristic equation**, which is found by setting the autoregressive polynomial to zero and replacing the lag operator $L$ with a complex variable $z$:

$$\Phi(z) = 1 - \phi_1 z - \phi_2 z^2 - \dots - \phi_p z^p = 0$$

This can feel like a "black box" mathematical trick. Why do we do this? The reason is that we are borrowing a powerful technique used for solving **linear difference equations** (note that this is NOT linear differential equations). You can find more information about this type of equations in the "Additional Materials" section of this lecture.

Our AR(p) model for the mean-centered series, $y'_t = \sum_{i=1}^{p} \phi_i y'_{t-i} + \epsilon_t$, is precisely such an equation. The value at time $t$ is a linear combination of previous values, plus an external term ($\epsilon_t$).

The stability and long-term behavior of such a system are determined by its **homogeneous part** (the equation without the error term $\epsilon_t$):

$$y'_t - \phi_1 y'_{t-1} - \phi_2 y'_{t-2} - \dots - \phi_p y'_{t-p} = 0$$

To understand the behavior of this system, mathematicians look for solutions of the form $y'_t = x^t$. Why this form? Because it has a convenient property where lags are just powers of $x$: $y'_{t-1} = x^{t-1}$, $y'_{t-2} = x^{t-2}$, and so on.

If we substitute $y'_t = x^t$ into the homogeneous equation, we get:

$$x^t - \phi_1 x^{t-1} - \phi_2 x^{t-2} - \dots - \phi_p x^{t-p} = 0$$

Now, we can divide the entire equation by $x^{t-p}$ (assuming $x \neq 0$) to eliminate the time index $t$:

$$x^p - \phi_1 x^{p-1} - \phi_2 x^{p-2} - \dots - \phi_p = 0$$

This is one form of the characteristic equation. To get the form we mentioned before, we just need to divide this equation by $x^p$:

$$1 - \phi_1 x^{-1} - \phi_2 x^{-2} - \dots - \phi_p x^{-p} = 0$$

and substitute $z = \frac{1}{x}$:

$$1 - \phi_1 z - \phi_2 z^2 - \dots - \phi_p z^p = 0$$

For mathematical convenience and consistency in time series literature, we use the polynomial in $L$ and replace $L$ with $z$.

In essence, replacing the lag operator $L$ with a variable $z$ transforms our time-domain problem into an algebraic problem. The variable $z$ allows us to use the powerful tools of polynomial algebra to analyze the fundamental properties (like stability and stationarity) of our time series model, independent of any specific values in the series.

Now, let's review the even more details. We've established the condition for stationarity: **all roots of the characteristic equation $\Phi(z) = 0$ must lie outside the unit circle**. Let's explore *why* this is the case, building our intuition from the AR(1) model up to the general AR(p) case.

The core idea is that for a series to be stationary, the impact of a random shock $\epsilon_t$ from the distant past must eventually fade away. If a shock from a year ago still has a significant and non-diminishing impact on the series today, then the variance of the series would not be constant, and the process would be non-stationary.

#### Intuition from the AR(1) Model

Recall our mean-centered AR(1) model: $y'_t = \phi_1 y'_{t-1} + \epsilon_t$. We can also write this using the lag polynomial: $(1 - \phi_1 L) y'_t = \epsilon_t$.

Let's formally "solve" for $y'_t$ by dividing by the polynomial:

$$y'_t = \frac{1}{1 - \phi_1 L} \epsilon_t = (1 - \phi_1 L)^{-1} \epsilon_t$$

Using the formula for a geometric series, where $(1-x)^{-1} = 1 + x + x^2 + x^3 + \dots$, we can expand this expression:

$$y'_t = (1 + \phi_1 L + \phi_1^2 L^2 + \phi_1^3 L^3 + \dots) \epsilon_t$$

Applying the lag operator to $\epsilon_t$:

$$y'_t = \epsilon_t + \phi_1 \epsilon_{t-1} + \phi_1^2 \epsilon_{t-2} + \phi_1^3 \epsilon_{t-3} + \dots$$

This is known as the **moving average (MA) representation** of the AR(1) process. It shows that the current value $y'_t$ is a weighted sum of all past random shocks.

For this series to be stationary, the weights on these past shocks must diminish to zero as we go further back in time. The weights are $1, \phi_1, \phi_1^2, \phi_1^3, \dots$. This sequence converges to zero if and only if $|\phi_1| < 1$. This is the same stationarity condition we derived earlier by calculating the variance.

Now, let's connect this back to the characteristic equation:
*   The equation is $1 - \phi_1 z = 0$.
*   The root is $z = 1 / \phi_1$.
*   If our stationarity condition $|\phi_1| < 1$ holds, then the absolute value of the root is $|z| = |1 / \phi_1| = 1 / |\phi_1|$.
*   Since $|\phi_1| < 1$, it follows that $1 / |\phi_1| > 1$.
*   Therefore, the condition $|\phi_1| < 1$ is mathematically equivalent to the condition that the root $z$ lies outside the unit circle ($|z| > 1$).

#### Generalizing to the AR(p) Model

This same logic extends to the AR(p) model. We start with the compact form:

$$y'_t = \Phi(L)^{-1} \epsilon_t$$

To have a valid stationary process, we must be able to express $\Phi(L)^{-1}$ as a convergent infinite series of lag operators, just as we did for the AR(1) case:

$$\Phi(L)^{-1} = \sum_{j=0}^{\infty} \psi_j L^j \quad \text{where} \quad \sum_{j=0}^{\infty} |\psi_j| < \infty$$

This ensures that the weights ($\psi_j$) on past shocks diminish over time. From the theory of polynomial algebra and complex analysis, we know that the power series expansion of a function like $1/\Phi(z)$ converges if and only if the evaluation point (in our case, the unit circle and its interior) does not contain any roots of the denominator polynomial $\Phi(z)$.

Therefore, for the moving average MA(∞) representation to be well-behaved and for the process to be stationary, all roots of the characteristic polynomial $\Phi(z)=0$ must lie *outside* the unit circle.

**What happens if a root is inside or on the unit circle?**

*   **A root on the unit circle ($|z|=1$)**: This is called a **unit root**. It means the effect of a past shock persists indefinitely and is never forgotten. The variance of the process becomes time-dependent and grows to infinity. This is a hallmark of non-stationary series like a random walk.
*   **A root inside the unit circle ($|z|<1$)**: This corresponds to an **explosive** process. The impact of a past shock is amplified over time, causing the series to diverge to infinity.

In summary, the condition that all roots lie outside the unit circle is the precise mathematical requirement to ensure that the influence of past shocks eventually dies out, which is the fundamental property of a stationary time series.

---

# Identifying Key Parameters: Unveiling the Model's Secrets

Once we have a time series, the first challenge is to determine if an AR model is appropriate and, if so, what its order $p$ is, and what the values of its coefficients ($\phi_i$) are.

## 4.1 Determining the Order (p): Autocorrelation and Partial Autocorrelation Functions

The **Autocorrelation Function (ACF)** and **Partial Autocorrelation Function (PACF)** are indispensable tools for identifying the order of an AR model. They help us understand how much past values directly or indirectly influence current values.

### Autocorrelation Function (ACF)

The ACF measures the linear relationship between an observation at time $t$ and an observation at a previous time $t-k$. It tells us the *total* correlation between $Y_t$ and $Y_{t-k}$, including indirect effects.

For a stationary time series, the autocorrelation at lag $k$, denoted $\rho_k$, is defined as:

$$ \rho_k = \frac{Cov(Y_t, Y_{t-k})}{\sqrt{Var(Y_t) Var(Y_{t-k})}} = \frac{\gamma_k}{\gamma_0} $$

where:
*   $Cov(Y_t, Y_{t-k}) = \gamma_k$ is the autocovariance between $Y_t$ and $Y_{t-k}$.
*   $Var(Y_t) = \gamma_0$ is the variance of the time series $Y_t$. Since we assume stationarity, $Var(Y_t) = Var(Y_{t-k})$.

**Behavior for AR(p) models**:
For an AR(p) process, the ACF will typically decay exponentially or with a dampened sine wave pattern. It does *not* cut off sharply; instead, the influence gradually diminishes over increasing lags. This decay pattern is characteristic of AR models.

### Partial Autocorrelation Function (PACF)

The PACF measures the *direct* linear relationship between $Y_t$ and $Y_{t-k}$, *after removing the influence of the intermediate observations* $Y_{t-1}, Y_{t-2}, \dots, Y_{t-k+1}$.

Think of it this way: Imagine a chain of dominoes. The ACF between the first and third domino falling would consider the total correlation, including the indirect effect through the second domino. The PACF, however, would try to measure the direct impact of the first domino on the third, *if the second domino's effect was somehow factored out*. In time series, the PACF for $Y_t$ and $Y_{t-k}$ attempts to isolate the correlation that isn't already explained by the linear combination of $Y_{t-1}, \dots, Y_{t-k+1}$.

**Behavior for AR(p) models**:
For an AR(p) process, the PACF is the key diagnostic tool for identifying the order $p$. The PACF will **cut off sharply after lag p**. This means that the partial autocorrelations at lags greater than $p$ will be close to zero and fall within the confidence bounds of statistical insignificance.

*   For an AR(1) model, the PACF will have a significant spike at lag 1 and then cut off.
*   For an AR(2) model, the PACF will have significant spikes at lags 1 and 2, and then cut off.

### Information Criteria (AIC, BIC)

While ACF and PACF plots are visual tools, information criteria provide a more quantitative approach to model selection.
*   **Akaike Information Criterion (AIC)**
*   **Bayesian Information Criterion (BIC)**

These criteria balance model fit with model complexity. They penalize models with more parameters to avoid overfitting. The model with the lowest AIC or BIC is generally preferred. We typically compute these values for AR models of different orders ($p=1, 2, 3, \dots$) and choose the $p$ that minimizes the criterion.

## 4.2 Estimating Coefficients ($\phi_i$) and Constant (c)

Once we have identified the likely order $p$ of our AR model, the next step is to estimate the coefficients $\phi_i$ and the constant $c$. Two common and effective methods for this are Ordinary Least Squares (OLS) and the Yule-Walker equations.

### Derivation of OLS for AR(1) Model

OLS works by finding the values of the coefficients that minimize the sum of the squared differences between the observed values ($Y_t$) and the values predicted by our model ($\hat{Y}_t$). These differences are the error terms $\epsilon_t$.

Let's derive the OLS estimators for the simplest case, the AR(1) model.

Our AR(1) model is:

$$Y_t = c + \phi_1 Y_{t-1} + \epsilon_t$$

We want to find $c$ and $\phi_1$ that minimize the sum of squared errors (SSE):

$$ SSE = \sum_{t=2}^{N} \epsilon_t^2 = \sum_{t=2}^{N} (Y_t - c - \phi_1 Y_{t-1})^2 $$

Note that the sum starts from $t=2$ because $Y_1$ is the first observation for which $Y_{t-1}$ (i.e., $Y_0$) is not available in our observed series. For large $N$, this starting point doesn't significantly impact the estimation.

To find the minimum, we take the partial derivatives of SSE with respect to $c$ and $\phi_1$ and set them to zero.

**1. Partial derivative with respect to $c$**:

$$ \frac{\partial SSE}{\partial c} = \frac{\partial}{\partial c} \sum_{t=2}^{N} (Y_t - c - \phi_1 Y_{t-1})^2 $$

$$ = \sum_{t=2}^{N} 2(Y_t - c - \phi_1 Y_{t-1})(-1) $$

Setting this to zero:

$$ \sum_{t=2}^{N} (Y_t - c - \phi_1 Y_{t-1}) = 0 $$

$$ \sum_{t=2}^{N} Y_t - \sum_{t=2}^{N} c - \sum_{t=2}^{N} \phi_1 Y_{t-1} = 0 $$

Let $N' = N-1$ be the number of observations used in the regression.

$$ \sum_{t=2}^{N} Y_t - N'c - \phi_1 \sum_{t=2}^{N} Y_{t-1} = 0 $$

This gives us the first "normal equation":

$$ N'c = \sum_{t=2}^{N} Y_t - \phi_1 \sum_{t=2}^{N} Y_{t-1} \quad (1) $$

**2. Partial derivative with respect to $\phi_1$**:

$$ \frac{\partial SSE}{\partial \phi_1} = \frac{\partial}{\partial \phi_1} \sum_{t=2}^{N} (Y_t - c - \phi_1 Y_{t-1})^2 $$

$$ = \sum_{t=2}^{N} 2(Y_t - c - \phi_1 Y_{t-1})(-Y_{t-1}) $$

Setting this to zero:

$$ \sum_{t=2}^{N} Y_{t-1}(Y_t - c - \phi_1 Y_{t-1}) = 0 $$

$$ \sum_{t=2}^{N} Y_{t-1}Y_t - \sum_{t=2}^{N} c Y_{t-1} - \sum_{t=2}^{N} \phi_1 Y_{t-1}^2 = 0 $$

$$ \sum_{t=2}^{N} Y_{t-1}Y_t - c \sum_{t=2}^{N} Y_{t-1} - \phi_1 \sum_{t=2}^{N} Y_{t-1}^2 = 0 $$

This gives us the second "normal equation":

$$ \sum_{t=2}^{N} Y_{t-1}Y_t = c \sum_{t=2}^{N} Y_{t-1} + \phi_1 \sum_{t=2}^{N} Y_{t-1}^2 \quad (2) $$

Now we have a system of two linear equations with two unknowns ($c$ and $\phi_1$):

1.  $N'c + \phi_1 \sum_{t=2}^{N} Y_{t-1} = \sum_{t=2}^{N} Y_t$
2.  $c \sum_{t=2}^{N} Y_{t-1} + \phi_1 \sum_{t=2}^{N} Y_{t-1}^2 = \sum_{t=2}^{N} Y_{t-1}Y_t$

Solving this system for $c$ and $\phi_1$ will give us the OLS estimators.

From equation (1), we can express $c$:

$$ c = \frac{1}{N'} \left( \sum_{t=2}^{N} Y_t - \phi_1 \sum_{t=2}^{N} Y_{t-1} \right) = \bar{Y}_t - \phi_1 \bar{Y}_{t-1} $$

where $\bar{Y}_t = \frac{1}{N'} \sum_{t=2}^{N} Y_t$ and $\bar{Y}_{t-1} = \frac{1}{N'} \sum_{t=2}^{N} Y_{t-1}$ are the sample means of $Y_t$ and $Y_{t-1}$ respectively over the regression period.

Substitute this expression for $c$ into equation (2):

$$ (\bar{Y}_t - \phi_1 \bar{Y}_{t-1}) \sum_{t=2}^{N} Y_{t-1} + \phi_1 \sum_{t=2}^{N} Y_{t-1}^2 = \sum_{t=2}^{N} Y_{t-1}Y_t $$

$$ \bar{Y}_t \sum_{t=2}^{N} Y_{t-1} - \phi_1 \bar{Y}_{t-1} \sum_{t=2}^{N} Y_{t-1} + \phi_1 \sum_{t=2}^{N} Y_{t-1}^2 = \sum_{t=2}^{N} Y_{t-1}Y_t $$

Rearrange to solve for $\phi_1$:

$$ \phi_1 \left( \sum_{t=2}^{N} Y_{t-1}^2 - \bar{Y}_{t-1} \sum_{t=2}^{N} Y_{t-1} \right) = \sum_{t=2}^{N} Y_{t-1}Y_t - \bar{Y}_t \sum_{t=2}^{N} Y_{t-1} $$

We know that $\sum_{t=2}^{N} Y_{t-1} = N' \bar{Y}_{t-1}$. So:

$$ \phi_1 \left( \sum_{t=2}^{N} Y_{t-1}^2 - N' \bar{Y}_{t-1}^2 \right) = \sum_{t=2}^{N} Y_{t-1}Y_t - N' \bar{Y}_t \bar{Y}_{t-1} $$

The terms in the parentheses and on the right side are related to sample variances and covariances. Specifically:
*   $\sum_{t=2}^{N} (Y_{t-1} - \bar{Y}_{t-1})^2 = \sum Y_{t-1}^2 - N' \bar{Y}_{t-1}^2$ (sample sum of squares for $Y_{t-1}$)
*   $\sum_{t=2}^{N} (Y_t - \bar{Y}_t)(Y_{t-1} - \bar{Y}_{t-1}) = \sum Y_t Y_{t-1} - N' \bar{Y}_t \bar{Y}_{t-1}$ (sample sum of cross-products)

Thus, the OLS estimator for $\phi_1$ is:

$$ \hat{\phi}_1 = \frac{\sum_{t=2}^{N} (Y_t - \bar{Y}_t)(Y_{t-1} - \bar{Y}_{t-1})}{\sum_{t=2}^{N} (Y_{t-1} - \bar{Y}_{t-1})^2} $$

This is precisely the formula for the sample correlation coefficient multiplied by the ratio of standard deviations, or more simply, the ratio of the sample autocovariance at lag 1 to the sample variance.

Once $\hat{\phi}_1$ is found, we can substitute it back into the equation for $c$:

$$ \hat{c} = \bar{Y}_t - \hat{\phi}_1 \bar{Y}_{t-1} $$

These are our OLS estimators for the AR(1) model.

### Generalization of OLS to AR(p)

For a general AR(p) model, the OLS method extends naturally. We would minimize the sum of squared errors:

$$ SSE = \sum_{t=p+1}^{N} (Y_t - c - \sum_{i=1}^{p} \phi_i Y_{t-i})^2 $$

This involves taking $p+1$ partial derivatives (one for $c$ and $p$ for $\phi_i$) and setting them to zero. This leads to a system of $p+1$ linear equations (the normal equations) that can be solved using matrix algebra. The principle remains the same: find the coefficients that best fit the data in a least squares sense.

### Yule-Walker Equations

The Yule-Walker equations provide another way to estimate the AR coefficients by relating them to the autocovariances (or autocorrelations) of the time series. These equations are derived by multiplying the AR($p$) equation by $Y_{t-k}$ for different lags $k$ and then taking expectations.

Let's derive them for an AR(1) model, assuming the series is stationary and has mean $\mu=0$ (we can always center the series by subtracting its mean if $c \neq 0$). So, $Y_t = \phi_1 Y_{t-1} + \epsilon_t$.

Multiply by $Y_{t-k}$ for $k \ge 1$:

$$Y_t Y_{t-k} = \phi_1 Y_{t-1} Y_{t-k} + \epsilon_t Y_{t-k}$$

Now, take the expectation of both sides:

$$E[Y_t Y_{t-k}] = E[\phi_1 Y_{t-1} Y_{t-k}] + E[\epsilon_t Y_{t-k}]$$

Since $E[Y_t Y_{t-k}] = \gamma_k$ (the autocovariance at lag $k$) and $E[\epsilon_t Y_{t-k}] = 0$ for $k \ge 1$ (because $\epsilon_t$ is uncorrelated with past values of $Y$), we get:

$$\gamma_k = \phi_1 \gamma_{k-1}$$

For $k=1$:

$$\gamma_1 = \phi_1 \gamma_0$$

Recall that $\gamma_0 = Var(Y_t) = \sigma_Y^2$.
We can divide by $\gamma_0$ to express this in terms of autocorrelations $\rho_k = \frac{\gamma_k}{\gamma_0}$:

$$\rho_1 = \phi_1 \rho_0$$

Since $\rho_0 = 1$ (correlation of a series with itself at lag 0 is 1):

$$\rho_1 = \phi_1$$

This gives us a direct way to estimate $\phi_1$ for an AR(1) model: it's simply the autocorrelation at lag 1.

For a general AR($p$) model, the Yule-Walker equations form a system of linear equations:

$$\rho_k = \phi_1 \rho_{k-1} + \phi_2 \rho_{k-2} + \dots + \phi_p \rho_{k-p} \quad \text{for } k=1, 2, \dots, p$$

In matrix form, for $p$ equations:

```math
\begin{pmatrix}
\rho_0 & \rho_1 & \dots & \rho_{p-1} \\
\rho_1 & \rho_0 & \dots & \rho_{p-2} \\
\vdots & \vdots & \ddots & \vdots \\
\rho_{p-1} & \rho_{p-2} & \dots & \rho_0
\end{pmatrix}
\begin{pmatrix}
\phi_1 \\
\phi_2 \\
\vdots \\
\phi_p
\end{pmatrix}
=
\begin{pmatrix}
\rho_1 \\
\rho_2 \\
\vdots \\
\rho_p
\end{pmatrix}
```

By replacing the theoretical autocorrelations $\rho_k$ with their sample estimates $\hat{\rho}_k$ (calculated from the observed data), we can solve this system of equations to get estimates for $\hat{\phi}_1, \dots, \hat{\phi}_p$.

---

# 5. Putting Theory into Practice: Python with `statsmodels`

Now that we have a solid theoretical foundation, let's see how we can apply these concepts using Python and the powerful `statsmodels` library. We will generate a synthetic AR(1) time series, test its stationarity, analyze its ACF and PACF, and then fit an AR model to it.

First, we need to import the necessary libraries:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
from statsmodels.tsa.ar_model import AutoReg # Recommended for pure AR models
from statsmodels.tsa.stattools import adfuller # For stationarity testing
import statsmodels.api as sm

# Set a random seed for reproducibility
np.random.seed(42)
```

## 5.1 Generating Synthetic AR(1) Data

Let's create an AR(1) process with known parameters. We will use the model:
$Y_t = 0.5 + 0.7 Y_{t-1} + \epsilon_t$
Here, $c = 0.5$ and $\phi_1 = 0.7$. Since $|\phi_1| = 0.7 < 1$, this series will be stationary. The error term $\epsilon_t$ will be standard normal white noise, meaning $E[\epsilon_t]=0$ and $Var(\epsilon_t)=1$.

```python
# Define AR coefficients and constant
ar_coeffs = [0.7] # AR(1) coefficient
constant_c = 0.5

# Define number of observations
n_samples = 200

# Generate white noise errors with mean 0 and standard deviation 1
errors = np.random.normal(0, 1, n_samples)

# Initialize the time series
y = np.zeros(n_samples)
y[0] = np.random.normal(0, 1) # Start with a random initial value

# Generate the AR(1) series using the defined equation
for t in range(1, n_samples):
    y[t] = constant_c + ar_coeffs[0] * y[t-1] + errors[t]

# Convert to a pandas Series for easier handling and plotting
ar1_series = pd.Series(y)

# Plot the generated series
plt.figure(figsize=(12, 6))
plt.plot(ar1_series)
plt.title('Generated AR(1) Time Series')
plt.xlabel('Time Step')
plt.ylabel('Value')
plt.grid(True)
plt.show()
```

## 5.2 Testing for Stationarity with Augmented Dickey-Fuller (ADF) Test

Before proceeding with AR modeling, especially with real-world data, it's crucial to verify stationarity. The Augmented Dickey-Fuller (ADF) test is a popular statistical test for this purpose.

The null hypothesis ($H_0$) of the ADF test is that the time series has a unit root (i.e., it is non-stationary). The alternative hypothesis ($H_1$) is that the time series is stationary. We typically look for a low p-value (e.g., less than 0.05) to reject the null hypothesis and conclude that the series is stationary.

```python
# Perform ADF test on the generated series
print("--- Augmented Dickey-Fuller Test ---")
adf_result = adfuller(ar1_series)

print(f"ADF Statistic: {adf_result[0]:.4f}")
print(f"P-value: {adf_result[1]:.4f}")
print("Critical Values:")
for key, value in adf_result[4].items():
    print(f"   {key}: {value:.4f}")

if adf_result[1] <= 0.05:
    print("\nConclusion: The series is likely stationary (reject H0).")
else:
    print("\nConclusion: The series is likely non-stationary (fail to reject H0).")
```
The output should show a small p-value, indicating that our simulated series is indeed stationary, as expected for $|\phi_1| < 1$.

## 5.3 Visualizing ACF and PACF

Now, let's plot the ACF and PACF of our generated AR(1) series. We expect the ACF to decay gradually and the PACF to cut off after lag 1.

```python
# Plot ACF and PACF
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

plot_acf(ar1_series, lags=20, ax=axes[0], title='Autocorrelation Function (ACF)')
plot_pacf(ar1_series, lags=20, ax=axes[1], title='Partial Autocorrelation Function (PACF)', method='ywm') # 'ywm' for Yule-Walker method

plt.tight_layout()
plt.show()
```

**Interpretation of the plots**:
*   The **ACF plot** on the left shows a gradual, exponential decay. This is characteristic of an AR process, where the correlation with past values slowly diminishes over time.
*   The **PACF plot** on the right shows a significant spike at lag 1, and then the values at subsequent lags quickly drop to near zero, falling within the blue shaded confidence interval. This "cutoff" at lag 1 strongly suggests that our series is an AR(1) process. If it were an AR(p) process, we would see $p$ significant spikes before the cutoff.

## 5.4 Fitting the AR Model

Based on our PACF analysis, we will fit an AR(1) model to our synthetic data using `statsmodels.tsa.ar_model.AutoReg`. The `lags` argument specifies the order $p$, and `trend='c'` tells the model to include a constant term (intercept).

```python
# Fit an AR(1) model
# The lags argument specifies the order p
# trend='c' indicates inclusion of a constant (intercept)
ar_model = AutoReg(ar1_series, lags=1, trend='c')
ar_results = ar_model.fit()

# Print the model summary
print(ar_results.summary())
```

**Interpreting Model Output**:

Let's look at the key parts of the `results.summary()` output. Note that the `const` term in `AutoReg` when `trend='c'` for a stationary series estimates the *mean* of the series ($\mu$), not the $c$ directly from our original equation. The relationship is $\mu = c / (1 - \phi_1)$. Our true mean for the generated series is $0.5 / (1 - 0.7) = 0.5 / 0.3 \approx 1.6667$.

```
                               AutoReg Results
==============================================================================
Dep. Variable:                      y   No. Observations:                  200
Model:                          AutoReg(1)   Log Likelihood                -281.424
Date:                ...              AIC                            568.848
Time:                ...              BIC                            578.740
Sample:                             0   HQIC                           572.822
                                - 200
Covariance Type:                  opg
==============================================================================
                 coef    std err          z      P>|z|      [0.025      0.975]
------------------------------------------------------------------------------
const          1.6730    0.237          7.069      0.000       1.209       2.137
y.L1           0.7025    0.045         15.611      0.000       0.614       0.791
sigma2         0.9634    0.096         10.038      0.000       0.775       1.152
===================================================================================
Ljung-Box (L1) (Q):                   0.00   Jarque-Bera (JB):                 0.42
Prob(Q):                              0.99   Prob(JB):                         0.81
Heteroskedasticity (H):               0.98   Skew:                            -0.03
Prob(H) (two-sided):                  0.94   Kurtosis:                         2.86
===================================================================================
```

*   **`const`**: This is our estimated mean $\mu$ of the stationary series. The estimated value is `1.6730`, which is very close to our true mean of approximately `1.6667`.
*   **`y.L1`**: This is our estimated $\phi_1$ coefficient for the first lag. The estimated value is `0.7025`, which is also remarkably close to our true value of `0.7`.
*   **`std err`**: The standard error of the coefficients. A small standard error indicates a more precise estimate.
*   **`z`**: The z-statistic, which is the coefficient divided by its standard error.
*   **`P>|z|`**: The p-value associated with the z-statistic. A p-value less than 0.05 (or your chosen significance level) indicates that the coefficient is statistically significant, meaning it's unlikely to be zero. Both our `const` and `y.L1` coefficients have p-values close to `0.000`, confirming their significance.
*   **`sigma2`**: This is the estimated variance of the error term $\epsilon_t$. Our true error variance was $1^2 = 1$, and the estimated value `0.9634` is close to that.
*   **Diagnostic Tests**: The `Ljung-Box (Q)` test checks for remaining autocorrelation in the residuals (errors). A high p-value (like `0.99`) indicates that there is no significant autocorrelation left in the residuals, which is good - it means our model has captured the AR structure. The `Jarque-Bera (JB)` test checks for normality of residuals. A high p-value (like `0.81`) suggests that the residuals are normally distributed, consistent with our assumption.

These results demonstrate that the `statsmodels` library successfully identified and estimated the parameters of our synthetic AR(1) process with high accuracy.

## 5.5 Forecasting

Once an AR model is fitted, we can use it to forecast future values of the time series. We can make in-sample predictions (within the observed data) to see how well the model fits, and out-of-sample forecasts (into the future).

```python
# Make in-sample predictions
# start=ar_model.lags[0] ensures we start prediction from the first point where all lags are available
predictions_in_sample = ar_results.predict(start=ar_model.lags[0], end=len(ar1_series)-1)

# Plot actual vs. predicted values
plt.figure(figsize=(12, 6))
plt.plot(ar1_series, label='Actual Values')
plt.plot(predictions_in_sample, label='In-sample Predicted Values', linestyle='--')
plt.title('AR(1) Model: Actual vs. In-sample Predicted')
plt.xlabel('Time')
plt.ylabel('Value')
plt.legend()
plt.grid(True)
plt.show()

# To make out-of-sample predictions (forecast into the future)
# Let's forecast 10 steps ahead
forecast_steps = 10
forecast_index = np.arange(len(ar1_series), len(ar1_series) + forecast_steps)
forecast = ar_results.predict(start=len(ar1_series), end=len(ar1_series) + forecast_steps - 1)

print("\nForecasted values for the next 10 steps:")
print(pd.Series(forecast.values, index=forecast_index)) # Print with appropriate index

# Plot the original series with the forecast
plt.figure(figsize=(12, 6))
plt.plot(ar1_series, label='Original Series')
plt.plot(forecast_index, forecast, label='Forecasted Values', linestyle=':', color='red')
plt.title('AR(1) Model: Original Series and Forecast')
plt.xlabel('Time Step')
plt.ylabel('Value')
plt.legend()
plt.grid(True)
plt.show()
```
Notice how the forecast converges to the series mean (which is approximately $1.6667$ in our case) as the forecast horizon increases. This behavior is typical for stationary AR models, as the influence of the last observed value $Y_t$ diminishes over time due to $|\phi_1| < 1$.

---

# 6. Conclusion: The Power of Self-Referential Modeling

We have thoroughly explored the concept of modeling a time series based on its own past values, focusing specifically on the Autoregressive (AR) model. We started by understanding the intuition behind using past values as predictors and then formally defined the AR(1) and general AR(p) models.

We delved into the crucial mathematical assumptions of stationarity and white noise errors, understanding why they are essential for valid model estimation and inference. We meticulously derived the stationarity condition for the AR(1) model (both mean and variance) and explained the characteristic polynomial approach for the general AR(p) model from scratch. We then learned how to identify the order $p$ of an AR model using the Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF), highlighting the distinct "cutoff" property of PACF for AR models.

Crucially, we derived the Ordinary Least Squares (OLS) estimators for the AR(1) model from scratch, demonstrating the underlying mathematical principles used to find the best-fitting coefficients. We also explored the Yule-Walker equations as an alternative estimation method. Finally, we brought these theoretical concepts to life with practical Python code using the `statsmodels` library, generating synthetic data, performing a stationarity test, analyzing its ACF/PACF, fitting an AR model with `AutoReg`, and interpreting the results and making predictions.

The AR model, while seemingly simple, provides a powerful framework for understanding and forecasting time series with inherent temporal dependencies. It forms the bedrock for more complex models like ARMA (Autoregressive Moving Average) and ARIMA (Autoregressive Integrated Moving Average), which we might explore in future discussions. By mastering the AR model, we've gained a fundamental tool in our time series analysis toolkit.

## Additional materials

### Linear difference equations

* https://mpaldridge.github.io/math2750/S04-ldes.html
* https://www.youtube.com/watch?v=_IDS9VVb8DY
* https://www.youtube.com/watch?v=kFOs-MKvnco
* https://www.youtube.com/watch?v=cj-kMkTEX-I
