
# **COVID-19 Data Exploration Project**

## **Overview**
The COVID-19 pandemic has had a profound global impact, making data analysis an essential tool for understanding its spread and consequences. This project leverages SQL to analyze a dataset of COVID-19 cases, deaths, and population data to uncover critical insights.

### **Objective**
- To analyze trends in infection and mortality rates globally and regionally.
- To calculate key metrics such as death percentages and infection rates.
- To identify countries and continents most affected by COVID-19.

---

## **Technologies and Skills Used**
- **SQL Techniques**:
  - Joins
  - Common Table Expressions (CTEs)
  - Temporary Tables
  - Window Functions
  - Aggregate Functions
  - Data Type Conversion
- **Database**: PortfolioProject
- **Data Cleaning and Transformation**:
  - Filtering null and irrelevant records.
  - Converting data types for consistency.

---

## **Dataset**
The dataset contains:
- **Fields**: `Location`, `Date`, `Total Cases`, `New Cases`, `Total Deaths`, `Population`, `Continent`, etc.
- **Scope**: COVID-19 statistics across multiple countries and continents.
- **Source**: The data is stored in the SQL table `PortfolioProject..CovidDeaths`.

---

## **Analysis Steps**

### **1. Data Exploration**
- Query 1: Filter data to exclude rows where `continent` is null.
```sql
SELECT * 
FROM PortfolioProject..CovidDeaths
WHERE continent IS NOT NULL
ORDER BY 3, 4;
```

- Query 2: Select essential fields for basic exploration.
```sql
SELECT Location, Date, Total_Cases, New_Cases, Total_Deaths, Population
FROM PortfolioProject..CovidDeaths
WHERE continent IS NOT NULL
ORDER BY 1, 2;
```

---

### **2. Key Metrics**

#### **A. Death Percentage**
- Formula: `(Total Deaths / Total Cases) * 100`
- Query:
```sql
SELECT Location, Date, Total_Cases, Total_Deaths, 
       (Total_Deaths / Total_Cases) * 100 AS DeathPercentage
FROM PortfolioProject..CovidDeaths
WHERE Location LIKE '%states%'
  AND continent IS NOT NULL
ORDER BY 1, 2;
```

#### **B. Infection Rate (Population Percentage)**
- Formula: `(Total Cases / Population) * 100`
- Query:
```sql
SELECT Location, Date, Population, Total_Cases, 
       (Total_Cases / Population) * 100 AS PercentPopulationInfected
FROM PortfolioProject..CovidDeaths
ORDER BY 1, 2;
```

---

### **3. Identifying Extremes**

#### **A. Countries with Highest Infection Rates**
- Query:
```sql
SELECT Location, Population, 
       MAX(Total_Cases) AS HighestInfectionCount,  
       MAX((Total_Cases / Population) * 100) AS PercentPopulationInfected
FROM PortfolioProject..CovidDeaths
GROUP BY Location, Population
ORDER BY PercentPopulationInfected DESC;
```

#### **B. Countries with Highest Death Counts**
- Query:
```sql
SELECT Location, MAX(CAST(Total_Deaths AS INT)) AS TotalDeathCount
FROM PortfolioProject..CovidDeaths
WHERE continent IS NOT NULL
GROUP BY Location
ORDER BY TotalDeathCount DESC;
```

---

### **4. Continent-Level Analysis**

#### **A. Death Counts by Continent**
- Query:
```sql
SELECT Continent, MAX(CAST(Total_Deaths AS INT)) AS TotalDeathCount
FROM PortfolioProject..CovidDeaths
WHERE continent IS NOT NULL
GROUP BY Continent
ORDER BY TotalDeathCount DESC;
```

---

### **5. Global Aggregates**
#### **Global Totals**
- Query:
```sql
SELECT SUM(New_Cases) AS TotalCases, 
       SUM(New_Deaths) AS TotalDeaths, 
       (SUM(New_Deaths) / SUM(New_Cases)) * 100 AS DeathRate
FROM PortfolioProject..CovidDeaths;
```

---

## **Insights**

1. **Death Likelihood**:
   - Regions like the United States had a significant death percentage among confirmed cases.
   - Death likelihood highlights disparities in healthcare systems.

2. **Infection Rates**:
   - Some countries had infection rates exceeding 20% of their populations.
   - Countries with dense populations or limited healthcare infrastructure were the most impacted.

3. **Global Trends**:
   - The overall death rate was calculated to understand the severity of the pandemic worldwide.
   - Insights provide a benchmark for comparing global versus regional impacts.

4. **Continental Impact**:
   - Europe and North America recorded the highest death counts.
   - Analysis by continent revealed stark contrasts in how COVID-19 spread and affected populations.

---

## **Challenges and Solutions**

- **Data Quality**:
  - Null or incomplete values were excluded to maintain accuracy.
  - Data types were standardized using `CAST` and `CONVERT` for numeric calculations.

- **Handling Large Data**:
  - Used aggregate functions and filtering to focus on meaningful data subsets.

- **Insights Presentation**:
  - Organized results into hierarchical levels (country, continent, global) for clarity.

---

## **Next Steps**
1. **Integrate New Datasets**:
   - Include vaccination data or economic impacts for broader insights.
2. **Data Visualization**:
   - Create interactive dashboards using Tableau or Power BI to visually represent trends.
3. **Time-Series Analysis**:
   - Analyze how metrics evolved across different pandemic waves.

---

## **Project Files**
- **SQL Script**: [Download the full SQL file here](#) *(Link to be added on GitHub)*.

