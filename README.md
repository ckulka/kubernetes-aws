# Kubernetes CloudFormation Template

This repository contains CloudFormation templates for Kubernetes clusters on AWS.

## Single Master Cluster

The `single-master-kubernetes.yaml` CloudFormation template creates a Kubernetes cluster with a single master node. The peristent files of the master node are stored on EFS.

The current setup requires exactly two subnets for the cluster to be deployed to.

During the initial cluster initialisation with `kubeadm`, this template also deploys the [Flannel](https://coreos.com/flannel/docs/latest/) ([Github](https://github.com/coreos/flannel)) overlay network as well as [Traefik](https://traefik.io/) ([Github](https://github.com/containous/traefik)) as ingress controller.

### Input & Output Parameters

The template has several parameters, the most important ones are

- VPC & Subnets
- Versions for Docker, Kubernetes, Flannel and Traefik
- Instance Types for the master and node instances

The template's output is the load balanced URL for the cluster.

### Resources

The following list only outlines the most important resources.

- Network Load Balancer
  - Routes HTTP(S) traffic to the nodes
  - Routes Kubernetes API (6443) requests to the master
- Cluster Master
  - EFS
  - Autoscaling Group
  - Launch Configuration
  - Security Group
  - IAM Instance Role
- Cluster Node
  - Autoscaling Group
  - Launch Configuration
  - Security Group
  - IAM Instance Role

### TODO

- Change advertise address from IP to ELB URL
- Master failover testing
