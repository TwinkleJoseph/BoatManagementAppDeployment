# Openshift Build and Deployment steps

1. Deploy PostgreSql database      
oc process -f postgresql-dc.yaml | oc apply -f -    

2. Build web api        
oc process -f webapi-bc.yaml | oc apply -f -

3. Deploy web api
oc process -f webapi-dc.yaml --param-file=dev.env --ignore-unknown-parameters=true | oc apply -f -

4. Build react web app        
oc process -f webapp-bc.yaml | oc apply -f -

4. Deploy react web app
oc process -f webapp-dc.yaml --param-file=dev.env --ignore-unknown-parameters=true | oc apply -f -

# Trouble shooting
oc get pods
oc port-forward postgresql-db-dev-1-hfxsm 5432:5432
