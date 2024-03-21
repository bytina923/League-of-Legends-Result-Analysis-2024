# League-of-Legends-Result-Analysis-2024
* [Introduction](#1)
* [Data Cleaning and Exploratory Data](#2)
<h2 id = "1"> Introduction <\h2>
Welcome to the adventure of Summoner's Rift, the heart of League of Legends, where strategy and skill stand between victory and defeat in one of the world's most famous multiplayer online battle arena video games. With millions of players engaging in this digital battleground, understanding the vast array of game data available is not only a matter of curiosity, but essential for players who wish to hone their skills and achieve mastery over the game. In this analysis, we aims to explore the rich tapestry of game data, seeking to unveil the pivotal factors that sway the tide of battle and shape the outcome of each match.

Our dataset contains informations of players and teams from over 10,000 League of Legends competitive matches from 2022, providing a comprehensive look at the dynamics at play. Each match unfolds across 12 rows of data, capturing the essence of both teams: five players row and one summary row for each team, across more than 100 columns with virtually all the data that can be collected from a game. When we cleaned out our dataset, we will be left with 45 columns with n major catefories: [].

Our project center around the question: "How do experience and gold differences between teams impact the match results?" The significance of this question lies in its ability to uncover strategic elements that are critical to victory, offering valuable insights into effective gaming strategies for diverse audiences. Competitive players and esports professionals can use these insights to refine their tactics. Likewise, game developers and designers might find the outcomes beneficial for future game development, balancing, and enhancing player engagement. The columns that are relevant to answer the question are [ ]. We chose these columns because [ ].

[descriptions of those relevant columns (in table format)]

<h2 id = "2"> Data Cleaning and Exploratory Data <\h2>
Our dataset initially features 123 columns, many of which are not pertinent to our analysis. To streamline our data and focus on the most impactful variables, we will selectively remove the extraneous columns and keep only relevent features. After the removing process, We are left with 45 essential columns that are directly relevant to our analytical objectives.


<h2 id = "3"> Assessment of Missingness <\h2>



Our observed statistic was: 0.9923034634414515

Our p-value was: 0.0

Here is the empirical distribution of the test statistic:



<h2 id = "4"> Hypothesis Testing <\h2>
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

<h2 id = "5"> Framing a Prediction Problem <\h2>
<h2 id = "6"> Baseline Model <\h2>
<h2 id = "7"> Final Model <\h2>
<h2 id = "8"> Fairness Analysis <\h2>
