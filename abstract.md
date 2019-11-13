---
title: 'Exploring and understanding the individual experience from longitudinal data, or "How to make better spaghetti (plots)"'
date: '2019-11-14'
---

This talk discusses two challenges of working with longitudinal (panel) data:

1) Visualising the data, and  

2) Understanding the model. 

Visualising longitudinal data is challenging as you often get a "spaghetti plot", where a line is drawn for each individual. When overlaid in one plot, it can have the appearance of a bowl of spaghetti. With even a small number of subjects, these plots are too overloaded to be read easily. For similar reasons, it is difficult to relate the model predictions back to the individual and keep the context of what the model means for the individual.

For both visualisation, and modelling, it is challenging to capture interesting or unusual individuals, which are often lost in the noise. Better tools, and a more diverse set of grammar and verbs are needed to visualise and understand longitudinal data and models, to capture the individual experiences.  

In this talk, I introduce the R package, **brolgar** (BRowse over Longitudinal data Graphically and Analytically in R), which provides a realisation of new concepts, verbs, and colour palettes to identify and summarise interesting individual patterns in longitudinal data. This package extends upon ggplot2 with custom facets, and the new tidyverts time series packages to efficiently explore longitudinal data.

