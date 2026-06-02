# Spark Performance Case Studies

This repository contains a collection of practical Spark performance engineering case studies.

The objective is to analyze how Spark behaves under different workloads, understand execution plans, inspect Spark UI metrics, and evaluate optimization techniques.

## How to Run These Case Studies

To reproduce these case studies, you will need an Apache Spark environment.

You can choose one of the following options:

* Install Apache Spark locally on your machine.
* Run Spark inside a Docker container.
* Use Databricks.
* Use Microsoft Fabric.
* Use any other Spark-compatible environment.

### Recommended Option

For learning purposes, running Spark locally or inside Docker is often the easiest approach because it provides full access to the Spark UI and execution details used throughout these case studies.

### Important Note

Many of the analyses presented in this repository rely on:

* Physical execution plans
* Spark UI metrics
* Stage and task analysis
* Shuffle metrics
* Spill metrics

If your environment does not provide access to the Spark UI, you will still be able to execute the code, but some of the performance investigations and comparisons may not be reproducible.


## Case Studies

### 1. Broadcast Join vs Shuffle Join

Topics:

- BroadcastHashJoin
- SortMergeJoin
- Shuffle Exchange
- Join Strategy Selection

### 2. Data Skew, AQE and Salting

Topics:

- Data Skew
- Adaptive Query Execution (AQE)
- Skew Join Optimization
- Coalesce Partitions
- Salting
- Spill Analysis

### Upcoming

- Window Functions & SCD2
- Repartition vs Coalesce
- Small Files Problem
- Delta Optimization
- AQE Deep Dive
