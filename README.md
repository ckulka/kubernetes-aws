# Kubernetes CloudFormation Template

This repository contains CloudFormation templates for Kubernetes clusters on AWS.

## Single Master (WIP)

The `single-master.yaml` CloudFormation template creates a Kubernetes cluster with a single master node. The peristent storage of the master node is stored on EFS. No `--cloud-provider` is used.