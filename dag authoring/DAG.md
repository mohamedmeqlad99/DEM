# Understanding DAGs in Apache Airflow

## What is a DAG?

A Directed Acyclic Graph (DAG) is a collection of tasks that define a workflow in Apache Airflow. It represents the sequence of operations in your data pipeline. Each task in a DAG is represented as a node, and the edges between these nodes represent dependencies between tasks. The acyclic nature of DAGs ensures that the tasks do not form a cycle, meaning that the workflow will not get stuck in an infinite loop.

## Key Components of a DAG

- **Tasks**: The basic unit of work in Airflow. Each task represents a single operation, such as running a script, executing a SQL query, or making an API call.
- **Operators**: Define the specific action that a task will execute. Airflow provides several built-in operators like `BashOperator`, `PythonOperator`, `PostgresOperator`, etc.
- **Dependencies**: You can set dependencies between tasks to control the order in which they are executed. This is done using the `>>` operator or the `set_downstream()` method.

## Creating a Simple DAG

Here's a basic example of a DAG that consists of two tasks: one that prints "Hello" and another that prints "World." The second task depends on the first one.

```python
from airflow import DAG
from airflow.operators.python_operator import PythonOperator
from datetime import datetime

def print_hello():
    print("Hello")

def print_world():
    print("World")

default_args = {
    'owner': 'airflow',
    'start_date': datetime(2023, 11, 1),
    'retries': 1,
}

dag = DAG(
    'hello_world_dag',
    default_args=default_args,
    description='A simple hello world DAG',
    schedule_interval='@daily',
)

task_hello = PythonOperator(
    task_id='print_hello',
    python_callable=print_hello,
    dag=dag,
)

task_world = PythonOperator(
    task_id='print_world',
    python_callable=print_world,
    dag=dag,
)

task_hello >> task_world  # Set task dependency
