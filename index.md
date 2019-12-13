---
layout: default
---

{% include youtubePlayer.html id="4EU7vvSvV-0" %}

* * *

# Overview

## Background and motivation

As the world's largest economy by nominal GDP and net wealth, United States has been famous for its prosperous retail industry over decades. Many retailers in the United States have earned their reputations all over the world, such as Walmart, Amazon, etc. Among all the job positions, retail sales managers play a key role in the company, since such competitative industry has been putting consecutively high expectations for them to adjust for rapid social innovation and keep the company's retail sales moving in the right direction. As sales managers, they are likely to be interested in not only getting prepared for the future sales, but also balancing the online and offline sales, as e-commerce concept is getting more and more popular in recent years. Many questions arise from them everyday: What are the factors that affect offline sales? Can we predict future sales? How do nationwide economic events affect the whole retail industry? What's new in this e-commerce era?

<img src="images/sales_cartoon.png" alt="sales manager cartoon" class = "ct" width = "80%">

These hard problems arose from retail sales managers call for a more systematic and scientific approach to model different sales types with potential influential factors. Unfortunately, there has been a gap between the need of sales managers and retail sales data for a long time. To cover such gap, we conducted this data science project using retail sales data, trying to provide comprehensive advice for retail sales managers.

## Objective

Through this project, we sought to answer four primary questions for retail sales managers:

* What are the factors that affect offline sales?

* Can we integrate features with advanced statistical methods to predict retail sales in the near future?

* How do nationwide economic events affect the whole retail industry?

* What are different patterns of e-commerce compared with offline sales?

## Data

Dataset from multiple sources have been collected and combined for use in our analysis, including

* [Walmart retail sales and store features data from Feb 5, 2010 to Oct 26, 2012](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting/data)

* [US total retail sales and e-commerce retail sales from 4th quarter 1999 to 3rd quarter 2019](https://www.census.gov/retail/index.html)

* [US Gross Domestic Product (GDP) data](https://fred.stlouisfed.org/series/GDP)

## Approach

The questions we sought to answer suggest the analysis being separated into two subprojects: one (first two questions) focus on Walmart retail sales and features, and the other one (the last two questions) focus on the general retail sales pattern in the United States. These two subprojects together help not only answering questions with respect to specific features that retail sales managers may be interested in (for example, would reducing temperature increase retail sales?), but also describing some general patterns of online and offline sales, serving as guidance for all retail sales managers in our approaching e-commerce world.

(The following two paragraphs are a little bit technical, skip if you want) In the first subproject, we started by exploring feature correlations and temporal distributions of retail sales individually, then exploring their joint relationship. Some advanced statistical methods are then applied, such as stepwise regression and generalized estimating equations, to extract key factors that have significant influences on sales outcome. The features collected, together with statistical knowledge of tree-based methods, informed the creation of three advanced tree-based predictive algorithms.

In the second subproject, we modelled the temporal trend differences between online and offline sales using splines, and quantified the effect of financial crisis in 2008 by testing the significance of spline coefficients. Their respective seasonal patterns were further analyzed through advanced statistical techniques, such as ANOVA test.

# Analysis

## Walmart retail sales inference and prediction

### Data visualization

Many factors may influence weekly sales of retailers, such as Unemployment rate, CPI, Temperature, Fuel price, Store size, etc. We explore the correlations between several temporal features (Unemployment rate, Fuel price, CPI, Temperature, GDP) and temporal variables with different scales (Year, Month, Quarter, Number of days since baseline date). Some of features display strong correlations with temporal variables (Fuel price, GDP) while others do not (Unemployment rate, CPI, Temperature) from this crude correlation plots. As for relationship between features, we do not observe large dependence except between Fuel price and GDP, where time is inferred to be a confounder based on their respective strong temporal trend.

<img src="images/corr.jpeg" alt="correlation" class = "ct" width = "55%">

One important feature of Walmart weekly sales is that two peaks occurred at the end of each year, where the second one is always higher than the first one, corresponding with Christmas and Thanksgiving respectively. This pattern is not to our surprise, as stores usually offer the largest promotion events during that period, and the family time can usually stimulate the shopping passion. For other promotion events around a year, the sales pattern looks stable with slight fluctuations. One interesting finding is, the lowest sales usually comes two or three weeks directly after Christmas, possibly due to the reduced needs and passion after Christmas carnival.

<img src="images/sales_temporal.jpeg" alt="average sales over time" class = "ct" width = "90%">

Linking weekly sales outcome with features described above, the plots below illustrate the relationship between averages sales and each individual factor stratifying by store type. The definition of store types A, B, C are not mentioned from data source, but we infer them to be Walmart Supercenter, Walmart Neighbourhood Market and Walmart Express stores respectively considering their size, amount and the [description](https://www.scrapehero.com/number-of-walmart-stores-and-an-analysis-of-related-store-data/) of Walmart store types before year 2016. The plot implies weak linear effects of most features, but meanwhile indicates possible interactions of these features with store type. For example, we observe a peak of average sales at the end of year for type A and type B stores from the upper-left plot, but quite flat temporal pattern for type C stores. However, the effects of some features look ambiguous, such as unemployment rate and temperature. 

<img src="images/sales_feature.jpeg" alt="sales-feature relationship" class = "ct" width = "80%">

The exploration work provides a general idea of how the features and weekly sales data look like and what are their respective relations. To identify "key" features and answer the second question, our visualization results suggest the application of some advanced statistical models as the next step.

### Key factors that influence weekly sales

We tried to build several statistical models, including linear model with stepwise regression, generalized estimating equations and generalized linear models. Technical parts are skipped here to keep our discussion on an appropriate level, and will be discussed in detail in the report. We divide selected features into two categories with converse effects on weekly sales:

**Positive effects**: Fuel price, CPI, Is Holiday indicator.

**Negative effects**: Temperature, Unemployment rate, Number of days since baseline date (temporal variable).

The effect of some key factors on weekly sales correspond well with the intuition before building the model. For example, temperature tends to negatively influence weekly sales, as low temperature usually indicates winter season, when stores tend to start their largest promotion events and sales reach their peaks in Thanksgiving and Christmas from weekly sales plot. It is also interesting to find some features, with vague idea on how to influence retail sales, are selected as key factors, such as fuel price. One worrying fact for sales managers is, we indeed find a decrease of retail sales over time, suggesting the further look at possible threats (e.g. e-commerce).

### Prediction

The sales in some period are assumed to have clear patterns, such as two peaks on Thanksgiving and Christmas. However, it has been hard for large retailers to make precise prediction on the sales in a near future around the year, with so many factors (temporal, spatial, other) to consider at the same time. We sought to change that by constructing some advanced tree-based predictive models, and compare them with traditional baseline methods to assess the performance. The first plot below shows ...... (wait for the plot)

## US retail sales pattern

E-commerce has been considered as both challenge and opportunity for many traditional retailers. The sales chain is often shorter by skipping the onsite stores step, and the promotion stategy can be slightly different, usually focusing on shipping discount for online sales. For sales managers and many other people who are not familiar with e-commerce, it is good to first have a look at its new features and differences before diving into this booming area.

### Financial crisis influence

The chart below describe the temporal trend of both e-commerce sales and non-ecommerce sales in the United States from 2000 to 2018, as well as the GDP during this time period. During the notable financial crisis in year 2008, it seems both GDP and non-ecommerce sales drops off in the following short period, but the e-commerce sales remained steady. Such different patterns were modeled and confirmed through spline coefficients, suggesting higher robustness of e-commerce during financial crisis, which might come from its more flexible operating mode.

<img src="images/ecom_time.jpeg" alt="average sales over time" class = "ct" width = "90%">

### Seasonal fluctuation

The seasonal fluctuation of e-commerce and offline sales also exhibits different patterns from the above charts, with especially lower offline sales in the 1st quarter and higher online sales in the 4th quarter. We extract and describe such pattern of e-commerce and non-ecommerce sales by summarizing their respective percentage of sales in each quarter for each year. The large proportion of e-commerce sales in the last quarter of a year may be attributed to large sales promotion events during this time, together with possible cold weather effects. For those retailers that are new to e-commerce industry, such different distribution of a year suggests the modification of current storage plan over time.

<img src="images/ecom_quarter.jpeg" alt="sales at each quarter" class = "ct" width = "60%">

# Summary

