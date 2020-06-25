---
author:
- Keigo Makino
date: 'Last updated: '
title: '"The Effect of Patient Cost Sharing on Utilization, Health, and
  Risk Protection" by Hitoshi Shigeoka 2014 AER'
---

Policy Issue: Medical Expenditure

-   Medical expenditures are rising.

    -   due to an aging population and coverage expansion

    -   acute fiscal challenge to governments!

-   Current expenditure on health (to GDP) in 2018 according to OECD
    Health Statistics 2019

    -   U.S.A. (16.9%), Switzerland (12.2%), Germany (11.2%), France
        (11.2%), Sweden (11.0%), Japan (10.9%)\...

-   One main strategy is higher patient cost sharing, that is, requiring
    patients to pay a larger share of the cost of care.

-   Question: how does patient cost sharing affect

    -   utilization (demand elasticity)?

    -   health?

    -   risk protection (out-of-pocket expenditures)?

Background and Cross-sectional Data

-   All Japanese citizens are mandatorily covered by health insurance.

-   Use a sharp reduction in cost sharing for patients aged over 70 in
    Japan.

-   The sources are the Patient Survey and the Comprehensive Survey of
    Living Conditions (CSLC). 1984-2008.

-   Advantages

    -   There are no confounding factors at age 70. We can isolate the
        effect of patient cost sharing.

    -   Medical providers do not have incentive to differentiate prices
        by the patients' insurance type.

    -   We can separate inpatient and outpatient.

Cost Sharing and Out-of-Pocket Medical Expenditure

-   In sum, the proportion is 30% for \<69 and 10% for 70$\leq$.

-   Out-of-pocket medical expenditure for impatient admissions can reach
    27% for a 69-year-old.

-   However, for 70, it would be reduced to 8.6%.

-   We need to take the stop-loss into account.

Identification Strategy

-   Standard RD designs.

-   Basic estimation equation for the CSLC is
    $$Y_{iat}=f(a)+\beta Post70_{iat}+X_{iat}^{\prime}\gamma+\varepsilon_{iat}.$$

    -   $Y_{iat}$: a measure of morbidity or out-of-pocket medical
        expenditure

    -   $f(a)$: a smooth function of age.

    -   $X_{iat}$: a set of individual covariates

    -   $Post70_{iat}$: $=0$ if individual $i$ is over 70.

-   Patient Survey/mortality data represents individuals who are present
    in the medical institutions/deceased.

-   As in Card, Dobkin, and Maestas (2004), basic estimation equation
    for the Patient Survey and mortality data is
    $$\log(Y_{at})=f(a)+\beta Post70_{at}+\mu_{at}.$$

-   We dealt with heaping, seasonality, and the catch-up effect.

Results: Outpatient Visits

-   Left: 10.3% increase in overall visits. The implied elasticity is
    $-0.18$.

-   Right: Sharp drop in the duration from the last visit by one day.

-   The effect is heterogeneous across institutions, genders, and
    diagnoses.

Results: Inpatient Admissions

-   Left: 8.2% increase in overall admissions. The implied elasticity is
    $-0.16$.

-   Right: Surge (increase by 12.0%) in admissions with surgery.

-   From robustness checks, the implied elasticity is around $-0.2$.

Benefits: Health Outcomes

-   We cannot find significant discontinuity in mortality.

-   This result is expected because health is stock (Grossman 1972).

-   There is no discontinuity in morbidity (self-reported health).

-   The available health measures here are limited, so we would
    underestimate the benefit.

![image](ShigeokaFig6.png)

Benefits: Risk Reduction

-   Another benefit is a lower risk of unexpected out-of-pocket medical
    spending.

-   We use a nonparametric estimator for quantile treatment effects.

-   Patients at the right tail of the distribution in particular are
    substantially benefited.

Discussion

-   Price Elasticities

    -   We cannot distinguish own- from cross-price effects.

    -   However, for some diagnosis groups, cross-price effects should
        be nearly zero.

    -   The overall effect of the price change for the groups is an
        approximately 10 percent increase in visits.

-   Cost-Benefit Analysis

    -   Imposing many assumptions, we speculate that the welfare gain of
        risk protection from lower patient cost sharing is comparable to
        the total social cost.

    -   We cannot include welfare gains from health improvements.
