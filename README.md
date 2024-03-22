<h1 id = "0"> League of Legends Predictive Analytics </h1>
BY: Zhenghao Gong, Bingyan Liu

<a href = "#1"> Introduction </a><br>
<a href = "#2"> Data Cleaning and Exploratory Data </a><br>
<a href = "#3"> Assessment of Missingness </a><br>
<a href = "#4"> Hypothesis Testing </a><br>
<a href = "#5"> Framing a Prediction Problem </a><br>
<a href = "#6"> Baseline Model </a><br>
<a href = "#7"> Final Model </a><br>
<a href = "#8"> Fairness Analysis</a><br>

<h1 id = "1"> Introduction </h1>

Welcome to the adventure of Summoner's Rift, the heart of League of Legends, where strategy and skill stand between victory and defeat in one of the world's most famous multiplayer online battle arena video games. With millions of players engaging in this digital battleground, understanding the vast array of game data available is not only a matter of curiosity, but essential for players who wish to hone their skills and achieve mastery over the game. In this analysis, we aims to explore the rich tapestry of game data, seeking to unveil the pivotal factors that sway the tide of battle and shape the outcome of each match.

Our dataset contains informations of players and teams from over 10,000 League of Legends competitive matches from 2022, providing a comprehensive look at the dynamics at play. Each match unfolds across 12 rows of data, capturing the essence of both teams: five players row and one summary row for each team, across more than 100 columns with virtually all the data that can be collected from a game. When we cleaned out our dataset, we will be left with 45 columns with 3 major categories: 
1. Game and player info: these columns contains `gameid`, `league`, `playerid`, `teamid`, `playername`, `teamname` and `result`.
2. Ban-Pick info: these columns contains the champions ban or picked by each team in the match
3. Game statistics at 10/15 minutes: these columns is about the `kill`, `death`, `assistsat`, `gold`, `experiences` for each players and whole teams in 10/15 minutes.
   
Our project center around the question: **"To what extent does the experience and gold differences between teams impact the match results?"** The significance of this question lies in its ability to uncover strategic elements that are critical to victory, offering valuable insights into effective gaming strategies for diverse audiences. Competitive players and esports professionals can use these insights to refine their tactics. Likewise, game developers and designers might find the outcomes beneficial for future game development, balancing, and enhancing player engagement. The columns that are relevant to answer the question are `golddiffat10`, `xpdiffat10`, `golddiffat15`, `xpdiffat15`. 

<table>
 <tbody>
 <tr>
  <th> column name </th>
    <th> Description </th>
 </tr>
 <tr>
  <td> golddiffat10 </td>
    <td> The gold difference between one player and his rival at 10 minutes in games </td>
 </tr>
 <tr>
  <td> golddiffat15 </td>
    <td> The gold difference between one player and his rival at 15 minutes in games </td>
  </tr>
 </tr>
  <td> xpdiffat10 </td>
    <td> The experience difference between one player and his rival at 10 minutes in games </td>
 </tr>
 </tr>
  <td> xpdiffat15 </td>
    <td> The experience difference between one player and his rival at 15 minutes in games </td>
  </tr>
 </tbody>
</table>

<h1 id = "2"> Data Cleaning and Exploratory Data </h1>
<h3 id = "2.1">Data Cleaning</h3>
After loading the dataset from the CSV file, we will proceed to the crucial step of data cleaning through the following steps to ensure the quality of our analysis: 

* **Feature selection:** Our dataset initially features 123 columns, many of which are not pertinent to our analysis. To streamline our data and focus on the most impactful variables, we will selectively remove the extraneous columns and keep only relevent features. After the removing process, We are left with 45 essential columns that are directly relevant to our analytical objectives. 

* **Data structure transformation:** Then, to consolidate our data, we'll transform the current structure, where each "gameid" corresponds to 12 rows (information for 2 teams, including 5 players per team and 1 team summary each), into a more concise format. Each game will now be represented by a single row that combines the information of the 5 players and their team summary.

* **Data type convertion:** In the previous step, we inadvertently homogenized the data types across our DataFrame as the conversion to a NumPy array and subsequent reconstruction into a DataFrame defaulted all columns to the object data type. Thus, we will reinstated the data type with its **most frequently occurring value type** to ensuring that each column was represented by its most suitable data type.

* **Add more features to the dataframe:** Lastly, to fully capture the dynamics of champion selection, we merge data from the opposing team with each team's data on a match-by-match basis. Incorporating this additional relevant information will improve the dataset's utility for predictive modeling and strategic analysis.

After all cleaning is done, we now have a dataframe with 24878 rows and 211 columns. Below is the first 5 rows for our cleaned dataframe:


graph



<h3 id = "2.2">Feature of data: Visualization</h3>

**Univariate Analysis**

In the univariate analysis, we analyze the frequency use of differnt champion character in the five different position: top, mid(middle), bot(bottom), jng(jungle), sup(support). Here are the bar plot:

<iframe src="asset/Top_Champion.html"  width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/Mid_Champion.html"  width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/Jng_Champion.html" width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/bot_Champion.html" width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/sup_Champion.html" width="800" height="600" frameborder="0"> </iframe>

In the bar plot of the five positions, we can see that the frequency of hero selection shows some common characteristics: **they all have a large number of champion choice and an unbalanced distribution of frequencies**. Heroes selected more than 30 times are relatively few in number, but account for a high total number of selections in matches. Conversely, although heroes chosen fewer than 30 times constitute the majority, their total number of selections is significantly lower than that of the heroes selected more than 30 times. Therefore, in later predictive tasks, a large number of low-frequency heroes may greatly increase the dimensionality of the one-hot encoding and the complexity of the model, but only bring slight improvement to the model. So, we will consider setting a threshold for unique encoding transformation in subsequent models, where only heroes selected more than a certain number of times will be counted into.

**Bivariate Analysis**

Then, we do bivariate analysis between the "team gold difference" and "team xp difference" sepreately at 10 mins ans 15 mins during the games.

<iframe src="asset/diff10m.html" width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/diff15m.html" width="800" height="600" frameborder="0"> </iframe>

The scatter plot shows a clear positive trend between gold and experience at both 10 and 15 minutes, which can be fitted with a linear regression. The results indicate a strong correlation between the charts, suggesting that multicollinearity should be considered when constructing future models. Also, we noticed that the categorical features exhibit high cardinality, while the bivariate analysis shows multicollinearity within the quantitative data. This will take in effect in later analysis.

**Aggregates Analysis**

In our aggregates analysis, we will examine the average gold difference at key moments in the game, notably at 10 and 15 minutes, between blue and red teams.

| side   |   bot_golddiffat10 |   jng_golddiffat10 |   mid_golddiffat10 |   sup_golddiffat10 |   team_golddiffat10 |   top_golddiffat10 |
|:-------|-------------------:|-------------------:|-------------------:|-------------------:|--------------------:|-------------------:|
| Blue   |           -4.53548 |            41.5775 |            9.22125 |            12.7987 |             86.9135 |            27.8516 |
| Red    |            4.21795 |           -41.6012 |           -9.39441 |           -13.2147 |            -87.0592 |           -27.0669 |

| side   |   bot_golddiffat15 |   jng_golddiffat15 |   mid_golddiffat15 |   sup_golddiffat15 |   team_golddiffat15 |   top_golddiffat15 |
|:-------|-------------------:|-------------------:|-------------------:|-------------------:|--------------------:|-------------------:|
| Blue   |            21.5759 |            94.3418 |            36.7647 |            36.5881 |             246.508 |            57.2372 |
| Red    |           -21.4593 |           -94.55   |           -37.4742 |           -38.0258 |            -247.213 |           -55.7041 |




The **pivot table** showcases how gold advantage correlates with team positioning. For instances, that overall teams on the **Blue side are more likely to win** with considerable gold advantages by the 15-minute mark across all positions, especially with notable leads in jungle and overall team gold.

<h1 id = "3"> Assessment of Missingness </h1>

The dataset we're analyzing contains numerous columns with missing data, a common issue in real-world datasets that may poses challenges for data analysis and modeling. 
<iframe src="asset/missing_proportion.html" width="800" height="600" frameborder="0"> </iframe>
To explore whether these missing values are Missing At Random (MAR) or Not Missing At Random (NMAR), we look for patterns in the missing data. If the presence of missing data is related to observed data, it might be MAR; if it’s related to unobserved data, it might be NMAR.

<h3 id = "3.1"> NMAR analysis </h3>

In examining the nature of these missing data, we've concluded that there is **no column that is NMAR(Not Missing at Random)**. The missineness seems to be influenced by the league from which the data originates. Specifically, some leagues do not publish "in-game data" and lead to systematic absences of information across certain columns for matches within those leagues. This aligns with the **MAR(Missing at Random)** assumption, as the missingness depends on a observed data (the league) rather than the unobserved (or missing) in-game data itself.

<h3 id = "3.2"> Missing Dependency </h3>

To assess the randomness of the missing data distribution across `leagues`, we will conduct a **permutation test** focusing on the `top_golddiffat15` column. This choice is based on the premise that all columns exhibit similar patterns of missingness. We hypothesize that the missingness in the `top_golddiffat15` column is random across different `leagues` and will set a sinificant lelve of 0.01.

Here is the empirical distribution of the test statistic:

<iframe src="asset/missing_dependency.html" width="800" height="600" frameborder="0"> </iframe>

**Our observed statistic was:** 0.9923034634414515

**Our p-value was:** 0.0

With a p-val below the threshold of 0.01, we **reject the null hypothesis**. This indicates that **the missingness in the "top_golddiffat15" data is not random across different leagues**. The permutation test results, as visualized in the plot, suggests that the pattern of missing data is associated with certain conditions inherent to the leagues and so we conclude it to be MAR.

<h1 id = "4"> Hypothesis Testing </h1>

**Null hypothesis**: The distribution of "team_golddiffat15" for the winning team is the **same** as the distribution of "team_golddiffat15" for the losing team.

**Alternative hypothesis**: The distribution of "team_golddiffat15" for the winning team is **different** than the distribution "team_golddiffat15" for the losing team.

**Test Statistic:** We will be using permutation test
  * We chose to use difference of mean because the team_golddiffat15 is quantatitive columns, and we expect that the win and lose team has a difference in the mean value for team gold difference at 15 minutes.

**Significance Level:** 1% 
  * We choose this significance level because 1% can reduce the risk of Type I error compared to 5% signifance level.

**P-value:** 0.003
  * We did 10000 simulations


<iframe src="asset/result_goldat15.html" width="800" height="600" frameborder="0"> </iframe>


**Conclusion:** Given the resulting p-value of 0.003 which falls below our significance threshold of 0.01, we reject the null hypothesis. This **suggests** that there is a statistically **significant difference** in the distribution of "team_golddiffat15" between winning and losing teams. The choice to focus on the "team_golddiffat15" metric as a means to explore how experience and gold differences impact match results is good. Gold is a tangible resource in the game that allows teams to purchase items and gain an advantage. By quantifying the gold difference, we can obtain a direct measure of one team's advantage over another, providing link to potential match outcomes. 

[put the visualization of our hypothesis test here]

<h2 id = "5"> Framing a Prediction Problem </h2>

Building on previous exploration of how experience and gold differences between teams impact the match results, we want to fo futher on the factors that affect game result. Specifically, **we want to predict the game "result" by utilizing statistical data from the 10 and 15-minute marks, the chosen ten champions, team ID, and player ID**. This presents a **binary classification problem**, where our goal is to predict the match `result` based on these variables. We choose "result" as our response variable because it can be distinctly classified into two categories (win or loss), leading our prediction into a binary classification framework and capturing the ultimate goal of every match. To evaluate our model, we will use the F1 score and the confusion matrix over other metrics such as accuracy. We choose the F1 score because of its balance between precision and recall, where it is capable of capturing both false positives and false negatives, which are crucial considerations in predicting game outcomes. We choose confusion matrix because it provides a comprehensive overview of the model's performance as it break down predictions into true positives, true negatives, false positives, and false negatives.

<h1 id = "6"> Baseline Model </h1>

<h3 id = "6.1"> Model and Features Description </h3>

Our baseline model is a **classifier model based on logistic regression**. It will process one-hot encoding on the team side(blue and red) information, using the quantitative data directly and fit into a logistic regression model with high regularization parameter. 

We have **12 quantitative feature** `team_xpdiffat15`, `top_xpdiffat15`, `mid_xpdiffat15`, `jng_xpdiffat15`, `bot_xpdiffat15`, `sup_xpdiffat15`, `team_golddiffat15`, `top_golddiffat15`, `mid_golddiffat15`, `jng_golddiffat15`, `bot_golddiffat15`, `sup_golddiffat15`, `result`; **0 ordinal feature** and **1 nominal feature** `side` used. 

Since categorical data like `side` cannot be fed directly into logistic regression models. We will **one-hot encoded the `side` column**, where we represented the "blue" side with a value of 1 and the "red" side with a value of 0. This ensuring that the logistic regression model can accurately interpret and utilize the categorical information without assuming any ordinal relationship between categories. 

<iframe src="asset/baseline_cm.html" width="800" height="600" frameborder="0"> </iframe>

<h3 id = "6.2"> Performance Evalution and Conclusion </h3>

The performance of our current model has an accuracy rate of **approximately 71%**. We believe it is relatively good but have more space to improve, especially considering the impact imposed by missing data. The prevalence of missing values in critical statistical data, particularly when entire rows of data are absent due to unreported metrics like kills, deaths, assists, and experience from certain matches, sinificantly reduces the model's ability to accurately predict outcomes based on incomplete data. 

To further enhance our model's accuracy, we can diversifying the feature set with additional predictive variables that are less susceptible to missingness. Specifically, we can incorporating champion selected by the ten players and the team's ID as classification features.
 
<h1 id = "7"> Final Model </h1>

To improve upon our baseline model, we added features **the champions chosen by the ten players and the team IDs** as different teams exhibit varying win rates, attributed to the distinct strengths, adaptability, and the synergies or counterplays of their chosen champions that affect game outcome. 

### Model selection
We choose a **stacking model based on one logistics regression and one gradient boosting tree**. This decison come with the following consideration:

 1. Categorical features solution: The features include categorical data with high cardinality, which posed the risk of **Curse of Dimensionality** if directly use one-hot encoding. To mitigate this and use these high-cardinality categorical data, we applied a **boundary-based one-hot encoder** to filter infrequently chosen categories, followed by **PCA** for dimensionality reduction and pivotal component extraction. Then, we implemented **Bayesian target encoding** to transform categorical data into numerical values reflective of win probabilities. This strategy will effectively enhance the model's interpretative power regarding the high cardinality caused by the categorical data. 

2. Quantitative features solution: For numerical data, we utilized **logistic regression with a high regularization parameter and a tree model**, this can ensure that our model will not fall into potential multicollinearity issues as the two methods has an insensitivity to collinearity.

### Finding hyperparameters
Finding optimal hyperparameter is cruical for model perfoermance, in our model, we will utilize the following hyperparamater:
* **PCA components:** this parameter specifies the number of principal components retained after PCA. This balance is important for reducing dimensionality while preserving important variance in the data.
* **Logistic regression parameter(C):** this parameter controls the regularization strength in logistic regression. A lower value use more regularization to prevent overfitting while higher value  make model more flecible to capture complex patterns.
* **Graidient boosting tree parameter**
    * **max_depth:** this parameter specifies the maximum depth of individual trees. It prevent the model to become too complex and overfit to the training data.

The method used to select the hyperparameters is **cross_validation on a  5-fold test**, with the average F1 score as the metric to perform grid search. After running **GrideSearchCV**, the best hyperparameters are the following:
* **PCA components:** 600. 
* **Logistic regression parameter(C):** 0.1 
* **Graidient boosting tree max_depth:** 20
 
<iframe src="asset/baseline_cm.html" width="800" height="600" frameborder="0"> </iframe>
 
<iframe src="asset/final_mdl_cm.html" width="800" height="600" frameborder="0"> </iframe>

### Model performance
Compared to the baseline model, our final model has a improvemnet of over 2% in F1 scores, particularly in contexts with missing statistical data. Using a stacked model, which integrate logistic regression and gradient boosting trees, has improve the model's capacity to capture complex relationships within the data, thus further boosting its predictive power.

<h1 id = "8"> Fairness Analysis </h1>

With a refined predictive model with an even better level of accuracy, we now want to access its fairness. This critical evaluation will ensure that our model does not disadvantage any group of players or teams based on arbitrary criteria. We define the 1 to perdition result that are correct and 0 to perdition result that are wrong. 

**Evaluation metric**: permutation test

**Group X**: `league`

**Group Y**: `correctness of our model's prediction` (1: correct, 0: wrong)

**Null Hypothesis**: The distribution of correct and incorrect classification results **is consistent** across all leagues.

**Alternative Hypothesis**: The distribution of correct and incorrect classification results is **not consistent** across all leagues.

**Test Statistic**: total variation distance

**Significant level**: 0.01

 <iframe src="asset/fairness_permutation.html" width="800" height="600" frameborder="0"> </iframe>

The analysis resulted in a p-value of 0.0. Since the p-value is less than the threshold 0.01, we **reject** the null hypothesis. This lead to the conclusion that our model **demonstrates unfairness** in terms of prediction accuracy across different leagues. This discrepancy is likely attributable to the distribution of missing data (which are mainly on data with the league DCcup, LPL and LDL).


<h1 id = "9"> Reference </h1>
