### Exercise 2: Integrate Apache Airflow with Apache Spark

1. Use Helm to deploy **Apache Airflow** in the same Minikube cluster.
2. Configure Airflow to **connect with Spark**.
3. Create an Airflow **DAG** that:
   - Triggers the PySpark ETL job created in Exercise 1 on a schedule or manually.
   - Ensures Airflow logs and tracks the execution of the ETL process.

**Deliverables:**
   - Airflow DAG file.
   - Screenshot of Airflow showing successful DAG execution.
   - Logs/output from the Airflow task showing the ETL process.

**Tips:**

- **Airflow Installation:** Ensure that your Airflow setup includes the necessary dependencies for interacting with Spark. Use the Helm chart values to configure the Airflow environment to include these.

- **DAG Example:** A basic DAG in Airflow might look like this:

  ```python
  from airflow import DAG
  from airflow.operators.dummy_operator import DummyOperator
  from airflow.operators.bash_operator import BashOperator
  from datetime import datetime

  default_args = {
      'owner': 'airflow',
      'start_date': datetime(2024, 1, 1),
      'retries': 1,
  }

  with DAG('spark_etl_dag', default_args=default_args, schedule_interval='@daily') as dag:
      start = DummyOperator(task_id='start')

      run_spark_etl = BashOperator(
          task_id='run_spark_etl',
          bash_command='spark-submit /path/to/your_spark_script.py'
      )

      start >> run_spark_etl
  ```

- **Running Spark Jobs from Airflow:** To run Spark jobs from Airflow, you can use the `BashOperator` to trigger `spark-submit` with your PySpark script or use the `SparkSubmitOperator` if configured.

---

### Submission Guidelines:
1. Push all relevant files (Helm values, PySpark script, DAG file) and documentation to a GitHub repository.
2. Include screenshots of Spark workers, Airflow execution, and ETL logs/output.

---

### Expected Learning Outcomes:
- Deploy and configure Apache Spark and Airflow on Kubernetes using Minikube.
- Perform a simple ETL process to filter and transform air quality data with Spark.
- Use Airflow to orchestrate the ETL process.
