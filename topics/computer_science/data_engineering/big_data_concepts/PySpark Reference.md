---
tags:
  - cs
  - cs/data_eng
created: 2025-01-15T15:32
modified: 2025-08-08T19:04
published:
sources:
topics:
  - PySpark
  - Apache Spark
  - Spark DataFrames
  - MLlib
authors:
ai-assisted:
hidden:
public: true
---
Footnote Sources: [^1]ChatGPT
# PySpark Reference
## Setting Up

```python
from pyspark.sql import SparkSession

# Create a SparkSession
spark = SparkSession.builder \
    .appName("MyApp") \
    .getOrCreate()

# Read a CSV file
df = spark.read.csv("path/to/file.csv", header=True, inferSchema=True)

# Show DataFrame
print(df.show())
```

---

## DataFrame Operations

### Viewing Data
```python
# Display top rows
df.show(n=10)

# Print schema
df.printSchema()

# Get column names
df.columns

# Get summary statistics
df.describe().show()
```

### Selecting and Filtering
```python
# Select specific columns
df.select("column1", "column2").show()

# Filter rows
df.filter(df["column"] > 100).show()

# Using SQL-like syntax
df.createOrReplaceTempView("table_name")
spark.sql("SELECT * FROM table_name WHERE column > 100").show()
```

---

## Transformations

### Adding or Modifying Columns
```python
# Add a new column
df = df.withColumn("new_column", df["existing_column"] * 2)

# Rename a column
df = df.withColumnRenamed("old_column", "new_column")

# Drop a column
df = df.drop("column_to_drop")
```

### Aggregations
```python
# Group by and aggregate
df.groupBy("column").count().show()

df.groupBy("column").agg({"another_column": "sum"}).show()

from pyspark.sql.functions import avg, max
df.groupBy("column").agg(avg("another_column"), max("another_column")).show()
```

---

## PySpark SQL Functions

### Common Functions
```python
from pyspark.sql.functions import col, lit, when

# Use `col` to reference columns
df.select(col("column1") * 2).show()

# Add a constant value
df = df.withColumn("constant_column", lit(42))

# Conditional column (like CASE WHEN)
df = df.withColumn("new_column", when(df["column"] > 10, "Yes").otherwise("No"))
```

---

## Saving Data

```python
# Save as Parquet file
df.write.parquet("output/path")

# Save as CSV
df.write.csv("output/path", header=True)
```

---

## Machine Learning with MLlib

### Example: Linear Regression
```python
from pyspark.ml.regression import LinearRegression
from pyspark.ml.feature import VectorAssembler

# Prepare data
feature_columns = ["feature1", "feature2"]
assembler = VectorAssembler(inputCols=feature_columns, outputCol="features")
transformed_df = assembler.transform(df)

# Split data
train, test = transformed_df.randomSplit([0.8, 0.2])

# Train model
lr = LinearRegression(featuresCol="features", labelCol="label")
model = lr.fit(train)

# Evaluate
predictions = model.transform(test)
predictions.select("label", "prediction").show()
```

---

## Debugging and Optimization

```python
# Check execution plan
df.explain()

# Cache a DataFrame for repeated use
df.cache()

# Count rows (forces evaluation)
df.count()
```

[^1]: Prompt: Hello, provide me a quick reference page for the common PySpark commands. Structure the page into a markdown.