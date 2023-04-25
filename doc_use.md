---
layout: page
title: Using Heimdall
permalink: /how_to_use
nav_order: 3
---

# Using Heimdall

By now you should have ran the install script and have Heimdall installed on your cluster. If not, please refer to the [Installation](/installation) section.

## Watch a Resource

Heimdall can be set to watch any Resources of your choosing. This can be a Core or a Custom Resource. If your Resource is a Pod that is managed by a Deployment, be sure to set the labels on the Deployment.

## Setting Watch Labels 

Your chosen Resources need the following two labels
```
labels:
    app.heimdall.io/priority: <priority>
    app.heimdall.io/owner: namespace.name
```

There are two fields here to set. 
- The `owner` label needs to be configured with the Owner's namespace and name. So if your owner is a Pod called `hello-world` in the namespace `default`, the label would be `default.hello-world`. Heimdall will detect this, find the Pod's IP address, and register it as the Owner by changing the label.
- The `priority` label needs to be configured with one of three options
  - `low`
  - `medium`
  - `high`
- These priorities are used to control the cadence of alerts sent to your Slack channel. The higher the priority, the more frequent the alerts. This is so that Heimdall won't flood your channel with messages!

You can use the below commands to label your Resource. First, replace all of the variables with your own values. Then, run the kubectl command.
```
export NAMESPACE=<namespace>
export RESOURCE_NAME=<resource_name>
export RESOURCE_TYPE=<resource_type>
export OWNER_NAME=<owner_name>
export OWNER_NAMESPACE=<owner_namespace>
export PRIORITY=<priority>

kubectl label $RESOURCE_TYPE $RESOURCE_NAME -n $NAMESPACE app.heimdall.io/owner=$OWNER_NAMESPACE.$OWNER_NAME app.heimdall.io/priority=$PRIORITY
```