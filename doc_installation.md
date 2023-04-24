---
layout: page
title: Installation
permalink: /installation
nav_order: 2
---

# Installation
This section will guide you through the commands needed to successfully install and configure Heimdall onto your cluster. 

> If you have not taken a look at the [Pre-Requisites](/pre-requisites) section, please do so before continuing.

### Clone Heimdall Repository

**SSH Clone**
```
git clone git@github.com:heimdall-controller/heimdall.git
```

**HTTPS Clone**
```
git clone https://github.com/heimdall-controller/heimdall.git
```

### Run Installation Script
```
cd templates/scripts/install.sh
```

You should wait until you are promted for input before continuing. You will be asked to enter 5 values:
- **Slack Bot Token**: The token for the Slack bot you created in the [Pre-Requisites](/pre-requisites) section.
- **Slack Channel Name**: The name of the Slack channel you want Heimdall to send notifications to. This should be the name of the channel, not the channel ID. *The token should begin with **xoxb-**.*
- **3 Notification Cadences**: The cadence at which Heimdall will send notifications to the Slack channel. This should be a number followed by seconds (s). Examples: 10s (10 seconds), 120s (2 minutes), 3600s (1 hour). You must include the *s* for the install script to accept your input. 

Once these variables are configured, Heimdall will be installed onto your cluster. You can verify this by running the following command:

```
kubectl get pods -n heimdall-controller
```