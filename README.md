# Intro

Helm chart which installs Kube Prom Stack(Prometheus Operator) and Grafana operator, along with a prometheus and a Grafana instance and 2 sets of dashboards for the CFK and CP Ansible clusters respectively.

# Purpose

To bring all Kafka clusters of an organization under a single fold.


# How to use

Customize helm values to add your CFK clusters,


```yaml
envSelectorLabel: "env"

cfkEnvs:
  - namespace: team1
    identifier: dev
    serviceType: kafka
  - namespace: team1
    identifier: dev
    type: schemaregistry
```

The above configuration will monitor the CFK Kafka and Schema registry services with label `env: dev` in the namespace `team1`.

To add CP Ansible clusters,

```yaml
ansibleEnvs:
  - name: sentinel
    labels:
      service_type: kafka
      env: sentinel
    targets:
      - 45.79.126.76:8080
```

will scrape the service at the above IP and add the above prescribed labels to all the metrics.


# TODO

1. option to add TLS-supported ingress for prometheus and grafana
2. fix chart promQL values
3. Add charts for ansible versions, schema registry and other components
4. Jenkins pipeline to deploy monitoring changes