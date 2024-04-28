Examples
========

Nginx
-----

Create a sample Kubernetes cluster for example:

```shell
k3d cluster create
kubectl cluster-info
```

Deploy a very small and primitive web application:

```shell
$ kubectl apply -f nginx.yaml
railsapp.jgaskins.dev/nginx created
```

Now you can check all events:

```shell
$ kubectl get events
...
38s         Normal    SuccessfulCreate                 job/nginx-before-create           Created pod: nginx-before-create-fw8hm
38s         Normal    Scheduled                        pod/nginx-before-create-fw8hm     Successfully assigned default/nginx-before-create-fw8hm to k3d-k3s-default-server-0
38s         Normal    Pulling                          pod/nginx-before-create-fw8hm     Pulling image "nginx"
24s         Normal    Pulled                           pod/nginx-before-create-fw8hm     Successfully pulled image "nginx" in 13.394s (13.394s including waiting)
24s         Normal    Created                          pod/nginx-before-create-fw8hm     Created container app
24s         Normal    Started                          pod/nginx-before-create-fw8hm     Started container app
21s         Normal    Completed                        job/nginx-before-create           Job completed
21s         Normal    ScalingReplicaSet                deployment/nginx-web              Scaled up replica set nginx-web-7d9ccbb696 to 1
21s         Normal    SuccessfulCreate                 replicaset/nginx-web-7d9ccbb696   Created pod: nginx-web-7d9ccbb696-hsvv5
21s         Normal    Scheduled                        pod/nginx-web-7d9ccbb696-hsvv5    Successfully assigned default/nginx-web-7d9ccbb696-hsvv5 to k3d-k3s-default-server-0
20s         Normal    Pulling                          pod/nginx-web-7d9ccbb696-hsvv5    Pulling image "nginx"
20s         Normal    Pulled                           pod/nginx-web-7d9ccbb696-hsvv5    Successfully pulled image "nginx" in 910ms (910ms including waiting)
20s         Normal    Created                          pod/nginx-web-7d9ccbb696-hsvv5    Created container app
20s         Normal    Started                          pod/nginx-web-7d9ccbb696-hsvv5    Started container app
```

Verify that everything is running:

```shell
$ kubectl get pod,deployment,service 
NAME                             READY   STATUS    RESTARTS   AGE
pod/nginx-web-7d9ccbb696-hsvv5   1/1     Running   0          2m27s

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx-web   1/1     1            1           2m27s

NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.43.0.1       <none>        443/TCP   9m38s
service/nginx-web    ClusterIP   10.43.110.115   <none>        80/TCP    2m27s
```
