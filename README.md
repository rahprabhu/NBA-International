# The Rise of International Players in the NBA

## Quick Links

1: [Web Scraping for EDA](https://github.com/rahprabhu/NBA-International/blob/main/Part%201%20-%20Web%20Scraping%20for%20EDA.ipynb)<br>
2: [Data Cleaning and EDA](https://nbviewer.org/github/rahprabhu/NBA-International/blob/main/Part%202%20-%20International%20NBA%20Player%20EDA.ipynb)<br>
3: [Web Scraping for Clustering](https://github.com/rahprabhu/NBA-International/blob/main/Part%203%20-%20Web%20Scraping%20for%20Clustering.ipynb)<br>
4: [Feature Extraction and K-Means Clustering](https://github.com/rahprabhu/NBA-International/blob/main/Part%204%20-%20Clustering%20International%20NBA%20Players.ipynb)<br><br>
**TL:DR** <br>
**Tableau Dashboard** - [**The Rise of International Players in the NBA**](https://public.tableau.com/app/profile/r.prabhu/viz/TheRiseofInternationalPlayersintheNBA/Dashboard1) <br>
**Tableau Dashboard** - [**K-Means Clustering: International NBA Players**](https://public.tableau.com/app/profile/r.prabhu/viz/K-MeansClusteringInternationalNBAPlayers/Dashboard1)


## About
The NBA has grown into a global game over the last few decades, as evidenced by the chart below. Additionally, basketball has evolved into a more positionless game, where players are more often categorized according to their skills, and some of today's top international players are known for defying their positions with their broad set of skills (i.e. big men that can put the ball of the floor and shoot, like Jokic, Embiid etc.). With these two trends in mind, I would like to do an EDA profiling the rise and history of international players in the NBA, and then better classify these players using clustering techniques.
![newplot (14)](https://user-images.githubusercontent.com/100224330/177050133-8e645662-f39e-4e0d-acf5-a035cd100606.png)
## Data Sources
- [Basketball Reference](https://www.basketball-reference.com/)
- [Wikipedia](https://en.wikipedia.org/wiki/List_of_NBA_players_born_outside_the_United_States)

## Data Acquisition
- To first acquire the list of International players in the NBA, I web scrape a table from the Wikipedia link above that contains all of the potentially relevant players. For player statistics, I leverage Basketball Reference for advanced, per 100 possession, and shooting statistics. For the initial EDA, I scrape the statistics on a season by season basis, as this helps me track the number of players that were active each season, and thus the growth in the number of players over time. For the clustering analysis, I only need to scrape the career average statistics for each player.

## EDA
Before beginning the analysis, it's important to define who an international player is. Below is the definition that I am using:
- A player that was born outside out the United States to at least one non-American parent (excludes players born to American parents living abroad) **OR**
- A player born in the United States to at least one non-American parent **OR**
- A player growing up outside of the United States for most of their childhood

The rationale behind this definition is to filter out American players that became naturalized citizens of other countries to represent that country in international competition without having familial ties to that country or having grown up in that country.

With this in mind, I filter the dataframe created from the Wikipedia list of players and perform some data cleaning, which primarily revolves around cleaning string values to remove unwanted characters and standardizing country naming conventions. After cleaning the players dataframe, I can join in the Basketball Reference dataframe containing the seasonal player statistics and begin performing the EDA.

**Question**: Which are the top 10 countries represented in the NBA all time?
![newplot (13)](https://user-images.githubusercontent.com/100224330/177049969-6884d0a7-7423-4532-a6d8-8eebecba1657.png)
Canada has the most international players to play in the NBA, while 5 of the top 10 countries are in Europe. Despite Canada producing the most NBA players outside of the United States, they have not fared as well in international tournaments, with their last Olympic appearance coming at the 2000 Sydney Olympics.

**Question**: What is the breakdown by player?

![newplot (11)](https://user-images.githubusercontent.com/100224330/177050240-c6d0536f-a751-48ce-b6aa-ef370aee4a14.png)

There is clearly a positional imbalance here, as the center position is more than twice as big as the next highest position, power forward, which is the position most similar to center. This is important to know before clustering, as we might have smaller clusters for the players that fall outside of the 'big man' clusters.

**Question**: Which teams have fielded the most international players?
![newplot (15)](https://user-images.githubusercontent.com/100224330/177050496-4a934528-c806-4220-9a92-653c885ef5b2.png)

**Question**: Who are the top international players by total win shares? What positions do they play?
![newplot (16)](https://user-images.githubusercontent.com/100224330/177050591-28061a0e-2a80-46b8-8109-49f72df91780.png)
![newplot (17)](https://user-images.githubusercontent.com/100224330/177050616-e4835d4d-0ff7-4f58-90eb-16992c4a4f43.png)

Over half of the top 20 players by win shares are centers, while 2/3 are frontcourt playes (PF and C). These positions are not only the most represented in the international player base, but are also some of the most impactful on winning.


## Clustering Process
Critieria for player inclusion in clustering analysis:
- Players playing at least 50% of their career after the year 2000 **AND**
- Players who have played at least 50 regular season games

Shooting statistics are only available as of the 1996-97 season, though Basketball Reference notes that shooting statistics are more unreliable for the 1990s. Additionally, the vast majority of international players have come from the last 2 decades, as evidenced by the chart below, so we will essentially be focusing on the recent generation of international players for whom we have reliable shooting statistics. Applying this criteria to the dataset will result in 280 players remaining.

Before fitting a K-Means clustering algorithm on the dataset, we will need to standardize the features and address the high dimensionality of the dataset that we are currently using. When combining shooting, per 100 possession, and advanced statistics, we have nearly 60 dimensions. High dimensionality may result in a more sparse dataset that yields more overfitted yet less meaningful clusters. To combat this we will explore two dimensionality reduction techniques: **Principal Componenent Analysis (PCA)** and **Linear Discriminant Analysis (LDA)**

### PCA

![image](https://user-images.githubusercontent.com/100224330/177051646-3f71408d-6fbe-4098-9a77-8a9265be0ef7.png)

### LDA
![image](https://user-images.githubusercontent.com/100224330/177051680-9e905e54-5dbb-4c76-8e21-ba0abda85a93.png)

With LDA doing a better job in explaining the variance in the dataset, we will use LDA to reduce the dimensionality of the dataset and fit the LDA-transformed dataframe into a K-Means clustering model. 

Using the elbow method, I choose to use k=8, or 8 clusters in the model, although this is a bit of a judgment call as there is not a clear-cut 'elbow' on the graph. 

![image](https://user-images.githubusercontent.com/100224330/177051936-8413c7f6-bc8a-4f5f-85dd-c48f50ff74b3.png)

## Clustering Results
![image](https://user-images.githubusercontent.com/100224330/177052743-2b309914-5595-4896-a0cd-778f83d81215.png)

Clusters with lower LDA 1 values appear to have less within-class scatter, whereas classes from the center to the right have more within-class scatter. Despite the discrepancy in within-class scatter, all of the classes appear to be mostly well-separated from each other. The 3 clusters on the left all correspond to players that play center or power forward, which makes sense as to why they are so close together with a little less separation than other clusters.

### Cluster PER
With these players now clustered, we can try to better understand how they stack up against one another and the league overall. One way we can evaluate their average performance is to look at their average PER and compare that to the average for the league. **PER, or Player Efficiency Rating**, is a per-minute rating that sums up all of a player's positive and negative on-court contributions. Positive stats include field goals, 3 pointers, free throws, assists, rebounds, blocks, and steals. Negative stats include missed shots, turnovers ans personal fouls. The league average for this stat is always 15.00, so let's see how these clusters stack up versus the league average.

![image](https://user-images.githubusercontent.com/100224330/177056312-aff6b782-cc61-4777-a5e9-fd3169911641.png)

Somewhat surprisingly, only the Defensive Big Men outperform the league average PER. While there are certainly some high PER players in this dataset, it looks like there is a strong prevalence of rotation/bench players that reduces the averages to be below the league average.

### Cluster Field Goal Attempts
Where does each cluster attempt their field goals?

![image](https://user-images.githubusercontent.com/100224330/177056843-c2acc4ef-1038-4e8e-8db5-e9b8d5fa9c6f.png)

Each cluster shows a fairly high percentage of shot being taken at the rim (0-3 ft), with the big men clusters having the highest percentage of shots taken here. Additionally, less field goals are being attempted in the midrange between the paint and the 3 point line, as the game has transitioned from high volume in the midrange to higher volume behind the 3 point line to maximize points scored. This has been league-wide trend over the last few decades, and the trend is clearly still present in this international subset of players. 

## Conclusion and Potential Next Steps
With the prevalence of international centers and power forwards in the NBA, it was no surprise that our clustering analysis yielded more than 1 cluster dedicated to primarily big men that were pretty statistically similar. Additionally, while there have been some incredible international players in the history of the league, most international players of the last few decades have been primarily bench/role players with less staying power, though there are a handful of exceptions. 

Some extensions of this project might be to try to create a roster or a draft style big board using these clusters and the player statistics, with the goal of ranking the players from highest to lowest and assembling an ideal roster that provides the necessary balance to build a team. This kind of clustering analysis can also be extended to the league as a whole, or perhaps to college players, where a clustering analysis might be helpful for scouts looking to evaluate a future pool of NBA prospects. 
