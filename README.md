# Soccer-SQL-Server
Analyzed the South African Soccer Dataset using SQL Server Management Studio (SSMS). Built 20 queries covering player stats, team performance, market value, accuracy metrics, contracts, injuries, and agent insights. Includes data cleaning for NVARCHAR fields and grouped analytical outputs.

  SELECT TOP 100 *
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced];




SELECT COUNT(*) AS TotalPlayers
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced];


SELECT DISTINCT Team
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced];


SELECT Team, COUNT(*) AS PlayersPerTeam
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY Team;



SELECT TOP 10 player_name, Goals
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
ORDER BY Goals DESC;


SELECT 
    Team,
    AVG(CAST(average_salary_zar AS FLOAT)) AS AvgSalary
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY Team;



SELECT TOP 10 player_name, market_value_zar
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
ORDER BY market_value_zar DESC;




SELECT 
    Position,
    AVG(CAST(passing_accuracy AS FLOAT)) AS AvgPassingAccuracy
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY Position;


SELECT player_name, Goals, shot_accuracy
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced];



SELECT 
    Team,
    SUM(CAST(Goals AS INT)) AS TotalGoals,
    SUM(CAST(Assists AS INT)) AS TotalAssists
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY Team;



SELECT marital_status, COUNT(*) AS TotalPlayers
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY marital_status;



SELECT Nationality, COUNT(*) AS TotalPlayers
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY Nationality;




SELECT 
    Nationality,
    AVG(CAST(REPLACE(market_value_zar, ',', '') AS FLOAT)) AS AvgMarketValue
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY Nationality;


SELECT YEAR(contract_end_year) AS ContractEndYear,
       COUNT(*) AS Players
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY YEAR(contract_end_year)
ORDER BY ContractEndYear;



SELECT Player_Name, contract_end_year
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
WHERE YEAR(contract_end_year) = YEAR(GETDATE()) + 1;


SELECT injury_status, COUNT(*) AS TotalPlayers
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY injury_status;



SELECT player_name,
       Goals,
       matches_played,
       CASE WHEN matches_played = 0 
            THEN 0 
            ELSE CAST(Goals AS FLOAT) / matches_played 
       END AS GoalsPerMatch
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced];


SELECT 
    [Agent], 
    COUNT(*) AS PlayersManaged
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY [Agent];



SELECT Position,
       AVG(height_cm) AS AvgHeight,
       AVG(weight_kg) AS AvgWeight
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
GROUP BY Position;


SELECT TOP 10 player_name,
       Goals,
       Assists,
       (Goals + Assists) AS TotalContributions
FROM [Soccer_Analysis_Db1].[dbo].[ketro_sa_soccer_dataset_advanced]
ORDER BY TotalContributions DESC;

