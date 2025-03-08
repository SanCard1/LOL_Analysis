<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Final Project</title>
    <style>
        body {
            font-family: sans-serif;
            text-align: center;
            margin: 50px;
            background-color: #f4f4f4;
        }
	table, th, td {
	
}
	ul {
	    font-family: sans-serif;
	    text-align: left;
	    margin: 25px;
	    backgroud-color: #f4f4f4;
        h1 {
            color: #333;
        }
        p {
            color: #666;
            line-height: 1.6;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            max-width: 600px;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Final Project</h1>
	<h3>by Santiago Cardenas Rey and Michael Luo</h3>
	<h5>Step 1: Description</h5>
        <p>We chose the league of legends dataset for this project because it provides a rich and dynamic set of variables that allow for meaningful hypothesis testing and predictive modeling. The dataset includes key performance metrics such as damage per minute, kills, assists, deaths, and game results which enable various statistical analyses. Unlike structured datasets like recipes or power outages, this dataset introduces human decision-making and variability, making the analysis more complex and engaging. Since I have an interest in gaming and data-driven insights, working with this dataset makes the project both enjoyable and intellectually stimulating. Fellow gamers may relate to what we are assessing to best determine the performance of players based on what kind of player they are or coe across (i.e. ADC bot or mid-lane player).</p>
	<p> Aggregating all data there are 1016472 rows and 161 columns. Our relevant columns for analysis will be:</p>
</body>
	<ul>
	    <li>gameid: ID of the game.</li>
	    <li>datacompleteness: Completeness of the data.</li>
	    <li>league: League level.</li>
	    <li>year: Year of the match</li>
	    <li>date: Date of the game (in case we decide to do time series analysis</li>
	    <li>game: The game title</li>
	    <li>side: The team assignation to the player.</li>
	    <li>position: The position of the player.</li>
	    <li>playername: In case we want to track the name of the player.</li>
	    <li>playerid: To keep up with the player specifically.</li>
	    <li>teamname: In case we want to track the name of the team.</li>
	    <li>teamid: To keep up with the team specifically.</li>
	    <li>gamelength: To measure magnitude of kill activity per game.</li>
	    <li>result: Outcome of the match.</li>
	    <li>kills: Number of kills.</li>
	    <li>deaths: Number of deaths.</li>
	    <li>assists: Number of assists.</li>
	    <li>teamkills: Number of kills by the whole team.</li>
	    <li>teamdeaths: Number deaths by the whole team.</li>
	    <li>doublekills: Number of double kills.</li>
	    <li>triplekills: Number of triple kills.</li>
	    <li>quadrakills: Number of quadruple kills.</li>
	    <li>pentakills: Number of penta kills.</li>
	    <li>firstblood: A binary value assigning who had first blood in the match.</li>
	    <li>firstbloodkill: A binary value assigning who had first blood kill in the match.</li>
	    <li>firstbloodassist: A binary value assigning who had first blood assists in the match.</li>
	    <li>team kpm: The kills per minute by the team.</li>
	    <li>ckpm: Average combined kills per minute (team kills + opponent kills).</li>
	    <li>damagetochampions: The damage done by the player to champions.</li>
	    <li>dpm: Damage per Minute.</li>
	    <li>damageshare: Share of the damage by the team.</li>
	    <li>damagetakenperminute: Amount of damage taken per minute.</li>
	    <li>damagemitigatedperminute: Average damage mitigated per minute.</li>
	    
	</ul>
    </div>
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
		</table>	
	</div>
</body>
