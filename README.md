# 🌤️ Weather Data ETL Pipeline

## 📌 Project Overview

This project implements an **ETL (Extract, Transform, Load) pipeline using Python** to collect real-time weather data for 10 cities in Egypt using the **OpenWeatherMap API**, transform and clean the data, and load the final dataset into **Azure SQL Server**.

The project demonstrates a complete data engineering workflow from API data extraction to structured storage in a relational database.

---

## 🎯 Objectives

* Extract weather data from the OpenWeatherMap API.
* Collect weather information for 10 Egyptian cities.
* Clean and transform the extracted data.
* Convert temperatures from Kelvin to Celsius.
* Create additional business-related categories.
* Validate the transformed dataset.
* Load the final data into Azure SQL Server using PyODBC.
* Store the data in a structured SQL table.

---

## 🛠️ Technologies Used

* **Python**
* **Requests** – API requests
* **Pandas** – Data cleaning and transformation
* **OpenWeatherMap API** – Weather data source
* **PyODBC** – SQL Server connection
* **Azure SQL Server** – Data storage

---

## 📍 Cities Covered

The pipeline collects weather data for the following cities:

```python
cities = [
    "Cairo",
    "Giza",
    "Alexandria",
    "Port Said",
    "Suez",
    "Ismailia",
    "Mansoura",
    "Tanta",
    "Luxor",
    "Aswan"
]
```

---

# 🔄 ETL Pipeline

## 1️⃣ Extract

The pipeline connects to the **OpenWeatherMap Current Weather API** and retrieves weather information for each city.

The extracted data includes:

* City
* Country
* Latitude
* Longitude
* Temperature
* Pressure
* Humidity
* Wind Speed
* Weather Main
* Weather Description

Example API request:

```python
url = "https://api.openweathermap.org/data/2.5/weather"

params = {
    "appid": "YOUR_API_KEY",
    "q": "Cairo"
}

response = requests.get(url, params=params)
data = response.json()
```

The API response is collected for all 10 cities and prepared for transformation.

---

## 2️⃣ Transform

After extracting the data, the pipeline performs several transformation and cleaning steps.

### 🧹 Data Cleaning

* Standardized city names.
* Handled missing values.
* Converted numerical fields to appropriate data types.
* Validated the final dataset.

### 🌡️ Temperature Conversion

OpenWeatherMap returns temperature values in Kelvin.

The pipeline converts all temperatures to **Celsius (°C)**:

```text
Celsius = Kelvin - 270
```

### 🗺️ Region Classification

A `Region` column was created to classify cities into Egyptian regions:

* Greater Cairo
* North Coast
* Lower Egypt
* Upper Egypt
* Canal
* Sinai
* Red Sea

### 🌡️ Temperature Category

A `TemperatureCategory` column was created to classify temperatures as:

* Cold
* Moderate
* Hot

### 💧 Humidity Category

A `HumidityCategory` column was created to classify humidity levels as:

* Low
* Medium
* High

### ⏰ Ingestion Time

An `IngestionTime` column was added to record the date and time when the weather data was processed by the ETL pipeline.

---

# 3️⃣ Load

The transformed data is loaded into **Azure SQL Server** using **PyODBC**.

The pipeline connects to the Azure SQL Server database and creates a table named:

```text
in this case --> My name (Habiba2)
```

The table uses an automatically generated ID through SQL Server `IDENTITY`.

The transformed records are then inserted into the SQL Server table using **PyODBC**.

---

# 📊 Database Schema

The final table contains the following columns:

| Column              | Description                   |
| ------------------- | ----------------------------- |
| City                | City name                     |
| Country             | Country code                  |
| Latitude            | Geographic latitude           |
| Longitude           | Geographic longitude          |
| Temperature         | Temperature in Celsius        |
| Pressure            | Atmospheric pressure          |
| Humidity            | Humidity percentage           |
| WindSpeed           | Wind speed                    |
| Region              | Egyptian geographical region  |
| TemperatureCategory | Cold / Comfortable / Hot      |
| HumidityCategory    | Low / Comfortable / High      |

---

# 🔐 Security

The API key and database credentials should **not be stored directly in the source code or uploaded to GitHub**.

For example:

```python
API_KEY = os.getenv("OPENWEATHER_API_KEY")
```

Database credentials can also be stored using environment variables.

A `.env` file can be used locally and added to `.gitignore`:

```text
.env
```

---

# 🔁 Final ETL Flow

```text
        OpenWeatherMap API
                 │
                 ▼
              EXTRACT
                 │
                 ▼
        Raw Weather Data
                 │
                 ▼
             TRANSFORM
        ┌────────┼────────┐
        │        │        │
   Clean Data  Celsius  Categories
        │        │        │
        └────────┼────────┘
                 │
          Ingestion Time
                 │
                 ▼
              VALIDATE
                 │
                 ▼
               LOAD
                 │
                 ▼
          Azure SQL Server
                 │
                 ▼
              Mydata
```

---

# 🚀 Key Data Engineering Concepts Demonstrated

This project demonstrates practical experience with:

* ETL Pipeline Development
* REST API Data Extraction
* Data Cleaning
* Data Transformation
* Data Validation
* Data Categorization
* Python Data Processing
* Pandas
* API Integration
* PyODBC
* Azure SQL Server
* Relational Database Design
* Automated Data Ingestion

---

# 📁 Project Structure

```text
Weather-Data-ETL/
│
├── weather_etl.py
├── README.md
├── requirements.txt
└── .gitignore
```

---

## ▶️ How to Run

### 1. Install the required libraries

```bash
pip install requests pandas pyodbc
```

### 2. Add your OpenWeatherMap API key

Set your API key as an environment variable:

```text
OPENWEATHER_API_KEY=your_api_key
```

### 3. Configure the Azure SQL Server connection

Add your database connection details using environment variables.

### 4. Run the ETL pipeline

```bash
python weather_etl.py
```

The pipeline will:

```text
Extract → Transform → Validate → Load
```

and store the final weather dataset in Azure SQL Server.

---



Computer and Communication Engineering Student

### Project Focus

**Data Engineering | ETL | Python | SQL Server | API Integration**
