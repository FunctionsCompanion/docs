---
layout: default
title: Known Issues
nav_order: 7
has_children: true
---

# Known Issues

Functions Companion is an observability, performance and cost management solution for Salesforce Functions. It consists of
a Lightning App that gets installed into your org, along with a logging library that the developer uses to instrument
their functions source code.

The Lightning App includes Apex Classes that the developer uses to 'wrap' their function invocations to gather
operational and performance data. Functions Companion also includes an invocation queue and throttle mechanism that
enables rate control for asynchronous functions. Data is forwarded to the (external) Functions Companion log processing
platform for display in the Functions Companion Lightning Dashboards.
