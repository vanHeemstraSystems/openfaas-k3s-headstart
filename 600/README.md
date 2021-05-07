# 600 - Aquire Password for OpenFaaS UI (OpenFaaS Portal)

Now the last step is to acquire the password for OpenFaaS UI which we will use to manage OpenFaaS. To do that execute the below command:

```
$ PASSWORD=$(kubectl get secret -n openfaas basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode; echo)
$ echo -n $PASSWORD | faas-cli login --username admin --password-stdin
```

You can then view the password by printing the value of the ```PASSWORD``` variable using the ```echo``` command.

```$ echo PASSWORD```

***Copy and save the password securely!***
