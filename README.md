# COVID-19 Data Exploration Project USING SQL

---

## **Project Overview**
I undertook the COVID-19 Data Exploration project to analyze global COVID-19 trends using SQL. The goal was to explore key metrics like total cases, new cases, total deaths, and population demographics, uncovering patterns and insights to better understand the pandemic's impact. This project was a hands-on exercise to enhance my SQL skills and apply them to real-world data.

### **Data Source**
The dataset for this project was sourced from **Our World in Data**, specifically from their [COVID-19 dataset](https://ourworldindata.org/covid-deaths). This dataset is well-recognized for providing comprehensive global COVID-19 statistics, including case counts, mortality data, and country-specific demographic and healthcare information.

---

## **Dataset Overview**
The dataset contains global COVID-19 data, covering multiple continents, countries, and dates. Key attributes I analyzed include:
- **COVID-19 Metrics**: Total cases, new cases, total deaths, and new deaths.
- **Demographics**: Population, GDP per capita, extreme poverty levels, smoking prevalence, diabetes prevalence, and life expectancy.
- **Healthcare Data**: Hospital beds per thousand and handwashing facilities availability.
- **Additional Metrics**: Human Development Index, cardiovascular death rates, and more.

This dataset provided a comprehensive view of the pandemic's spread, its impact on different regions, and how healthcare infrastructure influenced outcomes.

---

## **Project Approach and SQL Techniques**

I used advanced SQL techniques to explore, clean, and analyze the dataset. The process included filtering, aggregating, and visualizing the data to derive meaningful insights. Below is an outline of the analysis:

### **Data Exploration**

1. **Initial Data Selection**
   I began by extracting the main fields for exploration: `location`, `date`, `total_cases`, `new_cases`, `total_deaths`, and `population`. To focus on meaningful data, I filtered out records where the `continent` field was null. Sorting by location and date allowed me to analyze trends over time.

   **Query:**
   ```sql
   SELECT location, date, total_cases, new_cases, total_deaths, population
   FROM PortfolioProject..CovidDeaths
   WHERE continent IS NOT NULL
   ORDER BY location, date;
   ```

---

2. **Analyzing Total Cases vs Total Deaths**
   Next, I explored the relationship between total cases and total deaths to understand mortality rate trends. I calculated the mortality rate for each location as `(total_deaths / total_cases) * 100`.

   **Query:**
   ```sql
   SELECT location, 
          MAX(total_cases) AS max_cases, 
          MAX(total_deaths) AS max_deaths, 
          (MAX(total_deaths) * 100.0 / MAX(total_cases)) AS mortality_rate
   FROM PortfolioProject..CovidDeaths
   WHERE continent IS NOT NULL
   GROUP BY location
   ORDER BY mortality_rate DESC;
   ```

---

3. **New Cases and Population Analysis**
   I analyzed new COVID-19 cases as a percentage of the population to identify countries with high infection rates relative to their population. This highlighted regions most affected by the virus's spread.

   **Query:**
   ```sql
   SELECT location, 
          MAX(new_cases) AS peak_new_cases, 
          MAX(new_cases) * 100.0 / MAX(population) AS percent_population
   FROM PortfolioProject..CovidDeaths
   WHERE continent IS NOT NULL
   GROUP BY location
   ORDER BY percent_population DESC;
   ```

---

4. **Continent-wise Analysis**
   Aggregating data at the continent level, I compared COVID-19 trends across continents. Metrics like total cases, total deaths, and population percentages affected were analyzed.

   **Query:**
   ```sql
   SELECT continent, 
          SUM(total_cases) AS total_cases, 
          SUM(total_deaths) AS total_deaths, 
          SUM(total_cases) * 100.0 / SUM(population) AS infection_rate
   FROM PortfolioProject..CovidDeaths
   WHERE continent IS NOT NULL
   GROUP BY continent
   ORDER BY infection_rate DESC;
   ```

---

5. **Healthcare Infrastructure and COVID-19 Outcomes**
   Finally, I examined correlations between healthcare metrics (e.g., hospital beds per thousand) and COVID-19 outcomes. This analysis aimed to identify whether healthcare capacity influenced mortality rates.

   **Query:**
   ```sql
   SELECT location, 
          MAX(hospital_beds_per_thousand) AS hospital_beds, 
          MAX(total_deaths) * 100.0 / MAX(total_cases) AS mortality_rate
   FROM PortfolioProject..CovidDeaths
   WHERE continent IS NOT NULL
   GROUP BY location
   ORDER BY mortality_rate DESC;
   ```

---

## **Key Insights**
Through this project, I uncovered several meaningful insights:
1. **Global Mortality Rates**: Some countries showed disproportionately high mortality rates, often due to healthcare infrastructure challenges or delayed interventions.
2. **Population Impact**: Smaller nations with dense populations faced higher infection rates, highlighting their vulnerability.
3. **Healthcare Correlations**: Countries with more hospital beds per thousand had lower mortality rates, underlining the importance of healthcare preparedness.
4. **Continental Trends**: Infection and mortality rates varied significantly across continents, influenced by economic factors, demographics, and healthcare systems.

---

## **Visualizations and Further Analysis**

I identified several opportunities for visualizing and extending the analysis:

### **Visualizations**
1. **Global Heatmap**: A world map showing total cases and deaths with color gradients.
2. **Mortality Rate vs. Healthcare Infrastructure**: Scatter plot comparing hospital beds per thousand and mortality rates.
3. **Time-Series Trends**: Line graphs of total cases and deaths over time for specific regions.
4. **Continental Comparison**: Bar chart comparing infection and mortality rates by continent.
5. **Population Impact Pie Chart**: Pie chart of COVID-19 cases as a percentage of population.

### **Further Analysis**
1. **Economic Impact**: Exploring GDP per capita and poverty levels against COVID-19 outcomes.
2. **Demographic Vulnerabilities**: Investigating how factors like smoking prevalence and diabetes prevalence affected mortality rates.
3. **Predictive Modeling**: Using the data to predict future trends in infection and mortality rates.
4. **Time-Series Forecasting**: Analyzing trends in new cases and deaths to forecast future developments.

---

## **Conclusion**
This project allowed me to dive deep into SQL-based data exploration, deriving actionable insights from the COVID-19 dataset provided by [Our World in Data](https://ourworldindata.org/covid-deaths). By pairing SQL queries with the dataset, I was able to identify significant trends and relationships. I also identified opportunities for creating impactful visualizations and performing further predictive analyses, which can provide additional value to researchers and decision-makers. This project reinforced my SQL skills and gave me valuable experience analyzing large datasets to generate insights.
