# World-Bank-Health
### What’s the average age of first marriages for females around the world?
SELECT
  country_name,
  ROUND(AVG(value),2) AS average
FROM
  `bigquery-public-data.world_bank_health_population.health_nutrition_population`
WHERE
  indicator_code = "SP.DYN.SMAM.FE"
  AND year > 2000
GROUP BY
  country_name
ORDER BY
  average 
LIMIT 10;
![Screen Shot 2021-08-30 at 8 03 06 PM](https://user-images.githubusercontent.com/83669448/131356041-b2527d1f-542f-4244-ab24-4d7a11e93d40.png)

### What is the lowest unemployment rate 
SELECT 
    country_name AS Country,
    AVG(value) AS Unemployment_percent_avg
FROM
    `bigquery-public-data.world_bank_health_population.health_nutrition_population`
WHERE
    indicator_name = 'Unemployment, total (% of total labor force)'
GROUP BY country_name , indicator_name
ORDER BY Unemployment_percent_avg ASC
LIMIT 10;
![Screen Shot 2021-08-30 at 8 13 32 PM](https://user-images.githubusercontent.com/83669448/131359531-ca8cb9fd-fedd-4973-bf54-042b09f1993f.png)


### Life Expectancy
SELECT
  country_name, country_code, year, ROUND(value,2) as indicator
FROM
  `bigquery-public-data.world_bank_health_population.health_nutrition_population`
WHERE
  indicator_code = "SP.DYN.LE00.IN"
ORDER BY
  year
LIMIT 10;
![Screen Shot 2021-08-30 at 8 29 03 PM](https://user-images.githubusercontent.com/83669448/131359861-612dd305-bc14-4d4d-8ced-46156d9586f5.png)


### Difference between deathrate and Birth rate in 1960
                       WITH birthRateTable AS
            (SELECT 
                country_name, country_code, year, ROUND(value,2) AS birthRate 
             FROM 
                 `bigquery-public-data.world_bank_health_population.health_nutrition_population`
             WHERE
                 indicator_code = "SP.DYN.CBRT.IN"
            ),
                deathRateTable AS 
            (SELECT 
                country_name, country_code, year, ROUND(value,2) AS deathRate 
             FROM 
                 `bigquery-public-data.world_bank_health_population.health_nutrition_population`
             WHERE
                 indicator_code = "SP.DYN.CDRT.IN"
            )
            
            SELECT 
                 birthRateTable.country_name, birthRateTable.country_code, birthRateTable.year,
                 birthRateTable.birthRate, deathRateTable.deathRate
            FROM
                 birthRateTable
            INNER JOIN deathRateTable
                 ON birthRateTable.country_code = deathRateTable.country_code
                 AND birthRateTable.year = deathRateTable.year
            ORDER BY
                  birthRateTable.year, birthRateTable.birthRate ASC
       LIMIT 10;
       ![Screen Shot 2021-08-30 at 8 26 37 PM](https://user-images.githubusercontent.com/83669448/131359647-73e2b260-9683-4f56-823e-5f47e91e9c92.png)



