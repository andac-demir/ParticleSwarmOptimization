# Particle Swarm Optimization

PSO is a computational method that iteratively optimizes a problem by trying to improve a candidate solution
with regard to a given measure of quality.

We have a population of candidate solutions which are called as particles. They are initialized arbitrarily
in the search space in the beginning of the algorithm and we move those particles in the search space based on the position and velocity of the particle.
At each iteration, a particle is guided towards the best known position in the search space which is updated as
better solutions which are found by the other particles. This moves the swarm towards the best known best solutions.

Particle Swarm Optimization is a **metaheuristic algorithm** since it makes few or no assumptions about the problem
being optimized.
Additionally, unlike classic optimization methods like **gradient descent** and **quasi-newton methods**, PSO does not require that the optimization problem must be *differentiable* and PSO does not use the gradients of the problem being optimized.


## Algorithm:

There is a cost function (*f*) which must be minimized and it takes as an argument a candidate solution (a particle) in the form of a vector of real numbers. The gradient of the cost function is not known.

Let S be the number of particles in the swarm; each particle has a position *x_i* in the search space and a velocity *v_i*. *p_i* is the best known position of a particle *i* and *g* is the best known position of the entire swarm.

*b_up* and *b_low* are the upper and lower boundaries of the search space.

The termination criterion can be the:
i) number of iterations performed or
ii) a solution where the adequate objective function value is found.

The parameters *w*, *phi_p* and *phi_g* are selected by the practitioner and control the behavior of the PSO method.


## A basic PSO algorithm is then:

**for** each particle *i* = 1, ..., *S* **do**:
    Initialize the particle's position with a uniformly distributed random vector:
    *x_i* ~ U(*b_low*, *b_up*)
    Initialize the particle's best known position to its initial position:
    *p_i* = *x_i*
    **if** *f(p_i)* < *f(g)* **then**
        update the swarm's best known  position:
        *g* = *p_i*
    Initialize the particle's velocity:
    *v_i* ~ U(-|*b_up* - *b_low*|, |*b_up* - *b_low*|)

**while** a termination criterion is not met **do**:
    **for** each particle *i* = 1, ..., *S* **do**:
        **for** each dimension *d* = 1, ..., *n* **do**:
        Pick random numbers:
        *rp*, *rg* ~ U(0,1)
        Update the particle's velocity:
        *vi,d* = *w* * *vi,d* + *phi_p* * *rp* (*p_i,d* - *x_i,d*) + *phi_g* * *rg* (*g_d* - *x_i,d*)
    Update the particle's position:
    *xi* = *xi* + *vi*
    **if** *f(x_i)* < *f(p_i)* **then**
        Update the particle's best known position:
        *p_i* = *xi*
        **if** *f(p_i)* < *f(g)* **then**
            Update the swarm's best known position: *g* = *p_i*


## Parameters:

The choice of the parameters (*w*, *phi_p* and *phi_g*) selected by the practitioner has a huge impact on the efficiency of the PSO.

These parameters can be tuned by **meta-optimization** (a concept known for using one optimization method to tune another optimization)

*w*, *phi_p* and *phi_g* are the behavioral parameters that affect the performance of PSO. Meta-optimization is feasible for few behavioral parameters, but as the number of behavioral parameters  increases, the performance of meta-optimization is hugely disadvantaged by the **curse of dimensionality** (computation time increasing exponentially).

*w* -> constant inertia weight (how much you weigh the particle's previous velocity)
*phi_p* -> cognitive constant
*phi_g* -> social constant


## The School of Thought:

Common belief among the researchers is that the PSO is **an intersection between exploration and exploitation**.

That is PSO explores a broader region of the search-space, and exploits locally oriented search spaces to find a local optimum. Hence PSO can be categorized as a balance between exploration and exploitation to avoid premature convergence to a local optimum yet still ensures a good rate of convergence to the optimum.

One way to avoid premature convergence to a local optimum is:
**Multi-swarm optimization**!

**EXPLORATION** -> A diversification method that explores the broader search space and finds the best swarm position.
**EXPLOITATION** -> Finding local optima in one swarm position.


## Multi-Swarm Optimization:

Multi-swarm optimization is a variant of particle swarm optimization (PSO) based on the use of multiple sub-swarms instead of one (standard) swarm.

The general approach in multi-swarm optimization is that each sub-swarm focuses on a specific region,
while a specific diversification method decides where and when to launch the sub-swarms!

The multi-swarm framework is especially fitted for the optimization on multi-modal problems, where multiple local optima exist.

