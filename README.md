<html lang="en">
<body>
    <div class="container">
        <h1>League of Legends Analysis: Race to the Nexus</h1>
	<h3>by Santiago Cardenas Rey and Michael Luo</h3>
	<h5>Step 1: Description</h5>
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
<body>
    <div>
	<h5>Step 2: Data Cleaning and Exploratory Data Analysis</h5>
        <h1><b>FOR MICHAEL TO DO</b></h1>
    </div>
</body>
<body>
	<div>
		<h5>Step 3: Assessment of Missingness</h5>
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
		<h5>Step 4: Hypothesis Testing</h5>
	</div>	
	<div>
		<h6><b>Null Hypothesis</b><h6>
	</div>
	<div>
		<p>The mean carry potential (measured as Damage Per Minute / (Deaths + 1)) is the same for mid-lane and ADC (bot-lane) players.</p>
	</div>
	<div>
		<h6><b>Alternative Hypothesis</b></h6>
	</div>
	<div>
		<p>The mean carry potential is higher for mid-lane players than for ADC players.</p>
	</div>
	<div>
		<h6><b>Test Statistic</b><h6>
	</div>
	<div>
		<p>The test statistic will be the <u>observed difference</u> in means of carry potential between mid-lane and ADC players.</p>
	</div>
	<div>
		<h6><b>Significance Level</b></h6>
	</div>
	<div>
		<p>The significance level will be <b>0.05</b> as we understand there can be some variation among both types but for the null hypothesis, there should be a clear difference.</p>
	</div>
	<div>
		<h6><b>p-value</b></h6>
		<h1><b><u><i>MICHAEL DO THIS</u></i></b></h1>
	</div>
	<div>
		<h6><b>Results</b></h6>
		<h1><b><u><i>MICHAEL DO THIS</u></i></b></h1>
	</div>
	<div>
		<h6><b>Justifications</b></h6>
		<h1><b><u><i>MICHAEL DO THIS</u></i></b></h1>
	</div>
	<div>
		<h5>Step 5: Framing a Prediction Problem</h5>
	</div>
	<div>
		<p><b><u>Prediction Problem</u></b>: We want to identify the role of the player given their post-game data. This will imply for us to do a <u>classification model</u></p>	
		<p><b><u>Type of Classification</b></u>: multiclass classification. Some columns have non-binary data but are yet numeric (some columns are binary too), thus a suitable task for a multiclass classification.</p>
		<p><b><u>Response Variable</b></u>: since we are figuring the position of the player with the given player's match statistics, the response variable is <b><u>position</u></b>.</p>
		<p><b><u>Motivation</b></u>: The motivation behind this is to identify the patterns, statistics, strengths, weaknesses, and behaviors of distinct player positions. By using match performance statistics, we can inform people as to how different kind of players behave in the match (i.e. suppose a player is type 1, then we would be able to have a solid understanding of the player's skills and preferences such as firstblood count or damage per minute or even player location patterns). In here we are prioritizing previous match statistics and outcomes to predict future matches where the players have known positions (reverse causality).</p>
	</div>
	<div>
		<h5>Step 6: Baseline Model</h5>
	</div>
	<div>
		<table>
			<tr>
				<th>Features</th>
				<th>Type</th>
				<th>Encodings</th>
			</tr>
			<tr>
				<td>gameid</td>
				<td>Nominal</td>
				<td><b><u><i>MICHAEL DO THIS</b></u></i></td>
			</tr>
			<tr>
				<td>datacompleteness</td>
				<td>Ordinal</td>
				<td><b><u><i>MICHAEL DO THIS</b></u></i></td>
			</tr>
			<tr>
				<td>league</td>
				<td>Categorical</td>
				<td><b><u><i>MICHAEL DO THIS</b></u></i></td>
			</tr>
			<tr>
				<td>year</td>
				<td>Ordinal</td>
				<td><b><u><i>MICHAEL DO THIS</b></u></i></td>
			</tr>
			<tr>
				<td>date</td>
				<td>Ordinal</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>game</td>
				<td>Nominal</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>side</td>
				<td>Categorical</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>playername</td>
				<td>Categorical</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>playerid</td>
				<td>Nominal</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>teamname</td>
				<td>Categorical</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>teamid</td>
				<td>Nominal</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>gamelength</td>
				<td>Numeric</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>result</td>
				<td>Nominal</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>kills</td>
				<td>Numeric</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>deaths</td>
				<td>Numeric</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>assists</td>
				<td>Numeric</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
			<tr>
				<td>teamkills</td>
				<td>Numeric</td>
				<td><b><u><i>MICHAEL DO THIS</i></u></b></td>
			</tr>
		</table>	
	</div>
</body>
