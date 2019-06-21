# Jupyter as an IDE for Spark

It's not, some will say. Well, Depends on you definition of IDE. For me, it's
an environment where I can write my code, test it, interact with
services which I'm depend on, and finally bundle an ship it. I will
here stick to proving an example of interacting with Spark and 
writing some simple spark code.

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
echo venv > .gitignore
echo "tornado==5.1.1
jupyter" > requirements.txt
```

This need to be done when after creating the virtual environment, and
every time you want wo work on the project in a shell that has not
been activated for it yet.

```bash
venv/bin/activate
```
With the environment activated install dependencies, this only needs to
be done the first time.

```bash
pip3 install -r requirements.txt
```

## Start jupyter

We want to run a Jupiter that is aware of our Spark environment. This can
be defined through environment variables.

```bash
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS='notebook'
export SPARK_LOCAL_IP=127.0.0.1
pyspark
```

That should launch a jupyter notebook. Let's try it out.

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.getOrCreate()
df = spark.read.text('requirements.txt')
fdf = df.filter(df.value == "jupter")
fdf.show()
```

# Done 

That's is. You should now have something that looks like this.







