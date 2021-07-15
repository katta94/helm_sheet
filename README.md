To search all available charts in a repo
--- helm search repo <bitnami> 

To convert a helm chart to kubernetes yaml files
helm template my-chart stable/chart --output-dir /home/user/my-chart
  
Check previous releases 
  helm history <MY-RELEASE>
  
Rollback to previous old version 
  helm rollback MY-RELEASE 1
  
If you install first version of cluster with default password from chart, password will be stored in pvc & 
  second time when you upgrade helm chart will generate new random password which will be in conflict with first password.
  To avoid this check the password from first release and use it at the time of upgrade 
  
  For example : export POSTGRESQL_PASSWORD=$(kubectl get secret --namespace default MY-RELEASE-postgresql -o jsonpath="{.data.postgresql-password}" | base64 --decode)
  helm upgrade MY-RELEASE bitnami/postgresql --set postgresqlPassword=$POSTGRESQL_PASSWORD 
