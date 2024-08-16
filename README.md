# Project-2---Carbon-Emission-Analysis
## Table product_emissions
| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf | operations_percent_total_pcf | downstream_percent_total_pcf | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -------------------------: | ---------------------------: | ---------------------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                      | 17.36                        | 2.01                         | 
| 10261-1-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1488                 | 30.65                      | 5.51                         | 63.84                        | 
| 10261-2-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1818                 | 25.08                      | 4.51                         | 70.41                        | 
## Table industry_groups
| id | industry_group                                                         | 
| -: | ---------------------------------------------------------------------: | 
| 1  | "Consumer Durables, Household and Personal Products"                   | 
| 2  | "Food, Beverage & Tobacco"                                             | 
| 3  | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 
| 4  | "Mining - Iron, Aluminum, Other Metals"                                | 
| 5  | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 
## Table companies
| id | company_name                  | 
| -: | ----------------------------: | 
| 1  | "Autodesk, Inc."              | 
| 2  | "Casio Computer Co., Ltd."    | 
| 3  | "Cisco Systems, Inc."         | 
| 4  | "CNX Coal Resources, LP"      | 
| 5  | "Coca-Cola Enterprises, Inc." | 
## Table countries
| id | country_name | 
| -: | -----------: | 
| 1  | Australia    | 
| 2  | Belgium      | 
| 3  | Brazil       | 
| 4  | Canada       | 
| 5  | Chile        | 
#
## Which products contribute the most to carbon emissions
TOP 10 products contribute the most to carbon emission :
| product_name                                                                                                                       | carbon_foorprint | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044          | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187          | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608          | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625          | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687           | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000           | 
| TCDE                                                                                                                               | 99075            | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000            | 
| Electric Motor                                                                                                                     | 87589            | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 85000            | 
```
SELECT product_name,max(carbon_footprint_pcf) AS 'carbon_foorprint'
FROM product_emissions
GROUP BY product_name
ORDER BY max(carbon_footprint_pcf) DESC
LIMIT 10
```
#
## What are the industry groups of these products
Products by industry :
| product_name                                                                                                                       | industry_group                     | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------------------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 
| Wind Turbine G132 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 
| Wind Turbine G114 2 Megawats                                                                                                       | Electrical Equipment and Machinery | 
| Wind Turbine G90 2 Megawats                                                                                                        | Electrical Equipment and Machinery | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | Automobiles & Components           | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | Materials                          | 
| TCDE                                                                                                                               | Materials                          | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | Automobiles & Components           | 
| Electric Motor                                                                                                                     | Capital Goods                      | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | Automobiles & Components           | 
```
SELECT P.product_name, I.industry_group 
FROM product_emissions AS P
INNER JOIN industry_groups AS I ON P.industry_group_id = I.id
GROUP BY P.product_name
HAVING max(P.carbon_footprint_pcf)
ORDER BY max(P.carbon_footprint_pcf) DESC
LIMIT 10
```
#
## What are the industries with the highest contribution to carbon emissions?
In top 5 industries the highest contribution to carbon emissions, Electrical Equipment and Machinery is highest
| industry_group                     | carbon_footprint | 
| ---------------------------------: | ---------------: | 
| Electrical Equipment and Machinery | 9801558          | 
| Automobiles & Components           | 2582264          | 
| Materials                          | 577595           | 
| Technology Hardware & Equipment    | 363776           | 
| Capital Goods                      | 258712           | 
```
SELECT I.industry_group,sum(P.carbon_footprint_pcf) AS carbon_footprint
FROM product_emissions AS P
INNER JOIN industry_groups AS I ON P.industry_group_id = I.id
GROUP BY I.industry_group
ORDER BY sum(P.carbon_footprint_pcf) DESC
LIMIT 5
```
#
## What are the companies with the highest contribution to carbon emissions?
In top 5 companies the highest contribution to carbon emissions,Gamesa Corporación Tecnológica, S.A company is highest
| company_name                            | carbon_footprint | 
| --------------------------------------: | ---------------: | 
| "Gamesa Corporación Tecnológica, S.A."  | 9778464          | 
| Daimler AG                              | 1594300          | 
| Volkswagen AG                           | 655960           | 
| "Mitsubishi Gas Chemical Company, Inc." | 212016           | 
| "Hino Motors, Ltd."                     | 191687           | 

```
SELECT C.company_name,sum(P.carbon_footprint_pcf) AS carbon_footprint
FROM product_emissions AS P
INNER JOIN companies AS C ON P.company_id = C.id
GROUP BY C.company_name
ORDER BY sum(P.carbon_footprint_pcf) DESC
LIMIT 5
```
#
## What are the countries with the highest contribution to carbon emissions?
In top 5 countries the highest contribution to carbon emissions, Germany is highest
| country_name | carbon_footprint | 
| -----------: | ---------------: | 
| Germany      | 9778464          | 
| Lithuania    | 212016           | 
| Greece       | 191687           | 
| Japan        | 132012           | 
| Colombia     | 105600           | 
```
SELECT C.country_name,sum(P.carbon_footprint_pcf) AS carbon_footprint
FROM product_emissions AS P
INNER JOIN countries AS C ON P.company_id = C.id
GROUP BY C.country_name
ORDER BY sum(P.carbon_footprint_pcf) DESC
LIMIT 5
```
#
## What is the trend of carbon footprints (PCFs) over the years?
From 2013 to 2017, the high carbon footprints were in 2015. And then, the carbon footprint has been decreasing in 2016 - 2017
| year | Average_carbon_footprints | Total_carbon_footprints | 
| ---: | ------------------------: | ----------------------: | 
| 2013 | 2399.32                   | 503857                  | 
| 2014 | 2457.58                   | 624226                  | 
| 2015 | 43188.90                  | 10840415                | 
| 2016 | 6891.52                   | 1640182                 | 
| 2017 | 4050.85                   | 340271                  | 
```
SELECT year,round(avg(carbon_footprint_pcf),2) AS 'Average_carbon_footprints',sum(carbon_footprint_pcf) AS 'Total_carbon_footprints' 
FROM product_emissions 
GROUP BY year
ORDER BY year ASC
```
#
## Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time
The industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time is: 
**Semiconductors & Semiconductor Equipment**
| year | industry_group                                                         | Average_carbon_footprints | Total_carbon_footprints | 
| ---: | ---------------------------------------------------------------------: | ------------------------: | ----------------------: | 
| 2015 | "Consumer Durables, Household and Personal Products"                   | 116.38                    | 931                     | 
| 2013 | "Food, Beverage & Tobacco"                                             | 94.25                     | 4995                    | 
| 2014 | "Food, Beverage & Tobacco"                                             | 99.44                     | 2685                    | 
| 2015 | "Food, Beverage & Tobacco"                                             | 0.00                      | 0                       | 
| 2016 | "Food, Beverage & Tobacco"                                             | 4011.56                   | 100289                  | 
| 2017 | "Food, Beverage & Tobacco"                                             | 143.73                    | 3162                    | 
| 2015 | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 685.31                    | 8909                    | 
| 2015 | "Mining - Iron, Aluminum, Other Metals"                                | 2727.00                   | 8181                    | 
| 2013 | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 16135.50                  | 32271                   | 
| 2014 | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 40215.00                  | 40215                   | 
| 2015 | "Textiles, Apparel, Footwear and Luxury Goods"                         | 14.33                     | 387                     | 
| 2013 | Automobiles & Components                                               | 26037.80                  | 130189                  | 
| 2014 | Automobiles & Components                                               | 20910.45                  | 230015                  | 
| 2015 | Automobiles & Components                                               | 37146.68                  | 817227                  | 
| 2016 | Automobiles & Components                                               | 40138.09                  | 1404833                 | 
| 2013 | Capital Goods                                                          | 5015.83                   | 60190                   | 
| 2014 | Capital Goods                                                          | 10411.00                  | 93699                   | 
| 2015 | Capital Goods                                                          | 3505.00                   | 3505                    | 
| 2016 | Capital Goods                                                          | 796.13                    | 6369                    | 
| 2017 | Capital Goods                                                          | 18989.80                  | 94949                   | 
| 2015 | Chemicals                                                              | 1949.03                   | 62369                   | 
| 2013 | Commercial & Professional Services                                     | 144.63                    | 1157                    | 
| 2014 | Commercial & Professional Services                                     | 119.25                    | 477                     | 
| 2016 | Commercial & Professional Services                                     | 96.33                     | 2890                    | 
| 2017 | Commercial & Professional Services                                     | 370.50                    | 741                     | 
| 2013 | Consumer Durables & Apparel                                            | 286.70                    | 2867                    | 
| 2014 | Consumer Durables & Apparel                                            | 113.10                    | 3280                    | 
| 2016 | Consumer Durables & Apparel                                            | 40.07                     | 1162                    | 
| 2015 | Containers & Packaging                                                 | 373.50                    | 2988                    | 
| 2015 | Electrical Equipment and Machinery                                     | 891050.73                 | 9801558                 | 
| 2013 | Energy                                                                 | 750.00                    | 750                     | 
| 2016 | Energy                                                                 | 2506.00                   | 10024                   | 
| 2015 | Food & Beverage Processing                                             | 7.05                      | 141                     | 
| 2014 | Food & Staples Retailing                                               | 77.30                     | 773                     | 
| 2015 | Food & Staples Retailing                                               | 70.60                     | 706                     | 
| 2016 | Food & Staples Retailing                                               | 0.50                      | 2                       | 
| 2015 | Gas Utilities                                                          | 61.00                     | 122                     | 
| 2013 | Household & Personal Products                                          | 0.00                      | 0                       | 
| 2013 | Materials                                                              | 4177.35                   | 200513                  | 
| 2014 | Materials                                                              | 1513.56                   | 75678                   | 
| 2016 | Materials                                                              | 1401.06                   | 88267                   | 
| 2017 | Materials                                                              | 11217.74                  | 213137                  | 
| 2013 | Media                                                                  | 2411.25                   | 9645                    | 
| 2014 | Media                                                                  | 2411.25                   | 9645                    | 
| 2015 | Media                                                                  | 479.75                    | 1919                    | 
| 2016 | Media                                                                  | 602.67                    | 1808                    | 
| 2014 | Retailing                                                              | 6.33                      | 19                      | 
| 2015 | Retailing                                                              | 5.50                      | 11                      | 
| 2014 | Semiconductors & Semiconductor Equipment                               | 16.67                     | 50                      | 
| 2016 | Semiconductors & Semiconductor Equipment                               | 2.00                      | 4                       | 
| 2015 | Semiconductors & Semiconductors Equipment                              | 1.00                      | 3                       | 
| 2013 | Software & Services                                                    | 1.50                      | 6                       | 
| 2014 | Software & Services                                                    | 29.20                     | 146                     | 
| 2015 | Software & Services                                                    | 1523.73                   | 22856                   | 
| 2016 | Software & Services                                                    | 2538.44                   | 22846                   | 
| 2017 | Software & Services                                                    | 690.00                    | 690                     | 
| 2013 | Technology Hardware & Equipment                                        | 1053.45                   | 61100                   | 
| 2014 | Technology Hardware & Equipment                                        | 1780.44                   | 167361                  | 
| 2015 | Technology Hardware & Equipment                                        | 1895.66                   | 106157                  | 
| 2016 | Technology Hardware & Equipment                                        | 65.25                     | 1566                    | 
| 2017 | Technology Hardware & Equipment                                        | 788.34                    | 27592                   | 
| 2013 | Telecommunication Services                                             | 52.00                     | 52                      | 
| 2014 | Telecommunication Services                                             | 45.75                     | 183                     | 
| 2015 | Telecommunication Services                                             | 45.75                     | 183                     | 
| 2015 | Tires                                                                  | 1011.00                   | 2022                    | 
| 2015 | Tobacco                                                                | 1.00                      | 1                       | 
| 2015 | Trading Companies & Distributors and Commercial Services & Supplies    | 39.83                     | 239                     | 
| 2013 | Utilities                                                              | 61.00                     | 122                     | 
| 2016 | Utilities                                                              | 61.00                     | 122                     | 
```
SELECT P.year
,I.industry_group
,round(avg(P.carbon_footprint_pcf),2) AS 'Average_carbon_footprints'
,sum(P.carbon_footprint_pcf) AS 'Total_carbon_footprints' 
FROM product_emissions AS P
LEFT JOIN industry_groups AS I ON P.industry_group_id = I.id
GROUP BY I.industry_group,P.year
```                                                                                                                                                                                                                                                                                                                                                                                                                                 
