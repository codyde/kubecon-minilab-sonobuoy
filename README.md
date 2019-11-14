---
description: >-
    Sonobuoy is a diagnostic tool for understanding teh state of a KUbernetes cluster through conformance and recommended configuration tests.
---

# Sonobuoy: Introduction

## Key Capabilities


### Environment Overview

Your lab environment is hosted within public cloud. It is a single node Kubernetes instance. All necessary binaries have been installed for Kubernetes to function on this instance. In order to access this environment we will be leveraging a platform called [Strigo.io](https://strigo.io). When accessing via Strigo, you will notice you have several windows available to assist you with this lab.

* Terminal Windows
* Code Editor Window
* Web Browser Windows

**Note** - The web browser window does not correctly render in this lab. Please use the browser on your desktop, as well as the External FQDN that you can get using the `lab-info` command.

## Lab Goals

In this lab, we will be deploying Sonobuoy to our Kubernetes clusters and execute a check of the cluster. We will also show how to extract the results and view them.

### Step 1: Start Kubernetes

Execute the following command to get started in the lab!

```bash
k8s-start
```