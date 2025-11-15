# Introduction to Random Variables

## What is a Random Variable?

At its heart, a **random variable** is a function that maps the outcomes of a random experiment to real numbers. To truly understand this from the very beginning, let's briefly recall the formal setup of probability theory: a **probability space** consists of three parts:
1.  A **sample space** $\Omega$ (or $S$), which is the set of all possible outcomes of a random experiment. For example, if we flip two coins, $\Omega = \{\text{HH, HT, TH, TT}\}$.
2.  A **set of events** $\mathcal{F}$ (often called a sigma-algebra), which is a collection of subsets of $\Omega$ to which we can assign probabilities. These events are the things we can meaningfully talk about the probability of.
3.  A **probability measure** $P$, which assigns a probability (a number between 0 and 1) to each event in $\mathcal{F}$.

A random variable (often denoted by a capital letter like $X$, $Y$, or $Z$) is then formally defined as a function that maps each outcome $\omega$ from the sample space $\Omega$ to a real number.

$$X: \Omega \to \mathbb{R}$$

Crucially, for $X$ to be a valid random variable, it must also satisfy a technical condition called **measurability**. This means that for any interval $B$ on the real number line (specifically, any Borel set $B$), the set of outcomes $\omega \in \Omega$ for which $X(\omega) \in B$ must be an event in our set of events $\mathcal{F}$. In simpler terms, this ensures that we can actually calculate probabilities for statements like $P(X \le x)$ or $P(a < X < b)$. For most practical data science applications, we can safely assume this condition holds for the functions we define as random variables.

Why do we need them? Imagine we flip two coins. The possible outcomes are {HH, HT, TH, TT}. These are not numbers directly. However, if we are interested in the *number of heads*, we can define a random variable $X$ that assigns a number to each outcome:
*   $X(\text{HH}) = 2$
*   $X(\text{HT}) = 1$
*   $X(\text{TH}) = 1$
*   $X(\text{TT}) = 0$

This mapping from the non-numerical outcomes to the numbers {0, 1, 2} is what a random variable does. It acts as a bridge, allowing us to quantify qualitative outcomes and apply powerful mathematical and statistical tools to analyze and predict the behavior of random events. We use capital letters (e.g., $X$) to denote the random variable itself, and lowercase letters (e.g., $x$) to denote the specific values that the random variable can take.

Random variables are broadly categorized into two types based on the nature of the values they can take: discrete random variables and continuous random variables.

## Discrete Random Variables

A random variable is called a **discrete random variable** if its possible values are countable. This means we can list them out, even if the list is infinitely long. The values are typically integers, representing counts or categories.

Examples of discrete random variables include:
*   The number of heads when flipping a coin 3 times (possible values: 0, 1, 2, 3).
*   The number of cars passing a specific point on a road in an hour (possible values: 0, 1, 2, ...).
*   The result of rolling a single six-sided die (possible values: 1, 2, 3, 4, 5, 6).
*   The number of defects in a batch of 100 items (possible values: 0, 1, ..., 100).

## Continuous Random Variables

In contrast, a random variable is a **continuous random variable** if its possible values are uncountable and typically lie within an interval (or a collection of intervals) on the real number line. For continuous variables, it doesn't make sense to list out all possible values because there are infinitely many values between any two given values.

Examples of continuous random variables include:
*   The height of a randomly selected person (e.g., any value between 1.50 meters and 1.90 meters).
*   The weight of an apple (e.g., any value between 100 grams and 200 grams).
*   The time it takes for a bus to arrive (e.g., any value from 0 minutes upwards).
*   The temperature in a room (e.g., any value between 20°C and 25°C).

A crucial distinction for continuous random variables is that the probability of the variable taking on *any single specific value* is zero. We will delve deeper into why this is the case when we discuss the Probability Density Function.

---

## Probability Mass Function (PMF)

Once we have defined a discrete random variable, we need a way to describe the probabilities associated with each of its possible values. This is where the Probability Mass Function comes into play.

### What is a PMF?

For a discrete random variable $X$, the **Probability Mass Function (PMF)**, often denoted as $P(X=x)$ or $p_X(x)$, provides the probability that $X$ takes on a specific value $x$. In simpler terms, it tells us how the total probability "mass" of 1 is distributed among the discrete values that $X$ can take.

So, if we see $p_X(x) = 0.2$, it means there is a 20% chance that our random variable $X$ will take on the specific value $x$. PMFs are fundamental for modeling count data, categorical outcomes, and other phenomena where outcomes are distinct and countable.

### Properties of a PMF

For a function $p_X(x)$ to be a valid PMF, it must satisfy two fundamental properties, which are direct consequences of the Kolmogorov axioms of probability:

1.  **Non-negativity**: The probability of any specific outcome cannot be negative.

    $$p_X(x) \ge 0 \quad \text{for all possible values of } x$$

2.  **Normalization**: The sum of all probabilities for all possible values of $x$ must equal 1. This reflects the certainty that the random variable must take on one of its possible values, corresponding to the axiom that the probability of the entire sample space is 1.

    $$\sum_{x} p_X(x) = 1$$

    where the summation is over all possible values that $X$ can take.

### Construction and Intuition

The concept of a PMF is quite intuitive and directly extends from our basic understanding of probability. When we define a discrete random variable $X$, we are essentially grouping outcomes from our original sample space $\Omega$ and assigning a numerical value to them. The probability of $X$ taking a certain value $x$ is simply the sum of the probabilities of all original sample space outcomes that map to that numerical value $x$. We are "assigning mass" to each point.

For instance, if we roll a fair six-sided die, the sample space is $\Omega = \{1, 2, 3, 4, 5, 6\}$. Each outcome has a probability of $1/6$. If we define $X$ as the outcome of the roll, then:

*   $P(X=1) = 1/6$
*   $P(X=2) = 1/6$
*   ...
*   $P(X=6) = 1/6$

This list of probabilities for each $x$ value *is* our PMF. There's no complex "derivation" in the sense of calculus; it's a direct definition based on how probabilities are assigned to events (which are subsets of the sample space). We are simply listing the probabilities for each discrete outcome.

### Example with PMF

Let's consider an experiment where we flip two fair coins. Let $X$ be the discrete random variable representing the number of heads we observe.

The possible outcomes of the experiment in our sample space are:
*   HH (2 heads)
*   HT (1 head)
*   TH (1 head)
*   TT (0 heads)

Assuming the coins are fair, each of these four outcomes has a probability of $1/4$. Now, let's define the PMF for $X$:

*   For $X=0$ (TT):
    $$p_X(0) = P(X=0) = P(\text{TT}) = \frac{1}{4}$$

*   For $X=1$ (HT or TH):
    $$p_X(1) = P(X=1) = P(\text{HT}) + P(\text{TH}) = \frac{1}{4} + \frac{1}{4} = \frac{2}{4} = \frac{1}{2}$$

*   For $X=2$ (HH):
    $$p_X(2) = P(X=2) = P(\text{HH}) = \frac{1}{4}$$

*   For any other value of $x$ (e.g., $X=3$):
    $$p_X(x) = 0$$

Let's check the properties:
1.  All $p_X(x)$ values are $\ge 0$. (Yes: $1/4, 1/2, 1/4, 0$).
2.  The sum of probabilities is 1:
    $$p_X(0) + p_X(1) + p_X(2) = \frac{1}{4} + \frac{1}{2} + \frac{1}{4} = \frac{1}{4} + \frac{2}{4} + \frac{1}{4} = \frac{4}{4} = 1$$
    This confirms that our PMF is valid.

---

## Probability Density Function (PDF)

When we move from discrete to continuous random variables, the concept of assigning a probability to a single exact value becomes problematic. This is where the Probability Density Function (PDF) becomes essential.

### Why $P(X=x) = 0$ for Continuous Variables?

For a continuous random variable, the probability of $X$ taking any *exact* specific value $x$ is 0. This might seem counterintuitive at first. Consider a random number chosen uniformly between 0 and 1. What is the probability that it's exactly 0.5? Since there are infinitely many real numbers between 0 and 1, the chance of hitting precisely 0.5 is infinitesimally small. If we assigned a non-zero probability (even a tiny one) to each single point, and there are infinitely many points, the sum of these probabilities would diverge to infinity, violating the normalization axiom that total probability must be 1. Therefore, for continuous variables, we must have $P(X=x) = 0$.

Instead, for continuous random variables, we are interested in the probability that $X$ falls within a certain *interval*. The PDF tells us how "dense" the probability is at any given point.

### What is a PDF?

For a continuous random variable $X$, the **Probability Density Function (PDF)**, often denoted as $f_X(x)$, describes the *relative likelihood* for the random variable to take on a given value. It is crucial to understand that, unlike a PMF, the value of $f_X(x)$ at a specific point $x$ is *not* a probability. It is a *density*. A higher value of $f_X(x)$ simply means that values around $x$ are more probable.

The probability that $X$ falls within a specific interval $[a, b]$ is given by the integral of the PDF over that interval:

$$P(a \le X \le b) = \int_a^b f_X(x) dx$$

Because the probability of $X$ being exactly $a$ or $b$ is zero for continuous variables, it follows that $P(a \le X \le b) = P(a < X < b) = P(a \le X < b) = P(a < X \le b)$.

### Dimensionality of the PDF

It's important to note the dimensions of the PDF. Unlike probabilities (PMF values) which are dimensionless, the Probability Density Function $f_X(x)$ has dimensions of inverse of the random variable's units.

For example:
*   If $X$ represents time in seconds (s), then $f_X(x)$ has units of $1/\text{s}$.
*   If $X$ represents height in meters (m), then $f_X(x)$ has units of $1/\text{m}$.

This is because when we integrate the PDF over an interval $[a, b]$, we are multiplying $f_X(x)$ (units of $1/\text{unit of } X$) by $dx$ (units of $\text{unit of }X$), resulting in a dimensionless probability:

$$\int_a^b f_X(x) dx \quad \text{has units of } \left( \frac{1}{\text{unit of } X} \right) \cdot (\text{unit of } X) = \text{dimensionless probability}$$

This reinforces the idea that $f_X(x)$ itself is not a probability, but a *rate* or *density* of probability per unit of the random variable.

### Properties of a PDF

For a function $f_X(x)$ to be a valid PDF, it must satisfy the following properties, again, stemming from the probability axioms:

1.  **Non-negativity**: The density cannot be negative. This is because probabilities cannot be negative, and the integral of $f_X(x)$ gives probabilities.
    $$f_X(x) \ge 0 \quad \text{for all } x \in \mathbb{R}$$

2.  **Normalization**: The total area under the curve of the PDF must be equal to 1. This signifies that the random variable must take on some value across its entire range, corresponding to the axiom that the probability of the entire sample space is 1.
    $$\int_{-\infty}^{\infty} f_X(x) dx = 1$$

### Conceptual Derivation and Intuition

While a formal "derivation" of a PDF in the physical sense is not typical, we can understand its mathematical definition and intuitive meaning. Formally, a PDF $f_X(x)$ for a continuous random variable $X$ is defined as the derivative of its Cumulative Distribution Function (CDF), which we will discuss next:

$$f_X(x) = \frac{d}{dx} F_X(x)$$
(This holds where $F_X(x)$ is differentiable). This means the PDF is the *rate of change* of the cumulative probability.

To build intuition, imagine we create a histogram from a very large dataset of a continuous variable. If we normalize the bars of the histogram so that the *total area* of all bars equals 1, then the height of each bar represents a "frequency density." As the number of data points increases and the width of the bins (intervals) becomes infinitesimally small, this histogram approaches a smooth curve. This curve is the PDF.

From this intuition, we can consider the probability that $X$ falls into a very small interval $[x, x + \Delta x]$. This probability would be approximately the height of the curve at $x$ multiplied by the width of the interval:

$$P(x \le X \le x + \Delta x) \approx f_X(x) \Delta x$$

Here, $f_X(x)$ represents the "probability per unit length" or the probability density at point $x$. A higher $f_X(x)$ means that values around $x$ are more likely to occur.

From calculus, we know that an integral can be thought of as the sum of infinitely many infinitesimally small products (like $f_X(x) \Delta x$). So, if we want the probability over a larger interval $[a, b]$, we sum these tiny segments:

$$P(a \le X \le b) = \lim_{\Delta x \to 0} \sum_{\text{intervals in } [a,b]} f_X(x_i) \Delta x_i$$

As $\Delta x_i \to 0$, this sum becomes an integral:

$$P(a \le X \le b) = \int_a^b f_X(x) dx$$

Thus, the PDF $f_X(x)$ represents the rate at which probability accumulates around $x$. The area under the PDF curve over an interval gives us the actual probability for $X$ to fall within that interval. In data science, PDFs are crucial for modeling continuous data, performing statistical inference, and understanding the shape of data distributions.

### Example with PDF

Let's consider a continuous random variable $X$ that is uniformly distributed between 0 and 1. This means that any value between 0 and 1 is equally likely, and values outside this range are impossible.

The PDF for such a uniform distribution is defined as:

$$f_X(x) = \begin{cases} c & \text{for } 0 \le x \le 1 \\ 0 & \text{otherwise} \end{cases}$$

To find the constant $c$, we use the normalization property:

$$\int_{-\infty}^{\infty} f_X(x) dx = 1$$

$$\int_{0}^{1} c \, dx = 1$$

$$[cx]_{0}^{1} = 1$$

$$c \cdot 1 - c \cdot 0 = 1$$

$$c = 1$$

So, the PDF for this uniform distribution is:

$$f_X(x) = \begin{cases} 1 & \text{for } 0 \le x \le 1 \\ 0 & \text{otherwise} \end{cases}$$

Let's verify its properties:
1.  **Non-negativity**: $f_X(x)$ is either 1 or 0, so it's always $\ge 0$.
2.  **Normalization**: We already showed that $\int_{-\infty}^{\infty} f_X(x) dx = 1$.
    The total area under the curve is 1, so it's a valid PDF.

Now, let's find the probability that $X$ falls between 0.2 and 0.7:

$$P(0.2 \le X \le 0.7) = \int_{0.2}^{0.7} f_X(x) dx$$

Since $f_X(x) = 1$ in this interval:

$$P(0.2 \le X \le 0.7) = \int_{0.2}^{0.7} 1 \, dx = [x]_{0.2}^{0.7} = 0.7 - 0.2 = 0.5$$

This makes sense; an interval of length 0.5 within a total range of length 1 should have a probability of 0.5.

---

## Cumulative Distribution Function (CDF)

While PMFs and PDFs describe probabilities at specific points or densities, the **Cumulative Distribution Function (CDF)** offers a unified way to describe the probability distribution for *both* discrete and continuous random variables. It tells us the probability that a random variable takes on a value less than or equal to a given number.

### What is a CDF?

The **Cumulative Distribution Function (CDF)**, denoted as $F_X(x)$, for any random variable $X$ (discrete or continuous), gives the probability that $X$ will take a value less than or equal to $x$.

$$F_X(x) = P(X \le x)$$

This function is incredibly useful because it allows us to calculate probabilities for various intervals, and it provides a complete picture of the probability distribution from $-\infty$ up to any point $x$. CDFs are central to statistical inference, hypothesis testing, and understanding the overall shape and spread of a distribution.

### Properties of a CDF

Every CDF, regardless of whether the random variable is discrete or continuous, must satisfy these properties, which are derived from the basic axioms of probability:

1.  **Monotonically non-decreasing**: As $x$ increases, the cumulative probability cannot decrease. If $x_1 \le x_2$, then $F_X(x_1) \le F_X(x_2)$.
    This is logical; as we include more possible values up to a higher $x$, the cumulative probability can only stay the same or increase. We are accumulating probability, so the total accumulated cannot go down.

2.  **Limits**:
    *   As $x$ approaches negative infinity, the cumulative probability is 0 (there are no values less than or equal to $-\infty$). This reflects the probability of an impossible event.

        $$\lim_{x \to -\infty} F_X(x) = 0$$

    *   As $x$ approaches positive infinity, the cumulative probability is 1 (all possible values are included). This reflects the probability of the entire sample space.

        $$\lim_{x \to \infty} F_X(x) = 1$$

3.  **Right-continuity**: The CDF is always continuous from the right. This means that for any point $x_0$, the limit of $F_X(x)$ as $x$ approaches $x_0$ from values greater than $x_0$ is equal to $F_X(x_0)$.

    $$\lim_{x \to x_0^+} F_X(x) = F_X(x_0)$$

    This property is particularly important for discrete random variables, where the CDF exhibits "jumps" (step discontinuities) at each possible value. By defining $F_X(x) = P(X \le x)$, we include the probability of $x$ itself in the cumulative sum. For example, $F_X(x_0)$ includes $P(X=x_0)$, while $F_X(x_0 - \epsilon)$ for a tiny $\epsilon > 0$ does not. Right-continuity ensures that $F_X(x_0)$ properly captures all probability up to and including $x_0$. If we were to define it as $P(X < x)$, it would instead be left-continuous. The standard definition $P(X \le x)$ makes it right-continuous.

The CDF is incredibly useful because it allows us to easily calculate the probability that $X$ falls within any interval $(a, b]$:

$$P(a < X \le b) = F_X(b) - F_X(a)$$

For continuous random variables, since $P(X=a)=0$, we also have:

$$P(a \le X \le b) = F_X(b) - F_X(a)$$

This means the probability of $X$ falling into any interval can always be found using the CDF.

### Derivation for Discrete Random Variables

For a discrete random variable $X$, the CDF $F_X(x)$ is found by summing the probabilities of all possible values of $X$ that are less than or equal to $x$. This is a direct definition of cumulative probability from the PMF.

$$F_X(x) = P(X \le x) = \sum_{t \le x} p_X(t)$$

where $p_X(t)$ is the PMF of $X$.

The CDF for a discrete random variable will always be a step function, where the "jumps" occur at the specific values the random variable can take, and the height of each jump corresponds to the probability (PMF value) at that point.

Let's revisit our two-coin flip example where $X$ is the number of heads ($p_X(0)=1/4, p_X(1)=1/2, p_X(2)=1/4$).

*   For $x < 0$: There are no possible values less than or equal to $x$.

    $$F_X(x) = 0$$

*   For $0 \le x < 1$: Only $X=0$ is less than or equal to $x$.

    $$F_X(x) = p_X(0) = \frac{1}{4}$$

*   For $1 \le x < 2$: Values $X=0$ and $X=1$ are less than or equal to $x$.

    $$F_X(x) = p_X(0) + p_X(1) = \frac{1}{4} + \frac{1}{2} = \frac{3}{4}$$

*   For $x \ge 2$: Values $X=0, X=1, X=2$ are less than or equal to $x$.

    $$F_X(x) = p_X(0) + p_X(1) + p_X(2) = \frac{1}{4} + \frac{1}{2} + \frac{1}{4} = 1$$

So, the CDF for this discrete random variable is a step function:

$$F_X(x) = \begin{cases} 0 & \text{for } x < 0 \\ 1/4 & \text{for } 0 \le x < 1 \\ 3/4 & \text{for } 1 \le x < 2 \\ 1 & \text{for } x \ge 2 \end{cases}$$

### Derivation for Continuous Random Variables

For a continuous random variable $X$, the CDF $F_X(x)$ is found by integrating the PDF $f_X(t)$ from negative infinity up to $x$. This is also a direct definition, reflecting the accumulation of probability density over a continuous range.

$$F_X(x) = P(X \le x) = \int_{-\infty}^{x} f_X(t) dt$$

For continuous random variables, the CDF is always a continuous function, representing a smooth accumulation of probability.

Conversely, as mentioned earlier, if the CDF $F_X(x)$ is differentiable at a point $x$, then the PDF $f_X(x)$ can be found by differentiating the CDF with respect to $x$:

$$f_X(x) = \frac{d}{dx} F_X(x)$$

This relationship is a fundamental theorem of calculus applied to probability. **It shows that the PDF is essentially the "rate of change" of the cumulative probability.** Where the PDF is high, the CDF is rising steeply, indicating a region where values of $X$ are more probable.

Let's use our uniform distribution example, where $f_X(x) = 1$ for $0 \le x \le 1$ and $0$ otherwise.

*   For $x < 0$:

    $$F_X(x) = \int_{-\infty}^{x} 0 \, dt = 0$$

*   For $0 \le x < 1$: We integrate from 0 to $x$ because the PDF is 0 before 0.

    $$F_X(x) = \int_{-\infty}^{x} f_X(t) \, dt = \int_{0}^{x} 1 \, dt = [t]_{0}^{x} = x$$

*   For $x \ge 1$: We integrate the entire non-zero part of the PDF, which accumulates to 1.

    $$F_X(x) = \int_{-\infty}^{x} f_X(t) \, dt = \int_{0}^{1} 1 \, dt + \int_{1}^{x} 0 \, dt = [t]_{0}^{1} + 0 = 1 - 0 = 1$$

So, the CDF for the uniform random variable is:

$$F_X(x) = \begin{cases} 0 & \text{for } x < 0 \\ x & \text{for } 0 \le x < 1 \\ 1 & \text{for } x \ge 1 \end{cases}$$

We can check that differentiating $F_X(x)$ in the range $0 < x < 1$ gives us $f_X(x)$:

$$\frac{d}{dx} (x) = 1$$

which matches our PDF.

---

## Key Relationships between PMF, PDF, and CDF

The CDF serves as a central link between the PMF (for discrete variables) and the PDF (for continuous variables), providing a unified way to describe probability distributions.

*   **For discrete random variables**:
    *   **PMF to CDF**: We sum the PMF values to get the CDF.

        $$F_X(x) = \sum_{t \le x} p_X(t)$$

    *   **CDF to PMF**: We can find the PMF from the CDF by looking at the "jumps" in the step function.

        $$p_X(x) = F_X(x) - \lim_{t \to x^-} F_X(t)$$

        (This is the size of the jump at point $x$).

*   **For continuous random variables**:
    *   **PDF to CDF**: We integrate the PDF to get the CDF.

        $$F_X(x) = \int_{-\infty}^{x} f_X(t) dt$$

    *   **CDF to PDF**: We differentiate the CDF to get the PDF (where the CDF is differentiable).

        $$f_X(x) = \frac{d}{dx} F_X(x)$$

The CDF is also incredibly useful for calculating probabilities over intervals for *any* type of random variable:

$$P(a < X \le b) = F_X(b) - F_X(a)$$

For continuous random variables, since $P(X=a)=0$, we also have:

$$P(a \le X \le b) = F_X(b) - F_X(a)$$
This means the probability of $X$ falling into any interval can always be found using the CDF.

---

## Advanced Considerations and Deeper Insights

While we have covered the foundational aspects in detail, a truly thorough understanding benefits from exploring some edge cases and more abstract interpretations.

### Inverse CDF (Quantile Function)

An important concept related to the CDF, especially in data science and statistics, is the **inverse CDF**, also known as the **quantile function**, often denoted $F_X^{-1}(p)$. For a given probability $p \in [0, 1]$, the quantile function returns the value $x$ such that $P(X \le x) = p$.

$$F_X^{-1}(p) = x \quad \text{such that } F_X(x) = p$$

This is how we define percentiles, quartiles, and the median of a distribution. For instance, the median is $F_X^{-1}(0.5)$. In simulations, the inverse CDF is used to generate random numbers from any distribution, given a uniform random number. This is a powerful tool for Monte Carlo methods and bootstrapping.

### Mixed Random Variables

Our discussion has largely categorized random variables as strictly discrete or strictly continuous. However, some real-world phenomena exhibit characteristics of both. These are called **mixed random variables**. For example, the amount of rainfall in a day might have a non-zero probability of being exactly 0 (a discrete point) and then a continuous distribution for positive amounts of rain.

For mixed random variables:
*   Neither a PMF nor a PDF alone can fully describe the distribution.
*   The **CDF remains the unifying tool**, exhibiting both "jumps" (at discrete points with non-zero probability) and continuous, smoothly increasing segments.
*   The concept of a PDF can be extended to handle discrete points using the **Dirac delta function** ($\delta(x)$), which is a "generalized function" with infinite density at a single point and zero elsewhere, such that its integral is 1. For a degenerate discrete variable $X=c$, its "PDF" would be $f_X(x) = \delta(x-c)$. This shows how the PDF framework can be stretched to encompass point probabilities.

### Probability Distributions as Measures: The Unifying Mathematical View

At a more abstract level, probability distributions are fundamentally **probability measures**. The PMF and PDF can be seen as "densities" with respect to different underlying mathematical measures:
*   For **discrete random variables**, the PMF $p_X(x)$ acts as a density with respect to the **counting measure**. Summation is essentially integration with respect to the counting measure.
*   For **continuous random variables**, the PDF $f_X(x)$ acts as a density with respect to the **Lebesgue measure** (which corresponds to our intuitive notion of length or volume on the real line). Integration is then the standard Lebesgue integral.

This powerful mathematical framework, rooted in measure theory (specifically the Radon-Nikodym theorem), formally unifies the concepts of PMF and PDF, explaining *why* we sum for discrete cases and integrate for continuous cases, rather than just stating it as a definition. The CDF then serves as a way to represent this underlying probability measure.

### Information-Theoretic Perspective

From an information theory perspective, a probability distribution quantifies the uncertainty or "surprise" associated with the outcomes of a random variable. A distribution with high probability/density concentrated around a few values implies low uncertainty, while a more spread-out (e.g., uniform) distribution implies higher uncertainty. Concepts like entropy directly build upon these distributions to measure the average information content.

---

## Summary

## Additional materials