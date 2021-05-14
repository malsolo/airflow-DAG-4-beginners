# Airflow DAG: Coding your first DAG for Beginners 

By following https://www.youtube.com/watch?v=IH1-0hwFZRQ&t=1049s

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





