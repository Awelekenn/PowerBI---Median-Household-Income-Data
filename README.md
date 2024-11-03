**Description**:

Data analysis of the Median Household income .  **The goal of this project is to study and analyse the median income household of U.S. states and territories over the years 2010–2021, analysing the income values for each year, as well as the average annual growth rate for each state and Washington, D.C**. To do so, Power Bi will be employed as data manipulation and management tools.


---

## Introduction

This analysis focuses on understanding the income growth trends across U.S. states from 2010 to 2021, with the goal of identifying states with the highest economic growth between these years. This analysis could be used by companies looking to expand, in order to identify states with rapidly increasing income levels, which might indicate a growing consumer base with more disposable income. 

In order to carry out the proposed analysis, **the following questions are defined** to be resolved throughout the analysis:

1. **Growth Rate Analysis**: Compare the income growth rate for different states over the period 2010-2021 to see which states have experienced the fastest income growth.
2. a) **State-to-State Comparison:** Compare the median income values of different states at specific points in time (e.g., 2021 vs. 2010) to identify which states have the highest or lowest median household incomes.
b) **Growth Rate Comparison**: Analyse how the growth rates compare across different states. This can help identify which states have been improving economically at a faster pace and which have lagged behind.
3. **Ranking Analysis**
a) **State Ranking**: Rank states by median household income for any given year to identify the top and bottom performers.
b) **Rank Changes Over Time**: Track how states' rankings change over the 2010–2021 period. This helps in understanding which states have improved or declined in their income standings.
4. **Regional Analysis**
a) **Regional Trends**: Group states by region (e.g., Northeast, Midwest, South, and West) to see if there are any broader regional trends in income growth or declines.
b) **Outliers**: Identify outlier states with either exceptionally high or low growth compared to their region or the national average.
5. a) Which states have experienced the **highest growth** in household income from 2010 to 2021?
b) How does the income growth in **high-income states like Washington D.C. compare to lower-income states?**
c) Which states' growth rates suggest a **thriving economy**, and which states are falling behind?

---

## Dataset

**Source**:

The dataset was scraped from Wikipedia: [Link to dataset](https://en.wikipedia.org/wiki/list_of_U.S._states_and_territories_by_income)."

**Description**:

- *State*: Name of U.S. state or territory
- *Median Income (2010–2021)*: Household median income for each year
- *Average Annual Growth Rate*: The yearly percentage increase in income.

---

## Methodology

Outline the steps taken in the analysis. This could include:

1. **Data Collection**: The data was collected by web scraping via Power BI 
2. **Tools & Libraries**: Power Bi
3. **Assumptions**: The assumptions made for this analysis was that the 2020 column was not included as this was omitted after scraping the dataset from Wikipedia.

---

## Data Cleaning & Transformation

- Used PowerQuery to convert the first row to header
- Converted data type of ‘2010 to 2021’ year columns from **text** to whole number, changed using locale as Power Query  was unable to detect data type
- Entered ‘Regions’ table in order to assign each state to its region. Merged the ‘Regions’ table to the Median Income Table, connecting the tables by the States column
- Created an income rating for each state, categorising them into High, Mid or Low income, depending on what their average income over the period of 2010 to 2021 using this DAX expression

```jsx
Average Income Rating = IF('Median Income'[Average Income]<= 60000, "Low Income", IF('Median Income'[Average Income]<=75000, "Mid Income","High Income")
```

- Created new measure using DAX expression to generate the rank for the states from 2010 & 2021

```jsx
2010 Rank = RANKX(ALL('Median Income'[States]),'Median Income'[2010 income], ,DESC)
```

- Created a new column using DAX expression to show the difference between the median income in 2021 and 2010

```jsx
2021 - 2010 income= CALCULATE(SUM('Median Income'[2021])) - CALCULATE(SUM('Median Income'[2010]))
```

- Created an Average Income column using this DAX expression to analyse how it compares against different states and regions

```jsx
	Average Income = DIVIDE('Median Income'[2021] + 'Median Income'[2019] + 'Median Income'[2018]+ 'Median Income'[2017]+ 'Median Income'[2016]+ 'Median Income'[2015]+ 'Median Income'[2014]+ 'Median Income'[2013] + 'Median Income'[2012] + 'Median Income'[2011] + 'Median Income'[2010],10)
```

---

## Analysis & Insights

 - Average median income has generally **increased** from 2010 to 2021

- Northeastern states have seen the highest growth rate since 2010 at 3.11%

- Maryland was the top ranked state from 2010 through to 2021

-Top 3 states with the highest growth rate: Oregon, Idaho & Colorado

- Mid Income states have seen the highest growth rate at 3.21%

There were some anomalies: Idaho experienced an exceptionally high growth rate at 4% while Louisiana & Alaska experienced a very low growth rate at 1.89% and 1.75%

The average growth rate across all states is **3.04%**

**Key Questions Addressed**:

1. **Growth Rate Analysis**: Compare the income growth rate for different states over the period 2010-2021 to see which states have experienced the fastest income growth.
- *Oregon, Idaho, Colorado, Washington, and Washington D.C. emerged as the top 5 states with the fastest income growth rates during this period, with growth rates of 4%, 3.97%, 3.90%, 3.86%, and 3.68%, respectively.*
1. a) **State-to-State Comparison:** Compare the median income values of different states at specific points in time (e.g., 2021 vs. 2010) to identify which states have the highest or lowest median household incomes.
    - **Top performers by median income, comparing 2021 to 2010:**
        1. **Maryland** - (2021: $90,203 vs. 2010: $68,854)
        2. **New Jersey** - (2021: $89,296 vs. 2010: $67,681)
        3. **Massachusetts** - (2021: $89,645 vs. 2010: $62,072)
        4. **New Hampshire** - (2021: $88,465 vs. 2010: $61,042)
        5. **Washington D.C.** - (2021: $90,088 vs. 2010: $60,903)
    - **Bottom performers by median income, comparing 2021 to 2010:**
        1. **Louisiana** - (2021: $52,087 vs. 2010: $42,505)
        2. **Alabama** - (2021: $53,913 vs. 2010: $40,474)
        3. **Alaska** - (2021: $52,528 vs. 2010: $38,307)
        4. **West Virginia** - (2021: $51,248 vs. 2010: $38,218)
        5. **Mississippi** - (2021: $48,716 vs. 2010: $36,851)
    
    b) **Growth Rate Comparison**: Analyse how the growth rates compare across different states. This can help identify which states have been improving economically at a faster pace and which have lagged behind.
    
- **Maryland, Washington D.C., and Massachusetts** have experienced faster economic improvement, while **Louisiana, West Virginia, and Mississippi** seem to be lagging.

**Ranking Analysis**
a) **State Ranking**: Rank states by median household income for any given year to identify the top and bottom performers.

**For 2021,** states were ranked from 1 to 52 by their median household incomes:

- **Top-ranked states**: Maryland (1), Washington D.C. (2), Massachusetts (3), New Jersey (4), New Hampshire (5)
- **Lowest-ranked states**: Alabama (48), Arkansas (49), Louisiana (50), West Virginia (51), Mississippi (52)

b) **Rank Changes Over Time**: Track how states' rankings change over the 2010–2021 period. This helps in understanding which states have improved or declined in their income standings.

- **Maryland** remained ranked at number 1 in both 2010 and 2021. However, some states saw major declines, including **Alaska** (ranked 3 in 2010, dropped to 13 in 2021), **Delaware** (ranked 11 in 2010, dropped to 20 in 2021), **Nevada** (ranked 20 in 2010, dropped to 30 in 2021), and **Wyoming** (ranked 17 in 2010, dropped to 33 in 2021).
- Some states improved their rankings significantly, such as **Oregon** (from rank 31 in 2010 to rank 19 in 2021) and **Idaho** (from rank 40 in 2010 to rank 29 in 2021).
- **Mississippi** remained the lowest-ranked state, holding its 52nd position in both 2010 and 2021.

1. **Regional Analysis**
a) **Regional Trends**: Group states by region (e.g., Northeast, Midwest, South, and West) to see if there are any broader regional trends in income growth or declines.

All regions saw income growth from 2010 to 2021:

- **Western Region** had the highest increase at 3.17%.
- **Northeast** followed closely at 3.11%.
- **Midwest** had a growth of 3%.
- The **Southern Region** saw the lowest growth at 2.88%.

b) **Outliers**: Identify outlier states with either exceptionally high or low growth compared to their region or the national average.

- **Louisiana** showed notably low growth at 1.89%, far below both the Southern regional and national averages. **Alaska** had the lowest growth rate nationwide at 1.75%.
- **Washington D.C.** had an exceptionally high growth rate of 3.68%, outperforming both the Southern region and national averages, while **Oregon** also stood out with a high growth rate of 4%.
1. a) Which states have experienced the **highest growth** in household income from 2010 to 2021?
- **Washington D.C.** experienced the highest income growth, with a $29,200 increase from 2010 to 2021.

b) How does the income growth in **high-income states like Washington D.C. compare to lower-income states?**

- High-income states saw an average growth rate of 2.97%, while low-income states had a growth rate of 2.73%. The difference in growth rates between these groups was not very large.

c) Which states' growth rates suggest a **thriving economy**, and which states are falling behind?

- States with growth rates indicating a thriving economy include **Oregon, Idaho, and Colorado**.
- States falling behind include **Mississippi, Louisiana, and West Virginia**.

---

## Visualisations

Provide a brief overview of the visualisations included in the project.

For example:

- **Bar Chart**: Top 10 states by income growth (2010-2021)

![Screenshot 2024-10-24 at 17 44 41](https://github.com/user-attachments/assets/9a10322a-610f-453f-bb63-18fe7686f313)

- **Bar Chart**: Comparison between the states with the lowest & highest median income(2010-2021)

![Screenshot 2024-10-24 at 17 45 07](https://github.com/user-attachments/assets/8b789ced-c3bb-4412-b86d-f486540433d5)

![Screenshot 2024-10-24 at 17 45 25](https://github.com/user-attachments/assets/e3822d92-fe22-450a-842f-eb5152c6bcef)

- **Line Chart:**  Average income comparison between states in 2010 and 2021

![line chart ](https://github.com/user-attachments/assets/c20a6a47-e4d4-467c-a839-e8c6364e1443)

- Ranking by States between Highest to the Lowest Ranked

![ranking by states](https://github.com/user-attachments/assets/bd6785a6-7a37-4c65-8f57-d17d05330f06)

- Changes in the state rankings in 2010 & 2021

![Screenshot 2024-10-24 at 17 46 57](https://github.com/user-attachments/assets/326fd49b-c000-44ea-9295-e4c345b5103e)

- Region Comparison of Average Income

![Screenshot 2024-10-24 at 17 47 12](https://github.com/user-attachments/assets/e7326d2d-7e26-43ec-a80d-7e27255fb73c)

- Growth rate per region from 2010 to 2021

![- Growth rate per region from 2010 to 2021 ](https://github.com/user-attachments/assets/a18a4597-deda-4f82-9b23-d036949671a9)

- Distribution in growth rate and income to show outliers

![- Distribution in growth rate and income to show outliers ](https://github.com/user-attachments/assets/42065936-49fa-43c7-92e4-a5670c3686f7)

- **Bar Chart**: Top 5 states by average income

![bar chart](https://github.com/user-attachments/assets/f9539534-6cc8-48ed-93b7-e7f9fe6328fe)

- Comparison of Growth Rate by their income rating

![Screenshot 2024-10-24 at 17 48 49](https://github.com/user-attachments/assets/915843a5-c44d-4289-adc6-c36375b2b5c9)

- Map distribution showing states in High , Mid & Low income regions

![Screenshot 2024-10-24 at 17 49 21](https://github.com/user-attachments/assets/7187bfc7-6fab-4f1b-acc3-b0c741266366)

---

## Conclusions & Recommendations


- States in the West have shown the highest growth rates, which would suggest that a strong economic boost
- Focus economic support and development initiatives in lagging states like **Louisiana, Mississippi, and West Virginia**, which have shown slower growth and lower median incomes.
- Continue supporting states with fast-growing economies like **Oregon, Idaho, and Colorado** to maintain and expand their growth.

---
