# NYC Yellow Taxi – Sample Dataset

This project uses a sampled version of the official **NYC Yellow Taxi Trip Records** dataset published by the New York City Taxi & Limousine Commission (TLC).

Due to GitHub file size limitations and best practices for analytics repositories, the full dataset and derived Parquet files are **not stored in this repository**.

---

## Original Data Source

- **Provider:** NYC Taxi & Limousine Commission (TLC)
- **Official Portal:** https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
- **Dataset:** Yellow Taxi Trip Records
- **Year Used:** 2024

---

## Sample Description

- **Sampling Method:** Random sampling
- **Sample Size:** 7% of total 2024 Yellow Taxi trips
- **Rows after cleaning:** ~2.49 million
- **Storage Format:** Apache Parquet
- **Partitioning:** Spark default output partitions

This sample was created to:
- Enable scalable analysis in PySpark
- Preserve real-world data distributions
- Avoid storing very large files in GitHub

---

## Expected Schema (Key Columns)

| Column Name | Description |
|------------|------------|
| tpep_pickup_datetime | Trip pickup timestamp |
| tpep_dropoff_datetime | Trip dropoff timestamp |
| passenger_count | Number of passengers |
| trip_distance | Trip distance (miles) |
| fare_amount | Base fare |
| total_amount | Total trip charge |
| tip_amount | Tip amount |
| PULocationID | Pickup taxi zone ID |
| DOLocationID | Dropoff taxi zone ID |

Additional engineered features were created during analysis (trip duration, speed, fare per mile, time features).

---

## How to Reproduce the Sample

Download the raw Yellow Taxi data from the TLC website and run the sampling step in the notebook:

```python
df_sample = df_full.sample(fraction=0.07, seed=42)
df_sample.write.mode("overwrite").parquet("data/samples/nyc_taxi_2024_sample_7pct.parquet")
