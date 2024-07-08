LABELS AND SELECTORS

kubectl get pods -l env=dev
kubectl get pods -l env=dev --show-labels
kubectl get pods -l env=dev --show-labels --no-headers | wc -l
kubectl get pods -l bu=finance --no-headers | wc -l
kubectl get all -l env=prod --no-headers | wc -l
kubectl get pods -l bu=finance,env=prod,tier=frontend
kubectl get pods -l bu=finance -l env=prod -l tier=frontend

spec:
   replicas: 2
   selector:
      matchLabels:
        tier: front-end  <----
   template:
     metadata:
       labels:
        tier: front-end  <----
     spec:
       containers:
       - name: nginx
         image: nginx

kubectl label pod db-2-xg9jq day=friday
Or you can add the label in the MANIFEST

spec:
  selector:
    app: webapp-service

SERVICES
kubectl get services
kubectl describe service
6443

Remember that you can change the type of Service Type
This is one of the resources where you can use the help.
--node-port is optional and one will be given if not chosen

spec:
  selector:
    app: webapp-service


Do a DRY RUN to change the selector



DEPLOYMENTS UPGRADES


kubectl describe deployment
RollingUpdate vs Replace
kubectl edit deployment
Don't scroll, just look for things with / in vim

Explain:

  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate


Also type: Recreate
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

kubectl rollout status xxxx
kubectl rollout history deployment/nginx-deployment

CHANGE-CAUSE is copied from the Deployment annotation kubernetes.io/change-cause to its revisions upon creation. You can specify theCHANGE-CAUSE message by:

Annotating the Deployment with kubectl annotate deployment/nginx-deployment kubernetes.io/change-cause="image updated to 1.16.1"
Manually editing the manifest of the resource.


kubectl rollout history deployment/nginx-deployment --revision=2

kubectl rollout undo deployment/nginx-deployment

kubectl rollout undo deployment/nginx-deployment --to-revision=2







DEPLOYMENT STRATEGIES

Configure the deployment in such a way that the service called frontend-service routes less than 20% of traffic to the new deployment.
Do not increase the replicas of the frontend deployment.

Scale down the v1 version of the apps to 0 replicas and scale up the new(v2) version to 5 replicas.

kubectl scale ....