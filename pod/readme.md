## POD COMMANDS


### 1.	Creating a pod imperative way  run command
		❯ kc run nginx-pod --image nginx:latest $dr > simple-nginx-pod.yaml



### 2.	Creating a pod delarative way create command
		❯ kc create -f simple-nginx-pod.yaml 
		pod/nginx-pod created


### 3.	Listing pods
		❯ kc get pods
		NAME        READY   STATUS    RESTARTS   AGE
		nginx-pod   1/1     Running   0          2m13s

		❯ kc get pods -o wide
		NAME        READY   STATUS    RESTARTS   AGE     IP             NODE           NOMINATED NODE   READINESS GATES
		nginx-pod   1/1     Running   0          2m34s   10.98.158.48   data-node-01   <none>           <none>


### 4.	Getting custom columns 

		❯ kubectl get pods -o=jsonpath='{"Pod Name, Condition Initialized"}{"\n"}{range .items[*]}{.metadata.name},{@.status.conditions[?(@.type=="Initialized")].status}{"\n"}{end}'

		Pod Name, Condition Initialized
		nginx-pod,True



		❯ kubectl get pods -o=jsonpath='{"Pod Name\t\tHost IP\t\t\tPOD IP\t\t\tImage"}{"\n"}{range .items[*]}{.metadata.name}{"\t\t"}{@.status.hostIP}{"\t\t"}{@.status.podIP}{"\t\t"}{@.status.containerStatuses[].image}{"\n"}{end}'
		Pod Name                Host IP                 POD IP                  Image
		nginx-pod               10.10.0.101             10.98.158.48            docker.io/library/nginx:latest


### 5.	Running pod with commands
		pilot␥cockpit /devlabs/ckad/pod 
		❯ kc run nginx-pod-sleep --image nginx:latest $dr -- /bin/sh -c  "sleep 30 " > simple-nginx-pod-command.yaml

		❯ kc create -f simple-nginx-pod-command.yaml
		pod/nginx-pod-sleep created


### 6.	Deleting all pods in a given name space
		❯ kc delete pod --all --namespace ckad


### 7.	Updating a Pod with patch command json input

		❯ kc run nginx-pod --image nginx:latest 

		❯ kc patch pod nginx-pod -p '{"spec":{"containers":[{"name":"nginx-pod","image":"busybox:latest"}]}}'

		pod/nginx-pod patched

### 8.	Updating a Pod with patch command json input
		❯ kc patch pod nginx-pod -p '{"spec":{"containers":[{"name":"nginx-pod","image":"nginx:stable"}]}}'
		pod/nginx-pod patched


Events:
  Type    Reason     Age                  From               Message
  ----    ------     ----                 ----               -------
  Normal  Scheduled  9m2s                 default-scheduler  Successfully assigned ckad/nginx-pod to data-node-01
  Normal  Pulling    9m2s                 kubelet            Pulling image "nginx:latest"
  Normal  Pulled     8m57s                kubelet            Successfully pulled image "nginx:latest" in 4.539061715s
  Normal  Pulling    85s                  kubelet            Pulling image "nginx:stable"
  Normal  Pulled     67s                  kubelet            Successfully pulled image "nginx:stable" in 18.742099126s
  Normal  Created    66s (x2 over 8m57s)  kubelet            Created container nginx-pod
  Normal  Started    66s (x2 over 8m57s)  kubelet            Started container nginx-pod
  Normal  Killing    4s (x2 over 85s)     kubelet            Container nginx-pod definition changed, will be restarted
  Normal  Pulling    3s                   kubelet            Pulling image "busybox:latest"

### 9.	Updating a Pod with YAML patch file "pod-patch-file.yaml"

		❯ kc patch pod nginx-pod --patch-file pod-patch-file.yaml 
		pod/nginx-pod patched

		❯ kc get pods
		NAME        READY   STATUS    RESTARTS      AGE
		nginx-pod   1/1     Running   14 (6s ago)   52m

### 10.	Updating a Pod with replace command which accpets the full pod specification
		❯ kc get pods nginx-pod -o yaml > replace-pod.yaml 

		❯ vi replace-pod.yaml 

		❯ kc replace -f replace-pod.yaml 
		pod/nginx-pod replaced

		❯ kc get pods nginx-pod 
		NAME        READY   STATUS    RESTARTS       AGE
		nginx-pod   1/1     Running   15 (11s ago)   57m

