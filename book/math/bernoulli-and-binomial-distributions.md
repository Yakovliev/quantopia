# Bernoulli Distribution and Binomial Distributions

## Bernoulli Distribution

We will start the simplest of all probability distributions for a discrete random variable: the Bernoulli Distribution. It serves as the basic building block for understanding more complex distributions like the Binomial distribution.

The **Bernoulli distribution** models a single random experiment that has exactly two mutually exclusive possible outcomes. These outcomes are conventionally labeled "success" and "failure." Think of any situation where an event either happens or it doesn't. This single experiment is known as a **Bernoulli trial**.

Examples include:
*   Flipping a coin: heads (success) or tails (failure).
*   A product being defective (success) or not defective (failure).
*   A customer clicking on an advertisement (success) or not clicking (failure).
*   A student passing an exam (success) or failing (failure).

The random variable associated with a Bernoulli trial is a **discrete random variable** that takes on a value of 1 for a "success" and 0 for a "failure."

A Bernoulli distribution is characterized by a single parameter $p$: the probability of "success" in a single trial. This is a dimensionless quantity, constrained such that $0 \le p \le 1$.

Naturally, the probability of "failure" is $1-p$. We often denote this as $q = 1-p$.

### Probability Mass Function of a Bernoulli Distribution

The Probability Mass Function (PMF) of a Bernoulli random variable describes the probability of observing each of its two possible outcomes.

Let $X$ be a Bernoulli random variable.
*   The probability of observing a success (i.e., $X=1$) is $p$.
*   The probability of observing a failure (i.e., $X=0$) is $1-p$.

We can write this compactly as:

$$p_X(x) = P(X=x) = \begin{cases} p & \text{if } x=1 \\ 1-p & \text{if } x=0 \\ 0 & \text{otherwise} \end{cases}$$

While the PMF for a Bernoulli variable is primarily a direct definition based on the two outcomes and their probabilities, we can represent it elegantly in a single formula by observing the pattern:
1.  If $x=1$ (success): The probability is $p$. We can write this as $p^1 (1-p)^0 = p \cdot 1 = p$.
2.  If $x=0$ (failure): The probability is $1-p$. We can write this as $p^0 (1-p)^1 = 1 \cdot (1-p) = 1-p$.

Combining these, we arrive at the standard compact form of the Bernoulli PMF:

$$p_X(x) = P(X=x) = p^x (1-p)^{1-x} \quad \text{for } x \in \{0, 1\}$$

Here, $p$ is the **parameter** of the Bernoulli distribution. It must be a value between 0 and 1, i.e., $p \in [0, 1]$. Since $p$ is a probability, it is a dimensionless quantity. The random variable $X$ takes on values that are counts (0 or 1), which are also dimensionless.

Let's check the properties of a valid PMF:
1.  **Non-negativity**: Since $p \in [0, 1]$, both $p$ and $1-p$ are non-negative. Thus, $p_X(x) \ge 0$ for all $x$.
2.  **Normalization**: The sum of probabilities for all possible values of $x$ must equal 1.

    $$\sum_{x \in \{0,1\}} p_X(x) = p_X(0) + p_X(1) = (1-p) + p = 1$$

    Both properties hold, confirming this is a valid PMF.

### Expected Value (Mean) of a Bernoulli Distribution

The **expected value** or **mean** of a discrete random variable $X$, denoted $E[X]$ or $\mu$, is the weighted average of its possible values, where the weights are their probabilities.

$$E[X] = \sum_{x} x \cdot p_X(x)$$

For a Bernoulli random variable $X$:

$$E[X] = (0 \cdot P(X=0)) + (1 \cdot P(X=1))$$

$$E[X] = (0 \cdot (1-p)) + (1 \cdot p)$$

$$E[X] = p$$

The mean of a Bernoulli distribution is simply the probability of success $p$. This makes intuitive sense: if for example an event has a 30% chance of success (1) and 70% chance of failure (0), on average, over many trials, the outcome will be 0.3.

### Variance of a Bernoulli Distribution

The **variance** of a random variable, denoted $Var(X)$ or $\sigma^2$, measures the spread or dispersion of its values around the mean. It is defined as the expected value of the squared difference from the mean:

$$Var(X) = E[(X - E[X])^2]$$

Alternatively, a computationally convenient formula is:

$$Var(X) = E[X^2] - (E[X])^2$$

First, let's calculate $E[X^2]$:

$$E[X^2] = (0^2 \cdot P(X=0)) + (1^2 \cdot P(X=1))$$

$$E[X^2] = (0 \cdot (1-p)) + (1 \cdot p)$$

$$E[X^2] = p$$

Now, substitute this into the variance formula:

$$Var(X) = E[X^2] - (E[X])^2$$

$$Var(X) = p - (p)^2$$

$$Var(X) = p - p^2$$

$$Var(X) = p(1-p)$$

The variance of a Bernoulli random variable is $p(1-p)$. This quantity is maximized when $p=0.5$, indicating the highest uncertainty or spread when success and failure are equally likely. Since outcomes are dimensionless counts, the variance is also dimensionless.

### Standard Deviation

The **standard deviation**, denoted $\sigma$, is the square root of the variance. It provides a measure of spread in the same units as the random variable itself.

$$\sigma_X = \sqrt{Var(X)}$$

For a Bernoulli random variable:

$$\sigma_X = \sqrt{p(1-p)}$$

### Mode of the Bernoulli Distribution

The **mode** of a discrete distribution is the value that occurs with the highest probability.
*   If $p > 0.5$, then $P(X=1) = p$ is greater than $P(X=0) = 1-p$. So the mode is 1.
*   If $p < 0.5$, then $P(X=0) = 1-p$ is greater than $P(X=1) = p$. So the mode is 0.
*   If $p = 0.5$, then $P(X=0) = P(X=1) = 0.5$. In this case, the distribution is bimodal, with modes at 0 and 1.

### Cumulative Distribution Function (CDF)

The CDF for a Bernoulli random variable $X$ is a step function. The CDF $F_X(x) = P(X \le x)$ is found by summing the probabilities from the PMF for all values less than or equal to $x$.

*   For $x < 0$: No possible outcomes are less than or equal to $x$.
    $$F_X(x) = P(X \le x) = 0$$
*   For $0 \le x < 1$: Only $X=0$ is a possible outcome less than or equal to $x$.
    $$F_X(x) = P(X \le x) = P(X=0) = 1-p$$
*   For $x \ge 1$: Both $X=0$ and $X=1$ are possible outcomes less than or equal to $x$.
    $$F_X(x) = P(X \le x) = P(X=0) + P(X=1) = (1-p) + p = 1$$

So, the CDF for a Bernoulli random variable is:

$$F_X(x) = \begin{cases} 0 & \text{for } x < 0 \\ 1-p & \text{for } 0 \le x < 1 \\ 1 & \text{for } x \ge 1 \end{cases}$$

---

## Binomial Distribution

Now that we understand the Bernoulli distribution, we can extend it to model scenarios involving multiple independent trials. This brings us to the Binomial distribution.

### What it Models: Number of Successes in Fixed Trials

The **Binomial distribution** models the number of "successes" in a fixed number of independent and identically distributed (i.i.d.) Bernoulli trials. It's used when we are interested in how many times an event occurs out of a predetermined total number of attempts.

For a random variable $X$ to follow a Binomial distribution, the following conditions (often called the "BINOM" conditions) must be met:
1.  **Binary outcomes**: Each trial must have only two possible outcomes: "success" or "failure."
2.  **Independence**: Each trial is independent of the others. The outcome of one trial does not influence the outcome of any other trial.
3.  **Number of trials ($n$)**: The experiment consists of a fixed number of trials, say $n$. This is a dimensionless count, $n \in \{1, 2, 3, \ldots\}$.
4.  **Same probability ($p$)**: The probability of success $p$ is the same for every trial. This is a dimensionless quantity, $0 \le p \le 1$.

If any of these conditions are violated, the Binomial distribution may not be an appropriate model. For example, if trials are not independent (e.g., drawing cards without replacement), we might need a Hypergeometric distribution. If the probability of success changes over trials, a more complex model is needed.

Examples include:
*   The number of heads in 10 coin flips.
*   The number of defective items in a sample of 50 products.
*   The number of patients who recover from a disease in a group of 20, given a certain treatment.
*   The number of clicks an ad receives out of 100 impressions.

### Importance of i.i.d. Trials and Common Violations

The assumption of **independent and identically distributed (i.i.d.)** Bernoulli trials is paramount for the Binomial distribution.
*   **Violation of Independence**: If trials are not independent, such as drawing cards without replacement from a small deck, the probability of success changes with each draw. In such cases, the **Hypergeometric distribution** would be the correct model, as it accounts for sampling without replacement from a finite population.
*   **Violation of Identical Distribution (Constant $p$)**: If the probability of success $p$ changes from trial to trial (e.g., due to learning, fatigue, or external factors), the Binomial distribution is no longer appropriate. More advanced models, such as those incorporating trial-specific probabilities, would be necessary. Recognizing these violations through exploratory data analysis is a critical data science skill.

### Relationship to Bernoulli Distribution

A Binomial random variable $X$ can be thought of as the sum of $n$ independent and identically distributed (i.i.d.) Bernoulli random variables. If $X_1, X_2, \ldots, X_n$ are $n$ independent Bernoulli($p$) random variables, then their sum $X = X_1 + X_2 + \ldots + X_n$ follows a Binomial distribution. This is a crucial conceptual link.

### Parameters of the Binomial Distribution

A Binomial distribution is characterized by two parameters:
*   $n$: The total number of independent trials. This is a dimensionless count, $n \in \{1, 2, 3, \ldots\}$.
*   $p$: The probability of "success" in a single trial. This is a dimensionless quantity, $0 \le p \le 1$.

We denote a Binomial random variable as $X \sim \text{Binomial}(n, p)$. The possible values for $X$ are $k \in \{0, 1, 2, \ldots, n\}$.

### Probability Mass Function of a Binomial Distribution

The PMF of a Binomial random variable $X$ gives the probability of observing exactly $k$ successes in $n$ trials.

Let $X$ be a Binomial random variable with parameters $n$ (number of trials) and $p$ (probability of success on a single trial).

**Derivation of the PMF**

To derive the Binomial PMF, we need to consider two main components:
1.  The probability of a *specific sequence* of $k$ successes and $n-k$ failures.
2.  The *number of different ways* to arrange $k$ successes and $n-k$ failures among the $n$ trials.

Let's assume we want to find the probability of exactly $k$ successes in $n$ trials.
The probability of success on any single trial is $p$, and the probability of failure is $1-p$.

**Step 1: Probability of a specific sequence**

Consider a specific sequence of outcomes, for example, $k$ successes followed by $n-k$ failures:

$$ \underbrace{S, S, \dots, S}_{k \text{ successes}}, \underbrace{F, F, \dots, F}_{n-k \text{ failures}} $$

Since the trials are independent, the probability of this specific sequence occurring is the product of the individual probabilities:

$$P(\text{this specific sequence}) = p \cdot p \cdot \dots \cdot p \quad (k \text{ times}) \cdot (1-p) \cdot (1-p) \cdot \dots \cdot (1-p) \quad (n-k \text{ times})$$

$$P(\text{this specific sequence}) = p^k (1-p)^{n-k}$$

**Step 2: Number of different sequences**

Now, we need to account for all possible arrangements of $k$ successes and $n-k$ failures. For example, if $n=3$ and $k=1$, we could have SFF, FSF, or FFS. Each of these sequences has the same probability $p^1 (1-p)^2$.

The number of ways to choose $k$ positions for successes out of $n$ available positions is given by the **binomial coefficient**, denoted as $\binom{n}{k}$ (read as "n choose k").

$$\binom{n}{k} = \frac{n!}{k!(n-k)!}$$

where $n!$ (n factorial) is the product of all positive integers up to $n$ ($n! = n \times (n-1) \times \dots \times 2 \times 1$), and $0! = 1$.

**Step 3: Combining the components**

To get the total probability of exactly $k$ successes, we multiply the probability of one specific sequence (from Step 1) by the number of such sequences (from Step 2).

So, the PMF for a Binomial random variable $X$ is:

$$p_X(k) = P(X=k) = \binom{n}{k} p^k (1-p)^{n-k} \quad \text{for } k \in \{0, 1, \dots, n\}$$

Here, $n$ is the number of trials (a dimensionless count) and $p$ is the probability of success (dimensionless). The number of successes $k$ is also a dimensionless count.

Let's check the properties of a valid PMF:
1.  **Non-negativity**: Since $n!$, $k!$, $(n-k)!$ are positive, and $p \in [0, 1]$, $p^k \ge 0$ and $(1-p)^{n-k} \ge 0$. Thus, $p_X(k) \ge 0$ for all $k$.
2.  **Normalization**: The sum of probabilities for all possible values of $k$ must equal 1. This is a direct consequence of the **Binomial Theorem**:

    $$(a+b)^n = \sum_{k=0}^{n} \binom{n}{k} a^k b^{n-k}$$

    If we let $a=p$ and $b=1-p$, then:

    $$\sum_{k=0}^{n} P(X=k) = \sum_{k=0}^{n} \binom{n}{k} p^k (1-p)^{n-k} = (p + (1-p))^n = (1)^n = 1$$
    Both properties hold, confirming this is a valid PMF.

### Expected Value (Mean)

The expected value of a Binomial random variable $X \sim B(n, p)$ is:

$$E[X] = np$$

There are a few ways to derive this. We will use the property of **linearity of expectation**, which is a powerful tool in probability. 

Let $X$ be a Binomial random variable representing the number of successes in $n$ trials. We can think of $X$ as the sum of $n$ independent Bernoulli random variables.

Let $X_i$ be a Bernoulli random variable for the $i$-th trial, where $X_i=1$ if the $i$-th trial is a success and $X_i=0$ if it's a failure. Each $X_i$ has a probability of success $p$.

Then, $X = X_1 + X_2 + \dots + X_n$.

By linearity of expectation, the expected value of a sum of random variables is the sum of their individual expected values:

$$E[X] = E[X_1 + X_2 + \dots + X_n]$$

$$E[X] = E[X_1] + E[X_2] + \dots + E[X_n]$$

We already know that the expected value of a single Bernoulli random variable $X_i$ is $p$. So, $E[X_i] = p$ for each $i$.

$$E[X] = p + p + \dots + p \quad (n \text{ times})$$

$$E[X] = np$$

### Variance

The variance of a Binomial random variable $X \sim B(n, p)$ is:

$$Var(X) = np(1-p)$$

Since the $n$ Bernoulli trials are **independent**, the variance of their sum is the sum of their individual variances. This is a crucial property for independent random variables.
Let $X_i$ be independent Bernoulli random variables as defined above. We know that $Var(X_i) = p(1-p)$ for each $X_i$.

$$Var(X) = Var(X_1 + X_2 + \dots + X_n)$$

$$Var(X) = Var(X_1) + Var(X_2) + \dots + Var(X_n) \quad (\text{due to independence})$$

$$Var(X) = p(1-p) + p(1-p) + \dots + p(1-p) \quad (n \text{ times})$$

$$Var(X) = np(1-p)$$

The variance $np(1-p)$ is also dimensionless.

### Standard Deviation

The standard deviation for a Binomial random variable is:

$$\sigma_X = \sqrt{np(1-p)}$$

### Mode of the Binomial Distribution

The mode of the Binomial distribution, representing the most probable number of successes, is given by $\lfloor (n+1)p \rfloor$.

The symbols $\lfloor$ and $\rfloor$ represent the **floor function** in mathematics.

The **floor function** of a number $x$, denoted as $\lfloor x \rfloor$, is the largest integer that is less than or equal to $x$. Essentially, it means you **round the number down** to the nearest whole number.

*   If $(n+1)p$ is an integer, then there are two modes for binomial distribution: $(n+1)p - 1$ and $(n+1)p$.
*   If $(n+1)p$ is not an integer, then there is a unique mode: $\lfloor (n+1)p \rfloor$.
For example, if $n=10, p=0.5$, then $(10+1)0.5 = 5.5$. The mode is $\lfloor 5.5 \rfloor = 5$.
If $n=9, p=0.5$, then $(9+1)0.5 = 5$. The modes are $5-1=4$ and $5$.

#### Derivation of the Mode

To understand why this formula is true, we need to find the value of $k$ that maximizes the probability mass function, $P(X=k)$. We can do this by examining the ratio of the probability of $k$ successes to the probability of $k-1$ successes, $\frac{P(X=k)}{P(X=k-1)}$.

*   If this ratio is greater than 1, it means the probability is still increasing as we go from $k-1$ to $k$.
*   If the ratio is less than 1, the probability is decreasing, meaning we have passed the peak.
*   The mode is the value of $k$ for which the probability stops increasing.

Let's set up the ratio:

$$ \frac{P(X=k)}{P(X=k-1)} = \frac{\binom{n}{k} p^k (1-p)^{n-k}}{\binom{n}{k-1} p^{k-1} (1-p)^{n-k+1}} =$$

Now, let's expand the binomial coefficients and simplify:

$$ = \frac{\frac{n!}{k!(n-k)!}}{\frac{n!}{(k-1)!(n-k+1)!}} \cdot \frac{p^k (1-p)^{n-k}}{p^{k-1} (1-p)^{n-k+1}} =$$

$$ = \frac{(k-1)!(n-k+1)!}{k!(n-k)!} \cdot \frac{p}{1-p} =$$

Using the property that $k! = k \cdot (k-1)!$ and $(n-k+1)! = (n-k+1) \cdot (n-k)!$, we get:

$$ = \frac{n-k+1}{k} \cdot \frac{p}{1-p} $$

We are looking for the value of $k$ where the probability is greatest. This will occur when $P(X=k) \ge P(X=k-1)$, which is equivalent to our ratio being greater than or equal to 1.

$$ \frac{n-k+1}{k} \cdot \frac{p}{1-p} \ge 1 $$

Now, we solve for $k$:

$$ (n-k+1)p \ge k(1-p) $$

$$ np - kp + p \ge k - kp $$

$$ np + p \ge k $$

$$ k \le (n+1)p $$

This inequality tells us that the probability $P(X=k)$ continues to increase as long as $k$ is less than or equal to $(n+1)p$. The value of $k$ for which the probability is maximized (the mode) is therefore the largest integer that satisfies this condition. This is precisely the definition of the floor function.

Thus, the mode is $\lfloor (n+1)p \rfloor$.

**Handling the special cases:**
1.  **If $(n+1)p$ is not an integer**: The inequality $k < (n+1)p$ holds strictly for the largest integer $k$ below it, which is $\lfloor (n+1)p \rfloor$. For the next value, $k+1$, the inequality will be reversed, meaning the probability will start to decrease. This results in a single, unique mode.
2.  **If $(n+1)p$ is an integer**: Let's call this integer $m$. When $k = m$, the inequality becomes $m \le m$, which means our ratio is exactly equal to 1. This implies that $P(X=m) = P(X=m-1)$. Since the probability decreases for $k > m$, the distribution has two adjacent values with the same highest probability. Therefore, the distribution is bimodal with modes at $m-1$ and $m$, which is $(n+1)p - 1$ and $(n+1)p$.

## Cumulative Distribution Function of a Binomial Distribution

The CDF $F_X(x)$ for a Binomial random variable $X \sim B(n, p)$ is the sum of the probabilities for all possible values of successes up to $x$:

$$F_X(x) = P(X \le x) = \sum_{k=0}^{\lfloor x \rfloor} \binom{n}{k} p^k (1-p)^{n-k}$$

where $\lfloor x \rfloor$ is the floor function, representing the largest integer less than or equal to $x$. Due to the summation, there is generally no simple closed-form expression for the Binomial CDF. It is typically calculated using tables or computational software. Like all CDFs for discrete variables, it is a step function.

## Relationship to Bernoulli Distribution

It's important to recognize that a Bernoulli distribution is a special case of a Binomial distribution. If we set the number of trials $n=1$ in a Binomial distribution, we get the Bernoulli distribution.

Let's test this with the PMF:
For $X \sim B(1, p)$, the PMF is $P(X=k) = \binom{1}{k} p^k (1-p)^{1-k}$.
*   If $k=0$: $P(X=0) = \binom{1}{0} p^0 (1-p)^{1-0} = 1 \cdot 1 \cdot (1-p) = 1-p$.
*   If $k=1$: $P(X=1) = \binom{1}{1} p^1 (1-p)^{1-1} = 1 \cdot p \cdot 1 = p$.
This perfectly matches the Bernoulli PMF.

Similarly, for $n=1$:
*   Mean: $E[X] = np = 1 \cdot p = p$.
*   Variance: $Var(X) = np(1-p) = 1 \cdot p(1-p) = p(1-p)$.
These also match the Bernoulli distribution's properties.

## Example: Manufacturing Defects

Suppose a factory produces electronic components, and historically, 5% of the components are defective. We randomly select a sample of 10 components from the production line. Let $X$ be the number of defective components in our sample.

This is a Binomial experiment:
1.  **Fixed number of trials**: $n=10$ components.
2.  **Two outcomes**: Each component is either defective (success) or not defective (failure). We define "defective" as success since that's what we're counting.
3.  **Constant probability of success**: $p=0.05$ (5% chance of being defective).
4.  **Independent trials**: We assume the defect status of one component does not affect another.

So, $X \sim B(10, 0.05)$.

*   **What is the probability that exactly 2 components are defective?**

    We use the PMF with $k=2$:

    $$P(X=2) = \binom{10}{2} (0.05)^2 (1-0.05)^{10-2}$$

    $$P(X=2) = \binom{10}{2} (0.05)^2 (0.95)^8$$

    First, calculate $\binom{10}{2} = \frac{10!}{2!(10-2)!} = \frac{10!}{2!8!} = \frac{10 \times 9}{2 \times 1} = 45$.

    $$P(X=2) = 45 \times (0.0025) \times (0.95)^8 \approx 45 \times 0.0025 \times 0.66342$$

    $$P(X=2) \approx 0.0746$$

    So, there's about a 7.46% chance of finding exactly 2 defective components in a sample of 10.

*   **What is the expected number of defective components?**

    $$E[X] = np = 10 \times 0.05 = 0.5$$

    On average, we expect to find 0.5 defective components in a sample of 10. Note that the expected value doesn't have to be an integer.

*   **What is the variance and standard deviation of the number of defective components?**

    $$Var(X) = np(1-p) = 10 \times 0.05 \times (1-0.05) = 10 \times 0.05 \times 0.95 = 0.475$$

    $$\sigma_X = \sqrt{Var(X)} = \sqrt{0.475} \approx 0.689$$

---

## Further Insights and Advanced Considerations

To deepen our understanding of the Binomial distribution, let's explore its graphical representation, shape, and connections to other distributions.

### Shape and Skewness of the Binomial Distribution

The shape of the Binomial PMF, when plotted as a bar chart, is influenced significantly by the parameter $p$:
*   If $p = 0.5$, the distribution is **symmetrical**. The PMF values are highest around the mean $np$ and decrease symmetrically outwards.
*   If $p < 0.5$, the distribution is **skewed to the right** (positively skewed). This means the tail of the distribution extends further to the right, and more probability mass is concentrated at lower values of $k$.
*   If $p > 0.5$, the distribution is **skewed to the left** (negatively skewed). This means the tail extends further to the left, and more probability mass is concentrated at higher values of $k$.

As $n$ (the number of trials) increases, the Binomial distribution generally becomes more bell-shaped and less skewed, regardless of $p$.

<p><img src="https://upload.wikimedia.org/wikipedia/commons/3/33/Visualisation_mode_median_mean.svg" alt="Visualisation mode median mean.svg" height="500" width="291.6">
<br>
Fig. Geometric visualisation of the mode, median and mean of an arbitrary probability density function.
Author: <a href="https://commons.wikimedia.org/wiki/User:Cmglee" title="User:Cmglee">Cmglee</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/3.0" title="Creative Commons Attribution-Share Alike 3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=38969094">Link</a>. <a href="https://en.wikipedia.org/wiki/Mode_(statistics)">Wikipedia</a></p>


### Approximations to the Binomial Distribution

For certain conditions, the Binomial distribution can be well-approximated by other, often simpler, distributions. These approximations are incredibly useful in practice, especially when exact Binomial calculations become computationally intensive for very large $n$.

#### Normal Approximation

When $n$ is large, and $p$ is not too close to 0 or 1 (a common rule of thumb is $np \ge 5$ and $n(1-p) \ge 5$), the Binomial distribution can be approximated by a **Normal (Gaussian) distribution** (we will learn this distribution in the following lectures).

Specifically, if $X \sim B(n, p)$, then for large $n$, $X$ can be approximated by $X \sim N(\mu, \sigma^2)$ where $\mu = np$ and $\sigma^2 = np(1-p)$.

This approximation is widely used for hypothesis testing and confidence interval estimation when dealing with proportions from large samples. A "continuity correction" is often applied when using a continuous distribution (Normal) to approximate a discrete one (Binomial) for better accuracy.

#### Poisson Approximation

When $n$ is large and $p$ is small (i.e., we are looking for a rare event in many trials), the Binomial distribution can be approximated by a **Poisson distribution** (we will learn this distribution in the following lectures).

If $X \sim B(n, p)$ and $n \to \infty$ while $p \to 0$ such that the product $np$ remains constant, say $\lambda = np$, then $X$ can be approximated by a Poisson distribution with parameter $\lambda$.

The Poisson distribution is typically used to model the number of events occurring in a fixed interval of time or space, and its connection to the Binomial distribution highlights how it arises from counting rare successes in numerous trials.

## Summary

| Concept | Bernoulli Distribution | Binomial Distribution |
| :--- | :--- | :--- |
| **Description** | Models a single trial with two possible outcomes: success (1) or failure (0). | Models the number of successes in a fixed number, $n$, of independent Bernoulli trials. |
| **Parameters** | $p$ (probability of success) | $n$ (number of trials) and $p$ (probability of success) |
| **Probability Mass Function (PMF)** | $P(X=x) = p^x (1-p)^{1-x}$ for $x \in \{0, 1\}$ | $P(X=k) = \binom{n}{k} p^k (1-p)^{n-k}$ for $k \in \{0, 1, ..., n\}$ |
| **Expected Value (Mean)** | $E[X] = p$ | $E[X] = np$ |
| **Variance** | $Var(X) = p(1-p)$ | $Var(X) = np(1-p)$ |
| **Standard Deviation** | $\sigma = \sqrt{p(1-p)}$ | $\sigma = \sqrt{np(1-p)}$ |
| **Mode** | 1 if $p > 0.5$, 0 if $p < 0.5$, and 0 and 1 if $p = 0.5$ | $\lfloor (n+1)p \rfloor$. If $(n+1)p$ is an integer, modes are at $(n+1)p$ and $(n+1)p - 1$. |
| **Cumulative Distribution Function (CDF)** | $F_X(x) = \begin{cases} 0 & \text{for } x < 0 \\ 1-p & \text{for } 0 \le x < 1 \\ 1 & \text{for } x \ge 1 \end{cases}$ | $F_X(x) = \sum_{k=0}^{\lfloor x \rfloor} \binom{n}{k} p^k (1-p)^{n-k}$ |
| **Relationship** | The Bernoulli distribution is a special case of the Binomial distribution where $n=1$. | A Binomial random variable is the sum of $n$ independent and identically distributed Bernoulli random variables. |
| **Shape** | Asymmetric if $p \ne 0.5$, symmetric if $p=0.5$. | Skewed right if $p < 0.5$, skewed left if $p > 0.5$, and symmetric if $p=0.5$. Becomes more bell-shaped as $n$ increases. |
| **Approximations** | Not applicable. | **Normal Approx.**: When $n$ is large and $p$ is not near 0 or 1 (rule of thumb: $np \ge 5$ and $n(1-p) \ge 5$).<br>**Poisson Approx.**: When $n$ is large and $p$ is small, but $np = \lambda$ is constant. |

## Additional materials

* https://en.wikipedia.org/wiki/Binomial_coefficient
* https://en.wikipedia.org/wiki/Mode_(statistics)
* https://en.wikipedia.org/wiki/Median
* https://en.wikipedia.org/wiki/Standard_deviation
* https://en.wikipedia.org/wiki/Expected_value
* https://en.wikipedia.org/wiki/Probability_distribution
* https://en.wikipedia.org/wiki/Skewness
* https://en.wikipedia.org/wiki/Bernoulli_distribution
* https://en.wikipedia.org/wiki/Binomial_distribution























