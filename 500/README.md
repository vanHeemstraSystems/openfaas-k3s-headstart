# 500 - Installing OpenFaaS

Installing OpenFaaS with ```arkade``` is extremely simple and you can get the installation done by executing this command:

```$ arkade install openfaas```

This may result in errors, as shown below:

```
Using Kubeconfig: /home/cloud_user/.kube/config
[Warning] unable to create secret basic-auth, may already exist: time="2021-05-07T12:44:26.151530886Z" level=warning msg="Unable to read /etc/rancher/k3s/k3s.yaml, please start server with --write-kubeconfig-mode to modify kube config permissions"
error: error loading config file "/etc/rancher/k3s/k3s.yaml": open /etc/rancher/k3s/k3s.yaml: permission denied
Client: x86_64, Linux
2021/05/07 12:44:26 User dir established as: /home/cloud_user/.arkade/
https://get.helm.sh/helm-v3.5.2-linux-amd64.tar.gz
/tmp/linux-amd64 linux-amd64/
/tmp/helm linux-amd64/helm
/tmp/LICENSE linux-amd64/LICENSE
/tmp/README.md linux-amd64/README.md
2021/05/07 12:44:27 extracted tarball into /tmp: 3 files, 0 dirs (477.007766ms)
Downloaded to:  /home/cloud_user/.arkade/bin/helm helm
"openfaas" has been added to your repositories

Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "openfaas" chart repository
Update Complete. ⎈Happy Helming!⎈

VALUES values.yaml
Command: /home/cloud_user/.arkade/bin/helm [upgrade --install openfaas openfaas/openfaas --namespace openfaas --values /tmp/charts/openfaas/values.yaml --set basicAuthPlugin.replicas=1 --set gateway.replicas=1 --set queueWorker.maxInflight=1 --set basic_auth=true --set clusterRole=false --set gateway.directFunctions=false --set faasnetes.imagePullPolicy=Always --set ingressOperator.create=false --set queueWorker.replicas=1 --set serviceType=NodePort --set operator.create=false --set openfaasImagePullPolicy=IfNotPresent]
Error: Kubernetes cluster unreachable: Get "http://localhost:8080/version?timeout=32s": dial tcp [::1]:8080: connect: connection refused
Error: exit code 1, stderr: Error: Kubernetes cluster unreachable: Get "http://localhost:8080/version?timeout=32s": dial tcp [::1]:8080: connect: connection refused
```

There is a permission error in /etc/rancher/k3s/k3s.yaml. For the resolution of this error, I changed the permission on the file to 744 and the error goes away.

```
$ cd /etc/rancher/k3s/
-rw-------. 1 root root 2961 May  7 12:15 k3s.yaml
$ chmod 744 k3s.yaml 
$ ls -la
-rwxr--r--. 1 root root 2961 May  7 12:15 k3s.yaml
```

Try again:

```$ arkade install openfaas```

Now we may see this:

```
Using Kubeconfig: /home/cloud_user/.kube/config
Client: x86_64, Linux
2021/05/07 14:06:13 User dir established as: /home/cloud_user/.arkade/
"openfaas" already exists with the same configuration, skipping

Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "openfaas" chart repository
Update Complete. ⎈Happy Helming!⎈

VALUES values.yaml
Command: /home/cloud_user/.arkade/bin/helm [upgrade --install openfaas openfaas/openfaas --namespace openfaas --values /tmp/charts/openfaas/values.yaml --set operator.create=false --set openfaasImagePullPolicy=IfNotPresent --set faasnetes.imagePullPolicy=Always --set queueWorker.replicas=1 --set queueWorker.maxInflight=1 --set basic_auth=true --set clusterRole=false --set gateway.directFunctions=false --set basicAuthPlugin.replicas=1 --set gateway.replicas=1 --set ingressOperator.create=false --set serviceType=NodePort]
Error: Kubernetes cluster unreachable: Get "http://localhost:8080/version?timeout=32s": dial tcp [::1]:8080: connect: connection refused
Error: exit code 1, stderr: Error: Kubernetes cluster unreachable: Get "http://localhost:8080/version?timeout=32s": dial tcp [::1]:8080: connect: connection refused
```


