---
title: 'Program Evaluation (Causal Inference) 1: Introduction'
author: "Instructor: Yuta Toyama"
date: "Last updated: March 28, 2020"

output: 
  html_document:
#    theme: cerulean
    theme: readable
    highlight: haddock 
    #code_folding: show
    toc: yes
    toc_depth: 2
    toc_float: true
    keep_md: true
---

Introduction
============

Introduction

-   Program Evaluation, or Causal Inference

    -   Estimation of "treatment effect" of some intervention (typically
        binary)

    -   Example:

        -   effects of job training on wage
        -   effects of advertisement on purchase behavior
        -   effects of distributing mosquito net on children's school
            attendance

-   Difficulty: treatment is **endogenous decision**

    -   selection bias, omitted variable bias.

    -   especially in observational data (in comparison with
        experimental data)

Overview

-   Introduce Rubin's causal model (potential outcome framework)

    -   Generalization of the linear regression model: Nonparametric

-   Solutions to the selection bias

    1.  Randomized control trial (today)

    2.  Matching (today)

    3.  Instrumental Variable Estimation (today)

    4.  Difference-in-differences (next week)

    5.  Regression Discontinuity Design (week after next)

Reference

-   Angrist and Pischke:

    -   Mostly harmless econometrics : advanced undergraduate to
        graduate students

    -   Mastering Metrics: good for undergraduate students after taking
        econometrics course.

-   Ito: Data Bunseki no Chikara (in Japanese)

Framework
=========

Framework

-   $Y_{i}$: observed outcome for person $i$

-   $D_{i}$: treatment status $$D_{i}=\begin{cases}
    1 & treated\ (treatment\ group)\\
    0 & not\ treated\ (control\ group)
    \end{cases}$$

-   Define *potential outcomes*

    -   $Y_{1i}$: outcome for $i$ when she is treated (treatment group)

    -   $Y_{0i}$: outcome for $i$ when she is not treated (control
        group)

-   With this, we can write $$\begin{aligned}
    Y_{i} & =D_{i}Y_{1i}+(1-D_{i})Y_{0i}\\
     & =\begin{cases}
    Y_{1i} & if\ D_{i}=1\\
    Y_{0i} & if\ D_{i}=0
    \end{cases}\end{aligned}$$

Two Key points

-   Point 1: Fundamental problem of program evaluation

    -   We can observe $(Y_{i},D_{i})$, but never observe $Y_{0i}$ and
        $Y_{1i}$ **simultaneously**.

    -   **Counterfactual** outcome.

-   Point 2: Stable Unit Treatment Value Assumption (SUTVA)

    -   Treatment effect for a person does **not depend on the treatment
        status of other people.**

    -   Rules out externality / general equilibrium effects.

        -   Ex: If everyone takes the job training, the equilibrium wage
            would change, which affects the individual outcome.

Parameters of Interest

-   Define the individual treatment effect $Y_{1i}-Y_{0i}$

    -   Key: allowing for heterogenous effects across people

-   Individual treatment effect cannot be identified due to the
    fundamental problem.

-   Instead, we focus on the average effects

    -   Average treatment effect: $ATE=E[Y_{1i}-Y_{0i}]$

    -   Average treatment effect on treated:
        $ATT=E[Y_{1i}-Y_{0i}|D_{i}=1]$

    -   Average treatment effect on untreated:
        $ATT=E[Y_{1i}-Y_{0i}|D_{i}=0]$

    -   Average treatment effect conditional on covariates $X_{i}$:
        $ATE(x)=E[Y_{1i}-Y_{0i}|D_{i}=1,X_{i}=x]$

Relation to Regression Analysis

-   Assume that

    1.  linear (parametric) structure in $Y_{0i}$, and

    2.  constant (homogenous) treatment effect, $$\begin{aligned}
        Y_{0i} & =\beta_{0}+\epsilon_{i}\\
        Y_{1i}-Y_{0i} & =\beta_{1}\end{aligned}$$

-   You will have $$Y_{i}=\beta_{0}+\beta_{1}D_{i}+\epsilon_{i}$$

-   Program evaluation framework is nonparametric in nature.

    -   Though, in practice, estimation of treatment effect relies on a
        parametric specification.

Selection Bias

-   Consider the comparison of average outcomes between treatment and
    control group

-   Does this tell you average treatment effect? No in general!
    $$\begin{aligned}
    \underbrace{E[Y_{i}|D_{i}=1]-E[Y_{i}|D_{i}=0]}_{simple\ comparison}= & E[Y_{1i}|D_{i}=1]-E[Y_{0i}|D_{i}=0]\\
    = & \underbrace{E[Y_{1i}-Y_{0i}|D_{i}=1]}_{ATT}\\
     & +\underbrace{E[Y_{0i}|D_{i}=1]-E[Y_{0i}|D_{i}=0]}_{selection\ bias}\end{aligned}$$

-   The bias term $E[Y_{0i}|D_{i}=1]-E[Y_{0i}|D_{i}=0]$

    -   not zero in general: Those who are taking the job training
        **would do a good job even without job training**

    -   Cannot observe $E[Y_{0i}|D_{i}=1]$: the outcome of people in
        treatment group when they are NOT treated (counterfactual).

Solutions

-   The core of program evaluation is how to identify (estimate) the
    treatment effect parameters.

-   Randomized Control Trial (A/B test):

    -   Assign treatment $D_{i}$ randomly

-   Matching (regression):

    -   Using observed characteristics of individuals to control for
        selection bias

-   Instrumental variable

    -   Use the variable that affects treatment status but is not
        correlated to the outcome

-   Difference-in-differences

    -   Use the panel data to control for individual heterogeneity by
        fixed effects.

-   Regression Discontinuity Design

    -   Exploit the randomness around the thresholds.

-   Others: Bound approach, synthetic control method, regression kink
    design, etc..

RCT
===

What is RCT ?

-   RCT: Randomized Controlled Trial

-   Measure the effect of "treatment" by

    1.  randomly assigning treatment to a particular group (treatment
        group)

    2.  measure outcomes of subjects in both treatment and "control"
        group.

    3.  the difference of outcomes between these two groups is
        "treatment" effect.

-   Starts with clinical trial: measure the effects of medicine.

Example from Development Economics

-   Esther Duflo "Social experiments to fight poverty"

    -   <https://www.ted.com/talks/esther_duflo_social_experiments_to_fight_poverty?language=en>

Framework

-   Key assumption: Treatment $D_{i}$ is independent with potential
    outcomes $(Y_{0i},Y_{1i})$ $$D_{i}\perp(Y_{0i},Y_{1i})$$

-   Under this assumption, $$\begin{aligned}
    E[Y_{1i}|D_{i} & =1]=E[Y_{1i}|D_{i}=0]=E[Y_{1i}]\\
    E[Y_{0i}|D_{i} & =1]=E[Y_{0i}|D_{i}=0]=E[Y_{0i}]\end{aligned}$$

-   The sample selection does not exist! Thus, $$\begin{aligned}
    \underbrace{E[Y_{i}|D_{i}=1]-E[Y_{i}|D_{i}=0]}_{simple\ comparison}= & \underbrace{E[Y_{1i}-Y_{0i}|D_{i}=1]}_{ATT}\end{aligned}$$

-   Difference of the sample average is consistent estimator for the ATT
    $$\frac{\frac{1}{N}\sum_{i=1}^{N}Y_{i}\cdot\mathbf{1}\{D_{i}=1\}}{\frac{1}{N}\sum_{i=1}^{N}\mathbf{1}\{D_{i}=1\}}-\frac{\frac{1}{N}\sum_{i=1}^{N}Y_{i}\cdot\mathbf{1}\{D_{i}=0\}}{\frac{1}{N}\sum_{i=1}^{N}\mathbf{1}\{D_{i}=0\}}$$

Example: RAND Health Insurance Experiment (HIE)

-   Taken from Angrist and Pischke (2014, Sec 1.1)

-   1974-1982, 3958 people, age 14-61

-   Randomly assigned to one of 14 insurance plans.

    -   No insurance premium

    -   Different provisions related to cost sharing

-   4 categories

    -   Free

    -   Co-insurance: Pay 25-50% of costs

    -   Deductible: Pay 95% of costs, up to \$150 per person (\$450 per
        family)

    -   Catastrophic coverage: 95% of health costs. No upper limit.
        Approximate "no insurance"

First step: Balance Check

![image](figure_table/MMtbl13.pdf)

-   Differences in demographic characteristics & baseline health are
    statistically insignificant

-   Assignment of health insurance plans is indeed random!

Results of RAND HIE

![image](figure_table/MMtbl14.pdf)

-   HI increases health spending (Panel A)

-   But, HI has no statistically significant effect on health outcomes

Matching
========

Matching

-   Idea: Compare **individuals with the same characteristics $X$**
    across treatment and control groups

-   Let $X_{i}$ denote the observed characteristics: age, income,
    education, race, etc\...

-   Assumption 1: $$D_{i}\perp(Y_{0i},Y_{1i})\left|X_{i}\right.$$

    -   Conditional on $X_{i}$, no selection bias.

    -   Selection on observables assumption / ignorability

-   Assumption 2: Overlap assumption
    $$P(D_{i}=1|X_{i}=x)\in(0,1)\ \forall x$$

    -   Given $x$, we should be able to observe people from both control
        and treatment group.

Identification

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

ATT and ATE

-   ATT is given by $$\begin{aligned}
    ATT & =E[Y_{1i}-Y_{0i}|D_{i}=1]\\
     & =\int E[Y_{1i}-Y_{0i}|D_{i}=1,X_{i}=x]f_{X_{i}}(x|D_{i}=1)dx\\
     & =E[Y_{i}|D_{i}=1]-\int\left(E[Y_{i}|D_{i}=0,X_{i}=x]\right)f_{X_{i}}(x|D_{i}=1)\end{aligned}$$

-   ATE is $$\begin{aligned}
    ATE= & E[Y_{1i}-Y_{0i}]\\
    = & \int E[Y_{1i}-Y_{0i}|X_{i}=x]f_{X_{i}}(x)dx\\
    = & \int E[Y_{i}|D_{i}=1,X_{i}=x]f_{X_{i}}(x)dx\\
    = & +\int E[Y_{i}|D_{i}=0,X_{i}=x]f_{X_{i}}(x)dx\end{aligned}$$

Estimation Methods

-   We need to estimate $E[Y_{i}|D_{i}=1,X_{i}=x]$ and
    $E[Y_{i}|D_{i}=0,X_{i}=x]$

-   Several ways to implement the above idea

-   Regression: Nonparametric and Parametric

-   Nearest neighborhood matching

-   Propensity Score Matching: Skipped

Regression, or Analogue Approach

-   Let $\hat{\mu}_{k}(x)$ be an estimator of
    $\mu_{k}(x)=E[Y_{i}|D_{i}=k,X_{i}=x]$ for $k\in\{0,1\}$

-   The analog estimators are $$\begin{aligned}
    \hat{ATE} & =\frac{1}{N}\sum_{i=1}^{N}\hat{\mu}_{1}(X_{i})-\hat{\mu}_{0}(X_{i})\\
    \hat{ATT} & =\frac{N^{-1}\sum_{i=1}^{N}D_{i}(Y_{i}-\hat{\mu}_{0}(X_{i}))}{N^{-1}\sum_{i=1}^{N}D_{i}}\end{aligned}$$

-   How to estimate $\mu_{k}(x)=E[Y_{i}|D_{i}=k,X_{i}=x]$ ?

Nonparametric Estimation

-   Suppose that $X_{i}\in\{x_{1},\cdots,x_{K}\}$ is discrete with small
    $K$

    -   Ex: two demographic characteristics (male/female,
        white/non-white). $K=4$

-   Then, a nonparametric binning estimator is
    $$\hat{\mu}_{k}(x)=\frac{\sum_{i=1}^{N}\mathbf{1}\{D_{i}=k,X_{i}=x\}Y_{i}}{\sum_{i=1}^{N}\mathbf{1}\{D_{i}=k,X_{i}=x\}}$$

-   Here, I do not put any parametric assumption on
    $\mu_{k}(x)=E[Y_{i}|D_{i}=k,X_{i}=x]$.

-   Issue: Poor performance if $K$ is large due to many covariates

    -   **curse of dimensionality**

-   If $X$ can take continuum value, you can use kernel regression.

Parametric Estimation, or going back to linear regression

-   If you put parametric assumption such as $$\begin{aligned}
    E[Y_{i}|D_{i}=0,X_{i}=x] & =\beta'x_{i}\\
    E[Y_{i}|D_{i}=1,X_{i}=x] & =\beta'x_{i}+\tau_{0}\end{aligned}$$
    then, you will have a model
    $$y_{i}=\beta'x_{i}+\tau D_{i}+\epsilon_{i}$$

-   You can think the matching estimator as controlling for omitted
    variable bias by adding (many) covariates (control variables)
    $x_{i}$.

-   This is one reason why matching estimator may not be preferred in
    empirical research.

    -   Remember: Controlling for those covariates is of course
        important. This can be combined with other empirical strategies
        (IV, DID, etc).

$M-$Nearest Neighborhood Matching

-   Fine the counterpart in other group that is close to me.

-   Define $\hat{y}_{i}(0)$ and $\hat{y}_{i}(1)$ be the estimator for
    (hypothetical) outcomes when treated and not treated.
    $$\hat{y}_{i}(0)=\begin{cases}
    y_{i} & if\ D_{i}=0\\
    \frac{1}{M}\sum_{j\in L_{M}(i)}y_{j} & if\ D_{i}=1
    \end{cases}$$

-   $L_{M}(i)$ is the set of $M$ individuals in the opposite group who
    are "close" to individual $i$

    -   Closeness is defined as the distance between $X_{i}$ and $X_{j}$

    -   There are several ways to define the distance. For example,
        $$dist(X_{i},X_{j})=||X_{i}-X_{j}||^{2}$$

-   You need to choose (1) $M$ and (2) the measure of distance to
    implement this.

-   R has several packages for this.

Going Forward
=============

Other Approaches

-   Instrumental Variable: same idea.

    -   IV estimation in program evaluation framework involves with the
        argument of local average treatment effect (LATE), which is
        beyond the scope of this course.

-   Difference in differences (week 14)

-   Regression discontinuity design (week 15)
