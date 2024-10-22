### Exercise 1: Deploy Apache Spark and Perform ETL on Air Quality Data

1. **Set up Minikube** on your local machine.
2. Use Helm to deploy **Apache Spark** on the Minikube cluster.
3. **Scale Spark Workers** to ensure there are always 3 workers running.

**Dataset:**
Use the following air quality dataset:
- [Air Quality Data CSV](https://github.com/vincentarelbundock/Rdatasets/blob/master/csv/datasets/airquality.csv)

### ETL Task:

1. **Extract:**
   - Load the air quality CSV file into Spark. The file contains columns such as `Ozone`, `Solar.R`, `Wind`, `Temp`, and `Month`.

2. **Transform:**
   - **Select** the following columns: `Ozone`, `Temp`, and `Month`.
   - **Filter** the rows where `Ozone` levels exceed 50.
   - **Group** the data by `Month` and calculate the **average temperature (`Temp`)** for months where the `Ozone` levels are higher than 50.
   - **Sort** the results by the average temperature in descending order.

3. **Load:**
   - Save the transformed data back to the local file system in a new CSV file or a directory in Minikube.

**Deliverables:**
   - Helm values and Kubernetes configuration files.
   - PySpark script for the ETL process.
   - Screenshot showing 3 Spark workers running.
   - The resulting output CSV file or logs showing the output after the transformation.

**Tips:**

- **Data Loading in Spark:** You can use `spark.read.csv()` to load the CSV file and provide options such as `header=True` to ensure that Spark correctly identifies the columns. Example:

  ```python
  df = spark.read.csv("/path/to/airquality.csv", header=True, inferSchema=True)
  ```

- **Filtering Rows:** For filtering rows, you can use Spark's `.filter()` method. To filter `Ozone` values greater than 50, you might use:

  ```python
  filtered_df = df.filter(df.Ozone > 50)
  ```

- **Grouping and Aggregation:** To group by `Month` and calculate the average temperature, you can use the `.groupBy()` and `.agg()` functions. Example:

  ```python
  result_df = filtered_df.groupBy("Month").agg({"Temp": "avg"}).orderBy("avg(Temp)", ascending=False)
  ```

- **Saving the Output:** To write the transformed data back to a CSV file:

  ```python
  result_df.write.csv("/path/to/output/dir", header=True)
  ```

- **Handling Null Values:** Some columns might contain null or missing values. You can handle these using the `.na.drop()` or `.na.fill()` methods before filtering or grouping.

After finishing this Exercise, proceed to [Exercise 2](Task-2.md)