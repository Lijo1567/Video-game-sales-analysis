An Analysis of Global Video Game Sales (1980-2016)
Project Overview
This project analyzes a dataset of video game sales from 1980 to 2016 to identify trends in top-performing games, platforms, publishers, and regional market preferences. The goal was to practice data cleaning, SQL querying, and data visualization to derive actionable insights from the data.

Data Source
The dataset was sourced from Kaggle: Video Game Sales Dataset.

Tools Used
SQL (SQLite): For data cleaning, exploration, and aggregation.

DB Browser for SQLite: As the database management tool.

Tableau: For creating an interactive data visualization dashboard.

Analysis & Key Findings
The analysis aimed to answer several key questions about the video game industry:

1. What are the all-time best-selling games?
Finding: Wii Sports is the best-selling game by a significant margin, showcasing the massive success of the Nintendo Wii's motion-control gaming concept which appealed to a broad, casual audience.

-- SQL Query for Top 20 Best-Selling Games
SELECT Rank, Name, Platform, Global_Sales 
FROM sales 
ORDER BY Global_Sales DESC 
LIMIT 20;

2. Which gaming platforms have generated the most sales?
Finding: The PlayStation 2 and Xbox 360 are the top-grossing platforms, indicating the dominance of the sixth and seventh console generations in the history of video game sales.

-- SQL Query for Top 10 Platforms by Sales
SELECT Platform, SUM(Global_Sales) AS Total_Global_Sales 
FROM sales 
GROUP BY Platform 
ORDER BY Total_Global_Sales DESC 
LIMIT 10;

3. Which publishers have earned the most revenue?
Finding: Nintendo is the leading publisher by a substantial margin, highlighting its long-term success and ownership of highly valuable intellectual properties like Mario and Pokemon.

-- SQL Query for Top 10 Publishers by Sales
SELECT Publisher, SUM(Global_Sales) AS Total_Global_Sales 
FROM sales 
GROUP BY Publisher 
ORDER BY Total_Global_Sales DESC 
LIMIT 10;

4. Which publishers are the most prolific?
Finding: Electronic Arts has published the highest number of titles, indicating a business strategy focused on frequent releases across a wide variety of genres, especially annual sports franchises.

-- SQL Query for Top 10 Most Prolific Publishers (by game count)
SELECT Publisher, COUNT(Name) AS Number_of_Games
FROM sales
WHERE Publisher != 'Unknown'
GROUP BY Publisher
ORDER BY Number_of_Games DESC
LIMIT 10;

5. What are the most common game genres?
Finding: Action and Sports are the most frequently published game genres, suggesting they are considered the most commercially viable and have the broadest market appeal.

-- SQL Query for Most Common Game Genres (by game count)
SELECT Genre, COUNT(Name) AS Number_of_Games
FROM sales
GROUP BY Genre
ORDER BY Number_of_Games DESC;

6. How have video game sales trended over time?
Finding: The industry saw explosive growth from the mid-1990s, peaking in 2008-2009. Sales have since stabilized, reflecting a transition to digital distribution and a more mature market.

-- SQL Query for Sales Trend Over Time
SELECT Year, SUM(Global_Sales) AS Total_Global_Sales 
FROM sales 
WHERE Year IS NOT NULL AND Year != 'N/A' 
GROUP BY Year 
ORDER BY Year ASC;

7. What are the top genres in different regions?
Finding: Tastes vary significantly by region: North America prefers Action, Europe also prefers Action, while Japan shows a strong preference for Role-Playing Games, reflecting cultural differences in gaming preferences.

-- SQL Query for Top 3 Genres by Major Region
SELECT * FROM (
    SELECT 'North America' AS Region, Genre, SUM(NA_Sales) AS Total_Sales FROM sales GROUP BY Genre ORDER BY Total_Sales DESC LIMIT 3
) UNION ALL
SELECT * FROM (
    SELECT 'Europe' AS Region, Genre, SUM(EU_Sales) AS Total_Sales FROM sales GROUP BY Genre ORDER BY Total_Sales DESC LIMIT 3
) UNION ALL
SELECT * FROM (
    SELECT 'Japan' AS Region, Genre, SUM(JP_Sales) AS Total_Sales FROM sales GROUP BY Genre ORDER BY Total_Sales DESC LIMIT 3
) UNION ALL
SELECT * FROM (
    SELECT 'Other Regions' AS Region, Genre, SUM(Other_Sales) AS Total_Sales FROM sales GROUP BY Genre ORDER BY Total_Sales DESC LIMIT 3
);

8. What is the market share of the top publishers?
Finding: The top 5 publishers (Nintendo, Electronic Arts, Activision, Sony, and Ubisoft) control over 35% of the entire video game market, demonstrating significant market concentration.

-- SQL Query for Top 5 Publisher Market Share
SELECT Publisher, SUM(Global_Sales) AS Total_Sales, (SUM(Global_Sales) * 100.0 / (SELECT SUM(Global_Sales) FROM sales)) AS Market_Share_Percent
FROM sales
WHERE Publisher != 'Unknown'
GROUP BY Publisher
ORDER BY Total_Sales DESC
LIMIT 5;

Interactive Dashboard
An interactive dashboard was created in Tableau to visualize these findings. The dashboard allows for filtering and provides a comprehensive overview of the video game sales landscape.
https://public.tableau.com/app/profile/lijo.varghese4434/viz/VideoGameSales1980-2019/Dashboard1
