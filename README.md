# Description

A Chart project for poc-k8s-keycloak-angular microservice

## Deploye steps

**STEP01**: compile image

```
$ docker build -t poc-k8s-keycloak-angular:1.1.0 .
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

**STEP04**: publish chart package in Azure Container Registry

This command will publish our chart package inside our ACR repository

```
$ helm push poc-k8s-keycloak-angular-chart-1.1.0.tgz oci://registry-1.docker.io/ofertoio
```
