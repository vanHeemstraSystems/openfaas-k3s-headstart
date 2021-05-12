# 500 - Installing OpenFaaS

## 100 - Installation

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
$ sudo chmod 744 k3s.yaml 
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

If you scroll down to the end of the above output you will notice that there is another error which states that ```Kubernetes cluster unreachable```.

Even knowing that ```k3s``` service is up and running I was not able to figure out what could be a problem. So I searched the web and found [this issue thread on Github](https://github.com/k3s-io/k3s/issues/1126) in which one of the [commenters](https://github.com/k3s-io/k3s/issues/1126#issuecomment-560504204) were able to fix this error by running the below command.

```$ kubectl config view --raw > ~/.kube/config```

After this, you can run the installation of OpenFaaS using arkade again and this time it should be successfull. Here is the output on my system after the installation was successfull.

```$ arkade install openfaas```

As a result:

```
Using Kubeconfig: /home/cloud_user/.kube/config
[Warning] unable to create secret basic-auth, may already exist: Error from server (AlreadyExists): secrets "basic-auth" already exists
Client: x86_64, Linux
2021/05/07 14:11:11 User dir established as: /home/cloud_user/.arkade/
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/cloud_user/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /home/cloud_user/.kube/config
"openfaas" already exists with the same configuration, skipping
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/cloud_user/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /home/cloud_user/.kube/config

WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/cloud_user/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /home/cloud_user/.kube/config
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "openfaas" chart repository
Update Complete. ⎈Happy Helming!⎈
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/cloud_user/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /home/cloud_user/.kube/config

WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/cloud_user/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /home/cloud_user/.kube/config
VALUES values.yaml
Command: /home/cloud_user/.arkade/bin/helm [upgrade --install openfaas openfaas/openfaas --namespace openfaas --values /tmp/charts/openfaas/values.yaml --set serviceType=NodePort --set operator.create=false --set openfaasImagePullPolicy=IfNotPresent --set faasnetes.imagePullPolicy=Always --set basicAuthPlugin.replicas=1 --set ingressOperator.create=false --set queueWorker.replicas=1 --set queueWorker.maxInflight=1 --set clusterRole=false --set gateway.directFunctions=false --set gateway.replicas=1 --set basic_auth=true]
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/cloud_user/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /home/cloud_user/.kube/config
Release "openfaas" does not exist. Installing it now.
NAME: openfaas
LAST DEPLOYED: Fri May  7 14:11:12 2021
NAMESPACE: openfaas
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that openfaas has started, run:

  kubectl -n openfaas get deployments -l "release=openfaas, app=openfaas"
2021/05/07 14:11:13 stderr: WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/cloud_user/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /home/cloud_user/.kube/config

=======================================================================
= OpenFaaS has been installed.                                        =
=======================================================================

# Get the faas-cli
curl -SLsf https://cli.openfaas.com | sudo sh

# Forward the gateway to your machine
kubectl rollout status -n openfaas deploy/gateway
kubectl port-forward -n openfaas svc/gateway 8080:8080 &

# If basic auth is enabled, you can now log into your gateway:
PASSWORD=$(kubectl get secret -n openfaas basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode; echo)
echo -n $PASSWORD | faas-cli login --username admin --password-stdin

faas-cli store deploy figlet
faas-cli list

# For Raspberry Pi
faas-cli store list \
 --platform armhf

faas-cli store deploy figlet \
 --platform armhf

# Find out more at:
# https://github.com/openfaas/faas

Thanks for using arkade!
```

To address the following warning:

- WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/cloud_user/.kube/config

Change the permissions on this file as follows:

```
$ cd ~/.kube
$ ls -la
-rw-rw-r--.  1 cloud_user cloud_user 2961 May  7 14:10 config
$ sudo chmod 600 config```
$ ls -la
-rw-------.  1 cloud_user cloud_user 2961 May  7 14:10 config
```

Try once more:

```$ arkade install openfaas```

It will give an errorless result, as so:

```
Using Kubeconfig: /home/cloud_user/.kube/config
[Warning] unable to create secret basic-auth, may already exist: Error from server (AlreadyExists): secrets "basic-auth" already exists
Client: x86_64, Linux
2021/05/07 14:18:46 User dir established as: /home/cloud_user/.arkade/
"openfaas" already exists with the same configuration, skipping

Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "openfaas" chart repository
Update Complete. ⎈Happy Helming!⎈

VALUES values.yaml
Command: /home/cloud_user/.arkade/bin/helm [upgrade --install openfaas openfaas/openfaas --namespace openfaas --values /tmp/charts/openfaas/values.yaml --set basicAuthPlugin.replicas=1 --set ingressOperator.create=false --set clusterRole=false --set gateway.directFunctions=false --set faasnetes.imagePullPolicy=Always --set queueWorker.replicas=1 --set queueWorker.maxInflight=1 --set basic_auth=true --set serviceType=NodePort --set operator.create=false --set openfaasImagePullPolicy=IfNotPresent --set gateway.replicas=1]
Release "openfaas" has been upgraded. Happy Helming!
NAME: openfaas
LAST DEPLOYED: Fri May  7 14:18:47 2021
NAMESPACE: openfaas
STATUS: deployed
REVISION: 2
TEST SUITE: None
NOTES:
To verify that openfaas has started, run:

  kubectl -n openfaas get deployments -l "release=openfaas, app=openfaas"
=======================================================================
= OpenFaaS has been installed.                                        =
=======================================================================

# Get the faas-cli
curl -SLsf https://cli.openfaas.com | sudo sh

# Forward the gateway to your machine
kubectl rollout status -n openfaas deploy/gateway
kubectl port-forward -n openfaas svc/gateway 8080:8080 &

# If basic auth is enabled, you can now log into your gateway:
PASSWORD=$(kubectl get secret -n openfaas basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode; echo)
echo -n $PASSWORD | faas-cli login --username admin --password-stdin

faas-cli store deploy figlet
faas-cli list

# For Raspberry Pi
faas-cli store list \
 --platform armhf

faas-cli store deploy figlet \
 --platform armhf

# Find out more at:
# https://github.com/openfaas/faas

Thanks for using arkade!
```

The output contains important information which we need to get started with ```faas-cli``` and ```OpenFaaS```. 

Verify that openfaas has started:
```
$ kubectl -n openfaas get deployments -l "release=openfaas, app=openfaas"
NAME                READY   UP-TO-DATE   AVAILABLE   AGE
queue-worker        0/1     1            0           52m
gateway             0/1     1            0           52m
alertmanager        0/1     1            0           52m
prometheus          0/1     1            0           52m
nats                0/1     1            0           52m
basic-auth-plugin   0/1     1            0           52m
```

***NOTE*** that these nodes are UP-TO-DATE but not AVAILABLE.


## 200 - Forward the gateway to the machine

As we have already install ```faas-cli```, we will now need to forward the gateway to the machine.

First we will check the rollout status of the ```gateway``` by issuing the below command:

```$ kubectl rollout status -n openfaas deploy/gateway```

You may get below error:

```error: deployment "gateway" exceeded its progress deadline```

That happens if the deployment doesn’t proceed until the deadline is met, Kubernetes marks the deployment status as failed, which the rollout status command will be able to pick up.

See https://medium.com/polarsquad/check-your-kubernetes-deployments-46dbfbc47a7c

To get back to a stable, working state, we can use the ```rollout undo``` command to bring back the working pods and clean up the failed deployment.

```
$ kubectl rollout undo -n openfaas deploy/gateway
error: no rollout history found for deployment "gateway"
```

Try deleting the deployments:

```
$ kubectl -n openfaas delete deployments -l "release=openfaas, app=openfaas"
deployment.apps "queue-worker" deleted
deployment.apps "gateway" deleted
deployment.apps "alertmanager" deleted
deployment.apps "prometheus" deleted
deployment.apps "nats" deleted
deployment.apps "basic-auth-plugin" deleted
```

Now try again after having fixed above error:

```
$ kubectl -n openfaas get deployments -l "release=openfaas, app=openfaas"
No resources found in openfaas namespace.
```

Try once more:

```$ arkade install openfaas```


NOW WHAT ???



```
$ kubectl rollout status -n openfaas deploy/gateway
```

The above command should state that it is successfull. After this we can forward the gateway to the machine.

```$ kubectl port-forward -n openfaas svc/gateway 8080:8080 &```

The ```&``` sign in the end of the command will execute it in the background. You can type in ```jobs``` to check the status of the job.

We also need to check if the deployment is in ready state or not. To check the deployment state execute the command:

```$ kubectl get deployments -n openfaas -l "release=openfaas, app=openfaas"```

If any of the app deployed is not ready, you should be able to see it now. Check the ***READY*** column in the command output and you should see something ***0/1***. This would mean that the deployment is not ready and you should check back in sometime. Once you have the output like the one in the screenshot above, you are good to go.
