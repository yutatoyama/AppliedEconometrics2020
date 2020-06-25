---
title: 'Program Evaluation (Causal Inference) 2: Matching'
author: "Instructor: Yuta Toyama"
date: "Last updated: 2020-06-22"
fig_width: 6 
fig_height: 4 
output: 
  html_document:
    theme: lumen
    highlight: haddock 
    #code_folding: show
    toc: yes
    number_sections: true
    toc_depth: 2
    toc_float: true
    keep_md: true
    df_print: paged
  beamer_presentation:
    theme: "Madrid"
    colortheme: "lily"
    slide_level: 2
    includes:
      in_header: "../beamer_header_noRcode.tex"
    df_print: tibble
---

# Introduction

## Introduction: Matching Estimator

-   Idea: Compare **individuals with the same characteristics $X$**
    across treatment and control groups
\bigskip
-   Key assumption: Treatment is random once we control for the observed characteristics.
\bigskip
-   Do you remember we already learnt a similar idea before?

# Identification


## Matching


-   Let $X_{i}$ denote the observed characteristics:
    - age, income, education, race, etc..
\bigskip
-   Assumption 1: $$D_{i}\perp(Y_{0i},Y_{1i})\left|X_{i}\right.$$
    -   Conditional on $X_{i}$, no selection bias.
    -   Selection on observables assumption / ignorability
\bigskip
-   Assumption 2: Overlap assumption
    $$P(D_{i}=1|X_{i}=x)\in(0,1)\ \forall x$$
    -   Given $x$, we should be able to observe people from both control
        and treatment group.
    - We call $P(D_{i}=1|X_{i}=x)$ **propensity score**.

## Identification

-   The assumption implies that $$\begin{aligned}
    E[Y_{1i}|D_{i} & =1,X_{i}]=E[Y_{1i}|D_{i}=0,X_{i}]=E[Y_{1i}|X_{i}]\\
    E[Y_{0i}|D_{i} & =1,X_{i}]=E[Y_{0i}|D_{i}=0,X_{i}]=E[Y_{0i}|X_{i}]\end{aligned}$$

-   The $ATT$ for $X_{i}=x$ is given by $$\begin{aligned}
    E[Y_{1i}-Y_{0i}|D_{i}=1,X_{i}] & =E[Y_{1i}|D_{i}=1,X_{i}]-E[Y_{0i}|D_{i}=1,X_{i}]\\
     & =E[Y_{i}|D_{i}=1,X_{i}]-E[Y_{0i}|D_{i}=0,X_{i}]\\
     & =\underbrace{E[Y_{i}|D_{i}=1,X_{i}]}_{avg\ with\ X_{i}\ in\ treatment}-\underbrace{E[Y_{i}|D_{i}=0,X_{i}]}_{avg\ with\ X_{i}\ in\ control}\end{aligned}$$

-   The components in the last line are identified (can be estimated).

-   Intuition: Comparing the outcome across control and treatment groups
    after conditioning on $X_{i}$

## ATT and ATE

-   ATT is given by $$\begin{aligned}
    ATT & =E[Y_{1i}-Y_{0i}|D_{i}=1]\\
     & =\int E[Y_{1i}-Y_{0i}|D_{i}=1,X_{i}=x]f_{X_{i}}(x|D_{i}=1)dx\\
     & =E[Y_{i}|D_{i}=1]-\int\left(E[Y_{i}|D_{i}=0,X_{i}=x]\right)f_{X_{i}}(x|D_{i}=1)\end{aligned}$$

-   ATE is $$\begin{aligned}
    ATE= & E[Y_{1i}-Y_{0i}]\\
    = & \int E[Y_{1i}-Y_{0i}|X_{i}=x]f_{X_{i}}(x)dx\\
    = & \int E[Y_{i}|D_{i}=1,X_{i}=x]f_{X_{i}}(x)dx\\
    = & +\int E[Y_{i}|D_{i}=0,X_{i}=x]f_{X_{i}}(x)dx\end{aligned}$$

# Estimation

## Estimation Methods

-   We need to estimate $E[Y_{i}|D_{i}=1,X_{i}=x]$ and
    $E[Y_{i}|D_{i}=0,X_{i}=x]$
\bigskip
-   Several ways to implement the above idea
    1.   Regression: Nonparametric and Parametric
    2.   Nearest neighborhood matching
    3.   Propensity Score Matching

## Approach 1: Regression, or Analogue Approach

-   Let $\hat{\mu}_{k}(x)$ be an estimator of
    $\mu_{k}(x)=E[Y_{i}|D_{i}=k,X_{i}=x]$ for $k\in\{0,1\}$
\bigskip
-   The analog estimators are $$\begin{aligned}
    \hat{ATE} & =\frac{1}{N}\sum_{i=1}^{N}\hat{\mu}_{1}(X_{i})-\hat{\mu}_{0}(X_{i})\\
    \hat{ATT} & =\frac{N^{-1}\sum_{i=1}^{N}D_{i}(Y_{i}-\hat{\mu}_{0}(X_{i}))}{N^{-1}\sum_{i=1}^{N}D_{i}}\end{aligned}$$
-   How to estimate $\mu_{k}(x)=E[Y_{i}|D_{i}=k,X_{i}=x]$ ?

## Nonparametric Estimation

-   Suppose that $X_{i}\in\{x_{1},\cdots,x_{K}\}$ is discrete with small
    $K$
    -   Ex: two demographic characteristics (male/female,
        white/non-white). $K=4$
\bigskip
-   Then, a nonparametric binning estimator is
    $$\hat{\mu}_{k}(x)=\frac{\sum_{i=1}^{N}\mathbf{1}\{D_{i}=k,X_{i}=x\}Y_{i}}{\sum_{i=1}^{N}\mathbf{1}\{D_{i}=k,X_{i}=x\}}$$
\bigskip
-   Here, I do not put any parametric assumption on
    $\mu_{k}(x)=E[Y_{i}|D_{i}=k,X_{i}=x]$.


--- 

## Curse of dimensionality

-   Issue: Poor performance if $K$ is large due to many covariates.
\bigskip
  - So many potential groups, too few observations for each group.
  - With $K$ variables, each of which takes $L$ values, $L^K$ possible groups (bins) in total. 
- This is known as **curse of dimensionality**.
\bigskip 
-   Relatedly, if $X$ is a continuous random variable, can use kernel regression.

## Parametric Estimation, or going back to linear regression

-   If you put parametric assumption such as $$\begin{aligned}
    E[Y_{i}|D_{i}=0,X_{i}=x] & =\beta'x_{i}\\
    E[Y_{i}|D_{i}=1,X_{i}=x] & =\beta'x_{i}+\tau_{0}\end{aligned}$$
    then, you will have a model
    $$y_{i}=\beta'x_{i}+\tau D_{i}+\epsilon_{i}$$
-   You can think the matching estimator as controlling for omitted
    variable bias by adding (many) covariates (control variables)
    $x_{i}$.
\bigskip
-   This is one reason why matching estimator may not be preferred in
    empirical research.
    -   Remember: Controlling for those covariates is of course
        important. This can be combined with other empirical strategies
        (IV, DID, etc).

## Approach 2: $M-$Nearest Neighborhood Matching

-   Idea: Find the counterpart in other group that is close to me.
\bigskip
-   Define $\hat{y}_{i}(0)$ and $\hat{y}_{i}(1)$ be the estimator for
    (hypothetical) outcomes when treated and not treated.
    $$\hat{y}_{i}(0)=\begin{cases}
    y_{i} & if\ D_{i}=0\\
    \frac{1}{M}\sum_{j\in L_{M}(i)}y_{j} & if\ D_{i}=1
    \end{cases}$$
-   $L_{M}(i)$ is the set of $M$ individuals in the opposite group who
    are "close" to individual $i$
    -   Several ways to define the distance between $X_{i}$ and $X_{j}$, such as
        $$dist(X_{i},X_{j})=||X_{i}-X_{j}||^{2}$$
\bigskip    
-   Need to choose (1) $M$ and (2) the measure of distance
    -   R has several packages for this.
    
## Approach 3: Propensity Score Matching

- Use propensity score $P(D_{i}=1|X_{i}=x)$ as a distance to define who is the closest to me. 
\bigskip
- Implementation:
    1. Estimate propensity score function by logit or probit using a flexible function of $X_i$. 
    2. Calculate the propensity score for each observation. Use it to define the pair.

