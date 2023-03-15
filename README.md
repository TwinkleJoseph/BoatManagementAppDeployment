# IS 27 DevOps Specialist Technical Assignment

# Sample Application    

This deployment configuration is intended to build and deploy a publicly available
application hosted in a GitHub repository. For this demonstration, I am using the sample application
available in the following repository:

[https://github.com/TwinkleJoseph/EcoCoachToursBoatManagementApp]

This application has a react.js front end, node.js back-end and PostgreSQL  database components. OpenShift build script will checkout the application from the above GitHub repo during build time and push images to the OpenShift image registry.

# Design Considerations 

1. A sample application developed by me was chosen for the deployment. There is a front end, back-end and postgresql database for this application.
2. Openshift cluster should be running front end, back-end and database in their own pods.
3. Patroni is considered for making database Highly Available.
4. Build and Deployment configurations for each components are maintained in separate manifest files.
5. Secrets and Config Maps shall be used to keep sensitive information and environment specific configurations.

# Decisions 

1. For the deployment of the sample application, I have chosen RedHat OpenShift Community Distribution a.k.a OKD. This product has an open source backed by support from developer community. I don't have access to the enterprise version of RedHat Openshift. 

2. Another major decision taken was to keep the source code of sample application seperate from the deployment manifest. This is done to keep the deployment repo more focused, concise and avoiding conflicts with the sample repo.

3. Minishift was chosen for the initial development and testing. This helped to speed up the development and minimize AWS costs during the development.

4. Database High Availability is not considered in the initial phase due to time constraints and deployment complexities. 

5. Disaster recovery is not considered in the initial phase due to time considereations.



# Manual Deployment Instructions

Instructions to deploy manually on an openshift cluster could be found in [Deployment Instructions](deployment/openshift/README.md).

# Automated Deployment using GitHub Actions.

GitHub Action workflow is created for the automated deployment of Openshift resources.
A service account user has been created in OpenShift project for this. Please follow the steps below to configure service account token in GitHub.  

a. Login to OpenShift with the developer user   

 ```oc login <OpenShift Server URL> --token=<Token>```

b. Enable the service account with required permissions to create cluster resources.    

 ```oc create rolebinding github-sa-admin --clusterrole=admin --serviceaccount=myproject:github-sa -n myproject```

c.  Get the service account token   

 ```oc sa get-token github-sa -n myproject```

d. Login to GitHub and select project settings.

e. Click on Secrets and Variables.

f. Click on New Repository Secret

g. Add the service account token obtained in step c under the key OPENSHIFT_TOKEN

h. Add openshift server URL and environment under OPENSHIFT_SERVER and OPENSHIFT_SERVER_ENV respectively.

i. Now click on Actions and select Boat Tracker App Deployment

j. Click on Run Workflow and select the branch for the deployment.

# OpenShift Cluster Information 

Red Hat OpenShift is used for the build and deployment of the sample application. OpenShift is hosted in an AWS EC2 instance.

[OpenShift Console](https://ec2-15-222-27-129.ca-central-1.compute.amazonaws.com:8443/console)

Contact twinkleljoseph@gmail.com for login credentials.

Please refer to the User Guide for detailed information on the setup.

# Application URLs

1. Web Application could be accessed with the link below:   

[Echo Tour Boat Tracking Application](http://boat-tracker-web-myproject.15.222.27.129.nip.io/)

2. REST API could be accessed with the link below:

[Echo Tour Boat Tracking API](http://web-api-myproject.15.222.27.129.nip.io/api)

You can verify the health of the API by clicking the health check end point below:

[API Health Check](http://web-api-myproject.15.222.27.129.nip.io/api/health)
