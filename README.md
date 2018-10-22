# openshift-backup
Backup script for projects and databases in OpenShift Container Platform v3 

This script was copied from http://www.sterburg.nl/2017/05/28/backup-openshift/
and changed to run also against openshift-cluster where you are NOT administrator.

## Features
It will backup:
* Openshift Cluster
  * oc export of ALL objects to *.yaml
* Openshift Container
  Seek for container with a label named "backup" and value one out of [mysql|postgresql|fs].
  * "mysql" will start a mysqldump inside, output saved to .sql file
  * "postgresql" will start a custom pg_dump inside, output saved to a .pg_dump file
  * "mongodb" will start a mongodump, output saved as .gz archive
  * "fs" will need another label named "backupvolumemount" with value of a valid pod-volumename
    It will than rsync the mountpath to local directory

## Labeling

The following labels have to be set:

* The pods running the application need to have a "deploymentconfig" (auto-set by OpenShift for DeploymentConfig) or an "app" label.
* The label "backup" needs to be set inside the deploymentconfig/deployment at the jsonpath '.spec.template.metadata.labels'.
* For backup type "fs" also the additional "backupvolumemount" label must reside there.
