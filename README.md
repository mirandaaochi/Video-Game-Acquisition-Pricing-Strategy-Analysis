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

Below are the rotated factor loadings for each of our 40 attributes. Factor loadings show how strongly related the variables are to the underlying factor. They help us determine what the factor represents.

<p align="center" width="100%">
<img width="672" height="804" alt="Rotated Factor Loadings" src="https://github.com/user-attachments/assets/fae8eaa0-7986-4b4b-9180-f319a1ec96b2" />

Factor 1 has strong positive loadings in enj.strategy, enj.decisions, and enj.planning. It also has moderate positive loadings in imp.challenge, imp.difficulty, imp.mastery, and freq.study. This means there’s enjoyment in gameplay that requires long-term planning and strategy, careful decision-making, and a lot of thinking. There's also importance in taking on difficult challenges, playing a game at the highest difficulty level, and taking time to master a game. We can call this “Strategy Heavy.”

Factor 2 has strong negative loadings in imp.unlocks, imp.completion, and imp.collect. This means that it’s not important to complete all possible missions and collect all possible unlocks in a game, so we can call this “Anti-Unlock Completion.”

Factor 3 has strong negative loadings in imp.backstory, imp.characters, and imp.storyline. This means that getting to know all of the main characters and their backstories and an elaborate storyline are not important, so we can call this “Anti-Storytelling.” 

Factor 4 has strong positive loadings in enj.guns, enj.blow.up, enj.gore, and enj.destruction. This means that there’s enjoyment in using guns and explosives in gameplay with lots of blood and gore, so we can call this “Enjoy Violence.”

Factor 5 has strong negative loadings in imp.offbeat, freq.experiment, freq.explore, and freq.test.world. This means that discovering unconventional ways to play the game and experimenting and exploring within the world aren’t important nor frequent, so we can call this “Anti-Exploratory Play.”

Factor 6 has strong negative loadings in enj.fast, enj.excitement, and enj.react. This means that gameplay that is fast-paced or intense with constant action requiring quick reaction times is not enjoyable, so we can call this “Anti-Fast-Paced Action.”

Factor 7 has strong negative loadings in imp.fantasy, imp.power, enj.roleplay, enj.immersion, and imp.items. This means that being able to pretend you’re someone else, become as powerful as possible, and being immersed in another place are not important nor enjoyable, so we can call this “Anti-Fantasy-Power Roleplay.”

Factor 8 has strong negative loadings in enj.helping, enj.common.goal, and enj.others. This means that there’s no enjoyment in helping other players, working towards a common goal, or grouping up with others. We can call this “Anti-Teamwork.”

Factor 9 has strong positive loadings in imp.customize, freq.customize, and freq.char.creation. This means that having customization options is important, and these players frequently put a lot of effort into character creation and customization. We can call this “Customization.”

Factor 10 has strong positive loadings in enj.competition and enj.duels and a moderate positive loading in imp.dominate. This means there’s enjoyment in competing with other players in duels or matches, and it’s important to dominate other players. We can call this “Competition Dominance.”

Factor 11 has moderate negative loadings in imp.difficulty, imp.challenge, and imp.mastery. This means that it’s not important to play the game at the highest difficulty level, take on difficult challenges that may take many tries to succeed, or take the time to practice and master the game. We can call this “Anti-Difficult Challenge.”

**Cluster Analysis**

Before performing cluster analysis using K-means clustering to identify segments, we need to know how many clusters to use. Based on the following elbow plot, 8 clusters seems to be a good choice. We can use the cluster centers to name and interpret our 8 segments. 

<p align="center" width="100%">
<img width="585" height="444" alt="Elbow Plot" src="https://github.com/user-attachments/assets/3136fdcf-4d39-4cd6-907c-f3569e20e2f3" />

<p align="center" width="100%">
<img width="1071" height="440" alt="Cluster Centers" src="https://github.com/user-attachments/assets/7f555adb-ceb0-4bc7-a766-61c8b3aff034" />

Cluster 0 is very negative in Strategy Heavy, very positive in Enjoy Violence, moderately positive in Anti-Unlock Completion and Anti-Exploratory Play, and moderately negative in Anti-Storytelling. They’re really not interested in strategy-heavy games, really enjoy violence, are somewhat uninterested in unlocking everything within a game or exploring the world, and are somewhat interested in storytelling. We can call this cluster the “Violence/Story Fans.”

Cluster 1 is very positive in Anti-Storytelling, moderately positive in Anti-Fast-Paced Action, and moderately negative in Anti-Unlock Completion. They’re really not interested in storytelling, are somewhat interested in unlocking everything within a game, and are somewhat uninterested in fast-paced action. We can call this cluster “Completion-Focused/Non-Story Players.”

Cluster 2 is very negative in Anti-Unlock Completion and Anti-Storytelling but moderately positive in Strategy Heavy. They care heavily about unlocking everything and the storyline of a game and are somewhat interested in games that require a lot of strategy. We can call this cluster “Completion/Story Fans.”

Cluster 3 is very negative in Anti-Storytelling and Enjoy Violence, very positive in Anti-Exploratory Play and Anti-Fast-Paced Action, and moderately positive in Strategy Heavy and Anti-Unlock Completion. They care heavily about storytelling, don’t enjoy violence, don’t care about exploratory play or fast-paced action, are somewhat interested in games that require a lot of strategy, and are somewhat uninterested in unlocking everything within a game. We can call this cluster “Strategic Non-Violent Storytellers.”

Cluster 4 is very positive in Anti-Unlock Completion, very negative in Anti-Exploratory Play, and moderately negative in Strategy Heavy and Enjoy Violence. They really aren’t interested in unlocking everything with a game, care a lot about exploring the world, and are somewhat uninterested in strategy-heavy games or violence. We can call this cluster “Explorers.”

Cluster 5 is very positive in Anti-Storytelling and Anti-Exploratory Play, moderately positive in Anti-Unlock Completion and Anti-Teamwork, and moderately negative in Anti-Fast-Paced Action. They are really not interested in storytelling or exploratory play, are somewhat uninterested in unlocking everything within a game or teamwork, and are somewhat interested in fast-paced action. We can call this cluster “Fast-Paced Action Fans.”

Cluster 6 is very negative in Strategy Heavy, Anti-Unlock Completion, and Enjoy Violence. They are really not interested in strategy-heavy games, unlocking everything with a game, and don’t enjoy violence. We can call this cluster “Non-Competitive/Non-Action Players.”

Cluster 7 is very positive in Strategy Heavy and moderately negative in Anti-Exploratory Play and Anti-Teamwork. They are very interested in strategy-heavy games and are somewhat interested in exploratory play and teamwork. We can call this cluster “Strategy/Exploratory Team Players.”

**Cross Tabulation and Regression Analysis for Segments and Demographic Attributes**

The data contains four demographic attributes: gender, age, income, and location (state). For demographic variables measured on a ratio scale like income or age, we can use regression with dummy coding for cluster membership or crosstabs analysis to investigate relationships. For demographic variables measured using a nominal scale such as gender or location, we must always use crosstabs analysis.

_Gender_

The resulting table is statistically significant (p < 0.05), so there is a relationship between the segments and gender. We can use the critical value of 3.84 to determine which cells contribute to the relationship. The cells that contribute to this relationship are “Explorers x female,” “Explorers x male,” “Fast-Paced Action Fans x female,” “Non-Competitive/Non-Action Players x female,” and “Non-Competitive/Non-Action Players x male.” In particular, the “Explorers” segment has fewer females and more males than expected, “Fast-Paced Action Fans” has fewer females than expected, and “Non-Competitive/Non-Action Players” has more females and fewer males than expected. This suggests that certain segments are gender-skewed.

<p align="center" width="100%">
<img width="565" height="773" alt="Gender Crosstab" src="https://github.com/user-attachments/assets/a08a0072-43dd-40ae-94a7-04e116b2ceef" />

_Age_

“Completion-Focused/Non-Story Players” is the baseline group and has an average age of about 32.76 (from the intercept value). “Completion/Story Fans” are about 3.76 years older than the baseline on average, meaning their average age is 36.52. The rest of the segments are younger than the baseline on average. “Explorers” are about 12.22 years younger, meaning their average age is 20.54. “Fast-Paced Action Fans” are about 8.80 years younger, meaning their average age is 23.96. “Non-Competitive/Non-Action Players” are about 4.22 years younger, meaning their average age is 28.54. “Strategic Non-Violent Storytellers” are about 8.95 years younger, meaning their average age is 23.81. “Strategy/Exploratory Team Players” are about 9.50 years younger, meaning their average age is 23.26. “Violence/Story Fans” are about 4.07 years younger, meaning their average age is 28.69. All of the coefficients are statistically significant. This indicates that these differences in average age across segments are meaningful.

<p align="center" width="100%">
<img width="813" height="478" alt="Age Regression" src="https://github.com/user-attachments/assets/21456a89-7329-4e91-9239-f7e45c60c209" />

_Income_

“Completion-Focused/Non-Story Players” is the baseline group and has an average income of about $69,200 (from the intercept value). “Completion/Story Fans” earn about $63.42 more than the baseline on average, meaning their average income is $69,263.42. The rest of the segments have lower income than the baseline on average. “Explorers” earn about $42,070 less, meaning their average income is $27,130. “Fast-Paced Action Fans” earn about $26,370 less, meaning their average income is $42,830. “Non-Competitive/Non-Action Players” earn about $16,100 less, meaning their average income is $53,100. “Strategic Non-Violent Storytellers” earn about $31,290 less, meaning their average income is $37,910. “Strategy/Exploratory Team Players” earn about $30,160 less, meaning their average income is $39,040. “Violence/Story Fans” earn about $11,160 less, meaning their average income is $58,040. All of the coefficients are statistically significant except for “Completion/Story Fans.” This indicates that these differences in average income across the other segments are meaningful.

<p align="center" width="100%">
<img width="813" height="478" alt="Income Regression" src="https://github.com/user-attachments/assets/be61e90b-11f8-4f1c-903f-0cf1671de113" />

_Location_

Since the data contains state-level location data, it made sense to group states into regions (Midwest, Northeast, South, and West). From the crosstabs analysis on state, the resulting table is not statistically significant (p > 0.05), so there is not a relationship between the segments and location. The data isn’t necessarily sparse (more than 80% of the crosstab cells have an expected count of 5 more), so there is no need to collect more data or collapse the categories.

<p align="center" width="100%">
<img width="630" height="771" alt="Location Crosstab" src="https://github.com/user-attachments/assets/5c81ca4b-445a-4a8b-af8f-3cad81e48e1f" />

The resulting demographic attributes (% female, average age, and average income) of each segment regardless of statistical significance can be found in the table below.

<p align="center" width="100%">
<img width="698" height="465" alt="Demographic Table" src="https://github.com/user-attachments/assets/b0120413-6070-47fb-a1a8-c0c6140bcd16" />

### Task 3: Gabor Granger Response Investigation

**Addressing the Missing Data**

Each respondent was randomly presented with one of the three games (Warrior Guild, Seraph Guardians, or Evercrest). The survey identified the maximum price point at which each respondent would “probably purchase” the presented game, but there are 138 missing values – 40 for Warrior Guild, 47 for Seraph Guardians, and 51 for Evercrest. This accounts for about 5.4% of Warrior Guild data missing, 6.2% of Seraph Guardians, and 7.5% of Evercrest.

Since deletion would reduce the sample size and potentially alter the relationships between variables, we can use regression imputation to replace missing values with predicted scores from regression. This method gives better results compared to the other methods but risks overestimation of the model fit and correlations. 

**Gabor Granger Plots & Optimal Prices**

_Warrior Guild_

The ideal price point for Warrior Guild is $35. This is the price that corresponds with the maximum amount of revenue ($18,620) with about 71.51% of the surveyed customers willing to pay that price. 

<p align="center">
<img width="49%" alt="Warrior Guild WTP" src="https://github.com/user-attachments/assets/3cb397c3-81cb-4b36-9697-1d39173128d6"/>
<img width="49%" alt="Warrior Guild Revenue" src="https://github.com/user-attachments/assets/216db45f-43bd-4e95-8ce1-51c0a469835e"/>
</p>

_Seraph Guardians_

The ideal price point for Seraph Guardians is $32. This is the price that corresponds with the maximum amount of revenue ($18,560) with about 76.72% of the surveyed customers willing to pay that price.

<p align="center">
<img width="49%" alt="Seraph Guardians WTP" src="https://github.com/user-attachments/assets/0ea8a724-594e-4bf0-9341-11fd93e6ee43" />
<img width="49%" alt="Seraph Guardians Revenue" src="https://github.com/user-attachments/assets/113c8336-cf8b-40f9-878c-01760d2d178b" />
</p>

_Evercrest_

The ideal price point for Evercrest is also $32. This is the price that corresponds with the maximum amount of revenue ($15,808) with about 72.86% of the surveyed customers willing to pay that price.

<p align="center">
<img width="49%" alt="Evercrest WTP" src="https://github.com/user-attachments/assets/2a34b6cc-0b30-4678-ac96-7de02ee90112" />
<img width="49%" alt="Evercrest Revenue" src="https://github.com/user-attachments/assets/102c56b8-d58b-4dfa-86c5-b1ed89fe7f4d" />
</p>

**Linear Regressions (Interest Levels)**

_Warrior Guild_

“Completion-Focused/Non-Story Players”  (willing to pay $52.92) and “Completion/Story Fans” (willing to pay $53.14) are the most interested in Warrior Guild. “Explorers” are the least interested (willing to pay $37.51).

“Completion-Focused/Non-Story Players” is the baseline group with a max price of about $52.92. “Completion/Story Fans” are willing to pay about $0.22 more than the baseline on average, for a total of $53.14. The rest of the segments have negative coefficients, meaning they’re willing to pay less than the baseline on average. “Explorers” are willing to pay about $15.41 less, for a total of $37.51. “Fast-Paced Action Fans” are willing to pay about $7.87 less, for a total of $45.05. “Non-Competitive/Non-Action Players” are willing to pay about $9.47 less, for a total of $43.45. “Strategic Non-Violent Storytellers” are willing to pay about $11.71 less, for a total of $41.21. “Strategy/Exploratory Team Players” are willing to pay about $6.69 less, for a total of $46.23. “Violence/Story Fans” are willing to pay about $3.13 less, for a total of $49.79. 

All of the coefficients are statistically significant except for “Completion/Story Fans.” This indicates that these differences in willingness to pay across the other segments are meaningful.

<p align="center">
<img width="812" height="479" alt="Warrior Guild Interest" src="https://github.com/user-attachments/assets/668e5c87-ba52-4d0b-82d7-e83546c2c64a" />

_Seraph Guardians_

“Completion/Story Fans” (willing to pay $61.30) are the most interested in Seraph Guardians, and “Explorers” are the least interested (willing to pay $31.12).

“Completion-Focused/Non-Story Players” is the baseline group with a max price of about $53.64. “Completion/Story Fans” are willing to pay about $7.66 more than the baseline on average, for a total of $61.30. Once again, the rest of the segments have negative coefficients, meaning they’re willing to pay less than the baseline on average. “Explorers” are willing to pay about $22.52 less, for a total of $31.12. “Fast-Paced Action Fans” are willing to pay about $9.25 less, for a total of $44.39. “Non-Competitive/Non-Action Players” are willing to pay about $7.23 less, for a total of $46.41. “Strategic Non-Violent Storytellers” are willing to pay about $13.40 less, for a total of $40.24. “Strategy/Exploratory Team Players” are willing to pay about $6.62 less, for a total of $47.02. “Violence/Story Fans” are willing to pay about $3.66 less, for a total of $49.98. 

All of the coefficients are statistically significant, so these differences in willingness to pay across the other segments are meaningful. 

<p align="center">
<img width="811" height="479" alt="Seraph Guardians Interest" src="https://github.com/user-attachments/assets/e06d8688-a202-4b0e-849a-502e17e2e2df" />

_Evercrest_

“Completion-Focused/Non-Story Players” (willing to pay $53.47) and “Completion/Story Fans” (willing to pay $56.16) are the most interested in Evercrest. As we’ve seen with both Warrior Guild and Seraph Guardians, “Explorers” are the least interested (willing to pay $32.83).

“Completion-Focused/Non-Story Players” is the baseline group with a max price of about $53.47. “Completion/Story Fans” are willing to pay about $2.69 more than the baseline on average, for a total of $56.16. Like with the other two games, the rest of the segments have negative coefficients, meaning they’re willing to pay less than the baseline on average. “Explorers” are willing to pay about $20.64 less, for a total of $32.83. “Fast-Paced Action Fans” are willing to pay about $10.78 less, for a total of $42.69. “Non-Competitive/Non-Action Players” are willing to pay about $8.94 less, for a total of $44.53. “Strategic Non-Violent Storytellers” are willing to pay about $6.50 less, for a total of $46.97. “Strategy/Exploratory Team Players” are willing to pay about $7.93 less, for a total of $45.54. “Violence/Story Fans” are willing to pay about $6.89 less, for a total of $46.58. 

Similar to Warrior Guild, all of the coefficients are statistically significant except for “Completion/Story Fans.” This indicates that these differences in willingness to pay across the other segments are meaningful.

<p align="center">
<img width="811" height="479" alt="Evercrest Interest" src="https://github.com/user-attachments/assets/9bc7a45d-6f26-4eb9-a8cc-e763999595bd" />

**First Year Gross and Net Revenues**

Athena must pay 5% in royalties on the gross revenue to the original developer and spend $7 million to acquire and market the game. Warrior Guild costs an additional $5 million to finalize development, Seraph Guardians $5.5 million, and Evercrest $6 million. Additionally, Steam takes 30% of gross sales up to the first $10 million, 25% between $10 million and $50 million, and 20% after $50 million.

<p align="center">
<img width="695" height="156" alt="Gross and Net Revenues" src="https://github.com/user-attachments/assets/767af9f8-35dc-4329-bdaf-df87c6507efa" />

_Warrior Guild_

* Ideal Price Point: $35
* Surveyed Customers Willing to Pay $35: 71.51%
* Actual Purchases: 2,145,300 
* Gross Revenue: $35 x 2,145,300 = $75,085,500
* Total Costs: $15,754,275
  * Royalites: 5% x $75,085,500 = $3,754,275
  * Acquisition and Marketing: $7,000,000
  * Development: $5,000,000
* Steam's Cut (Gross Sales > $50,000,000): (30% x $10,000,000) + ([$50,000,000 - $10,000,000] x 25%) + ([$75,085,500 - $50,000,000] x 20%) = $18,017,100
* Net Revenue: $75,085,500 - $15,754,275 - $18,017,100 = $41,314,125

_Seraph Guardians_

* Ideal Price Point: $32
* Surveyed Customers Willing to Pay $32: 76.72%
* Actual Purchases: 2,301,600 
* Gross Revenue: $32 x 2,301,600 = $73,651,200
* Total Costs: $16,182,560
  * Royalites: 5% x $73,651,200 = $3,682,560
  * Acquisition and Marketing: $7,000,000
  * Development: $5,500,000
* Steam's Cut (Gross Sales > $50,000,000): (30% x $10,000,000) + ([$50,000,000 - $10,000,000] x 25%) + ([$73,651,200 - $50,000,000] x 20%) = $17,730,240
* Net Revenue: $73,651,200 - $16,182,560 - $17,730,240 = $39,738,400

_Evercrest_

* Ideal Price Point: $32
* Surveyed Customers Willing to Pay $32: 72.86%
* Actual Purchases: 2,185,800
* Gross Revenue: $32 x 2,185,800 = $69,945,600
* Total Costs: $16,182,560
  * Royalites: 5% x $69,945,600 = $3,497,280
  * Acquisition and Marketing: $7,000,000
  * Development: $6,000,000
* Steam's Cut (Gross Sales > $50,000,000): (30% x $10,000,000) + ([$50,000,000 - $10,000,000] x 25%) + ([$69,945,600 - $50,000,000] x 20%) = $16,989,120
* Net Revenue: $69,945,600 - $16,497,280 - $16,989,120 = $36,459,200

## Business Recommendations

Warrior Guild was ranked #1 by 287 / 2178 respondents, corresponding to a market share of about 13.18%. Seraph Guardians was ranked #1 by 1090 / 2178 respondents, corresponding to a market share of about 50.05%. Evercrest was ranked #1 by 213 / 2178 respondents, corresponding to a market share of about 9.78%. If Athena chooses not to acquire any of the candidate games, then it wouldn’t capture about 73.01% of the market (13.18% + 50.05% + 9.78%).

**I recommend that Athena acquire Seraph Guardians.** It demonstrates strategic fit with Athena’s existing portfolio and has the strongest market demand based on first-choice rankings and willingness-to-pay results. It also generates high projected net revenue, satisfying financial viability requirements. While Warrior Guild generates slightly higher projected revenue, Seraph Guardians’s demand and strategic alignment make it a stronger candidate. Choosing not to acquire Seraph Guardians would introduce competitive risk since a competitor can capture the unmet demand.

**I recommend pricing Seraph Guardians at a moderate price of $32.** This price maximizes revenue while maintaining a high proportion of customers willing to purchase. It also reinforces Athena’s premium brand positioning and supports market penetration.

**I recommend that Athena uses a targeted approach rather than a non-targeted strategy.** The linear regression results show that willingness to pay varies significantly across segments. Focusing marketing efforts on the most interested segments captures the majority of willing-to-pay customers and maximizes expected net revenue. Specifically, “Completion/Story Fans” have the highest willingness to pay ($61.30), followed by “Completion-Focused/Non-Story Players” ($53.64). Marketing could involve story-driven campaigns for Completion/Story Fans and challenge completion emphasis for both segments. While Athena could adopt a non-targeted approach, many other segments have significantly lower willingness to pay and are less likely to purchase Seraph Guardians, making that strategy less profitable.
