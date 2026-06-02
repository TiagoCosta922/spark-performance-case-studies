# Case Study 2 - Data Skew, AQE and Salting

## Overview

The objective of this case study is to analyze how Apache Spark behaves when performing a large-to-large join with extreme data skew.

In this scenario, both tables are large enough to prevent Broadcast Join from being a suitable strategy. As a result, Spark needs to perform a shuffle-based join.

The dataset contains five hot `order_id` values that represent more than 90% of the records in the order lines table. This creates highly unbalanced shuffle partitions and allows us to investigate how Spark handles skewed workloads.

---

## Notes

This repository is intended as a hands-on Spark learning exercise.

Most of the technical explanations, execution plan analysis, Spark UI observations, and performance discussions are documented directly inside the notebook alongside the code.

The README provides a high-level overview of the experiment, while the notebook contains the complete implementation and detailed analysis.

---

## Dataset

The case study uses two fact tables:

* **Fact_Orders**
* **Fact_OrderLines**

The join is performed using `order_id`.

The main challenge is that the `fact_order_lines` table has an extreme skew on the join key. A small number of `order_id` values contain most of the records, while the remaining orders have only a few records each.

---

## Study Structure

### 1. Data Generation

The first section creates synthetic Delta tables for orders and order lines.

The dataset is intentionally designed to simulate a real-world skew problem where a few keys dominate the workload.

---

### 2. Skew Analysis

Before executing the join, an exploratory analysis is performed on the `order_id` distribution.

The objective is to identify the hot keys and understand how much of the dataset they represent.

---

### 3. Baseline Scenario - AQE Disabled and No Salting

In this scenario, the following optimizations are disabled:

* Adaptive Query Execution (AQE)
* Skew Join Optimization
* Coalesce Partitions
* Broadcast Join

This allows us to observe the raw impact of data skew on a shuffle-based join.

---

### 4. AQE Enabled Scenario

In the second scenario, Spark adaptive optimizations are enabled:

* Adaptive Query Execution (AQE)
* Skew Join Optimization
* Coalesce Partitions

The goal is to understand how much Spark can improve the execution plan automatically at runtime.

---

### 5. AQE Enabled with Salting

In the final scenario, salting is applied to the hot `order_id` values.

The objective is to manually distribute the skewed keys across multiple salt buckets, reducing partition imbalance and memory pressure.

---

## Results and Comparison

The final section compares the three scenarios using Spark UI metrics, including:

* Number of tasks
* Task duration distribution
* Shuffle read size
* Memory spill
* Disk spill
* Executor workload balance

The key finding is that AQE helps mitigate skew, but it may not fully solve extreme skew problems.

In this case study, salting provided the best result by directly addressing the root cause: a small number of join keys containing most of the data.

## Notes

This repository is intended as a hands-on Spark learning exercise.

Most of the technical explanations, execution plan analysis, Spark UI observations, and performance discussions are documented directly inside the notebook alongside the code.

The README provides a high-level overview of the experiment, while the notebook contains the complete implementation and detailed analysis.

## Key Takeaway

Adaptive Query Execution is a powerful optimization mechanism, but it is not always enough when the dataset contains extreme skew.

When a few keys dominate the workload, manual techniques such as salting can significantly improve task distribution, reduce spill, and improve overall resource utilization.
