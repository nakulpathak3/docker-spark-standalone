#Spark 1.6.1 (Standalone)

##Start a standalone cluster

###Master
	
	docker run --name spark-master -d --net=host skrityak/spark-standalone master

Try to check if the master is running by going to WEBUI (port 8080) on the running machine. We need the url of spark master to start the workers.

###Worker1 
	
Get the url for the master (e.g. spark://192.168.1.50:7077) then start a worker with default port (7078 and 8081 for WebUI)  	

	docker run --name spark-worker1 -d --net=host skrityak/spark-standalone worker spark://${MASTER_HOST_OR_IP}:7077

###Worker2

Start anohter worker with different ports by setting environment variables.

	docker run --name spark-worker2 -d --net=host -e SPARK_WORKER_PORT=7079 -e SPARK_WORKER_WEBUI_PORT=8082 skrityak/spark-standalone worker spark://${MASTER_HOST_OR_IP}:7077


##Environment Variables

Spark reads environment variables in start script so we can adjust the variables to change ip/ports. Please see http://spark.apache.org/docs/latest/spark-standalone.html#cluster-launch-scripts for the available variables.

Basically, this docker image set default values to the following variables:-

	SPARK_MASTER_PORT=7077
	SPARK_MASTER_WEBUI_PORT=8080
	SPARK_WORKER_PORT=7078
	SPARK_WORKER_WEBUI_PORT=8081

