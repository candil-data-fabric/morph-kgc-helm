# Morph-KGC Helm Chart

## Current version: 1.4.0 (October 15th, 2024).

## Overview
This repository contains a Helm Chart for deploying Morph-KGC (tested with v2.8.0) on Kubernetes. 

## Features

### Flexible Deployment Options
Choose between deploying with a CronJob at specified intervals or as a one-time deployment. 

- To enable deployment with specified intervals, modify the cronJob.enabled parameter to true and set the desired schedule. For example, to deploy every minute:

```yaml
cronJob:
  enabled: true
  schedule: "* * * * *"
```

In this example:
- The first asterisk represents minutes and * means "every minute".
- The second asterisk represents hours and * means "every hour".
- The third asterisk represents days of the month and * means "every day".
- The fourth asterisk represents months and * means "every month".
- The fifth asterisk represents days of the week and * means "every day of the week".

### ConfigMap Integration
Ensures that the `config.ini` and `mappings.yaml` files are treated as ConfigMaps, with names specified in `values.yaml`.

Users can manually create ConfigMaps using: 

```shell
$ kubectl create configmap configmap-config --from-file=config.ini
$ kubectl create configmap configmap-mappings --from-file=mappings.yaml
```

### File mounting configuration
The configuration includes automatic mounting of files in the container:

- `config.ini` is mounted at `/app/config`.
- The mappings file is mounted at `/app/config/files`.

**Note:** Ensure that the `config.ini` file contains references to the mappings file starting with `config/files/`.

## Installation

### Using the Helm repository hosted in GitHub Pages

First, add the Helm repository:

```bash
$ helm repo add morph-kgc-helm https://candil-data-fabric.github.io/morph-kgc-helm/
```

Then, install the Helm Chart:

```bash
$ helm install morph-kgc morph-kgc-helm/morph-kgc
```

The chart will be installed using the default values. Use the provided [`values.yaml`](values.yaml) file in this repository as template to upgrade the installation with your desired parameters:

```bash
$ helm upgrade morph-kgc -f myvalues.yaml
```

To uninstall the Helm Chart, run the following command:

```bash
$ helm uninstall morph-kgc
```

### Cloning this repository

First, clone the repository:

```bash
$ git clone https://github.com/candil-data-fabric/morph-kgc-helm.git
```

Once cloned, edit the [`values.yaml`](values.yaml) file to match your deployment needs and run the following command:

```bash
$ helm install morph-kgc .
```

To uninstall the Helm Chart, run the following command:

```bash
$ helm uninstall morph-kgc
```
