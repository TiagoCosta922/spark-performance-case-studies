## Data

The datasets used in these case studies are synthetically generated within the notebooks.

The generated Delta tables are not included in this repository because they can become very large and are intended to be created locally by the user.

Before running any notebook, make sure you have a Spark environment configured and an active Spark session available.

To reproduce the experiments, simply execute the data generation section included in each notebook.

### Dataset Generation Approach

The two case studies use slightly different approaches for generating and storing the datasets.

#### Case Study 1

In Case Study 1, the synthetic datasets are initially generated and written as Parquet files. They are then converted and stored in Delta format before running the analysis.

This approach was intentionally chosen to explore the process of generating data, writing it as Parquet, and subsequently creating Delta tables from those files.

#### Case Study 2

In Case Study 2, the datasets are generated directly in Spark and written immediately in Delta format.

This approach simplifies the data generation process and allows the analysis to focus entirely on Spark execution behavior, data skew, AQE, and salting techniques.

### Note

The exact row distribution may vary slightly when regenerating the datasets. However, the important characteristics of each case study—such as table sizes, join patterns, and data skew distribution—remain the same and are sufficient to reproduce the results and observations presented in the notebooks.
