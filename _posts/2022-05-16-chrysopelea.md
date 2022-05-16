---
title: "Chrysopelea - A Python GPS Analysis Tool"
share: false
related: false
last_modified_at: 2022-05-16T19:30:00
categories:
  - Repo
tags:
  - coding
  - github
---

[Chrysopelea](https://2021.spaceappschallenge.org/challenges/statements/identifying-risk-with-science-communities/teams/team-carso/project) is a simple script for applying LSE to GPS data developed for the final project of the 2021 ICTP diploma/PhD Space Geodesy course.
The procedure implemented is a simplified version of the one described in\
Barzaghi, R., Borghi, A. Theory of second order stationary random processes applied to GPS coordinate time-series. *GPS Solut* **22**, 86 (2018). https://doi.org/10.1007/s10291-018-0748-4

## The implemented procedure 
 Using the 'colour noise' stochastic model, each component of the data has been processed with the following scheme:
1.  In a pre-processing phase the data are interpolated to remove possible data gap;
2.  Least squares are applied using the a white noise covariance matrix and the following deterministic model:\
    x(t)=A0+Av*t+ΣA1(T)*sin(2πt/T)+ΣA2(T)*sin(2πt/T)+ΣAco(Tco)*H(t-Tco)\
    with *T* periodicity within the signal, *T*<sub>*co*</sub> time of known discontinuities in the signals (due to coseismic displacements, instrumentation failures and changes, etc.).
3. The periodicities of the signals are derived from a periodogram of the residuals: initially, the data are fitted with a simplified linear regression model and the periodogram of the residual of the least squares fitting is computed, to find out the most significant periodicities in the time series. These periodicity are introduced one at a time until the least squares fitting doesn't improve.\
    The data are initially assumed uncorrelated using a white noise stochastic model.
4.  The least squares residuals *ϵ*(*t*) are computed and checked for the stationary hypothesis using the KPSS test;
5.  The empirical Auto-Covariance Function *α*(*τ*) of the residuals is computed and it is used to define a "colour noise" stochastic model: to avoid numerical problems, due to the inversion of the covariance matrix of the data, when estimating the parameters, the auto-covariance function *α*(*τ*) is fitted using a positive definite function.
6.  Least squares are applied using the updated stochastic model to evaluate the parameters **x̂**.
7.  The covariance matrix *C*<sub>**x̂**x̂</sub> of the parameters is computed.
The "white noise" stochastic model is computed in the same way but skipping steps 4-6.
