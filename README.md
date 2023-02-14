# Helm Chart for TimescaleDB Operator Installation

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


P.S.: this helm chart can be deployed either with an apache license image or a community license image. The apache license image does not allow clustering, only the community license does. Therefore, in case the user wants to enable clustering a docker registry secret has to be provided to the helm chart with the name "regcred" containing a token to the data team's docker registry on gitlab.
