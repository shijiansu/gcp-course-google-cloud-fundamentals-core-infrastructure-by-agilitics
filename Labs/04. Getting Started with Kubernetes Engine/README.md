
```shell
# For convenience, place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. At the Cloud Shell prompt, type this partial command:
export MY_ZONE=
# followed by the zone that Qwiklabs assigned to you. Your complete command will look like this:
export MY_ZONE=us-central1-a
# Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
# It takes several minutes to create a cluster as Kubernetes Engine provisions virtual machines for you.
# After the cluster is created, check your installed version of Kubernetes using the kubectl version command:
kubectl version
Client Version: version.Info{Major:"1", Minor:"12+", GitVersion:"v1.12.9-gke.7", GitCommit:"b6001a5d99c235723fc19342d347eee4394f2005", G
itTreeState:"clean", BuildDate:"2019-06-24T19:27:39Z", GoVersion:"go1.10.8b4", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"12+", GitVersion:"v1.12.8-gke.10", GitCommit:"f53039cc1e5295eed20969a4f10fb6ad99461e37", 
GitTreeState:"clean", BuildDate:"2019-06-19T20:48:40Z", GoVersion:"go1.10.8b4", Compiler:"gc", Platform:"linux/amd64"}

# The gcloud container clusters create command automatically authenticated kubectl for you.

# From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.)
kubectl run nginx --image=nginx:1.10.0
# View the pod running the nginx container:
kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
nginx-5fc69dfb5d-x2bxx   1/1     Running   0          28s
# Expose the nginx container to the Internet:
kubectl expose deployment nginx --port 80 --type LoadBalancer
# View the new service:
## You can use the displayed external IP address to test and contact the nginx container remotely.
kubectl get services
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP       PORT(S)        AGE
kubernetes   ClusterIP      10.51.240.1    <none>            443/TCP        4m24s
nginx        LoadBalancer   10.51.249.76   104.154.155.117   80:30593/TCP   82s
# Scale up the number of pods running on your service:
kubectl scale deployment nginx --replicas 3
# Confirm that Kubernetes has updated the number of pods:
kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
nginx-5fc69dfb5d-q8gdv   1/1     Running   0          17s
nginx-5fc69dfb5d-thz4t   1/1     Running   0          17s
nginx-5fc69dfb5d-x2bxx   1/1     Running   0          2m50s
# Confirm that your external IP address has not changed:
kubectl get services
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP       PORT(S)        AGE
kubernetes   ClusterIP      10.51.240.1    <none>            443/TCP        5m21s
nginx        LoadBalancer   10.51.249.76   104.154.155.117   80:30593/TCP   2m19s
```
