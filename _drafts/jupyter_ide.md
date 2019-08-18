---
title: Jupyter IDE

---

# Jupyter as an IDE for Spark

It's not, some will say. Well, depends on you definition of IDE. For me, it's an
environment where I can write my code, test, interspect outout and interact with
services my code depend on depend on. When working with Spark, jupyer can give
you that experience with some simple setup. I will in this post stick to proving
an example of interacting with Spark and writing some simple Spark code - so
will not go into details in how to bundle for deployments. I may investigate
that in a future post.

# Getting setup

## Basics used across projects

Let's start almost from square zero. I'll assume we're developing on
a recent Mac OS, and already have `python3` and `brew` accessible.

Get setup for virtual environments.

```bash
pip3 install virtualenv
```

Get spark.

```bash
brew install apache-spark
```

## Create a project

Now create a project. A project is here simply a folder, initialised with Git and with out most basic requirements.

```bash
mkdir my_spark_project
cd my_spark_project
git init
virtualenv venv
echo 'venv/' > .gitignore
echo 'tornado==5.1.1
jupyter' > requirements.txt
```

This need to be done after creating the virtual environment, and every time you
want wo work on the project in a shell that has not been activated for it yet.

```bash
venv/bin/activate
```
With the environment activated install dependencies, this only needs to be done
the first time.

```bash
pip3 install -r requirements.txt
```

## Start jupyter

We want to run a Jupiter that is aware of our Spark environment. This can be
defined through environment variables.

```bash
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS='notebook'
export SPARK_LOCAL_IP=127.0.0.1
pyspark
```

That should launch a jupyter notebook. Let's try it out. Create a new notebook
and copy the following into first cell.

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.getOrCreate()
df = spark.read.text('requirements.txt')
fdf = df.filter(df.value == "jupter")
fdf.show()
```

Done
---

That’s it! You should now have something that looks like this.

![Jupyter Screenshot][done image]

By the way. Here’s another external blog entry on the topic: get-started-pyspark-jupyter-guide-tutorial.

[done image]: /assets/img/jupyter_screenshot.png







