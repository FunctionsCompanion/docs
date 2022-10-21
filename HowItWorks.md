---
layout: default
title: How it Works
nav_order: 2
---

# How it Works

Functions Companion is an observability, performance and cost management solution for Salesforce Functions. It consists of a Lightning App that gets installed into your org, along with a logging library that the developer uses to instrument their functions source code. 

The Lightning App includes Apex Classes that the developer uses to 'wrap' their function invocations to gather operational and performance data. Functions Companion also includes an invocation queue and throttle mechanism that enables rate control for asynchronous functions. Data is forwarded to the (external) Functions Companion log processing platform for display in the Functions Companion Lightning Dashboards.

The diagrams below shows how Functions Companion is installed and how the components interact for synchronous and asynchronous invocations.
## Synchronous Invocations
![Image: components-sync.png](/assets/images/components-sync.png)
## Asynchronous Invocations
![Image: components-async.png](/assets/images/components-async.png)

### Get Functions Companion

Sign up for an account to get Functions Companion at [app.lastmileops.ai](https://app.lastmileops.ai) and get an invite to our Slack channel by sending an email request to slackinvite@lastmileops.ai.
