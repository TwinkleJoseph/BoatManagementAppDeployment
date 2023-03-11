# Openshift Build and Deployment steps

1. Deploy PostgreSql database
oc process -f postgresql-dc.yaml | oc apply -f -