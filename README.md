# IS 27 DevOps Specialist Technical Assignment

# Sample Application
This deployment configuration is intended to build and deployment a publically available
application hosted in a github repo. For the purpose of demonstration, I am using the sample application
available in the following repo:
https://github.com/TwinkleJoseph/EcoCoachToursBoatManagementApp

This application has a react.js front end, node.js back-end and postgresql database components.

# OpenShift environment
Red Hat OpenShift is used for the build and deployment of the sample application. OpenShift is hosted in an AWS EC2 instance.

Console: https://ec2-15-222-27-129.ca-central-1.compute.amazonaws.com:8443/console

Contact twinkleljoseph@gmail.com for login credentials.

Please refer to the User Guide for detailed information on the setup.

# Manual Deployment
Instructions to deploy manually on an openshift cluster could be found in deployment\openshift\README.md.

# Automated Deployment using GitHub Actions.
GitHub Action workflow is created for the automated deployment of Openshift resources.
A service account user has been created in OpenShift project for this. Please follow the steps below to configure service account token in GitHub.
a. Login to OpenShift with the developer user 
 oc login <OpenShift Server URL> --token=<Token>

b. Enable the service account with required permissions to create cluster resources.
 oc create rolebinding github-sa-admin --clusterrole=admin --serviceaccount=myproject:github-sa -n myproject

c.  Get the service account token
 oc sa get-token github-sa -n myproject

d. Login to GitHub and select project settings.

e. Click on Secrets and Variables.

f. Click on New Repository Secret

g. Add the service account token obtained in step c under the key OPENSHIFT_TOKEN

h. Add openshift server URL and environment under OPENSHIFT_SERVER and OPENSHIFT_SERVER_ENV respectively.

i. Now click on Actions and select Boat Tracker App Deployment

j. Click on Run Workflow and select the branch for the deployment.

