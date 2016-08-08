# HDPAdmin2Plus
- [Lab 1](https://github.com/HortonworksUniversity/HDPAdmin2Plus#lab-1)
  - Access cluster
  - 
  
---------------

# Lab 1

## Accessing your Cluster

Credentials will be provided for these services by the instructor:

* SSH
* Ambari

## Use your Cluster

### To connect using Putty from Windows laptop

- Download ppk from [here](https://github.com/HortonworksUniversity/HDPAdmin2Plus/raw/master/training-keypair.ppk)
- Use putty to connect to your node using the ppk key:
  - Connection > SSH > Auth > Private key for authentication > Browse... > Select training-keypair.ppk
![Image](https://raw.githubusercontent.com/HortonworksUniversity/HDPAdmin2Plus/master/screenshots/putty.png)

- Make sure to click "Save" on the session page before logging in

### To connect from Linux/MacOSX laptop

- SSH into Ambari node of your cluster using below steps:
  - Right click [this pem key](https://raw.githubusercontent.com/HortonworksUniversity/HDPAdmin2Plus/master/training-keypair.pem)  > Save link as > save to Downloads folder
  - Copy pem key to ~/.ssh dir and correct permissions
  ```
  cp ~/Downloads/training-keypair.pem ~/.ssh/
  chmod 400 ~/.ssh/training-keypair.pem
  ```
 - Login to the Ambari node of the cluster you have been assigned by replacing IP_ADDRESS_OF_AMBARI_NODE below with Ambari node IP Address (your instructor will provide this)   
  ```
  ssh -i  ~/.ssh/training-keypair.pem centos@IP_ADDRESS_OF_AMBARI_NODE
  ```
  - To change user to root you can:
  ```
  sudo su -
  ```

- Similarly login via SSH to each of the other nodes in your cluster as you will need to run commands on each node in a future lab

- Tip: Since in the next labs you will be required to run *the same set of commands* on each of the cluster hosts, now would be a good time to setup your favorite tool to do so: examples [here](https://www.reddit.com/r/sysadmin/comments/3d8aou/running_linux_commands_on_multiple_servers/)
  - On OSX, an easy way to do this is to use [iTerm](https://www.iterm2.com/): open multiple tabs/splits and then use 'Broadcast input' feature (under Shell -> Broadcast input)
  - If you are not already familiar with such a tool, you can also just run the commands on the cluster, one host at a time

#### Login to Ambari

- Login to Ambari web UI by opening http://AMBARI_PUBLIC_IP:8080 and log in with admin/BadPass#1

- You will see a Ambari's Management Page showing no clusters running. 

#### Finding internal/external hosts

- Following are useful techniques you can use in future labs to find your cluster specific details:

  - From SSH terminal, how can I find the cluster name?
  ```
  #run on ambari node to fetch cluster name via Ambari API
  PASSWORD=BadPass#1
  output=`curl -u admin:$PASSWORD -i -H 'X-Requested-By: ambari'  http://localhost:8080/api/v1/clusters`
  cluster=`echo $output | sed -n 's/.*"cluster_name" : "\([^\"]*\)".*/\1/p'`
  echo $cluster
  ```
  - From SSH terminal, how can I find internal hostname (aka FQDN) of the node I'm logged into?
  ```
  $ hostname -f
  ip-172-30-0-186.us-west-2.compute.internal  
  ```

  - From SSH terminal, how can I to find external hostname of the node I'm logged into?
  ```
  $ curl icanhazptr.com
  ec2-52-33-248-70.us-west-2.compute.amazonaws.com 
  ```

  - From SSH terminal, how can I to find external (public) IP  of the node I'm logged into?
  ```
  $ curl icanhazip.com
  54.68.246.157  
  ```
  
