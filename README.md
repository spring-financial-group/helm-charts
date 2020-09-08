# Elastic Stack Kubernetes Helm Charts

<br/>

## M:QUBE configuration changes

Parameter |  Default
--------- | --------
**definitions.policies** | 
**rabbitmqMemoryHighWatermark** | 256MB
**rabbitmqHipeCompile** | false
**service.type** | ClusterIP 
**resources** | {}
**prometheus.enabled** | false
**prometheus.resources** | {}
**prometheus.operator.enabled** | true
**prometheus.operator.alerts.enabled** | true

<br/>

## Charts

Please look in the chart directories for the documentation for each chart. These helm charts are designed to be a lightweight way to configure our official docker images. Links to the relevant docker image documentation has also been added below.

| Chart                                      | Docker documentation                                                            |
| ------------------------------------------ | ------------------------------------------------------------------------------- |
| [Elasticsearch](./elasticsearch/README.md) | https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html     |
| [Kibana](./kibana/README.md)               | https://www.elastic.co/guide/en/kibana/current/docker.html                      |
| [Logstash](./logstash/README.md)           | https://www.elastic.co/guide/en/logstash/current/docker.html                    |
| [Filebeat](./filebeat/README.md)           | https://www.elastic.co/guide/en/beats/filebeat/current/running-on-docker.html   |
| [Metricbeat](./metricbeat/README.md)       | https://www.elastic.co/guide/en/beats/metricbeat/current/running-on-docker.html |

## Kubernetes versions

The charts are [currently tested](https://devops-ci.elastic.co/job/elastic+helm-charts+master/) against all GKE versions available. The exact versions are defined under `KUBERNETES_VERSIONS` in [helpers/matrix.yml](/helpers/matrix.yml)

## Helm versions

While we are checking backward compatibility, the charts are only tested with Helm version mentioned in [helm-tester Dockerfile](helpers/helm-tester/Dockerfile) (currently 2.15.2).
Note that we don't support [Helm 3](https://v3.helm.sh/) version.
