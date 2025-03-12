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
		<div id="plotly-plot"></div>
<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
<script>
    // Full permutation differences data
    const permDiffs = [
         0.005534113357681836, 0.0002961060460862086, 0.004159112092919859, -0.008591200252746622,
        -0.007070255746995047, -0.002564078953252835, -0.0070993147888575026, 0.002673624454086476,
        0.0035846535658881074, 0.004921254889826532, 0.0030997649098776225, 0.004690908981795916,
        -0.0028564979114940048, 0.000659439285938257, -0.0006954863453354498, -0.0014507974949035107,
        0.00522705192528361, 0.0010225157467271817, 0.002790442542754734, 0.0004423489711302686,
        -0.0042462529596799525, -0.0035665851425346062, -0.008468299483905373, -0.009784794461444757,
        -7.555369906731002e-05, -0.003601639565977366, -0.0014664366318248856, -0.005088416868407664,
        -0.0033914611192882305, -0.005861459864752727, 0.0021761156297568363, 6.260440089356223e-05,
        0.005552304206106196, -0.01026097466703313, -0.0014469512096039194, 0.005816447792199142,
        0.0012509003771284943, -0.008248107523915915, -0.005965360661109642, 0.0031272656110412633,
        0.006613928334294306, -0.002142184064423347, -0.0004875081589675867, 0.0009232781496150144,
        0.009526336757563647, 0.008411714716703989, -0.00534040147651671, -0.0038196222212909525,
        -0.008842452464690842, 0.007093104224201396, 0.0038055331547679483, 0.0034910763804204548,
        -0.002999639853063951, -0.007113483868489867, 0.0003336445953516787, -0.0042869477305209625,
        -0.00011886410895500799, 0.007357006410535494, 0.0014628056280763246, 0.004526183063437106,
        0.0021518762372506606, -0.0029718462607496443, -0.0010070465023183095, 0.00471329707539081,
        -0.006624919880568125, -0.00015037832224673586, 0.007038591426628882, -0.003811698829020771,
        -0.0008932650744318815, 0.00089770841251402, 0.0030109605433349396, -0.0009116410455460855,
        6.875553083429686e-06, -0.0035303917467716106, -0.004111389888646566, 0.009329177168069802,
        0.001742519842079071, -0.00230279763988106, -0.0027200280446696423, 0.0037042217465933502,
        0.003523231373854352, 0.009350512131613531, -0.006129339525246746, -0.005162012520549375,
        -0.0021050644732287793, 0.00016720529369740333, -0.008708112004012114, 0.001393736291631087,
        0.0012817476760790258, -0.000724441188696634, -0.006476452100455887, 0.0010621029555547556,
        0.0031313383074575984, -0.004321156738489984, 0.004821531953137059, -0.0018721615576939854,
        0.008356811198058312, -0.00535860029667079, 0.002325982566086404, -0.01007890970905534,
        -0.00022027148853909218, 0.014995798333599542, 0.005329115883295876, 0.0031359348647476137,
        0.0004488152364303666, 0.0043794279396708324, 0.006707421871755548, 0.007211763213036959,
        -0.0007744294261772255, -0.006962796195944532, 0.0017771405115789563, 0.005355763418533499,
        0.01266407906327116, -0.009044178950288084, 0.004227350608864366, 0.00041366598667946786,
        -0.005514217707656921, 0.0020484632035199235, -0.01111891339174731, -0.01278075495344444,
        -0.007992821031674646, -0.0019272485373533765, -0.0036592503109514896, 0.0015447490687741094,
        -0.002348567387374434, -0.00011438986053047273, 0.006024824372115156, -0.007170956822761254,
        -0.00130847381319521, 0.006859404938486469, -0.002894049455910541, 0.010172265931537416,
        -0.009374624772322981, 0.0052964238828185906, -0.004895803185072545, 0.0046559383067454885,
        0.002915175586439722, 0.007214296180042767, -0.002691056421796234, -0.017969475431163895,
        0.00951283375909473, 0.00356754461040254, 0.002964361871258925, 0.010959437058931987,
        -0.00025613695346049514, -2.914036250523111e-05, -0.0033237222699393776, 0.0021377724464166636,
        0.002067125506830414, -0.0027043678221427836, 0.008834136277335536, 0.009121304775731254,
        0.006305151043252355, 0.008230691740411245, 0.0027578832494215, 0.004354879639969056,
        -0.006525109581233202, 0.003924231191166028, -0.0005139075184579234, 0.0011878492283151632,
        0.007846846909161376, 0.005735689029855551, -0.0014550601673906094, 0.004681714522116964,
        0.005433068231162963, 0.0067677174247606775, 0.007815375105711952, -0.012231309890937792,
        0.01101188195005387, -0.0002972263221796556, -0.0035500485868544818, 0.010049559787462248,
        0.00860034154434175, 0.0063179030746651765, 0.0071078279599903205, -0.00288467891090316,
        0.0073021272335390686, -0.010479907114689047, 0.0021862431700373497, 0.0030837908214981224,
        0.005272094393269033, -0.005188983335530528, 0.003514368955595204, 0.003385534756706554,
        -0.009671525759138655, 0.00201616249131209, 0.0008849005953724953, 0.012165200971578471,
        -0.005818079303145929, 0.007222383952823597, -0.0037486088316147637, -0.0031519317490785737,
        0.008243913477547271, 0.009357238815777436, -0.005681823469793401, -0.0008734660612238487,
        0.00978579804093338, -0.00012697283137408366, 0.00458250020603701, 0.011081635839191861,
        0.001157554634626079, 0.001041235684480224, 0.008831963729337033, -0.008269557481861534,
        0.00038879432635019473, 0.0033589899562911363, -0.002565543522222158, -0.006476731058620233,
        0.003991002479281303, 0.002997057904150835, 0.009762355112143295, 0.0019266158047899218,
        0.005257554262887099, -0.00030094904092858865, 0.0019182992309491054, 0.0002195648312679488,
        0.002287117218053414, 0.000719300404861567, 0.003973890281207093, -0.00011234958568007158,
        0.0027859121328035474, 0.0029399918872649033, 0.0008088669709922502, 0.006813221398721536,
        -0.0032966855911508164, -0.0019659064589218067, -0.004565712319851145, 0.00851856476293833,
        -0.001131133823209729, 0.006094897275763511, -0.001277138022329427, -0.011073802613322581,
        0.005498124830300544, -0.001933631780115963, -0.0016433763650344213, -0.009816706317125723,
        -0.008002459634973924, 0.00437010717014541, 0.005008982599607359, 0.0016124968896087388,
        -0.0034902397274301222, -0.004387010562627358, -0.008523540498467042, -0.0048804956430554824,
        0.00018191859389249387, 0.001360431085105196, -0.004387543898444202, 0.007502670906901154,
        0.005513020961317783, 0.0006645010416090891, -0.0017232407454242926, 0.004972342056452916,
        0.0016379436069817732, 0.0024151264647044313, -0.004737932599362282, 0.005434858810857257,
        -0.007284863478156822, -0.010721618593738658, 0.003611498146318004, -0.009087945954783128,
        0.006293474053873149, -0.004933816923387013, 0.0010515124498772233, 0.0009301124955845008,
        0.0022962477495669376, 0.005006066064492831, 4.8847246075234274e-05, -0.001143947982028215,
        0.006334221421098296, 0.006520138010227106, 0.01565649586502671, 0.0008449762131855776,
        -0.0009782656112135024, -0.007393288626164951, 0.011868405777618829, 0.0033816227419708467,
        -0.0012253622837161693, -0.0016038697834537263, 0.005058016374447805, 0.0052065119632320744,
        0.0014327334052458562, -0.005759927143831556, -0.0015109284880499008, 0.005567652189411576,
        -0.001247388105280911, -0.013358600100473295, -0.0012516323123317186, 0.00751252632516064,
        -0.002655327939848906, -0.006121884374174824, 0.0007310525630562781, 0.0025335832368855726,
        0.005311285421939482, 0.0044893256152049865, -0.009180385278853564, -0.002610346093299243,
        0.013997176218935814, 0.007492443656358594, -0.003213991802160754, -0.002778369454647156,
        -0.010569119305970709, 0.009629596494327264, 0.0027037340280779976, -0.018606395232520057,
        0.006695410030697735, -0.0017622374455338319, -0.007382889938924553, 0.006432671960529879,
        -0.008920936754461484, 0.007992848917599549, -0.010516202921691087, 0.008649346595305585,
        0.009073141082197811, -0.009092832059241496, -0.0006295032526774103, -0.009724212470648919,
        -0.005233926166832936, 0.004694241402593224, 0.01085228257143056, -0.008641222240359125,
        0.0046280981022839285, 0.004767525802102601, 0.00011623899251067549, -0.011073805943076942,
        -0.00731403014394405, -0.009810936210211563, 0.0024314341063926825, -0.004223838096925281,
        0.0025040972859061705, -0.0035312042483093276, -0.002233707784645933, 0.0019284745685834714,
        -0.00682389569889863, 0.006599456322393227, 0.0021701843438075574, 0.008084051273173465,
        -0.0039983425196314926, -0.0070626102662316725, 0.003920844795963774, 0.0040322524763851675,
        -0.0005025287549602631, 0.0076120009318786375, -0.01099492674047764, -0.0023526092246485275,
        -0.004564804546021817, -0.001733436464166238, 0.0031696688143104668, 0.008431569733596933,
        0.003864493284094661, -0.0012778366505546979, -0.0002370997179438339, 0.010128094388858866,
        0.0058353851545140945, 0.002213841922805715, 0.009838265925053324, -0.005456216051321516,
        -0.011154668402320378, -0.004484488868497061, 0.0012456246130639892, 0.0056282124045961,
        -0.005930759599303892, -0.0067098071863597175, -0.0008976646853200432, -0.008172739307884314,
        0.006635155464063569, -0.00012428780980167087, -0.007111334731909169, 0.010521004427335057,
        0.005524196801711678, -0.0074361494755781354, 0.007096563234470388, -0.003825645870333072,
        0.005030499460587645, 0.0001088880480206722, -0.003748513514958085, -0.004653368109637901,
        -0.0034475638192057456, 0.0016950723373659882, -0.004341983807780503, 0.004608372104558223,
        -0.004879114886367386, 0.0007278188241262029, -0.0006291397767459461, 0.013679740992

    ];

    // Create plot data configuration
    const plotData = [{
        name: 'Permutation Differences',
        type: 'histogram',
        x: permDiffs,
        nbinsx: 30,
        marker: {
            color: '#636efa',
            line: {
                color: '#2a3f5f',
                width: 0
            }
        }
    }];

    const layout = {
    title: {
        text: 'Permutation Test Results',
        font: {
            color: 'white'  // Set title font color to white
        }
    },
    xaxis: {
        title: {
            text: 'Difference in Precision (Permuted)',
            font: {
                color: 'white'  // Set x-axis title font color to white
            }
        },
        showgrid: true,
        zeroline: true
    },
    yaxis: {
        title: {
            text: 'Frequency',
            font: {
                color: 'white'  // Set y-axis title font color to white
            }
        },
        showgrid: true,
        zeroline: true
    },
    bargap: 0.1,
    shapes: [{
        type: 'line',
        x0: 0.09164558718119603,
        x1: 0.09164558718119603,
        y0: 0,
        y1: 1,
        xref: 'x',
        yref: 'paper',
        line: {
            color: 'red',
            dash: 'dash',
            width: 2
        }
    }],
    plot_bgcolor: '#232323',
    paper_bgcolor: '#232323',
    font: {
        color: 'white'  // Set general font color to white for all labels and text
    }
};

    // Create the plot
    Plotly.newPlot('plotly-plot', plotData, layout);
</script>

		<h4>Permutation Conclusion</h4>
	 	<p>After running the code displayed above we have accumulated a p-value of <b>0.0</b>. Therefore we have <b>strong evidence</b> that the accuracy is <u>heavily</u> biased towards the higher performing group (or Group 1). This would make sense as <code>'bot'</code>, <code>'mid'</code>, and <code>'top'</code> have very similar match performance statistics.</p>
		<img src="output.png" alt="output.png" width="600">
 	</div>
</body>

