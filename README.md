---
description: >-
    Sonobuoy is a diagnostic tool for understanding teh state of a KUbernetes cluster through conformance and recommended configuration tests.
---

# Sonobuoy: Introduction

## Key Capabilities

**Conformance Testing:** - Sonobuoy generates reports to indicate if clusters are properly configured and conformant to the official Kubernetes specifications
**Workload Debugging:** - Capable of generating reporting around workloads for debugging purposes
**Extensible:** - Leverage existing or create new plugins to test any custom confirmation for clusters

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

### Step 2: Install Sonobuoy

Execute the following commands to download the Sonobuoy binary

```bash
wget https://github.com/vmware-tanzu/sonobuoy/releases/download/v0.16.4/sonobuoy_0.16.4_linux_amd64.tar.gz
tar -zxvf /sonobuoy_0.16.4_linux_amd64.tar.gz
sudo mv ./sonobuoy /usr/local/bin/sonobuoy

```

### Step 3: Run Sonobuoy (Quickly)

Execute the following command start a run, the --wait flag will not return you to a command prompt until the run has completed. The quick mode significantly shortens the test cases, for a full conformance test, omit the `--mode quick` flag.

```bash
sonobuoy run --wait --mode quick
```

Running this command creates the necessary deployment objects in your Kubernetes cluster to test both the conformance of your cluster as well as any other custom test scenarios you have created via the plugin framework. While this test runs, you should see the various objects create via the debug menu.

### Step 4: Sonobuoy Logs

In Strigo, we have the ability to open up an additional terminal. While your current conformance test is running, you can select the "+" symbol on your terminal window to open up a new one. Select this, and run the following command

```bash
kubectl logs sonobuoy -n sonobuoy --follow

```

This will present you a live log of all tests that are being run as they are being executed. If you cancel out of this window (`ctrl+c`) and run the following command

```bash
kubectl get pods -A
```

You can see the pods that are being spun up for the individual tests. These pods are typically created in custom namespaces for each test.

### Step 5: Viewing Results

To access the results of a sonobuoy run, we will use the `sonobuoy retrieve` command, mapped to a variable, and then output that variable to the screen.

```bash
results=$(sonobuoy retrieve)
sonobuoy results $results

```

For more detailed data, we can export the contents of the tar file and inspect the individual reports.

### Step 6: Cleanup

Sonobuoy creates a number of resources in order for its run to complete. To clean our environment out, we can execute the following command...

```bash
sonobuoy delete --wait

```

As before, the --wait flag will ensure that the command completes before sending us back to the command prompt.
