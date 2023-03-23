Application Maintenance Page
Overview
This directory contains the manifest files needed to deploy a standard maintenance page into your namespace.

This directory also contains the maintenance page HTML file, along with a DockerFile to compile an image.

Deploying the page
Within the kubectl_deploy directory, there are 2 simple manifest files that make up the deployment, deploy.yaml and service.yaml.

From the root of this repository, simply run:

kubectl apply -f kubectl_deploy -n YOUR-NAMESPACE
The deployment will create a pod called maintenance-page-* and a service named maintenance-page-svc.

Redirecting traffic
Having deployed the maintenane page is not enough - traffic must be redirected to it.

This can be achieved by changing the serviceName field in your current ingress to point to maintenance-page-svc.
This can either be done by redeploying the ingress or doing an in-place edit of the ingress.

Custom HTML
The HTML provided by default is a basic MoJ-branded page. If you wish to customize it, you will need to:

Clone this repo
Update the index.html
docker build . -t 754256621582.dkr.ecr.eu-west-2.amazonaws.com/cloud-platform/maintenance:0.2.0-MY-APP-NAME 
docker push 754256621582.dkr.ecr.eu-west-2.amazonaws.com/cloud-platform/maintenance:0.2.0-MY-APP-NAME 
Update the image tag used in the deployment file.
Cleaning up
Once the maintenance page is not needed anymore :

Change the serviceName in your ingress back to the original value (pointing to your app)
Make sure the your app can be reached via the URL, as expected.
The maintenance page can be removed by running:
kubectl delete -f kubectl_deploy -n YOUR-NAMESPACE