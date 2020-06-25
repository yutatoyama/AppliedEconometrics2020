---
title: 'Program Evaluation (Causal Inference) 1: Introduction and Randomized Control Trial'
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

## Introduction

-   Program Evaluation, or Causal Inference
    -   Estimation of "treatment effect" of some intervention (typically
        binary)
    -   Example:
        -   effects of job training on wage
        -   effects of advertisement on purchase behavior
        -   effects of distributing mosquito net on children's school
            attendance
\bigskip
-   Difficulty: treatment is **endogenous decision**
    -   selection bias, omitted variable bias.
    -   especially in observational data (in comparison with
        experimental data)

## Overview

-   Introduce Rubin's causal model (potential outcome framework)
    -   Generalization of the linear regression model: Nonparametric
\bigskip
-   Solutions to the selection bias
    1.  Randomized control trial 
    2.  Matching 
    3.  Instrumental Variable Estimation 
    4.  Difference-in-differences 
    5.  Regression Discontinuity Design
    6.  Instrumental Variable
    -   Note: IV estimation in program evaluation framework involves with the
        argument of local average treatment effect (LATE), which is
        beyond the scope of this course.


## Reference

-   Angrist and Pischke:
    -   Mostly harmless econometrics : advanced undergraduate to
        graduate students
    -   Mastering Metrics: good for undergraduate students after taking
        econometrics course.
\bigskip
-   Ito: Data Bunseki no Chikara (in Japanese)

# Program Evaluation    

## Framework

-   $Y_{i}$: observed outcome for person $i$
\bigskip
-   $D_{i}$: treatment status $$D_{i}=\begin{cases}
    1 & treated\ (treatment\ group)\\
    0 & not\ treated\ (control\ group)
    \end{cases}$$
\bigskip
-   Define *potential outcomes*
    -   $Y_{1i}$: outcome for $i$ when she is treated (treatment group)
    -   $Y_{0i}$: outcome for $i$ when she is not treated (control
        group)
\bigskip
-   With this, we can write $$\begin{aligned}
    Y_{i} & =D_{i}Y_{1i}+(1-D_{i})Y_{0i}\\
     & =\begin{cases}
    Y_{1i} & if\ D_{i}=1\\
    Y_{0i} & if\ D_{i}=0
    \end{cases}\end{aligned}$$

## Key Points

-   Point 1: Fundamental problem of program evaluation
    -   We can observe $(Y_{i},D_{i})$, but never observe $Y_{0i}$ and
        $Y_{1i}$ **simultaneously**.
    -   **Counterfactual** outcome.
\bigskip
-   Point 2: Stable Unit Treatment Value Assumption (SUTVA)
    -   Treatment effect for a person does **not depend on the treatment
        status of other people.**
    -   Rules out externality / general equilibrium effects.
        -   Ex: If everyone takes the job training, the equilibrium wage
            would change, which affects the individual outcome.

## Parameters of Interest

-   Define the individual treatment effect $Y_{1i}-Y_{0i}$
    -   Key: allowing for heterogenous effects across people
\bigskip
-   Individual treatment effect cannot be identified due to the
    fundamental problem.
\bigskip
-   Instead, we focus on the average effects
    -   Average treatment effect: $ATE=E[Y_{1i}-Y_{0i}]$
    -   Average treatment effect on treated:
        $ATT=E[Y_{1i}-Y_{0i}|D_{i}=1]$
    -   Average treatment effect on untreated:
        $ATT=E[Y_{1i}-Y_{0i}|D_{i}=0]$
    -   Average treatment effect conditional on covariates $X_{i}$:
        $ATE(x)=E[Y_{1i}-Y_{0i}|D_{i}=1,X_{i}=x]$

## Relation to Regression Analysis

-   Assume that
    1.  linear (parametric) structure in $Y_{0i}$, and
    2.  constant (homogenous) treatment effect, $$\begin{aligned}
        Y_{0i} & =\beta_{0}+\epsilon_{i}\\
        Y_{1i}-Y_{0i} & =\beta_{1}\end{aligned}$$
\bigskip
-   You will have $$Y_{i}=\beta_{0}+\beta_{1}D_{i}+\epsilon_{i}$$
\bigskip
-   Program evaluation framework is nonparametric in nature.
    -   Though, in practice, estimation of treatment effect relies on a
        parametric specification.

## Selection Bias

-   Compare average outcomes between treatment and control group
\bigskip
-   Does this tell you average treatment effect? No in general!
    $$\begin{aligned}
    \underbrace{E[Y_{i}|D_{i}=1]-E[Y_{i}|D_{i}=0]}_{simple\ comparison}= & E[Y_{1i}|D_{i}=1]-E[Y_{0i}|D_{i}=0]\\
    = & \underbrace{E[Y_{1i}-Y_{0i}|D_{i}=1]}_{ATT}\\
     & +\underbrace{E[Y_{0i}|D_{i}=1]-E[Y_{0i}|D_{i}=0]}_{selection\ bias}\end{aligned}$$

---

-   The bias term $E[Y_{0i}|D_{i}=1]-E[Y_{0i}|D_{i}=0]$
    -   not zero in general: Those who are taking the job training
        **would do a good job even without job training**
    -   Cannot observe $E[Y_{0i}|D_{i}=1]$: the outcome of people in
        treatment group when they are NOT treated (counterfactual).

## Solutions

-   Randomized Control Trial (A/B test):
    -   Assign treatment $D_{i}$ randomly
\bigskip
-   Matching (regression):
    -   Using observed characteristics of individuals to control for
        selection bias
\bigskip
-   Instrumental variable 
    -   Use the variable that affects treatment status but is not
        correlated to the outcome
\bigskip
-   Difference-in-differences
    -   Use the panel data to control for individual heterogeneity by
        fixed effects.
\bigskip
-   Regression Discontinuity Design
    -   Exploit the randomness around the thresholds.
\bigskip
-   Others: Bound approach, synthetic control method, regression kink
    design, etc..

# RCT Framework

## What is RCT ?

-   RCT: Randomized Controlled Trial
\bigskip
-   Measure the effect of "treatment" by
    1.  randomly assigning treatment to a particular group (treatment
        group)
    2.  measure outcomes of subjects in both treatment and "control"
        group.
    3.  the difference of outcomes between these two groups is
        "treatment" effect.
\bigskip
-   Starts with clinical trial: measure the effects of medicine.

## Examples

-   Development economics: Esther Duflo "Social experiments to fight poverty"
    -   <https://www.ted.com/talks/esther_duflo_social_experiments_to_fight_poverty?language=en>
\bigskip 
-   Health economics: Amy Finkelstein "Randomized evaluations & the power of evidence | Amy Finkelstein"
    -   <https://www.youtube.com/watch?v=N8rD844McrA>
\bigskip

## Framework and Identification

-   Key assumption: Treatment $D_{i}$ is independent with potential
    outcomes $(Y_{0i},Y_{1i})$ $$D_{i}\perp(Y_{0i},Y_{1i})$$
\bigskip
-   Under this assumption, $$\begin{aligned}
    E[Y_{1i}|D_{i} & =1]=E[Y_{1i}|D_{i}=0]=E[Y_{1i}]\\
    E[Y_{0i}|D_{i} & =1]=E[Y_{0i}|D_{i}=0]=E[Y_{0i}]\end{aligned}$$
\bigskip
-   The sample selection does not exist! Thus, $$\begin{aligned}
    \underbrace{E[Y_{i}|D_{i}=1]-E[Y_{i}|D_{i}=0]}_{simple\ comparison}= & \underbrace{E[Y_{1i}-Y_{0i}|D_{i}=1]}_{ATT}\end{aligned}$$


## Estimation

-   Difference of the sample average is consistent estimator for the ATT
    $$\frac{\frac{1}{N}\sum_{i=1}^{N}Y_{i}\cdot\mathbf{1}\{D_{i}=1\}}{\frac{1}{N}\sum_{i=1}^{N}\mathbf{1}\{D_{i}=1\}}-\frac{\frac{1}{N}\sum_{i=1}^{N}Y_{i}\cdot\mathbf{1}\{D_{i}=0\}}{\frac{1}{N}\sum_{i=1}^{N}\mathbf{1}\{D_{i}=0\}}$$
\bigskip
- You can run a linear regression of $Y$ on $D$ along with other covariates $X_i$
$$ Y_i = \beta_0 + \beta_1 D_i + \beta' X_i + \epsilon_i$$

# Health Insurance Experiment

## Example: RAND Health Insurance Experiment (HIE)

-   Taken from Angrist and Pischke (2014, Sec 1.1)
\bigskip
-   1974-1982, 3958 people, age 14-61
\bigskip
-   Randomly assigned to one of 14 insurance plans.
    -   No insurance premium
    -   Different provisions related to cost sharing
\bigskip
-   4 categories
    -   Free
    -   Co-insurance: Pay 25-50% of costs
    -   Deductible: Pay 95% of costs, up to \$150 per person (\$450 per
        family)
    -   Catastrophic coverage: 95% of health costs. No upper limit.
        Approximate "no insurance"

## First step: Balance Check

![image](figure_table/MMtbl13.pdf)

-   Differences in demographic characteristics & baseline health are
    statistically insignificant
-   Assignment of health insurance plans is indeed random!

## Results of RAND HIE

![image](figure_table/MMtbl14.pdf)

-   HI increases health spending (Panel A)
-   But, HI has no statistically significant effect on health outcomes

