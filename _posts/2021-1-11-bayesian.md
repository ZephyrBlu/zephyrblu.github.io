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

## Using Bayes' Theorem with Distributions
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
            Side Note: Monte Carlo Simulations Explained
        </h3>
    </summary>
    <ul style="margin-top:0">
        <li>What exactly are Monte Carlo simluations?</li>
        <li>Purpose of Monte Carlo simulations: Approximating intractable problems numerically</li>
        <li>Specifics behind the process they use</li>
    </ul>
</details>

<details>
    <summary style="cursor:pointer">
        <h3 style="display:inline-block;">
            Side Note: Markov Chains Explained
        </h3>
    </summary>
    <ul style="margin-top:0">
        <li>What are Markov Chains?</li>
        <li>How do they work?</li>
    </ul>
</details>

---- Part 4: Real-World Applications -----
