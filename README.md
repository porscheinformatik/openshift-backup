# openshift-backup
Backup script for projects and databases in OpenShift Container Platform v3 

This script was copied from http://www.sterburg.nl/2017/05/28/backup-openshift/
and changed to run also against openshift-cluster where you are NOT administrator.

It will backup:
* Openshift Cluster
** oc export of ALL objects to *.yaml
* Openshift Container
Seek for container with a "backup" label. "backup"-label is a comma-separated list of [mysql|postgresql|fs:/some/path].
** "mysql" will start a mysqldump inside, output saved to .sql file
** "postgresql" will start a custom pg_dump inside, output saved to a .pg_dump file
** "fs:/some/path" will rsync /some/path to local backup-directory/some/path

