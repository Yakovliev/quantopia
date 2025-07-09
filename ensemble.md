# Statistical Ensembles and Liouville's Theorem
## What is an Ensemble?

In **classical mechanics**, we describe the state of a system (like a single particle) by its position and momentum. For a system with many particles, say $N$ particles, the state would be given by $3N$ position coordinates and $3N$ momentum coordinates. This $6N$-dimensional space is called **phase space**. Each point in phase space represents a unique microscopic state of the system.

However, when we deal with macroscopic systems (like a gas in a room), we have an enormous number of particles (on the order of Avogadro's number, $10^{23}$). It's practically impossible to know the exact microscopic state of such a system at any given time. Even if we could, solving the equations of motion for all those particles would be computationally intractable.

This is where the concept of an **ensemble** comes in. An ensemble is a **collection of a large number of identical systems**, all prepared in the same macroscopic way, but each in a different possible microscopic state consistent with the macroscopic conditions.

Imagine you have a box of gas. You know its volume, temperature, and the number of particles. An ensemble would be a vast collection of identical boxes, each with the same volume, temperature, and number of particles, but the individual gas molecules within each box would be in different positions and have different momenta.

The idea is that if we observe a single macroscopic system over a very long time, it will, on average, visit all the microscopic states consistent with its macroscopic properties. This is called the **ergodic hypothesis**. For practical purposes, instead of waiting for one system to explore all its possible states, we consider a large number of identical systems at a single instant in time. The average over this ensemble is then equivalent to the time average of a single system.

> **[Ergodic hypothesis](https://en.wikipedia.org/wiki/Ergodic_hypothesis)**. The ergodic hypothesis, in physics and thermodynamics, essentially states that for a system in thermal equilibrium, the time a system spends in a particular region of its phase space is proportional to the volume of that region. In simpler terms, over a long period, the system will visit all accessible states with equal probability. This allows us to calculate the average behavior of a system by averaging over its states, rather than over time. 

### Types of Ensembles

The type of ensemble used depends on which macroscopic quantities are kept constant:

* **Microcanonical Ensemble (NVE):** This ensemble represents an isolated system where the **number of particles ($N$), volume ($V$), and total energy ($E$) are fixed**. All systems in this ensemble have exactly the same energy.
* **Canonical Ensemble (NVT):** This ensemble represents a closed system in thermal contact with a heat reservoir. Here, the **number of particles ($N$), volume ($V$), and temperature ($T$) are fixed**. Energy can fluctuate between the system and the reservoir.
* **Grand Canonical Ensemble ($\mu$VT):** This ensemble represents an open system that can exchange both energy and particles with a reservoir. Here, the **chemical potential $\mu$, volume $V$, and temperature $T$ are fixed**. Both energy and particle number can fluctuate.

We will review all these different ensembles in detail a bit later.

---
## Liouville's theorem

Liouville's theorem in statistical mechanics states that the density of system points in phase space remains constant along the trajectories of a Hamiltonian system. In simpler terms, it means that the "volume" occupied by a group of particles in phase space remains unchanged as they move through time. This theorem is a cornerstone of statistical mechanics, particularly when dealing with conservative systems.

Liouville's theorem is a cornerstone of statistical mechanics, providing a fundamental insight into how systems evolve in **phase space**. It essentially states that the **density of points in phase space remains constant along the trajectories of the system**. This is analogous to an **incompressible fluid** flow in phase space.

**Phase space** is a $6N$-dimensional mathematical space where each point represents a unique **microstate** of the system, defined by all its position and momentum coordinates. As the system evolves over time, this point traces a path, or **trajectory**, in phase space.

Liouville's theorem has two equivalent interpretations:

1.  **Conservation of Phase Space Volume:** If you take a collection of initial microstates that occupy a certain volume in phase space, as these microstates evolve according to Hamilton's equations, the *volume* of the region they occupy in phase space remains constant. The shape of this region might distort significantly, but its total volume does not change.
2.  **Conservation of Phase Space Density:** Consider a "fluid" of representative points in phase space, where the density of this fluid, $\rho(q, p, t)$, represents the probability of finding the system in a particular microstate at a given time $t$. Liouville's theorem states that if you follow any specific point in this fluid (i.e., a specific system's trajectory), the density of points *around that specific point* remains constant. In other words, the fluid is incompressible.

This theorem applies to **conservative Hamiltonian systems**, meaning systems where the total energy is conserved and there are no external dissipative forces like friction.

Consider a large number of identical systems, each represented by a point in phase space. As time evolves, these points move through phase space according to Hamilton's equations of motion. Liouville's theorem states that the **density of points in phase space remains constant along any trajectory**. In simpler terms, if you take a small "blob" of phase space points, as these points evolve in time, the volume of that blob remains constant, even though its shape might distort.
The mathematical statement of Liouville's theorem is often expressed through the **Liouville equation**, which describes the time evolution of the phase space distribution function $\rho(q, p, t)$.

We start by considering the conservation of "probability" (or the number of representative points) in phase space. Imagine a small, fixed volume $dV$ in phase space. The change in the number of points within this volume over time must be due to the net flow of points across its boundaries. This is analogous to the continuity equation in fluid dynamics.

The **continuity equation** in phase space is:

$$\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0$$

Here:
* $\rho(q, p, t)$ is the phase space probability density.
* $\mathbf{v}$ is the "velocity" vector in phase space, whose components are the time derivatives of the generalized coordinates and momenta: $\mathbf{v} = (\dot{q}_1, \ldots, \dot{q}_{3N}, \dot{p}_1, \ldots, \dot{p}_{3N})$.
* $\nabla \cdot$ is the divergence operator in phase space, defined as:

    $$\nabla \cdot = \sum_{i=1}^{3N} \left( \frac{\partial}{\partial q_i} + \frac{\partial}{\partial p_i} \right)$$

Expanding the divergence term:

$$\nabla \cdot (\rho \mathbf{v}) = \sum_{i=1}^{3N} \left( \frac{\partial (\rho \dot{q}_i)}{\partial q_i} + \frac{\partial (\rho \dot{p}_i)}{\partial p_i} \right)$$

Using the product rule:

$$\nabla \cdot (\rho \mathbf{v}) = \sum_{i=1}^{3N} \left( \frac{\partial \rho}{\partial q_i} \dot{q}_i + \rho \frac{\partial \dot{q}_i}{\partial q_i} + \frac{\partial \rho}{\partial p_i} \dot{p}_i + \rho \frac{\partial \dot{p}_i}{\partial p_i} \right)$$

Rearranging terms:

$$\nabla \cdot (\rho \mathbf{v}) = \sum_{i=1}^{3N} \left( \dot{q}_i \frac{\partial \rho}{\partial q_i} + \dot{p}_i \frac{\partial \rho}{\partial p_i} \right) + \rho \sum_{i=1}^{3N} \left( \frac{\partial \dot{q}_i}{\partial q_i} + \frac{\partial \dot{p}_i}{\partial p_i} \right)$$

Now, we introduce **Hamilton's equations of motion** for a conservative system, which describe how the generalized coordinates and momenta evolve over time:

$$\dot{q}_i = \frac{\partial H}{\partial p_i}$$
$$\dot{p}_i = -\frac{\partial H}{\partial q_i}$$

where $H(q, p)$ is the Hamiltonian (the total energy) of the system.

Let's look at the second sum in the expanded divergence term:

$$\sum_{i=1}^{3N} \left( \frac{\partial \dot{q}_i}{\partial q_i} + \frac{\partial \dot{p}_i}{\partial p_i} \right) = \sum_{i=1}^{3N} \left( \frac{\partial}{\partial q_i} \left( \frac{\partial H}{\partial p_i} \right) + \frac{\partial}{\partial p_i} \left( -\frac{\partial H}{\partial q_i} \right) \right)$$

Since the order of differentiation for mixed partial derivatives of a well-behaved function like the Hamiltonian doesn't matter (assuming $H$ is sufficiently smooth), we have:

$$\frac{\partial^2 H}{\partial q_i \partial p_i} = \frac{\partial^2 H}{\partial p_i \partial q_i}$$
Therefore, the terms in the sum cancel out:

$$\sum_{i=1}^{3N} \left( \frac{\partial^2 H}{\partial q_i \partial p_i} - \frac{\partial^2 H}{\partial p_i \partial q_i} \right) = 0$$

This means the second term in the expanded divergence, $\rho \sum (\ldots)$, is zero. This is a crucial result, implying that the phase space "fluid" is **incompressible**. Let's review this statement in more details.

We can conclude that the phase space "fluid" is incompressible because the term $\sum_{i=1}^{3N} \left( \frac{\partial \dot{q}_i}{\partial q_i} + \frac{\partial \dot{p}_i}{\partial p_i} \right) = \nabla \cdot \mathbf{v}$ represents the **divergence of the phase space velocity field**, and for Hamiltonian systems, this divergence is identically zero.

Here's why that implies incompressibility:

In fluid dynamics, the **divergence of a velocity field** ($\nabla \cdot \mathbf{v}$) at a point tells you about the net outflow of fluid from an infinitesimally small volume around that point.
* If $\nabla \cdot \mathbf{v} > 0$, there's a net outflow, meaning the fluid is expanding.
* If $\nabla \cdot \mathbf{v} < 0$, there's a net inflow, meaning the fluid is compressing at that point.
* If $\nabla \cdot \mathbf{v} = 0$, there is no net outflow or inflow; the fluid density at that point is conserved as it moves. This is the definition of **incompressibility**.

In the context of phase space, our "velocity" vector $\mathbf{v}$ has components $(\dot{q}_1, \ldots, \dot{q}_{3N}, \dot{p}_1, \ldots, \dot{p}_{3N})$. The sum $\sum_{i=1}^{3N} \left( \frac{\partial \dot{q}_i}{\partial q_i} + \frac{\partial \dot{p}_i}{\partial p_i} \right)$ is precisely the **divergence of this phase space velocity field**.

As derived using Hamilton's equations:

$$\sum_{i=1}^{3N} \left( \frac{\partial \dot{q}_i}{\partial q_i} + \frac{\partial \dot{p}_i}{\partial p_i} \right) = \sum_{i=1}^{3N} \left( \frac{\partial}{\partial q_i} \left( \frac{\partial H}{\partial p_i} \right) + \frac{\partial}{\partial p_i} \left( -\frac{\partial H}{\partial q_i} \right) \right) = \sum_{i=1}^{3N} \left( \frac{\partial^2 H}{\partial q_i \partial p_i} - \frac{\partial^2 H}{\partial p_i \partial q_i} \right) = 0$$

Since this divergence is zero for Hamiltonian systems, it means that the phase space velocity field has no net sources or sinks. Therefore, if you consider a small "parcel" of phase space points, as it moves along the trajectories defined by Hamilton's equations, its volume in phase space will not change. This is the hallmark of an **incompressible flow**. The phase space "fluid" can stretch and deform, but its volume remains constant, just like an incompressible physical fluid might change shape while its total volume stays the same.

Substituting this back into the continuity equation:

$$\frac{\partial \rho}{\partial t} + \sum_{i=1}^{3N} \left( \dot{q}_i \frac{\partial \rho}{\partial q_i} + \dot{p}_i \frac{\partial \rho}{\partial p_i} \right) = 0$$
The sum on the left is precisely the **convective derivative** (or total time derivative) of $\rho$ with respect to time, assuming $\rho$ depends explicitly on $t$ as well as implicitly through $q(t)$ and $p(t)$. This is denoted as $d\rho/dt$.

$$\frac{d\rho}{dt} = \frac{\partial \rho}{\partial t} + \sum_{i=1}^{3N} \left( \frac{\partial \rho}{\partial q_i} \frac{dq_i}{dt} + \frac{\partial \rho}{\partial p_i} \frac{dp_i}{dt} \right)$$

So, the Liouville equation can be compactly written as:

$$\frac{d\rho}{dt} = 0$$

This equation implies that the **phase space probability density $\rho$ is constant along the trajectories of the system**. An observer "riding along" with a phase space point would always measure the same density of other points around them. $\frac{d\rho}{dt} = 0$ equation means that if you **follow a specific trajectory in phase space** (i.e., you are "riding along" with a specific phase space point), the density $\rho$ that you observe *at that specific point* will **not change with time**.

Imagine a fluid with dye markers. If you are standing still in the fluid, you might see the dye concentration change as different parts of the fluid flow past you ($\frac{\partial \rho}{\partial t} \neq 0$). However, if you attach yourself to one of the dye markers and move with it, you will always be within the same "parcel" of fluid, and the concentration of dye *within that parcel* (and thus around you) would remain constant, assuming the fluid is incompressible ($\frac{d\rho}{dt} = 0$).

In the context of Liouville's theorem, the phase space "fluid" is incompressible. Therefore, an observer moving with a specific system's trajectory in phase space will always perceive the local density of other nearby system trajectories (or representative points) to be constant.

Liouville's theorem is crucial for understanding statistical ensembles, particularly the microcanonical ensemble where all accessible microstates on a given energy hypersurface are equally probable.

## Liouville's theorem and equilibrium statistical mechanics

Liouville's theorem states that the **total time derivative** of the probability density function in phase space, $\frac{d\rho}{dt}$, is zero. This is a general result that holds for any Hamiltonian system, whether it's in equilibrium or not. This also means, that $\rho$ is a constant of motion because the total time derivative is equal to zero.

In statistical mechanics, a system is said to be in **equilibrium** when its macroscopic properties (like temperature, pressure, energy, volume, etc.) are **time-independent**. This doesn't mean that the individual particles have stopped moving; quite the opposite, they are in constant, dynamic motion. Instead, it means that the *average* behavior of the system, when observed over time, remains constant.

For this macroscopic constancy to hold, the **probability distribution** of the system's microstates must also be time-independent. 

$$\frac{d\rho}{dt} = \frac{\partial \rho}{\partial t} + \sum_{i=1}^{3N} \left( \dot{q}_i \frac{\partial \rho}{\partial q_i} + \dot{p}_i \frac{\partial \rho}{\partial p_i} \right) = 0$$

This equation, as we've established, tells us that the phase space density $\rho$ is constant along the trajectories of the system.

Now, for a system to be in **statistical equilibrium**, we require that the probability density function $\rho$ is **stationary**. Stationary means that the density does not explicitly depend on time. In mathematical terms, this means:

$$\frac{\partial \rho}{\partial t} = 0$$

If $\frac{\partial \rho}{\partial t} = 0$, then the Liouville equation simplifies to:

$$\sum_{i=1}^{3N} \left( \dot{q}_i \frac{\partial \rho}{\partial q_i} + \dot{p}_i \frac{\partial \rho}{\partial p_i} \right) = 0$$

This sum can also be written using the **Poisson bracket**:

$$\{\rho, H\} = \sum_{i=1}^{3N} \left( \frac{\partial \rho}{\partial q_i} \frac{\partial H}{\partial p_i} - \frac{\partial \rho}{\partial p_i} \frac{\partial H}{\partial q_i} \right)$$

Since $\dot{q}_i = \frac{\partial H}{\partial p_i}$ and $\dot{p}_i = -\frac{\partial H}{\partial q_i}$, the condition for equilibrium ($\frac{\partial \rho}{\partial t} = 0$) translates to:

$$\{\rho, H\} = 0$$

In addition to this result, we have one more: **in a case of equilibrium, $\rho$ is also a function of other constants of motion**.

For a system to be in **equilibrium** (a stationary state), the phase space density $\rho$ must not be changing at any fixed point in phase space. This means its **partial time derivative must be zero** ($\frac{\partial\rho}{\partial t} = 0$).

When $\rho$ is expressed solely as a function of the system's **other constants of motion** (like energy, momentum, angular momentum, etc.), then $\frac{\partial\rho}{\partial t}$ automatically becomes zero. This is because these other constants of motion do not explicitly depend on time, and their values are conserved along trajectories.

So, while $\frac{d\rho}{dt} = 0$ is always true for any Hamiltonian system (making $\rho$ a "constant of motion"), for the system to be in a **statistical equilibrium**, the stronger condition of $\frac{\partial\rho}{\partial t} = 0$ must also hold, which is achieved when $\rho$ depends only on the other conserved quantities of the system.
**Think of it this way:** If $\rho$ depended on a variable that changes over time for a given trajectory (e.g., a specific $q_i$ or $p_i$ that is not a constant of motion), then as the system evolves, its microstate $(q, p)$ would move to a new location in phase space, where that changing variable would have a different value. If $\rho$ directly depended on such a changing variable, then $\rho$ would necessarily change its value at that fixed point in phase space over time, contradicting the condition $\frac{\partial \rho}{\partial t} = 0$.

Therefore, for $\rho$ to be stationary ($\frac{\partial \rho}{\partial t} = 0$), it **must only be a function of quantities that are themselves constants of motion** for the system. The most important and universally applicable constant of motion for a conservative Hamiltonian system is its **total energy, $H$**.

### Example: The Hamiltonian as a Constant of Motion

The Hamiltonian $H(q, p)$ itself is a constant of motion for conservative systems:

$$\frac{dH}{dt} = \frac{\partial H}{\partial t} + \{H, H\}$$

Since $\{H, H\} = 0$ and for a conservative system, $\frac{\partial H}{\partial t} = 0$ (Hamiltonian has no explicit time dependence), then $\frac{dH}{dt} = 0$.

This means that any function of the Hamiltonian, say $f(H(q, p))$, will also be a constant of motion. For example, if $\rho = f(H)$, then:

$$\{\rho, H\} = \left\{ f(H), H \right\} = \frac{df}{dH} \{H, H\} = \frac{df}{dH} \cdot 0 = 0$$

This satisfies the condition for equilibrium. 

> This is why the canonical ensemble distribution, $\rho \propto e^{-\beta H}$, and the microcanonical ensemble distribution, where $\rho$ is constant for a given energy and zero elsewhere, are valid equilibrium distributions: they are both functions of $H$, the total energy of the system.

In statistical mechanics, we typically deal with equilibrium ensembles, thus, the following expression for the probability density is important:

$$\rho = \rho(q, p) = \rho(H(q,p)) $$

---

## Ensemble Average

> In statistical mechanics, we typically deal with equilibrium ensembles, where $\rho$ is time-independent. All the standard ensembles (microcanonical, canonical, and grand canonical) are fundamentally equilibrium ensembles. They are designed to describe systems in a state of statistical equilibrium with their environment (or isolated, in the case of the microcanonical ensemble). Thus, phase space probability density (or probability density function) is not dependent explicitly on time ($\rho = \rho(q, p)$).

Let's recall:

> The idea is that if we observe a single macroscopic system over a very long time, it will, on average, visit all the microscopic states consistent with its macroscopic properties. This is called the **ergodic hypothesis**. For practical purposes, instead of waiting for one system to explore all its possible states, we consider a large number of identical systems at a single instant in time. The average over this ensemble is then equivalent to the time average of a single system.

Since we cannot know the exact microscopic state of a macroscopic system, we are interested in the average values of macroscopic observables. The **ensemble average** of a physical quantity is the average of that quantity over all the systems in the ensemble, weighted by their phase space density.

Let $O(q, p)$ be a physical observable (a function of the phase space coordinates). The ensemble average of $O$, denoted by $\langle O \rangle$, is given by:

$$\langle O \rangle = \frac{\int O(q, p) \rho(q, p) dqdp}{\int \rho(q, p) dqdp}$$

If $\rho$ is normalized such that $\int \rho(q, p) dqdp = 1$, then:

$$\langle O \rangle = \int O(q, p) \rho(q, p, t) dqdp$$