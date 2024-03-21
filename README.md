<h1 id = "0"> League-of-Legends-Result-Analysis-2024 </h1>

<a href = "#1"> Introduction </a><br>
<a href = "#2"> Data Cleaning and Exploratory Data </a><br>
<a href = "#3"> Assessment of Missingness </a><br>
<a href = "#4"> Hypothesis Testing </a><br>
<a href = "#5"> Framing a Prediction Problem </a><br>
<a href = "#6"> Baseline Model </a><br>
<a href = "#7"> Final Model </a><br>
<a href = "#8">Fairness Analysis</a><br>

 
<h2 id = "1"> Introduction </h2>

<h3 id = "1.1"> Description of League-of-Legends </h3><br>
Welcome to the adventure of Summoner's Rift, the heart of League of Legends, where strategy and skill stand between victory and defeat in one of the world's most famous multiplayer online battle arena video games. With millions of players engaging in this digital battleground, understanding the vast array of game data available is not only a matter of curiosity, but essential for players who wish to hone their skills and achieve mastery over the game. In this analysis, we aims to explore the rich tapestry of game data, seeking to unveil the pivotal factors that sway the tide of battle and shape the outcome of each match.

<h3 id = "1.1"> Introduction of Dataset </h3><br>
Our dataset contains informations of players and teams from over 10,000 League of Legends competitive matches from 2022, providing a comprehensive look at the dynamics at play. Each match unfolds across 12 rows of data, capturing the essence of both teams: five players row and one summary row for each team, across more than 100 columns with virtually all the data that can be collected from a game. When we cleaned out our dataset, we will be left with 45 columns with 3 major categories: 
1. Game and player info: these columns contains `gameid`, `league`, `playerid`, `teamid`, `playername`, `teamname` and `result`.
2. Ban-Pick info: these columns contains the champions ban or picked by each team in the match
3. Game statistics at 10/15 minutes: these columns is about the `kill`, `death`, `assistsat`, `gold`, `experiences` for each players and whole teams in 10/15 minutes.

<h3 id = "1.2"> Our Research Question </h3><br>
Our project center around the question: "To what extent does the experience and gold differences between teams impact the match results?" The significance of this question lies in its ability to uncover strategic elements that are critical to victory, offering valuable insights into effective gaming strategies for diverse audiences. Competitive players and esports professionals can use these insights to refine their tactics. Likewise, game developers and designers might find the outcomes beneficial for future game development, balancing, and enhancing player engagement. The columns that are relevant to answer the question are golddiffat10, xpdiffat10, golddiffat15, xpdiffat15. 

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

<h2 id = "2"> Data Cleaning and Exploratory Data </h2>
<h3 id = "2.1">Data Cleaning</h3>
Our dataset initially features 123 columns, many of which are not pertinent to our analysis. To streamline our data and focus on the most impactful variables, we will selectively remove the extraneous columns and keep only relevent features. After the removing process, We are left with 45 essential columns that are directly relevant to our analytical objectives. Then, to consolidate our game data, we'll transform the current structure, where each "gameid" corresponds to 12 rows (information for 2 teams, including 5 players per team and 1 team summary each), into a more concise format. Each game will now be represented by a single row that combines the information of the 5 players and their team summary. In the process, we inadvertently homogenized the data types across our DataFrame as the conversion to a NumPy array and subsequent reconstruction into a DataFrame defaulted all columns to the object data type. Thus, we will reinstated the data type with its **most frequently occurring value type** to ensuring that each column was represented by its most suitable data type. Lastly, to fully capture the dynamics of champion selection, we merge data from the opposing team with each team's data on a match-by-match basis. Incorporating this additional relevant information will improve the dataset's utility for predictive modeling and strategic analysis. After all cleaning is done, we now have a dataframe with  24878 rows and 211 columns.

Below is the first 5 rows for our cleaned dataframe:

<h3 id = "2.2">Feature of data: Visualization</h3>
Univariate Analysis

<iframe src="asset/Top_Champion.html"  width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/Mid_Champion.html"  width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/Jng_Champion.html" width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/bot_Champion.html" width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/sup_Champion.html" width="800" height="600" frameborder="0"> </iframe>

<iframe src="asset/diff10m.html" width="800" height="600" frameborder="0"> </iframe>
<iframe src="asset/diff15m.html" width="800" height="600" frameborder="0"> </iframe>

In the univariate analysis, we analyze the frequency use of differnt champion character in the five different position: top, mid(middle), bot(bottom), jng(jungle), sup(support). 

<h3 id = "2.3">Pivot Table: Does side matter?</h3>



<h2 id = "3"> Assessment of Missingness </h2>
<h3 id = "3.1"> NMAR analysis </h3>
<h3 id = "3.2"> Missing Dependency </h3>



Our observed statistic was: 0.9923034634414515

Our p-value was: 0.0

Here is the empirical distribution of the test statistic:



<h2 id = "4"> Hypothesis Testing </h2>
**Null hypothesis:** The distribution of "team_golddiffat15" for the winning team is the same as the distribution of "team_golddiffat15" for the losing team.

**Alternative hypothesis:** The distribution of "team_golddiffat15" for the winning team is different than the distribution "team_golddiffat15" for the losing team.

**Test Statistic:** We will be using []
  * We chose to use [] because [].

**Significance Level:** 5% (0.05)
  * We choose this significance level because []

**P-value:** []
  * We did [] simulations

**Conclusion:** []

'''
~~subnote: delete after read!!
~~never use language that implies an absolute conclusion, since we are performing statistical tests and not randomized controlled trials, we cannot prove that either hypothesis is 100% true or false~
~~Justify why these choices are good choices for answering the question you are trying to answer.
'''
[put the visualization of our hypothesis test here]

<h2 id = "5"> Framing a Prediction Problem </h2>
Building on previous exploration of [to fill in], we want to fo futher on the factors that affect game outcomes. Specifically, we want to predict the game "result" by utilizing statistical data from the 10 and 15-minute marks, the chosen ten champions, team ID, and player ID. This presents a binary classification problem, where our goal is to accurately forecast the match result based on these variables.

<h2 id = "6"> Baseline Model </h2>
Our baseline model is a classifier model based on logistic regression. It will process one-hot encoding on the team side(blue and red) imformation, using the quantatitive data directly and fit into a logistic regression model with high regularization parameter. 

We have 12 quantitative feature "team_xpdiffat15", "top_xpdiffat15", "mid_xpdiffat15", "jng_xpdiffat15", "bot_xpdiffat15", "sup_xpdiffat15", "team_golddiffat15", "top_golddiffat15", "mid_golddiffat15", "jng_golddiffat15", "bot_golddiffat15", "sup_golddiffat15", "result"; 0 ordinal feature and 1 nominal feature "side" used. 

Since categotrivcal data like "side" cannot be fed directly into logistic regression models. We one-hot encoded the "side" column, where we represneted the "blue" side with a value of 1 and the "red" side with a value of 0. This ensuring that the logistic regression model can accurately interpret and utilize the categorical information without assuming any ordinal relationship between categories. 

[confusion matrix]

The performance of our current model has an accuracy rate of approximately 71%. We believe it is relatively good but have more space to improve, especially considering the impact imposed by missing data. The prevalence of missing values in critical statistical data, particularly when entire rows of data are absent due to unreported metrics like kills, deaths, assists, and experience from certain matches, sinificantly reduces the model's ability to accurately predict outcomes based on incomplete data. 

To further enhance our model's accuracy, we can diversifying the feature set with additional predictive variables that are less susceptible to missingness. Specifically, we can incorporating champion selected by the ten players and the team's ID as classification features.

 <h3 id = "6.1"> Feature Statement</h3>
nominal,ordinal,quantitive
 <h3 id = "6.2"> Model Description </h3>
 <h3 id = "6.3"> Performance Evalution </h3>
 <h3 id = "6.4"> Conclusion </h3> 
 
<h2 id = "7"> Final Model </h2>
To improve upon out baseline model, we added the champions choosen by the ten players and the team IDs different teams exhibit varying win rates, attributed to the distinct strengths, adaptability, and the synergies or counterplays of their chosen champions.

 <h3 id = "7.1"> New Features in Final Model </h3>
 <h3 id = "7.2"> Model Algorithm and hyperparameters </h3>

### Model selection
We choose a stacking model based on **one logistics regression** and **one gradient boosting tree**. This decison come with the following consideration:

 1. Categorical features solution: The features include categorical data with high cardinality, which posed the risk of **Curse of Dimensionality** if directly use one-hot encoding. To mitigate this and use these high-cardinality categorical data, we applied a **boundary-based one-hot encoder** to filter infrequently chosen categories, followed by **PCA** for dimensionality reduction and pivotal component extraction. Then, we implemented **Bayesian target encoding** to transform categorical data into numerical values reflective of win probabilities. These strategy will effectively enhancing the model's interpretative power regarding the high cardinality caused by the categorical data. 

2. Quantitative features solution: For numerical data, we utilized **logistic regression with a high regularization parameter and a tree model**, this can ensure that our model will not fall into potential multicollinearity issues as the two methos has an insensitivity to collinearity.

### Finding best hyperparameter

PCA_components: 600
logistic regression parameter: C = 0.1

graidient boosting tree parameter: min_samples_leaf = 40,max_leaf_nodes = 15,max_depth = 20,learning_rate = 0.05

### Finding hyperparameters
Finding optional hyperparameter is cruical for model perfoermance, in our model, we will utilize the following hyperparamater:
* PCA components: this parameter specifies the number of principal components retained after PCA. This balance is important for reducing dimensionality while preserving important variance in the data.
* Logistic regression parameter(C): this parameter controls the regularization strength in logistic regression. A lower value use more regularization to prevent overfitting while higher value  make model more flecible to capture complex patterns.
* Graidient boosting tree parameter: 
    * min_samples_leaf: this parameter minimizes overfitting by specifying the minimum number of samples required to be at a leaf node. A higher number will leads to more generalized models.
    * max_leaf_nodes: this parameter controls the growth of the tree by limiting the maximum number of leaf nodes, it regulate model complexity
    * max_depth: this parameter specifies the maximum depth of individual trees. It prevent the model to become too complex and overfit to the training data.
    * learning_rate: this parameter scales the contribution of each tree. A lower learning rate requires more trees to model the relationships effectively

The method used to select the hyperparameters is cross_validation on a  5-fold test, with the average F1 score as the metric to perform grid search. After running GrideSearchCV, the best hyperparameters are the following:
* PCA components: 600. 
* Logistic regression parameter(C): 0.1 
* Graidient boosting tree parameter: 
    * min_samples_leaf: 40
    * max_leaf_nodes: 15
    * max_depth: 20
    * learning_rate: 0.05

### Model performance
Compared to the baseline model, our final model has a improvemnet of over 2% in F1 scores, particularly in contexts with missing statistical data. Using a stacked model, which integrate logistic regression and gradient boosting trees, has improve the model's capacity to capture complex relationships within the data, thus further boosting its predictive power.

 <h3 id = "7.3"> The Improvement compared to Baseline </h3>
 
<h2 id = "8"> Fairness Analysis </h2>
With a refined predictive model with an even better level of accuracy, we now want to access its fairness. This critical evaluation will ensure that our model does not disadvantage any group of players or teams based on arbitrary criteria. We define the 1 to perdition result that are correct and 0 to perdition result that are wrong. 

**Group X**: `league`

**Group Y**: `correctness of our model's prediction` (1: correct, 0: wrong)

**Evaluation metric**: permutation test

**Null Hypothesis**: The distribution of correct and incorrect classification results **is consistent** across all leagues.

**Alternative Hypothesis**: The distribution of correct and incorrect classification results is **not consistent** across all leagues.

**Test Statistic**: total variation distance

**Significant level**: 0.01

<iframe src=" " width=800 height=600 frameBorder=0></iframe>

The analysis resulted in a p-value of 0.0. Since the p-value is less than the threshold 0.01, we **reject** the null hypothesis. This lead to the conclusion that our model **demonstrates unfairness** in terms of prediction accuracy across different leagues. This discrepancy is likely attributable to the distribution of missing data (which are mainly on data with the league DCcup, LPL and LDL).


