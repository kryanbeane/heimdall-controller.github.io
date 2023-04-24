---
layout: page
title: Pre-requisites
permalink: /pre-requisites
nav_order: 1
---

# Prerequisites

Before installing Heimdall, make sure you have the following tools installed:

- **Helm** (version 3 or later)
- **kubectl** (version 1.18 or later)
- **Go** (version 1.14 or later)
- **Docker** (version 19.03 or later)

In addition to these tools, you will also need a working Kubernetes cluster. If you don't already have a cluster set up, you can create one using a tool like Minikube or Kind. If you'd like to use Minikube a guide can be found [here](https://kubernetes.io/docs/tasks/tools/install-minikube/). If you'd like to use Kind a guide can be found [here](https://kind.sigs.k8s.io/docs/user/quick-start/).

Please make sure that these tools are installed and configured correctly before proceeding with the installation of Heimdall. If you encounter any issues during the installation process, check the documentation for each tool to ensure that you have installed and configured them correctly.

## Create Slack Bot

This is an extremely important step. Without a Slack bot token, Heimdall will not be able to support notifications. Integrating OAuth into Heimdall is on the roadmap and will hopefully be a feature to make setting up the bot easier. The steps to generate a token are as follows:
- Navigate to [api.slack.com/apps](https://api.slack.com/apps) and sign in using an account authorized with the Channel you want Heimdall to send notifications to.
- Click the **Create New App** button and choose **From an app manifest**.
- Choose your workspace.
- Paste the below manifest YAML into the text box.

```
display_information:
  name: Heimdall
  description: Atomic Resource Ownership Notifier
  background_color: "#1179f0"
features:
  bot_user:
    display_name: Heimdall
    always_online: true
oauth_config:
  scopes:
    user:
      - admin
      - chat:write
      - users:read
      - users.profile:read
      - im:write
      - im:read
      - im:history
      - channels:history
    bot:
      - incoming-webhook
      - chat:write
      - users:read
      - app_mentions:read
      - channels:history
      - im:history
      - im:read
      - im:write
      - users.profile:read
settings:
  org_deploy_enabled: false
  socket_mode_enabled: false
  token_rotation_enabled: false
```

- Finally click the **Create** button.

### Setup the Bot
- Now that your app is created, click on the app. If you didn't change the name in the YAML, it will say Heimdall.
- In the left hand panel you will see a section called **Settings** and a subsection called **Install App**. Click on **Install App**.
- This will show a page titled **OAuth Tokens for Your Workspace**. Click the **Install App to Workspace** button and select the channel you want Heimdall to send notifications to. This will add the bot to the channel and generate a **Bot User OAuth Token**.
- Take note of the **Bot User OAuth Token**. If for some reason you need to reinstall Heimdall at a later date, you will need this token.
- This is the token you will use during installation in [installation](/installation).