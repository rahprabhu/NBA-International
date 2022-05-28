# The Rise of International Players in the NBA

## Quick Links

1: [Web Scraping for EDA](https://github.com/rahprabhu/NBA-International/blob/main/Part%201%20-%20Web%20Scraping%20for%20EDA.ipynb)<br>
2: [Data Cleaning and EDA](https://nbviewer.org/github/rahprabhu/NBA-International/blob/main/Part%202%20-%20International%20NBA%20Player%20EDA.ipynb)<br>
3: [Web Scraping for Clustering](https://github.com/rahprabhu/NBA-International/blob/main/Part%203%20-%20Web%20Scraping%20for%20Clustering.ipynb)<br>
4: [Feature Extraction and K-Means Clustering](https://github.com/rahprabhu/NBA-International/blob/main/Part%204%20-%20Clustering%20International%20NBA%20Players.ipynb)<br><br>
Tableau Dashboard - [The Rise of International Players in the NBA](https://public.tableau.com/app/profile/r.prabhu/viz/TheRiseofInternationalPlayersintheNBA/Dashboard1)


## About
The NBA has grown into a global game over the last few decades, and I would like to do an EDA on the growth of international players in the NBA and better classify the players using clustering techniques. Basketball has evolved into a more position-fluid game, where players are more often categorized according to their skills, and some of today's top international players are known for defying their positions with their broad set of skills (see Nikola Jokic and Giannis Antetokounmpo). 

Before beginning the clustering exercise, some questions that I would like to answer include:
- What are the top countries that international players have come from?
- Which teams have the fielded the most international players?
- Which countries have produced the most valuable players?
- Which countries/players have contributed the most to winning games?

To acquire the data for the analyses, I will be primarily scraping Basketball Reference using Beautiful Soup. I will use Pandas for data cleaning and then Plotly and Seaborn for visual analysis. For the clustering analysis, I will first use Linear Discriminant Analysis and Principal Component Analysis for dimensionality reduction of the dataset before moving on to K-Means clustering.
