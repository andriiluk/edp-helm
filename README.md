# Helm Chart for Postgresql Operator Installation

This helm chart installs the operator for Postgresql and creates a timescaleDB cluster.

To be able to use this operator your local workstation should have the follow tools:

- helm
- kubectl

You must add the postgres-operator-charts repo:

```
helm repo add postgres-operator-charts https://opensource.zalando.com/postgres-operator/charts/postgres-operator
```

Once this repo is added to your instance of helm you can update dependencies.

```
helm dependency update
```

You are now ready to install the helm chart.

First create the required namespace. As an example we use tsdb (there is also an installation option via helm to autocreate the namespace).

```
kubectl create ns tsdb
```

Then perform the install.

```
cd edp-data-timescaledb-poc
helm install edp-data-timescaledb-poc . -n tsdb
```

Pre-configured connectivity options and tests will be displayed,

Once the pods are in a running state you can run helm automatic tests to verify the deployment is successful.

```
helm edp-data-timescaledb-poc test -n tsdb
```

Pre-configured connectivity options and tests will be displayed with the success determination of the tests.
