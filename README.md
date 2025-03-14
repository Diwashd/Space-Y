# Report on SpaceX Launch Data Analysis Using API and Web Scraping

## **Introduction**

In this assignment, I worked with SpaceX launch data to analyze past launches using the SpaceX REST API. The goal was to collect, clean, and process data to gain insights into rocket launches and prepare it for further analysis, including predicting whether SpaceX would attempt to land a rocket.

## **Key Learnings**

### **1. Collecting Data Using an API**

- Utilized the `requests` library to make a **GET request** to the SpaceX API (`api.spacexdata.com/v4/launches/past`).
- Parsed the JSON response using `.json()` and converted it into a structured Pandas DataFrame using `json_normalize()`.
- Understood the structure of API responses, which consisted of lists of JSON objects representing different launches.
- Identified that some fields contained only IDs (e.g., `rocket`, `launchpad`), requiring additional API requests to retrieve full details.

### **2. Web Scraping Falcon 9 Launch Data**

- Used the `BeautifulSoup` library to scrape Falcon 9 launch records from Wikipedia.
- Parsed the HTML tables and converted them into a Pandas DataFrame for further processing.
- Learned how to extract meaningful data from structured web content.

### **3. Data Wrangling and Preprocessing**

- Filtered the dataset to **only include Falcon 9 launches**, removing Falcon 1 data using:
  ```python
  data_falcon9 = data[data['BoosterVersion'] != 'Falcon 1']
  ```
- Reset the `FlightNumber` column to maintain a sequential order after filtering.
- Identified missing values in the dataset using:
  ```python
  data_falcon9.isnull().sum()
  ```

### **4. Handling Missing Values**

- Found missing values in the `PayloadMass` column and handled them by computing the mean:
  ```python
  payload_mass_mean = data_falcon9['PayloadMass'].mean()
  ```
- Replaced `NaN` values with the computed mean:
  ```python
  data_falcon9['PayloadMass'].fillna(payload_mass_mean, inplace=True)
  ```
- Retained `None` values in the `LandingPad` column since they indicate when a landing pad was not used.

### **5. Exporting the Cleaned Dataset**

- Saved the processed dataset to a CSV file for further analysis:
  ```python
  data_falcon9.to_csv('dataset_part_1.csv', index=False)
  ```

## **Conclusion**

Through this assignment, I gained hands-on experience with:

- Extracting data from APIs and handling structured JSON responses.
- Web scraping and parsing HTML tables into usable datasets.
- Filtering and cleaning data by handling missing values.
- Preparing a dataset for predictive modeling and further analysis.

This foundational knowledge will be valuable in real-world data science projects where APIs and web scraping are essential for data collection and preprocessing.

## **Final Takeaway**

✅ **SpaceX analysis provided a solid foundation** in data extraction, cleaning, and wrangling.

🚀 **For SpaceY, we can elevate the analysis by:**

- Enhancing **API structure** and enabling **real-time data streaming**.
- Automating **web scraping** from multiple sources.
- Using **machine learning** for **predictive missing value handling** and **launch success prediction**.
- Storing data in **databases (SQL/NoSQL)** instead of CSV files for better scalability.
- Building a **real-time dashboard** for better visualization.

Would you like a **more detailed plan** on implementing these improvements for SpaceY? 🚀
