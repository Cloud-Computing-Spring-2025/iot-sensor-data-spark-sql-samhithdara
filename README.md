

# IoT Sensor Data Processing using PySpark

This project processes and analyzes IoT sensor data using PySpark. The pipeline performs data loading, cleaning, filtering, aggregation, time-based analysis, ranking, and pivot-based interpretation.

## Dataset

The dataset used is `sensor_data.csv` which contains the following fields:
- `sensor_id`: Unique ID of the sensor
- `location`: Physical location of the sensor
- `timestamp`: Timestamp of the reading
- `temperature`: Temperature recorded by the sensor
- `humidity`: Humidity recorded by the sensor
- `sensor_type`: Type of sensor recorded the data.

---

## Tasks & Description

### ✅ Task 1: Load & Basic Exploration
- Load the CSV data into a Spark DataFrame.
- Display the first 5 rows.
- Count the total number of records.
- Retrieve distinct locations.
- Save the full DataFrame to `task1_output.csv`.

### ✅ Task 2: Filtering & Simple Aggregations
- Filter readings where temperature is between **18°C and 30°C**.
- Count and print the number of in-range and out-of-range readings.
- Compute average **temperature** and **humidity** per location.
- Save the aggregated results to `task2_output.csv`.

### ✅ Task 3: Time-Based Analysis
- Convert `timestamp` string into a Spark timestamp format.
- Extract the **hour** of the day from the timestamp.
- Compute average temperature grouped by hour.
- Save the results to `task3_output.csv`.

### ✅ Task 4: Ranking Sensors by Temperature
- Compute the average temperature for each sensor.
- Rank sensors based on their average temperature using Spark SQL `rank()` function.
- Display the top 5 ranked sensors.
- Save the ranked sensor data to `task4_output.csv`.

### ✅ Task 5: Pivot & Interpretation
- Pivot the data to show **hourly average temperature** for each location.
- Create a matrix-like structure with locations as rows and hours as columns.
- Save the pivoted table to `task5_output.csv`.

---

## How to Run

### 🔧 Prerequisites
- Python 3.x
- Apache Spark installed (`pyspark`)
- `sensor_data.csv` placed in the same directory as the script

###  Execution
Run the following command:

```bash
spark-submit sensor_analysis.py
```

Make sure the filename is the same as your script name.

---

## Output

Each task's results are saved as a CSV file in the working directory:

- `task1_output.csv` – Raw loaded data
- `task2_output.csv` – Filtered and aggregated temperature/humidity per location
- `task3_output.csv` – Hourly temperature trends
- `task4_output.csv` – Ranked sensors based on average temperature
- `task5_output.csv` – Pivot table showing average hourly temperatures by location

---

## Sample Output (Console)

```
+---------+-------------------+-----------+--------+----------------+-----------+
|sensor_id|          timestamp|temperature|humidity|        location|sensor_type|
+---------+-------------------+-----------+--------+----------------+-----------+
|     1095|2025-04-06 21:59:32|      22.26|   34.61|BuildingB_Floor1|      TypeA|
|     1091|2025-04-04 15:38:18|      30.12|   64.46|BuildingB_Floor1|      TypeC|
|     1014|2025-04-05 00:05:26|      20.91|   56.04|BuildingA_Floor1|      TypeC|
|     1013|2025-04-05 00:50:21|      30.19|   37.17|BuildingB_Floor2|      TypeB|
|     1071|2025-04-05 07:20:41|      17.46|   58.26|BuildingA_Floor2|      TypeC|
+---------+-------------------+-----------+--------+----------------+-----------+
only showing top 5 rows

Total number of records: 1000
+----------------+
|        location|
+----------------+
|BuildingA_Floor1|
|BuildingB_Floor2|
|BuildingA_Floor2|
|BuildingB_Floor1|
+----------------+

Out of range: 408, In range: 592
+----------------+------------------+------------------+
|        location|   avg_temperature|      avg_humidity|
+----------------+------------------+------------------+
|BuildingB_Floor2| 24.35450331125827|55.118211920529816|
|BuildingA_Floor1| 24.15565217391304|55.391801242236035|
|BuildingA_Floor2|  23.9957258064516| 55.47677419354837|
|BuildingB_Floor1|23.848910256410246| 52.98820512820512|
+----------------+------------------+------------------+

+-----------+------------------+
|hour_of_day|          avg_temp|
+-----------+------------------+
|          0|26.513269230769232|
|          1|25.744705882352946|
|          2|26.135909090909085|
|          3| 24.93977272727273|
|          4| 24.99648648648649|
|          5| 23.94849056603773|
|          6| 25.32945945945946|
|          7|25.875609756097557|
|          8|24.397692307692303|
|          9| 26.04822222222223|
|         10| 23.95971428571429|
|         11|23.809499999999996|
|         12|23.756666666666664|
|         13|24.578620689655175|
|         14|           24.3874|
|         15|25.672380952380948|
|         16| 25.11936170212766|
|         17|24.441538461538464|
|         18|24.911190476190477|
|         19| 25.42578947368421|
+-----------+------------------+
only showing top 20 rows


+---------+------------------+---------+
|sensor_id|          avg_temp|rank_temp|
+---------+------------------+---------+
|     1010|29.552500000000002|        1|
|     1080|29.009999999999998|        2|
|     1020|28.377999999999997|        3|
|     1093|28.172142857142855|        4|
|     1091|27.961666666666662|        5|
+---------+------------------+---------+
---
