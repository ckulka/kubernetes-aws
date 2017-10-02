# Kubernetes CloudFormation Template

This repository contains CloudFormation templates for Kubernetes clusters on AWS.

## Single Master Cluster

The `single-master-kubernetes.yaml` CloudFormation template creates a Kubernetes cluster with a single master node. The peristent files of the master node are stored on EFS.

The current setup requires exactly two subnets for the cluster to be deployed to.

### Main Parameters

The template has several parameters, the most important ones are

- VPC & Subnets
- Versions for Docker, Kubernetes, Flannel and Traefik
- Instance Types for the master and node instances

### Main Resources

- Network Load Balancer
  - Routes HTTP(S) traffic to the nodes
  - Routes Kubernetes API (6443) requests to the master
- Master
  - EFS
  - Autoscaling Group
  - Launch Configuration
  - Security Group
  - IAM Instance Role
- Node instance
  - Autoscaling Group
  - Launch Configuration
  - Security Group
  - IAM Instance Role

### TODO

- Master failover testing
- Further restrict Master IAM Instance Role
- Further restrict Node IAM Instance Role
- Further restrict Master Security Group
- Further restrict Node Security Group