# Databricks ETL Pipeline 🚀

This repository contains a comprehensive Databricks ETL pipeline designed to process and validate data through various stages: Bronze, Silver, and Gold. 

The pipeline ensures data integrity and quality at each stage, transforming raw data into valuable insights. It includes scripts for configuration, setup, historical data loading, and testing in both batch and streaming modes. The project is structured to facilitate easy deployment and integration with Azure DevOps for continuous integration and delivery.

## Project Structure 📂


### Files and Directories

- **01-config.py**: Configuration settings for the pipeline.
- **02-setup.py**: Setup helper functions and initializations.
- **03-history-loader.py**: Loads historical data into the pipeline.
- **04-bronze.py**: Processes raw data into the Bronze stage.
- **05-silver.py**: Processes Bronze data into the Silver stage.
- **06-gold.py**: Processes Silver data into the Gold stage.
- **07-run.py**: Main script to run the pipeline.
- **08-batch-test.py**: Script to test the pipeline in batch mode.
- **09-stream-test.py**: Script to test the pipeline in streaming mode.
- **10-producer.py**: Produces test data for the pipeline.
- **azure_build_pipeline.yaml**: Azure DevOps pipeline configuration.

## Classes and Functions

### [05-silver.py](05-silver.py)

- **`Upserter`**: Class to handle upsert operations.
  - `__init__(self, merge_query, temp_view_name)`: Initializes the Upserter with a merge query and temporary view name.
  - `upsert(self, df_micro_batch, batch_id)`: Performs the upsert operation on the micro-batch DataFrame.

### [06-gold.py](06-gold.py)

- **`Gold`**: Class to handle Gold stage operations.
  - `__init__(self, env)`: Initializes the Gold stage with the environment.
  - `upsert_workout_bpm_summary(self, once=True, processing_time="15 seconds", startingVersion=0)`: Upserts workout BPM summary.
  - `upsert(self, once=True, processing_time="5 seconds")`: Upserts data.
  - `assert_count(self, table_name, expected_count, filter="true")`: Asserts the count of rows in a table.
  - `assert_rows(self, location, table_name, sets)`: Asserts the rows in a table.
  - `validate(self, sets)`: Validates the Gold stage data.

### [10-producer.py](10-producer.py)

- **`Producer`**: Class to produce test data.
  - `__init__(self)`: Initializes the Producer with configuration settings.
  - `user_registration(self, set_num)`: Produces user registration data.
  - `profile_cdc(self, set_num)`: Produces profile CDC data.
  - `workout(self, set_num)`: Produces workout data.
  - `bpm(self, set_num)`: Produces BPM data.
  - `gym_logins(self, set_num)`: Produces gym login data.
  - `produce(self, set_num)`: Produces all data sets.
  - `validate(self, sets)`: Validates the produced data.

## Running the Pipeline

1. Set up the environment by running the setup script:
    ```sh
    %run ./02-setup
    ```

2. Run the main pipeline script:
    ```sh
    %run ./07-run
    ```

3. To test the pipeline in batch mode, run:
    ```sh
    %run ./08-batch-test
    ```

4. To test the pipeline in streaming mode, run:
    ```sh
    %run ./09-stream-test
    ```

## Azure DevOps Pipeline

The Azure DevOps pipeline is configured in the `azure_build_pipeline.yaml` file. It includes steps to set up the Python environment, install dependencies, and publish build artifacts.

## License

This project is licensed under the MIT License.