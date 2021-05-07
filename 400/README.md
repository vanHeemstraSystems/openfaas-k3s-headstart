# 400 - Installing arkade

[Arkade](https://github.com/alexellis/arkade) is a Kubernetes app installer. It allows you to install apps and charts to your cluster in one command. The official documentation of OpenFaaS states that using ```arkade``` is the fastest option. If you wish you can also make use of ```Helm``` to install but as I am installing it on a single node machine, I will stick with ```arkade``` option.

Run the below command to download and install it.

```$ curl -SLsf https://dl.get-arkade.dev/ | sudo sh```

It will return something like:

```
[sudo] password for cloud_user: 
x86_64
Downloading package https://github.com/alexellis/arkade/releases/download/0.7.13/arkade as /tmp/arkade
Download complete.

Running with sufficient permissions to attempt to move arkade to /usr/local/bin
New version of arkade installed to /usr/local/bin
which: no ark in (/sbin:/bin:/usr/sbin:/usr/bin)
Creating alias 'ark' for 'arkade'.
sh: line 176: arkade: command not found
[cloud_user@ae464350731c openfaas-k3s-headstart]$
```

Check the success of the installation, like so:

```$ arkade version```

It will return something like:

```
            _             _      
  __ _ _ __| | ____ _  __| | ___ 
 / _` | '__| |/ / _` |/ _` |/ _ \
| (_| | |  |   < (_| | (_| |  __/
 \__,_|_|  |_|\_\__,_|\__,_|\___|

Get Kubernetes apps the easy way

Version: 0.7.13
Git Commit: a7418b1652e1f96c6f86985572c828a96d136836
```

Help with arkade can be found this way:

```$ arkade --help```

Which returns:

```
Usage:
  arkade [flags]
  arkade [command]

Available Commands:
  completion  Output shell completion for the given shell (bash or zsh)
  get         The get command downloads a tool
  help        Help about any command
  info        Find info about a Kubernetes app
  install     Install Kubernetes apps from helm charts or YAML files
  uninstall   Uninstall apps installed with arkade
  update      Print update instructions
  venafi      Sponsored Apps for Venafi
  version     Print the version

Flags:
  -h, --help   help for arkade

Use "arkade [command] --help" for more information about a command.
```
