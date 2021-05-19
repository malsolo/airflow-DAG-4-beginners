# Airflow DAG: Coding your first DAG for Beginners 

By following https://www.youtube.com/watch?v=IH1-0hwFZRQ

## More links:

* https://www.notion.so/Your-First-DAG-in-5-minutes-5d15bb2c51b044ea9b8266b2ac07c1fe
* https://marclamberti.com/blog/airflow-dag-creating-your-first-dag-in-5-minutes/
* https://github.com/marclamberti/docker-airflow
	* https://github.com/marclamberti/docker-airflow/blob/main/docker-compose.yml
* http://airflow.apache.org/
	* https://airflow.apache.org/docs/apache-airflow/stable/start/local.html
		* https://github.com/apache/airflow
	* https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html

# Steps

## Create a Python virtual environment

$ virtualenv venv

$ source ./venv/bin/activate

(venv) $ deactivate

$ source ./venv/bin/activate

:)

$ python -V
Python 3.8.5

## Install airflow libraries

See:
* https://airflow.apache.org/docs/apache-airflow/stable/start/local.html
* https://github.com/apache/airflow

Install with extras, constrained to python 3.8.

$ pip install apache-airflow[postgres,google]==2.0.2 \
 --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.0.2/constraints-3.8.txt"

 :thinking it failed

 ```
 INFO: pip is looking at multiple versions of apache-airflow[google,postgres] to determine which version is compatible with other requirements. This could take a while.
ERROR: Cannot install connexion[flask,swagger-ui]==2.6.0 because these package versions have conflicting dependencies.

The conflict is caused by:
    connexion[flask,swagger-ui] 2.6.0 depends on connexion 2.6.0 (from https://files.pythonhosted.org/packages/a7/27/d8258c073989776014d49bbc8049a9b0842aaf776f462158d8a885f8c6a2/connexion-2.6.0-py2.py3-none-any.whl#sha256=c568e579f84be808e387dcb8570bb00a536891be1318718a0dad3ba90f034191 (from https://pypi.org/simple/connexion/) (requires-python:>=3.6))
    The user requested (constraint) connexion==2.7.0

To fix this you could try to:
1. loosen the range of package versions you've specified
2. remove package versions to allow pip attempt to solve the dependency conflict

ERROR: ResolutionImpossible: for help visit https://pip.pypa.io/en/latest/user_guide/#fixing-conflicting-dependencies
(venv) javier@javier-Inspiron-13-5378:~/Projects/github.com/malsolo/airflow-DAG-4-beginners$ pip install apache-airflow[postgres,google]==2.0.2  --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.0.2/constraints-3.8.txt"
 ```

 Let's review it later.

 In the meantime, let's try without google or postgres

 $ pip install apache-airflow==2.0.2 \
 --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.0.2/constraints-3.8.txt"

 It worked! :D

 ## Create the DAG

 A python file within the dags folder.

## Run the DAG

Run airflow by using Docker.

See https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html for detailed instructions.

Here we provide a docker-compose file from https://github.com/marclamberti/docker-airflow/blob/main/docker-compose.yml.

See https://github.com/marclamberti/docker-airflow/blob/main/README.md.

In linux:
$ echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env

$ docker-compose up airflow-init

$ docker-compose up

# Website tutorial

After following:
* https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html
* https://airflow.apache.org/docs/apache-airflow/stable/start/local.html
* https://airflow.readthedocs.io/en/1.10.14/installation.html

Let's try:
* https://airflow.apache.org/docs/apache-airflow/stable/tutorial.html

Maybe later: 
* https://airflow.apache.org/docs/apache-airflow/stable/tutorial_taskflow_api.html
* https://airflow.apache.org/docs/apache-airflow/stable/howto/index.html

## Let's code the DAG

Done.

# Udemy Apache Airflow: The Hands-On Guide

## Section 3: the forex data pipeline

### DAG with first task: check if the API is available - HttpSensor

forex_data_pipeline.py

Don't forget to Admin > Connection > new:
Conn Id: forex_api
Conn type: HTTP
Host: https://gist.github.com/

Then

```
$ docker exec -it [docker airflow worker] /bin/bash

default@5eeb714fe107:/opt/airflow$ airflow tasks list forex_data_pipeline

[2021-05-18 14:59:24,521] {dagbag.py:451} INFO - Filling up the DagBag from /opt/airflow/dags
is_forex_rates_available
default@5eeb714fe107:/opt/airflow$ airflow tasks test forex_data_pipeline is_forex_rates_available 2021-01-01
[2021-05-18 15:00:04,890] {dagbag.py:451} INFO - Filling up the DagBag from /opt/airflow/dags
[2021-05-18 15:00:04,930] {taskinstance.py:877} INFO - Dependencies all met for <TaskInstance: forex_data_pipeline.is_forex_rates_available 2021-01-01T00:00:00+00:00 [None]>
[2021-05-18 15:00:04,940] {taskinstance.py:877} INFO - Dependencies all met for <TaskInstance: forex_data_pipeline.is_forex_rates_available 2021-01-01T00:00:00+00:00 [None]>
[2021-05-18 15:00:04,941] {taskinstance.py:1068} INFO - 
--------------------------------------------------------------------------------
[2021-05-18 15:00:04,941] {taskinstance.py:1069} INFO - Starting attempt 1 of 2
[2021-05-18 15:00:04,942] {taskinstance.py:1070} INFO - 
--------------------------------------------------------------------------------
[2021-05-18 15:00:04,945] {taskinstance.py:1089} INFO - Executing <Task(HttpSensor): is_forex_rates_available> on 2021-01-01T00:00:00+00:00
[2021-05-18 15:00:05,474] {taskinstance.py:1283} INFO - Exporting the following env vars:
AIRFLOW_CTX_DAG_EMAIL=malsolo.com@gmail.com
AIRFLOW_CTX_DAG_OWNER=airflow
AIRFLOW_CTX_DAG_ID=forex_data_pipeline
AIRFLOW_CTX_TASK_ID=is_forex_rates_available
AIRFLOW_CTX_EXECUTION_DATE=2021-01-01T00:00:00+00:00
[2021-05-18 15:00:05,475] {http.py:102} INFO - Poking: marclamberti/f45f872dea4dfd3eaa015a4a1af4b39b
[2021-05-18 15:00:05,483] {base.py:78} INFO - Using connection to: id: forex_api. Host: https://gist.github.com/, Port: None, Schema: , Login: , Password: None, extra: None
[2021-05-18 15:00:05,488] {http.py:140} INFO - Sending 'GET' to url: https://gist.github.com/marclamberti/f45f872dea4dfd3eaa015a4a1af4b39b
[2021-05-18 15:00:05,924] {base.py:245} INFO - Success criteria met. Exiting.
[2021-05-18 15:00:05,938] {taskinstance.py:1192} INFO - Marking task as SUCCESS. dag_id=forex_data_pipeline, task_id=is_forex_rates_available, execution_date=20210101T000000, start_date=20210518T150004, end_date=20210518T150005
default@5eeb714fe107:/opt/airflow$ 

```

### DAG second task: check if the currency file is available - FileSensor

First:

Admin > Connections 
	New
		Conn Id: forex_path
		Conn type: File (path)
		Extra: {"path" : "/opt/airflow/files"}

Again, validate the task

$ docker ps

$ docker exec -it [airflow worker docker id] /bin/bash

default@4d97751e58a4:~$ ls /opt/airflow/files/
forex_currencies.csv

default@4d97751e58a4:~$ airflow tasks list forex_data_pipeline
[2021-05-19 09:54:57,761] {dagbag.py:451} INFO - Filling up the DagBag from /opt/airflow/dags
is_forex_currencies_file_available
is_forex_rates_available


default@4d97751e58a4:~$ airflow tasks test forex_data_pipeline is_forex_currencies_file_available 2021-01-01
...
[2021-05-19 09:57:54,440] {taskinstance.py:1192} INFO - Marking task as SUCCESS. dag_id=forex_data_pipeline, task_id=is_forex_currencies_file_available, execution_date=20210101T000000, start_date=20210519T095754, end_date=20210519T095754
default@4d97751e58a4:~$ 