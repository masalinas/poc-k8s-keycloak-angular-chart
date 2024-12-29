# Description

A Chart project for poc-k8s-keycloak-angular microservice

## Deploye steps

**STEP01**: compile image

```
$ docker build --build-arg ARG_ANGULAR_PROFILES_ACTIVE=build-minikube -t poc-k8s-keycloak-angular:1.1.0 .
$ docker tag poc-k8s-keycloak-angular:1.1.0 ofertoio/poc-k8s-keycloak-angular:1.1.0
$ docker push ofertoio/poc-k8s-keycloak-angular:1.1.0
```

**STEP02**: create a helm chart projection

```
$ helm create poc-k8s-keycloak-angular-chart
```

**STEP03**: build chart package

This command will generate zip file locally with our chart configuration. The name depends on the  chart name and version configured

```
$ helm package .
```

**STEP04**: publish chart package in Dockerhub Registry

This command will publish our chart package inside our ACR repository

```
$ helm push poc-k8s-keycloak-angular-chart-1.1.0.tgz oci://registry-1.docker.io/ofertoio
```

**STEP05**: install last helm chart in kubernetes
```
$ helm install poc-k8s-keycloak-angular-chart oci://registry-1.docker.io/ofertoio/poc-k8s-keycloak-angular-chart
```

List helm charts installed
```
$ helm list
```

**STEP06**: backup helm chart
```
$ velero backup create poc-k8s-keycloak-angular-chart --or-selector "app.kubernetes.io/name=poc-k8s-keycloak-angular-chart or name=poc-k8s-keycloak-angular"
```

**STEP07**: restore helm chart
```
$ velero restore create --from-backup poc-k8s-keycloak-angular-chart
```

**STEP08**: remove backup
```
$ helm backup delete poc-k8s-keycloak-angular-chart
```