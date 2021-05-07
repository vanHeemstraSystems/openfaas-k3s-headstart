# 300 - Installing faas-cli

```faas-cli``` is a command line utility which let you work with OpenFaaS.

Install it like so:

```$ curl -sL https://cli.openfaas.com | sudo sh```

It will show you something like this:

```
Finding latest version from GitHub
0.13.9
Downloading package https://github.com/openfaas/faas-cli/releases/download/0.13.9/faas-cli as /tmp/faas-cli
Download complete.

Running with sufficient permissions to attempt to move faas-cli to /usr/local/bin
New version of faas-cli installed to /usr/local/bin
Creating alias 'faas' for 'faas-cli'.
sh: line 176: faas-cli: command not found
[cloud_user@ae464350731c openfaas-k3s-headstart]$ 
```

Check the success of the installation as follows:

```$ faas-cli -version```

Should show something like:

```
Found deprecated go-style flags in command, translating to new format:
  faas-cli version
  ___                   _____           ____
 / _ \ _ __   ___ _ __ |  ___|_ _  __ _/ ___|
| | | | '_ \ / _ \ '_ \| |_ / _` |/ _` \___ \
| |_| | |_) |  __/ | | |  _| (_| | (_| |___) |
 \___/| .__/ \___|_| |_|_|  \__,_|\__,_|____/
      |_|

CLI:
 commit:  2cec97955a254358de5443987bedf8ceee272cf8
 version: 0.13.9
```

Or type:

```$ faas-cli --help```

Which gives:

```

Manage your OpenFaaS functions from the command line

Usage:
  faas-cli [flags]
  faas-cli [command]

Available Commands:
  auth           Obtain a token for your OpenFaaS gateway
  build          Builds OpenFaaS function containers
  cloud          OpenFaaS Cloud commands
  completion     Generates shell auto completion
  deploy         Deploy OpenFaaS functions
  describe       Describe an OpenFaaS function
  generate       Generate Kubernetes CRD YAML file
  help           Help about any command
  invoke         Invoke an OpenFaaS function
  list           List OpenFaaS functions
  login          Log in to OpenFaaS gateway
  logout         Log out from OpenFaaS gateway
  logs           Fetch logs for a functions
  namespaces     List OpenFaaS namespaces
  new            Create a new template in the current folder with the name given as name
  publish        Builds and pushes multi-arch OpenFaaS container images
  push           Push OpenFaaS functions to remote registry (Docker Hub)
  registry-login Generate and save the registry authentication file
  remove         Remove deployed OpenFaaS functions
  secret         OpenFaaS secret commands
  store          OpenFaaS store commands
  template       OpenFaaS template store and pull commands
  up             Builds, pushes and deploys OpenFaaS function containers
  version        Display the clients version information

Flags:
      --filter string   Wildcard to match with function names in YAML file
  -h, --help            help for faas-cli
      --regex string    Regex to match with function names in YAML file
  -f, --yaml string     Path to YAML file describing function(s)

Use "faas-cli [command] --help" for more information about a command.
```
