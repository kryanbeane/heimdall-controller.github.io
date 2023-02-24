---
layout: page
title: Configuration
permalink: /configuration
nav_order: 3
---

# Configuration
This section will guide you through the necessary steps to configure Heimdall correctly. There are two main components to configure, a Config Map and a Secret.

## Config Map
A Config Map is used to store some main components of Heimdall:
* A Slack Channel name
* Low-Priority Resource notification cadence
* Medium-Priority Resource notification cadence
* High-Priority Resource notification cadence
  
Below is the create command. If you have not already installed Heimdall, or created the config map yourself, you can run this command to create the necessary Config Map. You can either edit the values before running the command, or edit them in-cluster. Heimdall will reconcile this Config Map, and if for some reason it is deleted, Heimdall will re-create it with the default values and thus won't be able to send notifications.

**Note**: You must include the time unit with your cadence intervals. 
Examples: 10s (10 seconds), 20m (20 minutes), 30h (30 hours).


``` 
kubectl create -f - <<EOF
    kind: ConfigMap
    apiVersion: v1
    metadata:
        name: heimdall-config
        namespace: heimdall-controller
    data:
        high-priority-cadence: '60s'
        medium-priority-cadence: '300s'
        low-priority-cadence: '600s'
        slack-channel: slack-channel-name
EOF
```
Below is the patch command. If Heimdall has already been installed and has created the Config Map, or if you have created it with incorrect values, changing the below key-value pairs and running the command will update the pre-existing Config Map.


```
kubectl patch configmap heimdall-config -n heimdall-controller --type merge --patch "$(cat <<EOF
    data:
        high-priority-cadence: '60s'
        medium-priority-cadence: '300s'
        low-priority-cadence: '600s'
        slack-channel: slack-channel-name
EOF)"
```


## Secret
A Secret is used to store one component which you should have 

