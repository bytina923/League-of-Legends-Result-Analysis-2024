<h1 id = "0"> League-of-Legends-Result-Analysis-2024 </h1>
<ul>
<a href = "#1"> Introduction </a><br>
<a href = "#2"> Data Cleaning and Exploratory Data </a><br>
<a href = "#3"> Assessment of Missingness </a><br>
<a href = "#4"> Hypothesis Testing </a><br>
<a href = "#5"> Framing a Prediction Problem </a><br>
<a href = "#6"> Baseline Model </a><br>
<a href = "#7"> Final Model </a><br>
<a href = "#8">Fairness Analysis</a><br>
</ul>
 
<h2 id = "1"> Introduction </h2>

<h3 id = "1.1"> Description of League-of-Legends </h3><br>
Welcome to the adventure of Summoner's Rift, the heart of League of Legends, where strategy and skill stand between victory and defeat in one of the world's most famous multiplayer online battle arena video games. With millions of players engaging in this digital battleground, understanding the vast array of game data available is not only a matter of curiosity, but essential for players who wish to hone their skills and achieve mastery over the game. In this analysis, we aims to explore the rich tapestry of game data, seeking to unveil the pivotal factors that sway the tide of battle and shape the outcome of each match.

<h3 id = "1.1"> Introduction of Dataset </h3><br>
Our dataset contains informations of players and teams from over 10,000 League of Legends competitive matches from 2022, providing a comprehensive look at the dynamics at play. Each match unfolds across 12 rows of data, capturing the essence of both teams: five players row and one summary row for each team, across more than 100 columns with virtually all the data that can be collected from a game. When we cleaned out our dataset, we will be left with 45 columns with 3 major categories: 
1. id and name: these columns contains the playerID, teamID, player names and team names.
2. Ban-Pick information: these columns contains the champions ban or picked by each team in the competitions
3. statistics data in the 10/15 minutes: these columns is about the kill,death,assistsat,gold,experiences for each players and whole teams in 10/15 minutes.
And, the "result" column which indicates whether a team win or lose in the competition. 

<h3 id = "1.2"> Our Research Question </h3><br>
Our project center around the question: "To what extent does the experience and gold differences between teams impact the match results?" The significance of this question lies in its ability to uncover strategic elements that are critical to victory, offering valuable insights into effective gaming strategies for diverse audiences. Competitive players and esports professionals can use these insights to refine their tactics. Likewise, game developers and designers might find the outcomes beneficial for future game development, balancing, and enhancing player engagement. The columns that are relevant to answer the question are golddiffat10,xpdiffat10,golddiffat15,xpdiffat15. 

<table>
 <tr>
  <th> column name </th>
    <th> Description </th>
 </tr>
 <tr>
  <th> golddiffat10 </th>
    <th> The gold difference between one player and his rival at 10 minutes in games </th>
 </tr>
 <tr>
  <th> golddiffat15 </th>
    <th> The gold difference between one player and his rival at 15 minutes in games </th>
  </tr>
 </tr>
  <th> xpdiffat10 </th>
    <th> The experience difference between one player and his rival at 10 minutes in games </th>
 </tr>
 </tr>
  <th> xpdiffat15 </th>
    <th> The experience difference between one player and his rival at 15 minutes in games </th>
  </tr>
 
</table>

<h2 id = "2"> Data Cleaning and Exploratory Data </h2>
Our dataset initially features 123 columns, many of which are not pertinent to our analysis. To streamline our data and focus on the most impactful variables, we will selectively remove the extraneous columns and keep only relevent features. After the removing process, We are left with 45 essential columns that are directly relevant to our analytical objectives.
<h3 id = "2.1">Data Cleaning</h3>
<h3 id = "2.2">Feature of data: Visualization</h3>
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
<h2 id = "6"> Baseline Model </h2>
 <h3 id = "6.1"> Feature Statement</h3>
nominal,ordinal,quantitive
 <h3 id = "6.2"> Model Description </h3>
 <h3 id = "6.3"> Performance Evalution </h3>
 <h3 id = "6.4"> Conclusion </h3>
<h2 id = "7"> Final Model </h2>
 <h3 id = "7.1"> New Features in Final Model </h3>
 <h3 id = "7.2"> Model Algorithm and hyperparameters </h3>
 <h3 id = "7.3"> The Improvement compared to Baseline </h3>
<h2 id = "8"> Fairness Analysis </h2>
