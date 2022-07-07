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
- configuration is managed *automagically*  (``kedro-mlflow`` uses hooks inside the hood which are automatically registered, so installing the package "just work"). 
- each object as a clear place in the template which improves readability and reduces maintenance costs 
- updates are easy: we just need to bump a dependency version

## Motivation 1 : automatic tracking

Switch to [kedro-mlflow-tutorial](https://github.com/Galileo-Galilei/kedro-mlflow-tutorial).  

```bash
git clone https://github.com/Galileo-Galilei/kedro-mlflow-tutorial
cd kedro-mlflow-tutorial
conda create -n kedro_mlflow_tutorial python=3.9
conda activate kedro_mlflow_tutorial
pip install -e src
```

1. Look a the configuration file ``mlflow.yml`` which was generated with ``kedro mlflow init`` command.
2. Let's vizualize the pipeline first with ``kedro viz``
3. look at ``etl_instances`` and ``etl_labels`` codes. They emulate querying a "real" dataset, e.g. from a sql storage and create an instance dataset as a csv.
4. Run the pipelines with ``kedro run -p etl_instances`` and ``kedro run -p etl_labels``.
5. Open the  mlflow UI: ``kedro mlflow ui``
6. Parameters and tags have been created automatically 🎉 #

## Motivation 2: advanced tracking

1. Let's vizualize the pipeline first with ``kedro viz``
2. look at ``training`` and ``inference`` codes. They represent a training pipeline and the associated inference one:  notice that it is extremely similar to scikit-learn ``fit`` and ``transform`` 💡.
3. Run the pipelines with ``kedro run -p training``.
4. Open the  mlflow UI: ``kedro mlflow ui``
5. Notice that we logged metrics, a picture as artifact, and always more parameters (thanks to advanced configuration and catalog datasets, show the code!).  

## Motivation 3: a mlops framework

Switch entirely to kedro mlflow tutorial and showcase ``pipeline_ml_factory``
