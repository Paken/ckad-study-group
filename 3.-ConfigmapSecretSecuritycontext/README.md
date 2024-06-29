COMMANDS AND ARGUMENTS
containers:
- name: xxx
  command:
  - sleep
  - "4800"


  or command: ["sleep","4800"]

kubectl exec ubuntu-sleeper-2 -it -- ps aux
IF YOU WANT TO CHANGE THE COMMAND, DESTROY THE POD FIRST

    command: ["python", "app.py"]
    args: ["--color", "pink"]

difference between COMMAND and ARGS, the first one is ENTRYPOINT and the second one is CMD (argument to ENTRYPOINT)
Show a Dockerfile





SECURITYCONTEXT

kubectl explain pod.spec.containers.securityContext.runAsUser

  containers:
  - command:
    - sleep
    - "4800"
    image: ubuntu
    name: ubuntu
    securityContext:
      runAsUser: 1010


  Show difference between putting it under SPEC or under CONTAINERS.

      securityContext:
      capabilities:
        add:
        - SYS_TIME


        



CONFIGMAP

containers:
- env:
  - name: APP_COLOR
    value: pink

kubectl get pods webapp-color -o yaml > webapp-color.yaml
AND DELETE POD AND EDIT
kubectl exec webapp-color -- env

kubectl get cm
kubectl describe cm db-config
kubectl get cm db-config -o yaml

kubectl create cm -h
kubectl create cm webapp-config-map --from-literal=APP_COLOR=darkblue --from-literal=APP_OTHER=disregard
kubectl get cm webapp-config-map -o yaml

kubectl explain pod.spec.containers.envFrom.configMapRef
kubectl explain pod.spec.containers.env.valueFrom.configMapKeyRef


  - env:
    - name: APP_COLOR
      valueFrom:
       configMapKeyRef:
         name: webapp-config-map
         key: APP_COLOR


  - envFrom:
    - configMapRef:
        name: webapp-config-map



SECRET
kubectl get secrets
kubectl get secret -o yaml
kubectl describe secret <THIS ONE IS A BETTER OPTION>

kubectl create secret generic -h

kubectl create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123

echo -n TEXT | base64

-n removes the endline

Add secret to pod
kubectl get pods
   16  kubectl get pod webapp-pod -o yaml > webapp-pod.yaml
   17  vim webapp-pod.yaml 
   18  kubectl exec webapp-pod -- env
   19  kubectl exec webapp-pod -- env | grep DB
   20  kubectl delete pod webapp-pod --force
   21  ls
   22  kubectl apply -f webapp-pod.yaml 
   23  vim webapp-pod.yaml 
   24  kubectl apply -f webapp-pod.yaml 
   25  kubectl get pods
   26  kubectl exec webapp-pod -- env | grep DB

kubectl explain pod.spec.containers.envFrom.secretRef.name


kubectl get secrets db-secret -o yaml | grep DB_Password: | awk '{print $2}' | base64 -d





