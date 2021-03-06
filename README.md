# Kubernetes Operator for Apache Flink

**This is not an officially supported Google product.**

Kubernetes Operator for Apache Flink is a control plane for running [Apache Flink](https://flink.apache.org/) on
[Kubernetes](https://kubernetes.io/).

## Community

Ask questions, report bugs or propose feature requests [here](https://github.com/GoogleCloudPlatform/flink-on-k8s-operator/issues)
or join our [Slack](https://app.slack.com/client/T09NY5SBT/CQYSE926R) channel.

## Project Status

*Beta*

The operator is under active development, backward compatibility of the APIs is not guaranteed for beta releases.

## Prerequisites

* Version >= 1.9 of Kubernetes
* Version >= 1.7 of Apache Flink

## Overview

The Kubernetes Operator for Apache Flink extends the vocabulary (e.g., Pod, Service, etc) of the Kubernetes language
with custom resource definition [FlinkCluster](docs/crd.md) and runs a
[controller](controllers/flinkcluster_controller.go) Pod to keep watching the custom resources.
Once a FlinkCluster custom resource is created and detected by the controller, the controller creates the underlying
Kubernetes resources (e.g., JobManager Pod) based on the spec of the custom resource. With the operator installed in a
cluster, users can then talk to the cluster through the Kubernetes API and Flink custom resources to manage their Flink
clusters and jobs.

## Features

* Support for both Flink [job cluster](config/samples/flinkoperator_v1beta1_flinkjobcluster.yaml) and
  [session cluster](config/samples/flinkoperator_v1beta1_flinksessioncluster.yaml) depending on whether a job spec is
  provided
* Custom Flink images
* Flink and Hadoop configs and container environment variables
* Init containers and sidecar containers
* Remote job jar
* Configurable namespace to run the operator in
* Configurable namepsace to watch custom resources in
* Configurable access scope for JobManager service
* Taking savepoints periodically
* Taking savepoints on demand
* Restarting failed job from the latest savepoint automatically
* Cancelling job with savepoint
* Cleanup policy on job success and failure
* GCP integration (service account, GCS connector, networking)
* Support for Beam Python jobs

## Installation

The operator is still under active development, there is no Helm chart available yet. You can follow either
* [User Guide](docs/user_guide.md) to deploy a released operator image on `gcr.io/flink-operator` to your Kubernetes
  cluster or
* [Developer Guide](docs/developer_guide.md) to build an operator image first then deploy it to the cluster.

## Documentation

* [User Guide](docs/user_guide.md)
* [Developer Guide](docs/developer_guide.md)
* [Custom resource definition (v1beta1)](docs/crd.md)
* [Managing savepoints with the Flink Operator](docs/savepoints_guide.md)
* [Using GCS connector with custom Flink images](images/flink/README.md)
* [Using init container to download remote job jar](config/samples/flinkoperator_v1beta1_remotejobjar.yaml)
* [Testing the Flink Operator with Apache Kafka](docs/kafka_test_guide.md)
* [Running Apache Beam Python jobs with the Flink Operator](docs/beam_guide.md)

## Contributing

Please check [CONTRIBUTING.md](CONTRIBUTING.md) and the [Developer Guide](docs/developer_guide.md) out.
