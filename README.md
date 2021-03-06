# pyspark-1.2
Docker image with Hadoop 2.6.0 and spark 1.2.0, with python machine learning libraries installed. Numpy, scipy, scikit-learn installed on the base container.

In short, this Docker image helps you to run Spark (on Docker) with the following versions of softwares:

pySpark (Spark 1.2.0) on Hadoop 2.6.0
python 2.6.6
numpy 1.9.0
scipy 0.14.0
scikit-learn 0.15.2

## Pull the Spark 1.2.0 container 

docker pull swatisoni/pyspark-docker:1.2.0

## Running the image

docker run -i -t -h sandbox swatisoni/pyspark-docker:1.2.0 /etc/bootstrap.sh -bash
or

docker run -d -h sandbox swatisoni/pyspark-docker:1.2.0 /etc/bootstrap.sh -d

# Testing

There are two deploy modes that can be used to launch Spark applications on YARN.

## YARN-client mode

In yarn-client mode, the driver runs in the client process, and the application master is only used for requesting resources from YARN.
run the spark shell
spark-shell --master yarn-client --driver-memory 1g --executor-memory 1g --executor-cores 1

### execute the the following command which should return 1000
scala> sc.parallelize(1 to 1000).count()

## YARN-cluster mode

In yarn-cluster mode, the Spark driver runs inside an application master process which is managed by YARN on the cluster, and the client can go away after initiating the application.

### Estimating Pi (yarn-cluster mode):

#### execute the the following command which should write the "Pi is roughly 3.1418" into the logs
spark-submit --class org.apache.spark.examples.SparkPi --master yarn-cluster --driver-memory 1g --executor-memory 1g --executor-cores 1 $SPARK_HOME/lib/spark-examples-1.2.0-hadoop2.4.0.jar

### Estimating Pi (yarn-client mode):

### execute the the following command which should print the "Pi is roughly 3.1418" to the screen
spark-submit --class org.apache.spark.examples.SparkPi --master yarn-client --driver-memory 1g --executor-memory 1g --executor-cores 1 $SPARK_HOME/lib/spark-examples-1.2.0-hadoop2.4.0.jar
