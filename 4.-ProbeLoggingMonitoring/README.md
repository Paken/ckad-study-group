First of all I need to check what happened with the creation of pods with envs configmaps and secrets
Also, about accessing the pod with exec and /bin/bash

READINESS/LIVENESS PROBE

We have seen:
  - Help
  - Explain
Now it is turn to check the documentation

Talk about:
- Differencess between Start/Ready/LivenessProbe
- initialDelaySeconds
- periodSeconds
- types of probes

I need to review this one.



LOGGING

Explain 
kubectl logs <POD>
DO SOME PODS

MONITORING

git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git


kubectl top node
INSTALL top

kubectl top node --sort-by='cpu'
kubectl top node --sort-by='memory'
ORDER is from more to less

kubectl top pod --sort-by='memory'

kubectl top pod --sort-by='cpu'

