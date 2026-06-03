# Case Study 1 - Broadcast Join vs Sort Merge Join

## Overview

The objective of this case study is to analyze the performance of two different Spark join strategies: **Sort Merge Join** and **Broadcast Join**.

The dataset consists of:

* A **Fact Table** containing approximately **90 million records**
* A **Dimension Table** containing approximately **50 thousand records**

Although the dimension table is relatively small, the join key distribution is not perfectly balanced and exhibits data skew. This allows us to observe how Spark behaves under realistic conditions where some keys are significantly more frequent than others.

---

## Study Structure

### 1. Data Loading

In the first section, both Delta tables (Fact and Dimension) are loaded.

The schema, record counts, and basic dataset characteristics are reviewed before performing any transformations.

---

### 2. Exploratory Analysis

Before executing the join, an exploratory analysis is performed on the join keys.

The objective is to:

* Understand the cardinality of the join columns
* Identify potential data skew
* Evaluate how the distribution of keys may impact join performance

---

### 3. Sort Merge Join Scenario

In this scenario, the following Spark optimizations are intentionally disabled:

* Adaptive Query Execution (AQE)
* Skew Join Optimization
* Coalesce Partitions
* Broadcast Join

The dimension table is smaller than Spark's default broadcast threshold (10 MB), meaning Spark would normally choose a Broadcast Hash Join automatically.

However, to analyze the behavior of a Sort Merge Join, these optimizations are disabled and Spark is forced to execute a shuffle-based join.

---

### 4. Broadcast Join Scenario

In the second scenario, Spark's default optimizations are enabled:

* Adaptive Query Execution (AQE)
* Skew Join Optimization
* Coalesce Partitions
* Broadcast Join

Since the dimension table fits within the broadcast threshold, Spark automatically selects a Broadcast Hash Join strategy.

This allows us to compare the execution characteristics and performance differences between the two approaches.

---

### 5. Results and Comparison

The final section summarizes the results obtained from both executions.

Key metrics analyzed include:

* Execution time
* Number of stages and tasks
* Shuffle operations
* Data movement across executors
* Resource utilization

The goal is to understand when a Broadcast Join can provide significant advantages over a Sort Merge Join and how Spark's optimizer influences the execution plan,
but we need to be aware that broadcast join is useful on small tables, you need to have enough memory in each executor, because the dataset will be broadcasted will be inside of each executor,
When i enable the setting of broadcast join, I choose the default value of  10Mb for broadcast Join, each dataset with 10Mb or less will be broadcasted, you can choose a bigger value but you need to have in mind that you need to have enough memory on your executors.



## Notes

This repository is intended as a hands-on Spark learning exercise.

Most of the technical explanations, execution plan analysis, Spark UI observations, and performance discussions are documented directly inside the notebook alongside the code.

The README provides a high-level overview of the experiment, while the notebook contains the complete implementation and detailed analysis.
