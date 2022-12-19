---
layout: default
title: Installation on Existing Projects
nav_order: 4
---

# Installation and Configuration

Functions Companion is an observability, performance and cost management solution for Salesforce Functions. It consists of
a Lightning App that gets installed into your org, along with a logging library that the developer uses to instrument
their functions source code.

The Lightning App includes Apex Classes that the developer uses to 'wrap' their function invocations to gather
operational and performance data. Functions Companion also includes an invocation queue and throttle mechanism that
enables rate control for asynchronous functions. Data is forwarded to the (external) Functions Companion log processing
platform for display in the Functions Companion Lightning Dashboards.

If you already have an existing Salesforce Project deployed to an org with its own Compute Envrionments, you can still install Functions Companion.

Set a log drain on your Compute Envrionment to point to the Functions Companion syslog endpoint.

`sf env logdrain add -e "${envname}" -l syslog://logger.lastmileops.ai:20514`

See [Developers Guide](DevelopersGuide.md) for details on how to instrument your functions with the `apexsyslogjs` logger.