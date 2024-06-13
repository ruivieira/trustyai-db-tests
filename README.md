# trustyai_mariadb_deployment
Manifests to deploy a MariaDB container alongside TrustyAI

## Setup
1) Install Authorino, Serverless, ServiceMesh, ODH operators
2) Create the default ODH DSCI
3) Create a DSC, using [the provided dsc.yaml](odh/dsc.yaml).
4) Create a model namespace
5) In the model namespace, deploy all files within the [maria directory](maria/):
   1) `for file in $(ls maria); do oc apply -f maria/$file; done`
6) Deploy the provided credentials [db-credentials.yaml](odh/db_credentials.yaml) (*or change them if needed*)
6) Deploy the provided [trustyai_cr_db.yaml](odh/trustyai_cr_db.yaml).
7) Set up port-forwarding:
   1) `oc port-forward $(oc get pods -o name | grep maria) 3306:3306`
8) Connect your database client:
   1) Driver: `mysql`
   2) Username: 'quarkus'
   3) Password: `quarkus`
   4) Host: `localhost`
   5) Port: `3306`
