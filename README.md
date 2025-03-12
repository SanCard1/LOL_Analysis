<html lang="en">
<body>
    <div class="container">
        <h1>League of Legends Analysis: Race to the Nexus</h1>
	<h2>by Santiago Cardenas Rey and Michael Luo</h2>
	<h3>Step 1: Description</h3>
        <p>We chose the league of legends dataset for this project because it provides a rich and dynamic set of variables that allow for meaningful hypothesis testing and predictive modeling. The dataset includes key performance metrics such as damage per minute, kills, assists, deaths, and game results which enable various statistical analyses. Unlike structured datasets like recipes or power outages, this dataset introduces human decision-making and variability, making the analysis more complex and engaging. Since I have an interest in gaming and data-driven insights, working with this dataset makes the project both enjoyable and intellectually stimulating. Fellow gamers may relate to what we are assessing to best determine the performance of players based on what kind of player they are or coe across (i.e. ADC bot or mid-lane player). League of Legends (LoL) is a highly competitive esport with a global fanbase, featuring professional teams battling across various leagues and tournaments. Each role within a team has a distinct responsibility, but two of the most crucial damage-dealing roles are ADC (Attack Damage Carry) and Mid Laner. These roles often dictate the outcome of fights and matches, making their performance a key aspect of a team's success.
One of the most important metrics in evaluating a player's impact is damage per minute per deaths + 1 (DPM / (Deaths + 1)), which adjusts raw damage output by factoring in survivability. This statistic can help determine which role exerts more influence in professional play.
Our central question is:
Which role—ADCs or Mid Laners—carries their team more often based on DPM / (Deaths + 1)?
By analyzing professional match data, we aim to uncover whether ADCs or Mid Laners consistently contribute more adjusted damage and assess how this impacts team success. Understanding this can provide insights into optimal team compositions, strategic drafting, and in-game decision-making.
</p>
	<p> The dataset contains 97,980 rows after filtering out team summary data, focusing solely on individual player statistics. Below are the key columns relevant to our analysis:
</p>
</body>
	<ul>
	    <li>gameid:  A unique identifier for each match played.</li>
	    <li>position: The role played by an individual player within their team composition. The roles include top, jungle, mid, bot(ADC), and support.</li>
	    <li>dpm (Damage per Minute): The amount of damage a player deals per minute. This is the base metric we will use to evaluate player performance, which will later be adjusted using deaths.</li>
	    <li>kills: The number of enemy champions a player successfully eliminated during the match.</li>
	    <li>deaths: The number of times a player was eliminated by enemy champions.</li>
	    <li>assists: The number of assists credited to a player, indicating instances where they contributed to eliminating an enemy champion without securing the kill themselves.</li>
	    <li>result: This column indicates the outcome of a match for a specific player's team. 1 represents a win, while 0 represents a loss.</li>
	    <li>league: The specific league tournament in which the match took place.</li>
		<li>effectiveness: Column created calculated using damage per minute / (deaths + 1)</li>
	</ul>
<body>
    <div>
        <h3>Step 2: Data Cleaning and Exploratory Data Analysis</h3>
        <h4>Data Cleaning</h4>
        <p>We first only keep the relevant columns: <code>gameid</code>, <code>position</code>, <code>dpm</code>, <code>kills</code>, <code>deaths</code>, <code>assists</code>, <code>result</code>, <code>league</code>. In this dataset, each game has 12 rows, with 10 rows representing each of the players and 2 rows for summarizing the overall team performance and result (i.e. team summary rows). We removed the 2 rows for each game that summarized the overall team performance, which brought the initial number of rows from 117,576 to 97,980. We then dropped all the rows that had missing values and found out that it was the same as without dropping, so our data doesn't have any rows with missing data.</p>
		<p>Below is the head of our league_clean dataframe.</p>
		<img src="head_cleaned.png" alt="head_cleaned.png" width="600">
		<img src="dpm_distribution.png" alt="DPM Distribution Histogram" width="600">
        <p>We performed univariate analysis on the distribution of DPM, which is almost normal with a slight right skew. This shows that the data is well-behaved, where most players deal moderate damage, while fewer achieve very high DPM, which is typical of gaming scenarios. The box plot above the histogram shows several outliers on the right-hand side. These represent exceptionally high DPM performances, likely from players who dominated the game or played specific high-damage champions.</p>
		<img src="bivariateanalysis_distribution.png" alt="bivariateanalysis_distribution.png" width="600">
		<p>The box plot represents a bivariate analysis of effectiveness (DPM / (Deaths + 1)) across different roles in League of Legends, allowing us to compare how different positions contribute to sustained damage while accounting for deaths. This analysis highlights clear trends: bot lane (ADC) and mid lane exhibit the highest median effectiveness, suggesting that these roles tend to have the most impact in terms of damage output. The jungle and support roles generally have lower effectiveness, with supports showing the lowest median and least spread, aligning with their more utility-focused playstyle. The presence of extreme outliers, especially in ADC and mid, suggests that performance in these roles can vary significantly, possibly influenced by champion picks, game state, or player skill.</p>
		<img src="grouped_data.png" alt="grouped_data.png" width="600">
		<p>We first grouped the cleaned dataset by position and then calculated the mean and median of all key statistics. By comparing player performance across different roles, we gained a clearer understanding of how each position contributes to the game. Mid and Bot lane players have the highest DPM and effectiveness scores, reinforcing their roles as primary damage dealers. Support players have the lowest DPM and kills but lead in assists, highlighting their role in enabling teammates. Jungle players balance kills and assists, as they frequently roam to support other lanes. Top lane maintains moderate stats across all metrics, indicating a mix of durability and damage potential. This grouping helped visualize the distinct impact each position has on overall gameplay.</p>
    </div>
</body>
	<div>
		<h3>Step 3: Assessment of Missingness</h3>
	</div>
	<div>
		<p><b>playername</b>: MD (Missing by Design)</p>
		<ul>
			<li><b>playername</b> is missing by design since you can take a look at the <b>position</b> column and if you see the value "team" then you can predict with certainty that the <b>playername</b> value is going to be null.</li>
		</ul>
	</div>
	<div>
		<p><b>playerid</b>: MD (Missing by Design)</p>
		<ul>
			<li><b>playerid</b> is missing by design since you can take a look at the <b>playername</b> column and if you see a null value then you can predict with certainty that the <b>playerid</b> value is going to be null.</li>
		</ul>
	</div>
	<div>
		<p>We conclude our assessment of missingness analysis by stating that <b>among our relevant columns</b> we found no column that has null values, therefore it is impossible to find any columns that are <b>NMAR</b> and/or <b>MAR</b>.</p>
	</div>
	<div>
		<h3>Step 4: Hypothesis Testing</h3>
	</div>	
	<div>
		<h4><b>Null Hypothesis</b><h4>
	</div>
	<div>
		<p>The mean carry potential (measured as Damage Per Minute / (Deaths + 1)) is the same for mid-lane and ADC (bot-lane) players.</p>
	</div>
	<div>
		<h4><b>Alternative Hypothesis</b></h4>
	</div>
	<div>
		<p>The mean carry potential is higher for mid-lane players than for ADC players.</p>
	</div>
	<div>
		<h4><b>Test Statistic</b><h4>
	</div>
	<div>
		<p>The test statistic will be the <u>observed difference</u> in means of carry potential between mid-lane and ADC players.</p>
	</div>
	<div>
		<h4><b>Significance Level</b></h4>
	</div>
	<div>
		<p>The significance level will be <b>0.05</b> as we understand there can be some variation among both types but for the null hypothesis, there should be a clear difference.</p>
	</div>
	<div>
		<h4><b>p-value</b></h4>
		<u><i>1.0</i></u>
	</div>
	<div>
		<h4><b>Results</b></h4>
		<p>To perform the permutation test, we first calculated the observed difference in mean carry potential (effectiveness) between mid-lane and ADC players. This provided the baseline difference we aimed to test. Next, to simulate the null hypothesis, we randomly shuffled the effectiveness values across all players, ensuring that any inherent role-based differences were removed. We then reassigned these shuffled values to the mid-lane and ADC groups while maintaining their original sample sizes and recalculated the difference in means. This process was repeated 1000 times to generate a distribution of permuted differences under the assumption that there is no true difference between the roles. The p-value was computed as the proportion of these permuted differences that were greater than or equal to the observed difference.</p>
	</div>
	<div>
		<h4><b>Justifications</b></h4>
		<img src="hypothesis_test_results.png" alt="hypothesis_test_results.png" width="600">
		<p>Based on the hypothesis test performed, with a p-value of 1.000, we fail to reject the null hypothesis. This suggests that the observed difference in carry potential is entirely consistent with what we would expect under random chance. The histogram shows that the observed difference in means (-14.761) lies well within the range of the permuted distribution, meaning there is no statistical evidence to suggest that mid-lane players have a higher mean carry potential than ADC players. This result implies that the differences in carry potential between these roles may be due to normal game variations rather than an inherent positional advantage.</p>
	</div>
	<div>
		<h3>Step 5: Framing a Prediction Problem</h3>
	</div>
	<div>
		<p><b><u>Prediction Problem</u></b>: We want to identify the role of the player given their post-game data. This will imply for us to do a <u>classification model</u>.</p>	
		<p><b><u>Type of Classification</u></b>: multiclass classification. Some columns have non-binary data but are yet numeric (some columns are binary too), thus a suitable task for a multiclass classification.</p>
		<p><b><u>Response Variable</u></b>: since we are figuring the position of the player with the given player's match statistics, the response variable is <b><u>position</u></b>.</p>
		<p><b><u>Motivation</u></b>: The motivation behind this is to identify the patterns, statistics, strengths, weaknesses, and behaviors of distinct player positions. By using match performance statistics, we can inform people as to how different kind of players behave in the match (i.e. suppose a player is type 1, then we would be able to have a solid understanding of the player's skills and preferences such as firstblood count or damage per minute or even player location patterns). In here we are prioritizing previous match statistics and outcomes to predict future matches where the players have known positions (reverse causality).</p>
		<p><b><u>Standard Metric</u></b>: We will be using prediction accuracy as our standard metric. The purpose of this is to assess how accurate our model is in predicting position of players given their match performance statistics. This would lead for players in future matches to have a proportional level of confidence (to classification accuracy) in expected behavior of given position players.</p>
	</div>
	<div>
		<h3>Step 6: Baseline Model</h3>
	</div>
	<div>
		<p>For the baseline model, we used a <b>Random Forest Classifier</b>, with the following six features: <b>kills, deaths, dpm_per_death, teamkills, monsterkills, and minionkills</b>.</p>
    <p>All six features are <b>quantitative</b>:</p>
    <table>
        <tr>
            <th>Features</th>
            <th>Type</th>
            <th>Encodings</th>
        </tr>
        <tr>
            <td>kills</td>
            <td>Numeric</td>
            <td><b>StandardScaler</b></td>
        </tr>
        <tr>
            <td>deaths</td>
            <td>Numeric</td>
            <td><b>StandardScaler</b></td>
        </tr>
        <tr>
            <td>dpm_per_death</td>
            <td>Numeric</td>
            <td><b>StandardScaler</b></td>
        </tr>
        <tr>
            <td>teamkills</td>
            <td>Numeric</td>
            <td><b>StandardScaler</b></td>
        </tr>
        <tr>
            <td>monsterkills</td>
            <td>Numeric</td>
            <td><b>StandardScaler</b></td>
        </tr>
        <tr>
            <td>minionkills</td>
            <td>Numeric</td>
            <td><b>StandardScaler</b></td>
        </tr>
    </table>
    <p>We applied the <b>StandardScaler Transformer</b> to normalize all numerical features. This step ensures that differences in game length do not disproportionately influence the model, as players in longer matches accumulate more statistics, making direct comparisons unfair.</p>
	<img src="model_results.png" alt="model_results.png" width="600">
	<p>Our model achieved an overall accuracy of 67.53%, with varying performance across different roles. The highest precision, recall, and F1-score were observed for the jng (jungle) role, achieving a perfect score of 1.00, indicating that the model identified jungle players with complete accuracy. Similarly, the sup (support) role performed well, with an F1-score of 0.96, suggesting strong classification ability. However, performance was lower for bot (bottom), mid (middle), and top (top lane) roles, with F1-scores ranging from 0.40 to 0.53, indicating greater misclassification in these categories. The macro and weighted averages align closely with overall accuracy, reinforcing that while the model performs well on some roles, it struggles with others, particularly mid and bot.</p>
	</div>
		<h3>Step 7: Final Model</h3>
		<p>In our final model, we added three new features: kill participation and gold efficiency, along with including wards placed as a feature. We introduced these features because they provide valuable insights into a player's role in the game. Kill participation captures how involved a player is in team fights by measuring the proportion of team kills they contributed to through kills or assists. This is particularly important for differentiating between roles like support, which has high assist numbers, and jungle, which is heavily involved in team fights. Gold efficiency was introduced to reflect how effectively a player converts earned gold into performance while penalizing deaths. This is useful for distinguishing between roles like bot lane carry, which aims for high gold efficiency, and mid, which may take more risks for solo plays. Additionally, wards placed was incorporated to help separate mid and support roles, as supports typically place more wards than other positions.</p>
    	<p>Our final model continues to use a Random Forest Classifier, consistent with our baseline model. Since all of our newly added features are numerical, we applied a StandardScaler transformation to ensure fair weighting. We then used GridSearchCV with a 5-fold cross-validation to optimize three key hyperparameters:</p>
    <ul>
        <li><strong>n_estimators</strong> (100, 200): Controls the number of trees in the forest.</li>
        <li><strong>max_depth</strong> (None, 10, 20): Limits the depth of each tree to prevent overfitting.</li>
        <li><strong>min_samples_split</strong> (2, 5): Determines the minimum number of samples required to split a node.</li>
    </ul>
    	<p>After tuning, we identified the best combination of hyperparameters and trained our final model accordingly.</p>
    <h6>Results</h6>
    <p>The final model achieved an accuracy of 0.6989, marking an improvement from the baseline model's accuracy of 0.6753.</p>
    <p>From the classification report, we observed:</p>
    <ul>
        <li>Notable improvements in precision and recall for the top lane role (f1-score increased from 0.53 to 0.59).</li>
        <li>Bot and mid roles continue to be challenging to separate, though slight improvements were made.</li>
        <li>Jungle and support roles remain highly distinguishable with near-perfect precision and recall.</li>
    </ul>
		<img src="confusion_matrix.png" alt="confusion_matrix.png" width="600">
    <p>The confusion matrix highlights that most misclassifications still occur between bot and mid lanes. Despite these challenges, the improved feature engineering and hyperparameter tuning resulted in a more robust classification model.</p>
</body>
<body>
	<div>
		<h3>Step 8: Fairness Analysis</h3>
	</div>
	<div>
		<p>Since our model is doing a multi-class classifier predicting the five categories, we see that it has done a good job on identifying <code>'jng'</code> and <code>'sup'</code> but is inconsistent with <code>'bot'</code>, <code>'mid'</code>, and <code>'top'</code> player types. Considering this nature we can form a permutation test to identify any formal bias towards roles that are easier to predict such as <code>'jng'</code> and <code>'sup'</code>, we will separate the position types in two groups:</p>
		<ul>
			<li><b><u>Group 1</u></b>: High-Performing Roles (<code>'jng'</code> and <code>'sup'</code>).</li>
			<li><b><u>Group 2</u></b>: Lower-Performing Roles (<code>'bot'</code>, <code>'mid'</code>, and <code>'top'</code>).</li>
		</ul>
	</div>
	<div>
		<h4>Hypothesis</h4>
	</div>
	<div>
		<ul>
			<li><b><u>Null Hypothesis</u></b>: Our classification model is unbiased in which the discrepancy between <code>Group 1</code> and <code>Group 2</code> was a simple occurence of chance.</li>
			<li><b><u>Alternative Hypothesis</u></b>: Our classification model <b>is</b> biased towards <code>Group 1</code> due to the chance of occurring being statistically significant.</li>
		</ul>
	</div>
 	<div>
		<h4>Permutation Test</h4>
	</div>
	<div>
		<p>First we will grab the predicted variables column with the rest of the dataset and then classify True or False if our actual label false in the predicted label's group (either Group 1 or Group 2 explained above). We will take the average of <code>True</code> values within each group and then calculate the observed difference between the Group 1 and Group 2 means.</p>
		<p>Then we will perform <b>1000</b> permutation (for good measure) to assess any bias among the two distributions and find the proportion of the differences greater than or equal to our original observation. Since we set our <code>p-value</code> is 0.05 if it exceeds the p-value then we fail to reject the null (the difference in accuracy could be at random), otherwise we reject the null (there is solid proof of bias towards the "High-Performing Roles").</p>
		<p>We will then use <code>sklearn.metrics</code> and more specifically <code>precision_score</code> to assess the accuracy of our classification model upon the two groups.</p>
		<h4>Permutation Conclusion</h4>
	 	<p>After running the code displayed above we have accumulated a p-value of <b>0.0</b>. Therefore we have <b>strong evidence</b> that the accuracy is <u>heavily</u> biased towards the higher performing group (or Group 1). This would make sense as <code>'bot'</code>, <code>'mid'</code>, and <code>'top'</code> have very similar match performance statistics.</p>
		<img src="output.png" alt="output.png" width="600">
 	</div>
</body>

