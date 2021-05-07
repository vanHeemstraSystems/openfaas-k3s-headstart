# 200 - Installing k3s

I am making use of Lightweight Kubernetes also known as k3s. This is a certified Kubernetes distribution built for IoT and Edge computing.

```$ curl -sfL https://get.k3s.io | sh -```

It will show something like this:

```
[sudo] password for cloud_user: 
[INFO]  Finding release for channel stable
[INFO]  Using v1.20.6+k3s1 as release
[INFO]  Downloading hash https://github.com/k3s-io/k3s/releases/download/v1.20.6+k3s1/sha256sum-amd64.txt
[INFO]  Downloading binary https://github.com/k3s-io/k3s/releases/download/v1.20.6+k3s1/k3s
[INFO]  Verifying binary download
[INFO]  Installing k3s to /usr/local/bin/k3s
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: d36uatko69830t.cloudfront.net
 * epel: d2lzkl7pfhq30w.cloudfront.net
 * extras: d36uatko69830t.cloudfront.net
 * nux-dextop: mirror.li.nux.ro
 * updates: d36uatko69830t.cloudfront.net
Package yum-utils-1.1.31-54.el7_8.noarch already installed and latest version
Nothing to do
Loaded plugins: fastestmirror
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: d36uatko69830t.cloudfront.net
 * epel: d2lzkl7pfhq30w.cloudfront.net
 * extras: d36uatko69830t.cloudfront.net
 * nux-dextop: mirror.li.nux.ro
 * updates: d36uatko69830t.cloudfront.net
rancher-k3s-common-stable                                                                                    | 2.9 kB  00:00:00     
rancher-k3s-common-stable/primary_db                                                                         | 2.2 kB  00:00:00     
Resolving Dependencies
--> Running transaction check
---> Package k3s-selinux.noarch 0:0.3-0.el7 will be installed
--> Processing Dependency: container-selinux >= 2.107-3 for package: k3s-selinux-0.3-0.el7.noarch
--> Running transaction check
---> Package container-selinux.noarch 2:2.119.2-1.911c772.el7_8 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

====================================================================================================================================
 Package                       Arch               Version                               Repository                             Size
====================================================================================================================================
Installing:
 k3s-selinux                   noarch             0.3-0.el7                             rancher-k3s-common-stable              14 k
Installing for dependencies:
 container-selinux             noarch             2:2.119.2-1.911c772.el7_8             extras                                 40 k

Transaction Summary
====================================================================================================================================
Install  1 Package (+1 Dependent package)

Total download size: 53 k
Installed size: 123 k
Downloading packages:
(1/2): container-selinux-2.119.2-1.911c772.el7_8.noarch.rpm                                                  |  40 kB  00:00:00     
warning: /var/cache/yum/x86_64/7/rancher-k3s-common-stable/packages/k3s-selinux-0.3-0.el7.noarch.rpm: Header V4 RSA/SHA1 Signature, key ID e257814a: NOKEY
Public key for k3s-selinux-0.3-0.el7.noarch.rpm is not installed
(2/2): k3s-selinux-0.3-0.el7.noarch.rpm                                                                      |  14 kB  00:00:00     
------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                61 kB/s |  53 kB  00:00:00     
Retrieving key from https://rpm.rancher.io/public.key
Importing GPG key 0xE257814A:
 Userid     : "Rancher (CI) <ci@rancher.com>"
 Fingerprint: c8cf f216 4551 26e9 b9c9 18be 925e a29a e257 814a
 From       : https://rpm.rancher.io/public.key
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                               1/2 
  Installing : k3s-selinux-0.3-0.el7.noarch                                                                                     2/2 
  Verifying  : k3s-selinux-0.3-0.el7.noarch                                                                                     1/2 
  Verifying  : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                               2/2 

Installed:
  k3s-selinux.noarch 0:0.3-0.el7                                                                                                    

Dependency Installed:
  container-selinux.noarch 2:2.119.2-1.911c772.el7_8                                                                                

Complete!
[INFO]  Creating /usr/local/bin/kubectl symlink to k3s
[INFO]  Creating /usr/local/bin/crictl symlink to k3s
[INFO]  Creating /usr/local/bin/ctr symlink to k3s
[INFO]  Creating killall script /usr/local/bin/k3s-killall.sh
[INFO]  Creating uninstall script /usr/local/bin/k3s-uninstall.sh
[INFO]  env: Creating environment file /etc/systemd/system/k3s.service.env
[INFO]  systemd: Creating service file /etc/systemd/system/k3s.service
[INFO]  systemd: Enabling k3s unit
Created symlink from /etc/systemd/system/multi-user.target.wants/k3s.service to /etc/systemd/system/k3s.service.
[INFO]  systemd: Starting k3s
[cloud_user@ae464350731c openfaas-k3s-headstart]$ 
```

After the installation is completed, you can check if the k3s service is running by executing the below command.

```$ sudo systemctl status k3s```
