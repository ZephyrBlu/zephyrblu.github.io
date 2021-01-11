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

### Side Note: Bayesian Networks - Chaining Bayes' Theorem
- Chaining events into one another
- Directed Acyclic Graph (DAG) of network
- Conditional independence between nodes
- Updating a network
- https://en.wikipedia.org/wiki/Bayesian_network

----- Part 2: Distributions -----

## Using Bayes' Theorem with Distributions
- Replace static prior with distribution
- Posterior is also now a distribution
- Show analytical calculation of posterior distribution
- Explain law of total probability: https://en.wikipedia.org/wiki/Law_of_total_probability
- Alpha and Beta hyperparameters

### Side Note: Bayesian Hierachical Modelling - Stacking Priors
- Hyperparameters
- Hyperpriors
- Extended Bayes' Theorem: Modelling with hyperpriors (I.e. multiple layers of priors)
- https://en.wikipedia.org/wiki/Bayesian_hierarchical_modeling#2-stage_hierarchical_model

## Conjugate Priors
- Conjugate prior distributions
- Basic model/prior conjugates
- Conjugates explained intuitively
 - Certain distributions are underpinned by more generic distributions defined by the Alpha and Beta hyperparameters
- https://www.lesswrong.com/posts/u2gWM2poRPkBPFeLc/the-joys-of-conjugate-priors

## Side Note: The Beta Distribution - Building a Deeper Understanding of Conjugate Priors
- Intuition for beta distribution: https://stats.stackexchange.com/questions/47771/what-is-the-intuition-behind-beta-distribution
- Interpreting Alpha and Beta as successes and failures in the dataset (Relationship to other distributions)
- Simplifying posterior calculation using Beta function
- Gamma & Beta function explained: http://www.mhtl.uwaterloo.ca/courses/me755/web_chap1.pdf

---- Part 3: Simulations -----

## Markov Chain Monte Carlo (MCMC) Simulations
- Common modern technique
- What happens without a conjugate prior or high dimensional problems?
 - The probabilty of p(x) can't be easily analytically simplified
 - Apparently very common situation in realy world
- Allows solving intractable p(x) integrals numerically instead of analytically
- Basically random sampling based on a probability distribution

## Side Note: Monte Carlo Simulations

## Side Note: Markov Chains
