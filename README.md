# Video Game Acquisition & Pricing Strategy Analysis for Athena Softworks
This was a project completed for Marketing 552Q: Market Intelligence as part of the Marketing track for the Master of Quantitative Management: Business Analytics program at the Duke University Fuqua School of Business.  Due to privacy constraints, code cannot be shared.

## Executive Summary
Athena Softworks, Inc. is a video game developer and publisher specializing in premium role-playing games (RPGs) for PC Play. Athena is considering acquiring a new game title, and there are three candidate games.

There are three key decisions that need to be made in conjunction: 
1. Which game should Athena pursue, if any?
2. How should the game be priced?
3. How should Athena position this game?

Data resources for this project included:
* SuperData 2019 Year in Review
* Newzoo’s Gamer Segmentation
* Quantic Fountry’s Gamer Motivation Model
* Quantic Fountry’s Gamer Segmentation
* Gamasutra’s Personality And Play Styles: A Unified Model
* Survey Data

## Methodology

1. Assess Market Size
    * Determine the market size for the types of games Athena sells in 2019.
    * Project the market size in 2020, ignoring COVID-19.

2. Identify Potential Segments from the Survey Data
    * Use factor analysis to identify the most relevant survey statements for each factor.
    * Perform cluster analysis (K-means) to identify segments and their most relevant factors.
    * Use cross tabulation and regression analysis to investigate the relationship between the segments and various demographic attributes (gender, age, income, location).
    
3. Investigate Gabor Granger Responses
    * Address missing data.
    * Plot the percent of customers willing to pay and the predicted revenue as a function of price to determine the ideal price point for each game.
    * Use linear regression to predict which segments are most and least interested in each game.
    * Find the gross and net revenues for each game in the first year with the assumption that 30% of respondents will actually purchase the game within the first year.

4. Provide final recommendations.

## Skills

**Programming**
- Python

**Statistical & Analytical Techniques**
- Factor Analysis (PCA, Varimax Rotation)
- K-Means Clustering
- Cross Tabulation
- OLS Regression
- Multinomial Logistic Regression

**Modeling & Business Applications**
- Gabor–Granger Pricing Optimization
- Revenue Forecasting
- Customer Segmentation 

## Key Analysis

### Task 1: Market Size Estimation

* **2019 Estimation:** Athena specializes in premium RPGs for PC play, and SuperData’s 2019 Year in Review reports that the premium PC games market was $5.2 billion in 2019.
* **2020 Projection:** SuperData projects the premium PC market to grow to $5.3 billion in 2020, ignoring COVID-19 effects.
* **Impact of COVID-19:** COVID-19 would likely have a positive impact on the premium PC market. As lockdowns kept consumers at home, demand for digital entertainment and online social interaction would be expected to increase. However, this impact may only be short-term, as consumer gaming time and premium game spending could go back to normal once restrictions are lifted.

### Task 2: Customer Segmentation

**Factor Analysis**

To identify potential segments in the market, we can first perform factor analysis on our 40 statement variables. We must first evaluate the data using Bartlett’s Test of Sphericity and the KMO-test to determine if factor analysis is appropriate. With Bartlett’s Test of Sphericity, we want p < 0.05. With the KMO-test, we want an overall MSA > 0.6. Both tests passed these thresholds (p = 0.0, MSA ≈ 0.89), so we can proceed with factor analysis.

Next, we can standardize the 40 attributes and determine the number of factors that emerge from the data using PCA. We want the factors to explain roughly 70% or more of the variance in the data, so we will focus on the factors with an eigenvalue > 1. From the PCA results, 11 factors have eigenvalues > 1, so we can use 11 factors to explain the 40 attributes.

<p align="center" width="100%">
<img width="512" height="541" alt="PCA" src="https://github.com/user-attachments/assets/c8d2a315-ae84-4db6-af44-b14ffbf04ff3" />









## Business Recommendations
