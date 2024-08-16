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
                                                                                                                                                                                                                                                                                                                                                                                                                                 
