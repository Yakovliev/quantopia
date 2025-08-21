# Microcanonical ensemble

## Definition

Consider a completely **isolated** physical system containing $N$ particles with total energy $E$ confined within volume $V$. Such a system operates under strict isolation conditions, meaning it cannot exchange either matter or energy with its environment. Think of it as a snapshot of all possible microscopic arrangements (called **microstates**) a system can have when its total energy, volume, and number of particles are fixed.

The fundamental assumption underlying thermal equilibrium states that the probability distribution function $\rho(q, p)$ describing the system depends solely on its total energy:

$$\rho(q, p) = \rho(H(q, p)), \quad \frac{d \rho(q, p)}{dt} = 0$$

This relationship yields a time-independent $\rho(q, p)$, which aligns perfectly with ergodic theory principles and the fundamental postulate that all accessible microstates possess equal a priori probabilities. The **probability distribution function** ($\rho(q, p)$) describes the likelihood of finding the system in a particular microstate. For an isolated system in equilibrium, this probability *only* depends on the system's total energy ($H(q, p)$ represents the system's total energy, also called the Hamiltonian). It doesn't change over time, meaning $\frac{d \rho(q, p)}{dt} = 0$. This stability is a hallmark of equilibrium.

---

Let's use an example: Imagine a simple system with just two particles that can each have an energy of either 1 unit or 2 units. The total energy of the system is fixed at 3 units.

Here are the possible microstates:

* Particle 1 has 1 unit, Particle 2 has 2 units.
* Particle 1 has 2 units, Particle 2 has 1 unit.

Both these microstates have the same total energy (3 units). In a microcanonical ensemble, we assume these two microstates are equally probable. There are no other ways to get a total energy of 3 units with these rules.

---
## Energy Boundary Layer: Defining the Ensemble

In reality, precisely fixing the energy to a single value ($E$) is often impossible or impractical. Instead, we consider a very narrow range of energies, from $E$ to $E + \Delta E$. Think of $\Delta E$ as a tiny "fuzziness" around the exact energy $E$.

Consider a narrow but measurable energy interval $[E, E + \Delta E]$ situated near the constant energy surface $E$. The **microcanonical ensemble** can be mathematically expressed as:

$$
\rho(q, p) = \begin{cases}
\frac{1}{\Gamma(E, V, N)} & E < H(q, p) < E + \Delta E \\
0 & \text{elsewhere}
\end{cases}
$$ (ensemble_1)

What does this mean?

* If a microstate's energy $H(q, p)$ falls *within* the narrow range $[E, E + \Delta E]$, then its probability is a constant value: $\frac{1}{\Gamma(E, V, N)}$. This constant ensures that all microstates within this energy range are equally probable.
* If a microstate's energy is *outside* this range, its probability is $0$.
The term $\Gamma(E, V, N)$ is a **normalization factor**. It's the "volume" in **phase space** that these allowed microstates occupy. Phase space is an abstract mathematical space where each point represents a unique microstate of the system (defined by the positions 'q' and momenta 'p' of all particles).

$$
\Gamma(E, V, N) = \int \int_{E<H(q,p)<E+\Delta E} d^{3N}q \, d^{3N}p
$$ (ensemble_2)

This integral essentially sums up all the tiny "volumes" in phase space that correspond to microstates with energies between $E$ and $E + \Delta E$. The "volume" $V$ of the physical system influences this integral because the particles are confined within that spatial volume. The spatial volume $V$ influences equation {eq}`ensemble_2` through the integration boundaries for the coordinate differentials $dq$.
## Infinitesimally Thin Energy Layer: Approaching the Limit

Sometimes, we want to consider an even more precise energy. We can imagine $\Delta E$ becoming incredibly, infinitesimally small, almost approaching zero.

Let $\Phi(E, V)$ be the total phase space volume for *all* microstates with energy *less than or equal to* $E$.

Then, the phase space volume within the narrow energy range $[E, E + \Delta E]$ can be approximated as the difference between two $\Phi$ values:

$$\Gamma(E) = \Phi(E + \Delta E) - \Phi(E)$$

As $\Delta E$ gets smaller and smaller (approaches zero), this difference becomes a derivative:

$$\Gamma(E) = \frac{\partial \Phi(E)}{\partial E} \Delta E \equiv \Omega(E) \Delta E, \quad \Delta E \ll E$$

The term $\Omega(E)$ is called the **density of states**. It tells us how many microstates are available *per unit of energy* at a given energy $E$. It's essentially the "concentration" of microstates at that specific energy level.

$$
\Omega(E) \equiv \frac{\partial \Phi(E)}{\partial E} = \int d^{3N}q \int d^{3N}p \, \delta(E - H(q, p))
$$

The term $\delta(E - H(q, p))$ is a Dirac delta function (a mathematical tool that's zero everywhere except when $E - H(q, p) = 0$, where it's infinitely large), which effectively "picks out" only those microstates where the energy $H(q, p)$ is exactly equal to $E$. **We will derive this equation a moment later**.

With $\Omega(E)$, we can rewrite the probability distribution for the microcanonical ensemble:

$$\rho(q, p) = \begin{cases}
\frac{1}{\Omega(E)\Delta E} & E < H(q, p) < E + \Delta E \\
0 & \text{elsewhere}
\end{cases}$$

This means that for an isolated system in the microcanonical ensemble, the probability of finding it in a specific microstate within the narrow energy range is inversely proportional to the density of states at that energy multiplied by the energy width. In essence, if there are more available microstates at a given energy ($\Omega(E)$ is large), then each individual microstate is less probable.


---

Let's derive the aforementioned equation

$$
\Omega(E) \equiv \frac{\partial \Phi(E)}{\partial E} = \int d^{3N}q \int d^{3N}p \, \delta(E - H(q, p))
$$

We begin by defining $\Phi(E)$ as the total **phase space volume** for all microstates with energy **less than or equal to** $E$. Think of it as a "cumulative" volume in phase space.

Mathematically, this means:

$$\Phi(E) = \int \int_{H(q,p) \le E} d^{3N}q \, d^{3N}p$$


The integral runs over all positions $q$ and momenta $p$ such that the Hamiltonian (total energy) $H(q,p)$ is less than or equal to $E$.

Recall that $\Gamma(E, V, N)$ was defined as the phase space volume within a *narrow energy interval* $[E, E + \Delta E]$. This means $\Gamma(E, V, N)$ is the volume between two energy surfaces:

$$\Gamma(E, V, N) = \Phi(E + \Delta E) - \Phi(E)$$

$$\Gamma(E, V, N) = \frac{\Phi(E + \Delta E) - \Phi(E)}{\Delta E} \Delta E$$

When we take the limit as $\Delta E$ approaches zero, the expression for $\Gamma(E, V, N)$ becomes the **derivative** of $\Phi(E)$ with respect to $E$:

$$\lim_{\Delta E \to 0} \frac{\Phi(E + \Delta E) - \Phi(E)}{\Delta E} = \frac{\partial \Phi(E)}{\partial E}$$

We *define* this derivative as the **density of states**, $\Omega(E)$:

$$
\Omega(E) \equiv \frac{\partial \Phi(E)}{\partial E}
$$

Now, how does the integral with the Dirac delta function come into play? The Dirac delta function, $\delta(x)$, has the property that $\int f(x) \delta(x-a) dx = f(a)$. It "picks out" the value of $f(x)$ at the point where its argument is zero.
Consider the definition of $\Phi(E)$ again:

$$\Phi(E) \equiv \int \int_{H(q,p) \le E} d^{3N}q \, d^{3N}p = \int d^{3N}q \int d^{3N}p \, \Theta(E - H(q, p))$$

Here, $\Theta(x)$ is the **Heaviside step function**, which is $0$ if $x < 0$ and $1$ if $x \ge 0$. So, $\Theta(E - H(q, p))$ is $1$ when $H(q, p) \le E$ and $0$ otherwise. This correctly defines $\Phi(E)$ as the integral over the phase space volume where the energy is less than or equal to $E$.

> The key property that connects the step function and the Dirac delta function is that the derivative of the Heaviside step function is the Dirac delta function: $\frac{d}{dx}\Theta(x) = \delta(x)$.

Therefore, when we take the derivative of $\Phi(E)$ with respect to $E$:

$$\Omega(E) = \frac{\partial \Phi(E)}{\partial E} = \frac{\partial}{\partial E} \left( \int d^{3N}q \int d^{3N}p \, \Theta(E - H(q, p)) \right)$$

Since the integration is over $q$ and $p$, we can bring the derivative inside the integral:

$$\Omega(E) = \int d^{3N}q \int d^{3N}p \, \frac{\partial}{\partial E} \Theta(E - H(q, p))$$

Using the chain rule, $\frac{\partial}{\partial E} \Theta(E - H(q, p)) = \delta(E - H(q, p)) \cdot \frac{\partial}{\partial E} (E - H(q, p)) = \delta(E - H(q, p)) \cdot 1 = \delta(E - H(q, p))$.

This leads directly to the integral form:

$$\Omega(E) = \int d^{3N}q \int d^{3N}p \, \delta(E - H(q, p))$$

You may have some questions regarding the dimensions when you compare this equation with the definition $\Omega(E) \equiv \frac{\partial \Phi(E)}{\partial E}$.

We can review this in different ways. First of all, we analyze a well known equation

$$ \int_{-\infty}^{\infty} \delta(x) \, dx = 1 $$

If $x$ has some dimension (for example, a dimension of energy), then $dx$ has the same dimension. As a result, the Dirac delta function $\delta (x)$ has the dimension of $\frac{1}{x}$ in order to get dimensionless result of the integral.

Secondly, $\frac{d}{dx}\Theta(x) = \delta(x)$ and $\Theta(x)$ is dimensionless. Thus, the dimension of $\delta(x)$ is totally defined by $\frac{1}{dx}$ (actually by $x$).

Therefore, the Dirac delta function $\delta(x)$ has dimensions of $1/(\text{dimension of } x)$. In our case, the argument of the delta function is $(E - H(q, p))$, which has dimensions of energy. Therefore, the dimension of $\delta(E - H(q, p))$ is $\text{Energy}^{-1}$.

---