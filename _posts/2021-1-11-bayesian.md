---
layout: post
title: Bayesian Statistics for Programmers
---

----- Part 1: Conditional Probability ------

## Preface
- Why did I write this?
    - Information is already out there 1000x, but often behind a wall of jargon and overly complex or generalized explanations
    - Aiming to be a relatively short guide to Bayesian Statistics
    - Think 80/20, 80% of the information in 20% of the words
- Why learn about bayesian statistics?
    - Understanding probability is important for everyone
    - Bayesian statistics provide a different but possibly more intuitive method for calculating and interpreting probabilities
    - Framework provided by bayesian statistics can be applied in your day to day life (Often called a bayesian mindset)
- Assumptions of knowledge
    - Solid understanding of basic conditional probability
    - Solid understanding of basic probability distributions
    - Solid understanding of basic calculus (Integration is most important)
    - That's it. Any notation and jargon will be explained
    - If you're not sure you know enough, try to follow along anyway. You'll probably be able to pick it up
- What to expect
    - Written by a programmer, for programmers
    - Informal explanations with minimal jargon
    - References to specific statistical material
    - Covers mostly theory, not practical application
- Covered content
- Side notes
    - More in-depth explanations
    - Not necessary knowledge, but helps build a deeper understanding

## Bayes' Theorem
- What is Bayes' Theorem? (Conditional probability)
- How is it derived? (It's basically definitional)
- Why use a bayesian approach over frequentist? https://www.youtube.com/watch?v=R6d-AbkhBQ8

## The Bayesian Mindset
- Conditional probability (Event A given event B)
- Bake beliefs into the model using priors
- Models produce "degree of belief" (Bayesian) instead of "frequency of occurence" (Frequentist)
    - Frequentist: In 95/100 trials, x will be value y +- z
    - Bayesian: There is a 95% probability that x is inside the range y +- z
- Update the model as new information is acquired
- https://stats.stackexchange.com/questions/22/bayesian-and-frequentist-reasoning-in-plain-english

## Simple Application of Bayes' Theorem
- Computing posterior probability based on values
- Bayesian tables
- Simple conditional probability
- Multiple ways of computing the answer
- These are discrete

<details>
    <summary style="cursor:pointer">
        <h3 style="display:inline-block;">
            Side Note: Bayesian Networks - Chaining Bayes' Theorem
        </h3>
    </summary>
    <ul style="margin-top:0">
        <li>Chaining events into one another</li>
        <li>Directed Acyclic Graph (DAG) of network</li>
        <li>Conditional independence between nodes</li>
        <li>Updating a network</li>
        <li>https://en.wikipedia.org/wiki/Bayesian_network</li>
    </ul>
</details>

----- Part 2: Distributions -----

## Using Bayes' Theorem with Continuous Distributions
- Replace static prior with distribution
- Posterior is also now a distribution
- Show analytical calculation of posterior distribution
- Explain law of total probability: https://en.wikipedia.org/wiki/Law_of_total_probability
- Alpha and Beta hyperparameters

<details>
    <summary style="cursor:pointer">
        <h3 style="display:inline-block;">
            Side Note: Bayesian Hierachical Modelling - Stacking Priors
        </h3>
    </summary>
    <ul style="margin-top:0">
        <li>Hyperparameters</li>
        <li>Hyperpriors</li>
        <li>Extended Bayes' Theorem: Modelling with hyperpriors (I.e. multiple layers of priors)</li>
        <li>https://en.wikipedia.org/wiki/Bayesian_hierarchical_modeling#2-stage_hierarchical_model</li>
    </ul>
</details>

## Conjugate Priors
- Conjugate prior distributions
- Basic model/prior conjugates
- Conjugates explained intuitively
    - Certain distributions are underpinned by more generic distributions defined by the Alpha and Beta hyperparameters
- https://www.lesswrong.com/posts/u2gWM2poRPkBPFeLc/the-joys-of-conjugate-priors

<details>
    <summary style="cursor:pointer">
        <h3 style="display:inline-block;">
            Side Note: The Beta Distribution Explained
        </h3>
    </summary>
    <ul style="margin-top:0">
        <li>Beta distribution is a common prior</li>
        <li>Intuition for beta distribution: https://stats.stackexchange.com/questions/47771/what-is-the-intuition-behind-beta-distribution</li>
        <li>Interpreting Alpha and Beta as successes and failures in the dataset (Relationship to other distributions)</li>
        <li>Simplifying posterior calculation using Beta function</li>
        <li>Gamma & Beta function explained: http://www.mhtl.uwaterloo.ca/courses/me755/web_chap1.pdf</li>
    </ul>
</details>

<details>
    <summary style="cursor:pointer">
        <h3 style="display:inline-block;">
            Side Note: Understanding the Math Behind Conjugate Priors
        </h3>
    </summary>
    <ul style="margin-top:0">
        <li>Gamma & Beta function explained: http://www.mhtl.uwaterloo.ca/courses/me755/web_chap1.pdf</li>
    </ul>
</details>

---- Part 3: Simulations -----

## Markov Chain Monte Carlo (MCMC) Simulations
- Common modern technique
- What happens without a conjugate prior or high dimensional problems?
    - The probabilty of p(x) can't be easily analytically simplified
    - Apparently very common situation in realy world
- Allows solving intractable p(x) integrals numerically instead of analytically
- Basically random sampling based on a probability distribution

<details>
    <summary style="cursor:pointer">
        <h3 style="display:inline-block;">
            Side Note: MCMC Simulations Explained
        </h3>
    </summary>
    <ul style="margin-top:0">
        <li>What exactly are Monte Carlo simluations?</li>
        <li>Purpose of Monte Carlo simulations: Approximating intractable problems numerically</li>
        <li>Specifics behind the process they use</li>
    </ul>
    First, let's quickly go over what "Markov Chain Monte Carlo" actually means.

    Markov Chains are basically just a stateless random process (I.e the next state is purely based on the current state).

    Monte Carlo in this case refers to a family of algorithms known as "Monte Carlo methods", which are generally used for numerical approximation of an intractable or otherwise difficult computation.

    They approach this by randomly sampling from a probability distribution, then aggregating the sampled values and calculating an approximation. This is a well laid out example: https://en.wikipedia.org/wiki/Monte_Carlo_method#Overview

    In this case, we use a Monte Carlo algorithm to approximate the integral of p(x) (I.e. the area ).
</details>

<details>
    <summary style="cursor:pointer">
        <h3 style="display:inline-block;">
            Side Note: The Metropolis-Hastings and Hamiltonian Monte Carlo Sampling Algorithms
        </h3>
    </summary>
    <ul style="margin-top:0">
        <li>These are common MCMC sampling algorithms</li>
        <li>MH is older, HMC is more modern and common nowadays</li>
        <li>Brief overview of each</li>
        <li>Similarities and differences</li>
        <li>Why is HMC 'better'?</li>
    </ul>

    <h4>Metropolis-Hastings</h4>
    Metropolis-Hastings does not directly sample from a distribution, but uses a clever technique to *effectively* sample the distribution.

    To generate samples, the algorithm only requires that you have a function f(x) that is *proportional* to the distribution P(x). That is, f(x) * k = P(x).

    How does this work? We'll step through how the algorithm works to find out:

    1) Choose and arbitrary starting point for the initial sample, x<sub>t</sub>. Also choose an arbitrary probability distribution, g(x|y) (Called the "proposal density" or "jumping distribution"), to serve as a sample generator. This is usually a Gaussian (Normal) distribution centered on y, which means that points close to y are more likely to be selected as the next sample candidate.

    2a) Randomly generate a candidate sample for the iteration from g like so: g(x'|x<sub>t</sub>)

    2b) Calculate the acceptance ratio of the candidate. This is the special sauce. Earlier we said that the algorithm only requires a function f(x) which is proportional to P(x), rather than being exact. Calculating the acceptance ratio leverages this fact.

    a = f(x')/f(x<sub>t</sub>) = P(x')/P(x<sub>t</sub>)

    This works because the normalizing constant is cancelled out

    a = (f(x') * k)/(f(x<sub>t</sub>) * k) = P(x')/P(x<sub>t</sub>)

    What we are calculating here is the probability of the new sample, relative to the previous sample. If the new sample is more probable, it means it is in a higher density (I.e. higher frequency) region of P(x) distribution.

    This is the core reason why the algorithm converges on the P(x) distribution over many samples. Values from high density regions of P(x) are sampled more frequently simply by virtue of them being more likely, and vice versa.

    2c) Accept or reject the candidate sample. Here is where we use the acceptance ratio to generate randomness in the process. We generate a random number in range [0, 1] from a uniform distribution (I.e. every value has an equal chance).

    If this number is <= to the acceptance ratio, we accept the new sample, update x<sub>t</sub> to x<sub>t+1</sub> and set x<sub>t+1</sub> to equal the newly generated sample.

    If the number of less than the acceptance ratio, x<sub>t</sub> is updated to x<sub>t+1</sub>, but the value remains unchanged for the next iteration.

    3) Repeat step 2 until you reach the desired number of iterations

    The Metropolis-Hastings algorithm works well, but has a couple of drawbacks.

    Remember how Markov Chains generate new states based on the current state? That means that states (And therefore generated samples) are somewhat correlated. This is bad because it means that locally, samples will not reflect P(x) (Though globally samples will converge on P(x)).

    Another problem related to the distribution of samples is that even though they eventually converge on P(x), initial samples may not. This may require specifying a "burn-in" period where initial samples are discarded to reduce bias in the generated samples.

    https://en.wikipedia.org/wiki/Metropolis%E2%80%93Hastings_algorithm

    <h4>Hamiltonian Monte Carlo</h4>
</details>

---- Part 4: Real-World Applications -----
