# general introduction

## This is where I've come from

> I want to talk a bit about where I've started from, because I think it might be useful to understand my perspective, and why I'm interested in doing these things.

- Psychology. I wanted to be a child psychologist, but I discovered that I did not have the mental fortitude for child psychology.
- My honours thesis was in psychophysics (aka vision science).  I studied monocular occlusion and 3D perception of edges (can I get any of my old honours files from somewhere?)
- In my honours year I discovered an interest in public health and statistics. This quote stands out:

> You could get every psychologist in the world to deliver gold standard smoking cessation group therapy, and the rate of smoking would still increase. You need to change policy to make change. And to make effective policy changes, you need to have good data, and do good statistics.

## PhD statistics

- I started a PhD in statistics at QUT, under (now distinguished) Professor Kerrie Mengersen.
- Looking at people's health over time.
- There were several things that I noticed:
  - There were equations, but not as many clear-cut, black and white answers
  - There was a whole lot of exploring the data before and after analysis, and not as much of "input in, output out" that I thought there might be.
- This contrasted my time in psych.
    - We spend so much time on the design of the data, that we tend to know the analysis that we want to do, there is less emphasis (and training) on exploring your data
- Despite there being a lot of research in new statistical methods:
  - spatial statistics
  - better imputation
  - better prediction
  - better inference
- There was not much research on how we explore our methods, and our behaviour.

- An analogy:
  > We focus on building a bridge across a river, but we don't focus on how we build the bridge, and the tools that we use to build it.

- I became very interested in how we explore our data - exploratory data analysis.
    
## What is EDA?

- Explore the definition from Tukey + Mosteller, Cleveland.
- Explore where this fits into the analysis process

# These are some of my R packages

## visdat (2 minutes)

## naniar (2 minutes)

- brief description of this as well

# Some overall themes of the talk

- EDA is really important
- But sometimes seen as an art
- Not so much emphasis on its study
- We need to think more carefully as a culture about the importance / role of EDA

## So let's talk about another type of exploratory data analysis: longitudinal data

# What is longitudinal data?

- Show the definition
- Show the data

# All of Australia, and more

- Show the data visualisation
- The problem is:
  - Lots of overplotting.
  - We get an overall sense of the data
  - We don't see the individuals
  - We could look at 153 individual plots, but this doesn't help.

# Does transparency + a model help?

- This helps reduce the overplotting
- We only get the overall average. We dont get the rest of the information

# This is still useful

- We get information on what the average is, and how that behaves
- But we don't get the full story
- So, it depends on your need. If you have a designed experiment, where you stated that you would run some analysis, then you are doing this.
- ... But even then, wouldn't you rather _explore_ the data?
- Who fits the models well / worst / best?

# But we forget about the **individuals**

- The model might make some good overall predictions
- But it can be really _ill suited_ for some individual
- Exploring this is somewhat clumsy - we need another way to explore

# How do we get the most out of this plot?

- Problem #1: How do I look at **some** of the data?
- Problem #2: How do I find **interesting** observations?
- Problem #3: How do I **understand** my statistical model

# Introducing `brolgar`: brolgar.njtierney.com

- How does brolgar help with these problems?

# Defining longitudinal data

- Thinking of longitudinal data as a time series
- Defining what a `tsibble` is, and why that is so useful.

# Helpful techniques to look at longitudinal data

## Look at only a subsample: 

- What does this allow us to do?
  - This is what that behaviour / action looks like.
  - This is what it tells us

- What are some of the barriers to doing this?
  - You need to sample a random group of individuals
  - `sample_n()` to sample n rows
  - `sample_n_keys()` to sample ... **keys**
    - So, adding the metadata of this kind of information is key (har-har-har)

## Look at many subsamples

- What does this allow us to do?
  - This means we can see more of the raw data. It expands the number of raw data plots that we can look at.
  - The "recipe" for this is:
    - Decide the number of subsample plots
    - Decide the number of lines per plot
    - Allocate each group to a number, and repeat that process for each group

- abstract it away with `facet_sample()`

- We can look at all the subsamples, and then play with how we **arrange** that information.
  - "recipe" is

- `facet_strata()`: See all individuals
- arrange these subsamples to have some meaningful ordering:
  - `facet_strata(along = -year)`: see all individuals **along** some variable
  - (under the hood these are powered by `facet_strata()` & `facet_sample()`, so you can still get at the data and do more manipulations

- This helps us look at some of the data
- Other ways to look at a lot of the data?
  - heatmaps?
  - clustering?
  - ?

# Problem #2: How do I find **interesting** observations?

- **Define** interesting?
- The **principle** seems to be something like: 

> Summarise each time series
> Explore these summaries by finding the "most, least, best, worst" of these summaries

- Identify one feature per **key** (you can think of a feature as a statistic - which is roughly defined as any time you reduce several numbers down to one or so numbers)
- `features` are similar to `summarise`, but **aware of data structure** 
- `feat_five_num` is  the five number summary (from Tukey)

- the process:
  - Summarise down to one observation
  - Identify important features
  - Decide how to filter 
  - Join this feature back to the data

As an example of "the process" (needs a name? Sweeping? high dimensional sweeping/cleaning/wrangling? Whisking, scour, glide):

  - Countries with smallest and largest max height
  - summarise down to one observation
  - Identify important features (maximum)
  - Decide how to filter (take the highest maximum)
  - (equally you coudl take the mean closest to the mean of means...)
  - Join summaries back to data
  
(can I relate this back to some equation or algorithm?)

- What are some examples of other features?
  - What is the range of the data? `feat_ranges`
  - Does my data only increase or decrease? `feat_monotonic`
  - What is the spread of my data? `feat_spread`
  - and more in `feasts` 

- What do we learn from doing this process? I guess we get an understanding for
what is in the data?

- Let's fit a simple mixed effects model to the data
    - now let's go through these same principles:
      - Sample the fits
      - Many samples of the fits
      - Explore the residuals
      - Find the best, worst, middle of the ground residuals
      - Which are most similar to which stats?
      - follow the "gliding" process again.
  

      - "who is similar to me?"
      - "who is the most average?"
      - "who is the most extreme?"
      - "Who is the most different to me?"

- `keys_near()`
  - which keys are **nearest** to the some statistics


- A brief digression into `palap`?
  - (This would be quite a bit of a sidestep, but could be useful)
  - Let's briefly talk about colour palettes:
    1. **Qualitative**: categorical variables
    2. **Sequential**: low to high numeric values
    3. **Diverging**: negative to positive values

A fourth colour palette is needed, to cover cases where things diverge, but maintain some constant value/meaning as they get further from the center point. A "symmetric" colour palette:

4\. **Symmetric**: Diverging values with equivalent meaning as they get further from the diverging point.

  - Symmetric colour palettes can be used in specific cases when 
  you need values tha are above and below the middle point that have different values, but similar meaning. For example, the first and third quantiles. You can think of symmetric colour palettes as a combination of sequential and diverging colour palettes. The goal of palap is to provide "symmetric" colour palettes. Broadly speaking, there are three categories of colour palette:

# Take homes



# Thanks
# Resources
# Learning more



This talk discusses two challenges of working with longitudinal (panel) data:

1) Visualising the data, and  

2) Understanding the model. 

Visualising longitudinal data is challenging as you often get a "spaghetti plot", where a line is drawn for each individual. When overlaid in one plot, it can have the appearance of a bowl of spaghetti. With even a small number of subjects, these plots are too overloaded to be read easily. For similar reasons, it is difficult to relate the model predictions back to the individual and keep the context of what the model means for the individual.

For both visualisation, and modelling, it is challenging to capture interesting or unusual individuals, which are often lost in the noise. Better tools, and a more diverse set of grammar and verbs are needed to visualise and understand longitudinal data and models, to capture the individual experiences.  

In this talk, I introduce the R package, **brolgar** (BRowse over Longitudinal data Graphically and Analytically in R), which provides a realisation of new concepts, verbs, and colour palettes to identify and summarise interesting individual patterns in longitudinal data. This package extends upon ggplot2 with custom facets, and the new tidyverts time series packages to efficiently explore longitudinal data.

