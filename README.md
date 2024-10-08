# 🚀 Data Engineering & Analysis Project: Building a Scalable Data Pipeline from S3 to Snowflake with Databricks & PySpark 🚀

## 📊 Project Overview

This project covers the development of an end-to-end data pipeline integrating multiple tools to handle both data engineering and analysis. The focus is on storing, processing, and analyzing retail transaction data efficiently.

### 📌 Key Components:

1. **Data Storage**: A retail transactions CSV dataset is stored on **AWS S3** as a data lake.
2. **Data Processing**: The data is loaded and preprocessed on **Databricks** using **PySpark**.
3. **Data Storage**: The processed data is then pushed into **Snowflake** for scalable storage and analysis.

![Architecture Diagram](/images/arch.png) <!-- Replace with the actual path to your architecture image -->


## 🛠️ Technologies Used

- **AWS S3**: Data lake for storing raw data.
- **Databricks**: Processing data using PySpark.
- **Snowflake**: Scalable storage solution for processed data.

## 📈 Getting Started

### 1. Clone the Repository

To get started, clone this repository:

```bash
git clone https://github.com/abdelkhalek-haddany/ETL-Project-S3-Databricks-Pyspark-Snowflake.git
cd ETL-Project-S3-Databricks-Pyspark-Snowflake
```

### 2. Set up your AWS credentials for accessing S3

To interact with AWS S3, you'll need to configure your AWS credentials. Here’s how to do it:

1. **Create an AWS Account**: If you don’t have an account yet, sign up at [AWS](https://aws.amazon.com/).

2. **Create IAM User**:
   - Go to the [AWS Management Console](https://aws.amazon.com/console/).
   - Navigate to **IAM** (Identity and Access Management).
   - Click on **Users** and then **Add user**.
   - Enter a user name, select **Programmatic access**, and click **Next: Permissions**.
   - Choose **Attach existing policies directly**, and select **AmazonS3FullAccess** (or a custom policy with specific S3 permissions).
   - Click **Next: Tags**, then **Next: Review**, and finally **Create user**.
   - Note down the **Access Key ID** and **Secret Access Key**.

3. **Configure AWS CLI**:
   - Install the [AWS CLI](https://aws.amazon.com/cli/) if you haven't already.
   - Open your terminal and run the following command:
     ```bash
     aws configure
     ```
   - Enter your **Access Key ID**, **Secret Access Key**, and the **default region name** (e.g., `us-west-2`) when prompted.
   - You can skip the default output format by pressing Enter.

4. **Verify Configuration**:
   - Run the following command to test your configuration:
     ```bash
     aws s3 ls
     ```
   - If set up correctly, you should see a list of your S3 buckets (if any).

### 3. Configure Databricks and Snowflake connections

To connect Databricks with Snowflake, follow these steps:

1. **Create a Databricks Account**: If you don't have one, sign up at [Databricks](https://databricks.com/).

2. **Set Up a Databricks Workspace**: Follow the instructions in Databricks to set up your workspace.

3. **Create a Snowflake Account**: If you don't have one, sign up at [Snowflake](https://snowflake.com/).

4. **Get Snowflake Credentials**:
   - You’ll need your Snowflake account name, username, password, and the database/schema you plan to use.

5. **Configure Snowflake Connector in Databricks**:
   - In your Databricks notebook, use the following code to set up the Snowflake connector:
     ```python
     # Install Snowflake connector
     %pip install snowflake-spark-connector

     # Import necessary libraries
     from pyspark.sql import SparkSession

     # Create a Spark session
     spark = SparkSession.builder \
         .appName("Databricks to Snowflake") \
         .getOrCreate()

     # Set Snowflake options
     options = {
         "sfURL": "<your_snowflake_account>.snowflakecomputing.com",
         "sfDatabase": "<your_database>",
         "sfWarehouse": "<your_warehouse>",
         "sfSchema": "<your_schema>",
         "sfRole": "<your_role>",  # optional
         "sfUser": "<your_username>",
         "sfPassword": "<your_password>"
     }
     ```

6. **Test the Connection**:
   - Try running a simple query to test the connection:
     ```python
     df = spark.read \
         .format("snowflake") \
         .options(**options) \
         .option("query", "SELECT * FROM <your_table> LIMIT 10") \
         .load()

     df.show()
     ```

### 4. Run the data pipeline scripts as per the instructions in the `scripts` directory

- Navigate to the `scripts` directory in your cloned repository.
- Execute the relevant scripts in order to load, process, and store the data as defined in your project.

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Acknowledgments

- Thanks to the open-source community for the tools and libraries used in this project.
- Special thanks to mentors and peers for their guidance and support.