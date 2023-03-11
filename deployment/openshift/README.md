# Openshift Build and Deployment steps

1. Deploy PostgreSql database      
oc process -f postgresql-dc.yaml | oc apply -f -    

2. Build web api        
oc process -f webapi-bc.yaml | oc apply -f -
