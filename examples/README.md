# Application examples

This contains examples showing a applications, that produces a docker image which is compatible with the Flink operator. Please use these examples as a reference while building applications to run with the flink operator.

* The Flink operator custom resource containes **image** field, and expects the image to have both flink and application code to be packaged in it.
* The operator starts up Jobmanager and Taskmanager pods using [Container Args](https://godoc.org/k8s.io/api/core/v1#Container).
* The operator submits the flink job through the [REST API](https://ci.apache.org/projects/flink/flink-docs-stable/monitoring/rest_api.html#jars-jarid-run) in the Jobmanager.
* The operator adds flink configuration through [environment variables](https://github.com/lyft/flinkk8soperator/blob/master/pkg/controller/flink/container_utils.go#L84). The image should have support to integrate these into the existing configuration as illustrated in [example here](https://github.com/lyft/flinkk8soperator/blob/master/examples/wordcount/docker-entrypoint.sh#L26)
* If there are issues in the **image** that causes either pods to restart, or Flink cluster to not respond to REST API requests, the state machine will not transition beyond the **READY** state.