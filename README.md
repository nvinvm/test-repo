# Fast API demo

Project is Fast API boilerplate with K8s integration.

## Installation

Clone the project and set below secrets in Github actions secrets(Request for Google project credentials from Admin).

```bash 
# unique app name for the app used to generate docker image
GCP_APP_NAME 

# check in GCP credentials file
GCP_EMAIL 

# check in GCP credentials file
GCP_PROJECT_ID
 
# GCP credentials json
GCP_CREDENTIALS

#Sonarqube homepage url
SONARQUBE_HOST 

#Sonarqube app token
SONARQUBE_TOKEN
```

## Steps to use
* Create an app on Sonarqube and get the `APP TOKEN` and `PROJECT KEY`.
* Update the `sonar.projectKey` in the `sonar-project.properties` file in root of your project.
* Update the deployment, service, configs, secrets names in respective files under **`k8s`** folder.
* Update the deployment name in `.github/workflows/deploy.yaml` to match the name in `k8s/deployment.yml`
* For configs, in `k8s/config-map.yml` replace the keys in data section with your project configurations.
* Similarly update the secrets in `k8s/secrets.yml`.
* **If no secrets or configs are required**, please comment lines which include secrets and configs in `kustomization.yml` in your root folder.

## Next steps
The above steps will create a deployment, clusterIP service, secrets and configs on k8s cluster.
* Update the ingress file in GCP cluster for DNS mapping by adding new rule under **`spec`** section.
#### For TLS
* connect to cluster and generate certificates and update the ingress files **`tls`** section.

## Important
* Configuration data can be database end-points, service end-points etc. don't store passwords in configs.
* Any protected data such as passwords, auth keys etc. should be stored as secrets.
* When updating secrets on `k8s/secrets.yml` make sure the data is `base64` ecrypted. You can generate base64 of your data using below command

```
echo -n "mysecret" | base64     
```

## References
* [Using Google Container Registry with Kubernetes](https://blog.container-solutions.com/using-google-container-registry-with-kubernetes)
* [How to secure applications running on Kubernetes (SSL/TLS Certificates)](https://medium.com/avmconsulting-blog/how-to-secure-applications-on-kubernetes-ssl-tls-certificates-8f7f5751d788)
* [Generate Certificates Manually](https://kubernetes.io/docs/tasks/administer-cluster/certificates/)
