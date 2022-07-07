# Introduction to kedro-mlflow

## What are kedro and mlflow?

[``kedro`` is a framework about building efficient data science pipelines in python](https://kedro-mlflow.readthedocs.io/en/stable/source/01_introduction/01_introduction.html#what-is-kedro) and [``mlflow`` is a library which manages the lifecycle of machine learning models](https://kedro-mlflow.readthedocs.io/en/stable/source/01_introduction/01_introduction.html#what-is-mlflow).

## Why a plugin?

``mlflow`` is extremely to use in a new project: you can just start logging the relevant objects inside your functions: 

```python
def my_func(param1, param2, data):
   mlflow.log_param("param1", param1)
   mlflow.log_param("param2", param2)
   trained_model, metric =train_model(data)
   mlflow.log_metric("auc", metric)
   mlflow.log_model("my_model", trained_model)
```

This [breaks many of kedro principles and sofware engineering best practices](https://kedro-mlflow.readthedocs.The advantages of a plugin are: 
- the logging is treated as I/O operations and is decoupled from the compute, so functions are reusable outside of a mlflow setup
- configuration is managed *automagically*
- each object as a clear place in the template which improves readability and reduces maintenance costs 
- updates are easy: we just need to update a dependency version

## Motivation 1 : automatic tracking

Switch to [kedro-mlflow-tutorial](https://github.com/Galileo-Galilei/kedro-mlflow-tutorial).  
