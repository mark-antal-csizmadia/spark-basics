# spark-basics

<a href="https://nbviewer.org/github/mark-antal-csizmadia/spark-basics/blob/main/spark-basics.ipynb">
  <img align="center" src="https://img.shields.io/badge/Jupyter-spark%5Fbasics.ipynb-informational?style=flat&logo=Jupyter&logoColor=F37626&color=blue" />
</a>
  
## Install Spark

### General Installation

Download Spark from the [Apache Spark Archive](https://spark.apache.org/downloads.html) or do:
```
wget https://dlcdn.apache.org/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2.tgz
```
Specify an alternative version if needed.

Extract Spark:
```
tar xvf spark-3.1.2-bin-hadoop3.2.tgz 
```
Modify the ```.profile``` file and source it:
```
export SPARK_HOME=/opt/spark
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
export PYSPARK_PYTHON=/usr/bin/python3
```
Start Spark:
```
start-master.sh
```
To view the Spark Web user interface, open a web browser and enter the localhost IP address on port 8080 (http://127.0.0.1:8080/). 

Enter the Spark shell (Python) as follows:
```
pyspark
```
Then, set the environment variables in ```.bashrc``` to make Jupyter Notebook the Spark driver (and source it):
```
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS='notebook'
```
Then ```pyspark``` in the shell should open a Jupyter Notebook instance on the localhost.


### Via FindSpark in Python

For Jupyter Notebook, an alternative Python way is to use the FindSpark package.
Create a virtual environment (either via Conda, etc.), install findspark, and make the environment available in Jupyter Noteobook:
```
conda create -n spark-env python=3.8
conda activate spark-env
pip install findspark
pip install ipykernel
python -m ipykernel install --user --name spark-env --display-name "Python (Spark)"
```
Then the Python (Spark) environment is available in Jupyter Notebook.

## Exploring the Page Views of Wikimedia Projects with Spark

Apache Spark is used to explore the page views of Wikimedia projects. As a dataset, we use the page view statistics generated between 0-1am on Jan 1, 2016, which is available at ```data/pagecounts.zip```.
Each line of the dataset, delimited by a white space and contains the statistics for one Wikimedia page. The schema looks as follows:
- Project code: The project identifier for each page.
- Page title: A string containing the title of the page.
- Page hits: Number of requests on the specific hour.
- Page size: Size of the page.

