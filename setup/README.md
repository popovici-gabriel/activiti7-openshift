# Usage: #

1. Create the services, by running the following command:

```bash
oc apply -f ./01-services.yaml
```

2. Retrieve the service ip, by running the following commandL

```bash
oc get svc act-keycloak-http --template '{{ .spec.clusterIP }}'
```

3. Update all the host aliases IP within the 03-misc.yaml file accordingly, by using the IP address obtained above


4. Expose the previously created services, by running the following command:

```bash
oc apply -f ./02-routes.yaml
```

5. Create the deployments, SA's and what not

```bash
oc apply -f ./03-misc.yaml
```

6. Now, finally, deploy the Kong API Gateway, along with its management dashboard.

```bash
oc apply -f ./04-kong.yaml
```

# *IMPORTANT* #

Please note that the yaml files presume that you are running the application
within a project called activiti7, on the QA BS iCaaS cluster. Beforehand, please
update the routes accordingly. Also, before trying to access the services, please go to the the Konga admin dashboard, and define a service and a route for the modeler backend service, and enable CORS headers on it.

# *NOTES* #
All above have been generated using Helm charts from project https://activiti.gitbook.io/activiti-7-developers-guide/getting-started/getting-started-activiti-cloud. In order to regenarate template files one needs to setup HELM and OKD/kubectl in his local CLI environment 
and run following commands: 
```bash
helm fetch --untar activiti-cloud-charts/activiti-cloud-full-example --untardir ./
helm template --name act activiti-cloud-full-example --set global.gateway.domain={REPLACEME}.nip.io --set global.activiti-cloud-modeling.ingress.enabled=true > ./template.yaml
```
{REPLACEME} with given IP address. Than genrated file has to be manually stripped out of k8s networking policies and miscelanous. 

# *CREDENTIALS* #
1. For modeler user: modeler & password: password 
2. For admin: user:admin & password:admin to access admin resources
3. For konga API Gateway: admin / asdf654321