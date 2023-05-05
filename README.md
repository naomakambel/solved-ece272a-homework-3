Download Link: https://assignmentchef.com/product/solved-ece272a-homework-3
<br>
This is the third homework assignment to get you familiar with the machine learning tools. We’re introducing another type of machine learning algorithm, which is unsupervised learning. Specifically, we are performing outlier detection with unsupervised learning.

Recall that you went to the employee party last Friday, and you won the wine tasting competition. As a reward, you earned a week of paid vacation. But, due to COVID-19, you have nowhere to go so you are just laying on the couch, watching Netflix. All of sudden you receive a message from your NBA team manager friend and the conversation goes like this:

<h1>1           Dataset</h1>

<strong>Ensure you’ve download the latest version of the data set from Piazza</strong>

We are using data from the <em>Basketball Reference </em>website, a data set related to NBA player in the 2020-2021 season. For more details, consult:

<a href="https://www.basketball-reference.com/leagues/NBA_2021_per_game.html">https://www.basketball-reference.com/leagues/NBA_2021_per_game.html</a><a href="https://www.basketball-reference.com/leagues/NBA_2021_per_game.html">.</a>

The file is provided in a format known as Comma Separated Values (CSV). You can open it as raw text to take a look! The data have 30 columns of features describing the players. These fields come in strings, integers, and floating-point numbers. This data set does have missing values.

This dataset doesn’t contain any labels because it is meant for unsupervised learning.

You can use any method to load in the CSV file. Refer to the <em>Getting Started </em>guide if you are not sure about this step.

<h1>2           Recommended Flow</h1>

<ol>

 <li>Make a function to load the data.</li>

 <li>Clean the dataset so that all string entries and missing values are convertedto floating-point numbers.</li>

 <li>Make a function to plot the data, to see the distribution of each feature.(Hint: Histogram and Cumulative distribution function (CDF).) Identify three important features. (Hint: If you don’t know which features are important, you can try the 3 features mentioned in the introduction.) Approximate the percentage of outlier samples.</li>

 <li>Make a function to alter/preprocess the data (delete the features that arenot important, normalize the data, and so-on…)</li>

 <li>Train an Outlier Detection model.</li>

 <li>Score each player based on the model’s outlier score. Identify the topthree outliers.</li>

 <li>Verify the top three outliers by plotting the player’s feature values ontothe graphs from step 3. Check the location of the top 3 outliers with a 3-D scatter plot (the axes of the plot should be the three selected features from step 3.)</li>

 <li>Save the outlier scores and the plots used to verify the top three outliers.</li>

 <li>Repeat the previous steps until satisfied.</li>

</ol>

<h1>3           Problem Formulation</h1>

<table width="496">

 <tbody>

  <tr>

   <td width="53"><strong>Input</strong></td>

   <td width="100"><strong>Data Type</strong></td>

   <td width="343"><strong>Description</strong></td>

  </tr>

  <tr>

   <td width="53">Rk</td>

   <td width="100">Integer</td>

   <td width="343">Rank Based on Last Name</td>

  </tr>

  <tr>

   <td width="53">Player</td>

   <td width="100">String</td>

   <td width="343">Name of the NBA Player</td>

  </tr>

  <tr>

   <td width="53">Pos</td>

   <td width="100">String</td>

   <td width="343">Position of the NBA Player</td>

  </tr>

  <tr>

   <td width="53">Age</td>

   <td width="100">Integer</td>

   <td width="343">Age of the NBA Player</td>

  </tr>

  <tr>

   <td width="53">Tm</td>

   <td width="100">String</td>

   <td width="343">Team of the NBA Player</td>

  </tr>

  <tr>

   <td width="53">G</td>

   <td width="100">Integer</td>

   <td width="343">Number of Games Played</td>

  </tr>

  <tr>

   <td width="53">GS</td>

   <td width="100">Integer</td>

   <td width="343">Number of Games Started with the Player on the Court</td>

  </tr>

  <tr>

   <td width="53">MP</td>

   <td width="100">Floating-Point</td>

   <td width="343">Minutes Played Per Game</td>

  </tr>

  <tr>

   <td width="53">FG</td>

   <td width="100">Floating-Point</td>

   <td width="343">Field Goals Per Game</td>

  </tr>

  <tr>

   <td width="53">FGA</td>

   <td width="100">Floating-Point</td>

   <td width="343">Field Goals Attempts Per Game</td>

  </tr>

  <tr>

   <td width="53">FG%</td>

   <td width="100">Floating-Point</td>

   <td width="343">Field Goal Percentage</td>

  </tr>

  <tr>

   <td width="53">3P</td>

   <td width="100">Floating-Point</td>

   <td width="343">3-Point Field Goals Per Game</td>

  </tr>

  <tr>

   <td width="53">3PA</td>

   <td width="100">Floating-Point</td>

   <td width="343">3-Point Field Goals Attempts Per Game</td>

  </tr>

  <tr>

   <td width="53">3P%</td>

   <td width="100">Floating-Point</td>

   <td width="343">3-Point Field Goal Percentage</td>

  </tr>

  <tr>

   <td width="53">2P</td>

   <td width="100">Floating-Point</td>

   <td width="343">2-Point Field Goals Per Game</td>

  </tr>

  <tr>

   <td width="53">2PA</td>

   <td width="100">Floating-Point</td>

   <td width="343">2-Point Field Goal Attempts Per Game</td>

  </tr>

  <tr>

   <td width="53">2P%</td>

   <td width="100">Floating-Point</td>

   <td width="343">2-Point Field Goal Percentage</td>

  </tr>

  <tr>

   <td width="53">eFG%</td>

   <td width="100">Floating-Point</td>

   <td width="343">Effective Field Goal Percentage</td>

  </tr>

  <tr>

   <td width="53">FT</td>

   <td width="100">Floating-Point</td>

   <td width="343">Free Throws Per Game</td>

  </tr>

  <tr>

   <td width="53">FTA</td>

   <td width="100">Floating-Point</td>

   <td width="343">Free Throws Attempts Per Game</td>

  </tr>

  <tr>

   <td width="53">FT%</td>

   <td width="100">Floating-Point</td>

   <td width="343">Free Throw Percentage</td>

  </tr>

  <tr>

   <td width="53">ORB</td>

   <td width="100">Floating-Point</td>

   <td width="343">Offensive Rebounds Per Game</td>

  </tr>

  <tr>

   <td width="53">DRB</td>

   <td width="100">Floating-Point</td>

   <td width="343">Defensive Rebounds Per Game</td>

  </tr>

  <tr>

   <td width="53">TRB</td>

   <td width="100">Floating-Point</td>

   <td width="343">Total Rebounds Per Game</td>

  </tr>

  <tr>

   <td width="53">AST</td>

   <td width="100">Floating-Point</td>

   <td width="343">Assists Per Game</td>

  </tr>

  <tr>

   <td width="53">STL</td>

   <td width="100">Floating-Point</td>

   <td width="343">Steals Per Game</td>

  </tr>

  <tr>

   <td width="53">BLK</td>

   <td width="100">Floating-Point</td>

   <td width="343">Blocks Per Game</td>

  </tr>

  <tr>

   <td width="53">TOV</td>

   <td width="100">Floating-Point</td>

   <td width="343">Turnovers Per Game</td>

  </tr>

  <tr>

   <td width="53">PF</td>

   <td width="100">Floating-Point</td>

   <td width="343">Personal Fouls Per Game</td>

  </tr>

  <tr>

   <td width="53">PTS</td>

   <td width="100">Floating-Point</td>

   <td width="343">Points Per Game</td>

  </tr>

 </tbody>

</table>

Your task is to build an outlier model to identify the outlier players in the given CSV. An outlier player can be an extremely good player or an extremely bad player depending on which side of the spectrum the player’s stats lie on the distribution graphs.

You are required to use the Python scikit-learn library to construct your models. You are required to use the following three methods:

<ul>

 <li><strong>One Class Support Vector Machine (SVM)</strong></li>

 <li><strong>Elliptic Envelope</strong></li>

 <li><strong>Isolation Forest</strong></li>

</ul>

However, you can experiment with any other algorithms you find interesting! Link to the documentation for more methods is available on (<a href="https://scikit-learn.org/stable/modules/outlier_detection.html"><strong>Outlier </strong></a><a href="https://scikit-learn.org/stable/modules/outlier_detection.html"><strong>Detection in SciKit Learn</strong></a><a href="https://scikit-learn.org/stable/modules/outlier_detection.html">)</a>

For every algorithm, train it on the data and give an outlier score to each player. Identify the outlier players, based on the outlier model’s scores. Then, pick the top three outliers and verify that they are indeed an outlier by using the CDF plot and the 3D scatter plot. Make a new CSV file, <em>MODEL NAME </em><em>Scores.csv</em>, with two columns, the player’s name and the player’s outlier score. The CSV should be <strong>sorted from min to max </strong>based on the player’s outlier score. Submit the CSV files with your report.

You also must write a brief report answering the following questions: • <strong>Describe in your own words what are Outlier Detection and Novelty Detection. </strong>And, how are they different? (Hint: training samples) Does our current problem belong to Outlier Detection or Novelty Detection and why?

<ul>

 <li><strong>Explain the data preprocessing/transformation methods you applied.</strong></li>

 <li><strong>Show the distribution of the feature values. </strong>Use histogram (Number of Occurrences vs Feature Values) and CDF (Percentage of Player vs Feature Values). Pick three features to train your models. Approximately, how many percent of the players are outliers, and how did you come to that conclusion based on the plots?</li>

 <li><strong>Describe in your own words how each of the three algorithms creates a model. </strong>How do the model decide the boundary between inliers and outliers? How are the outlier scores calculated? Explain your choice of hyperparameters if any.</li>

 <li><strong>For each algorithm, pick the top three outliers, verify that they are indeed an outlier, and check whether the player is an outlier due to being bad or being good </strong>Explain your reasoning with the model’s outlier scores and the CDF plots.</li>

 <li><strong>For each algorithm, show a 3-D scatter plot marking the inliers, outliers, and the top three outliers data points. </strong>Describe how the inlier region different from the outlier region.</li>

 <li><strong>Could this model be used to predict outlier players in the next season? </strong>Justify your answer and state your assumptions.</li>

</ul>