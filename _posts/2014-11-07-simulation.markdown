---
layout: post
author: Nathan Epstein
title:  "Simulation Foundations"
date:   2014-08-07 12:00:00
categories: jekyll update
img: "../img/bell.png"
---
##Introductory Note
Courses on simulation generally start with the assumption that you can generate a uniform random variable and nothing else. You can simulate probability distributions, stochastic processes, and more by transforming the generated uniform. Below, we take a quick look at a few key ideas in simulation. This tutorial is by no means exhaustive but introduces the key tools for addressing many problems in simulation.

##Simulation by Inversion
Consider a continuous random variable (call it X) with the cumulative distribution function (CDF) F. By definition, F(x) is the probability that X < x. Thus, F(X) is also a random variable that ranges from 0 to 1. Moreover, F(X) turns out to be uniformly distributed between 0 and 1.

Proof: X < x bi-directionally implies F(X) < F(x) (because the CDF is monotonically increasing) which implies that P(X < x) = P(F(X) < F(x)) which implies that F(x) = P(F(X) < F(x)). Letting u = F(x), we have P(F(X) < u) = u for F(X) ranging from 0 to 1 (i.e. F(X) has the CDF of a standard uniform). Thus, **F(X) is distributed uniform(0,1).**

This result turns out to be extremely useful. Assume that F is invertible and let G be its inverse (i.e. F(x) = y iff G(y) = x). Because F(X) = U (where U ~ uniform(0,1)) for **any continuous random variable X**, we can see that G(F(X)) = G(U) implies that **X = G(U).**

**Example:** Let X be an exponential random variable with lambda = 1. Then F(x) = 1 -exp(-x). So 1 -exp(-X) = U which implies that exp(-X) = U (because 1 -U is also distributed uniform(0,1)). Solving for X, we get X = -ln(U). We simulate a U = uniform(0,1) (this is native in just about any programming language), and set our simulated value of x = -ln(U).

**Big takeaway:** If X is a continuous random variable with an invertible CDF (this includes distributions such as exponential, arcsine, Pareto, Cauchy, and many others) then **we can simulate X with a uniform by setting X = G(U).**

It’s important to note that there are many continuous random variables that cannot be simulated by inversion (the normal distribution being a prominent example). Such distributions require special methods to simulate (in the case of the normal distribution, we use a method known as <a href="http://en.wikipedia.org/wiki/Box%E2%80%93Muller_transform">Box Muller</a>).

##Discrete Random Variables
In simulating discrete random variables with a uniform, the idea is to assign each outcome in the state space to a unique interval of length equal to the probability of that outcome (and contained within the open interval (0,1)).

**Example 1:** Consider a random variable X such that P(X = 0) = 0.25, P(X = 1) = 0.35, and P(X = 2) = 0.4. We can simulate such a random variable as follows. Generate U ~ uniform(0,1). If U < 0.25, then x = 0. If 0.25 < U < 0.6, then x = 1. If U > 0.6, then x = 2.

**Example 2:** Let X be a Poisson random variable with parameter lambda = 1. Then for all non-negative k, P(X = k) = (exp(-1)/ k!). We can simulate X by the following procedure.

1) Initialize sum = n = 0 and generate U ~ uniform(0,1).

2) sum = sum + exp(-1)/n!

3) If sum > U, then x = n. Else, n = n + 1 and return to step 2.

##Simulate Stochastic Processes
A stochastic process is a collection of random variables which represent the evolution of a system of random values over time. To simulate the stochastic process, we need only simulate the random variables which govern its behavior.

**Example:** Let N(t) be a Poisson process with parameter lambda = 1. Thus, the time between arrivals in this process is exponentially distributed with parameter lambda = 1. We can simulate this N(t) by the following procedure.

1) Initialize sum = n = 0.

2) Generate U ~ uniform(0,1). sum = sum + (-ln(U)), noting that -ln(U) ~ exponential(1).

3) If sum > t, then N(t) = n. Else, n = n + 1 and return to step 2.


##Monte Carlo Integration
Simulation has applications outside of probability theory as well. In particular, Monte Carlo methods involve repeated random sampling to develop numerical approximations of values that are difficult to approximate analytically. A common application of Monte Carlo methods is approximating definite integrals that are difficult to solve by hand.

A definite integral is simply the area under a curve over the bounds of integration. In Monte Carlo Integration we define a space of known area which encloses the section of the function we wish to integrate over (for example, a square of unit area in the first quadrant with a corner at the origin would enclose f(x)= x/2 from 0 to 1).

If we select random points uniformly distributed over the enclosing area, the proportion that land under the curve is the proportion of the enclosing area occupied by the function. Put another way, the **indefinite integral is approximately equal to (area of the enclosing)(number of random points that fall under the curve)/(total number of random points).**

In the example of f(x) = x/2, the area under the function takes up 1/4 of the unit square. Thus, approximately 1/4 of randomly generated points will fall under the curve. This, correctly, tells us that the integral of f(x) from 0 to 1 is (1/4)(area of the unit square) = 1/4.

While this method may not seem useful for f(x) = x/2, it is valuable for more complicated functions. Suppose you needed to integrate f(x) = exp(cos(x)) from (-2,2). This is not easily done analytically. However, establishing boundaries (x in (-2,2) and f(x) in (0, exp(1))) is quite simple. From there, we generate points uniformly over that area and apply the bolded formula. Full code for this example is available <a href="https://github.com/NathanEpstein/MonteCarloIntegration/blob/master/integralSolver.cpp">here.</a>