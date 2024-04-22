# Lostops Infrastructure

## Server Structure

The Lostops Infrastructure is composed of 3 servers:

- Backend Server
- Database Server
- Monitoring Server

The servers are VMs hosted by Azure, the DevOps team does not have the permission to create or modify the nature (flavor, image...) of the VMs.

### Backend Server

The backend server is the server where we host our Laravel web app. Besides SSH access via port 22, it should be reachable from the internet via port 80 and 443, and the connection should be restricted to HTTPS. Of course, additional port usage for Prometheus monitoring is accepted. Other than this, the server should not open other ports or install other package.

### Database Server

The database server is the server where we launch a mysql database instance with docker. Besides SSH access via port, it should be reachable only from the backend server via HTTPS. Additional port usage for Prometheus monitoring is accepted.

### Monitoring Server

The monitoring server is the server where we launch Prometheus and Grafana. Besides SSH access via port, it should be reachable from the internet via port 80 and 443, and the connection should be restricted to HTTPS.

## Tools Used

### IaC (Infrastructure as Code) Tools

#### Terraform

Used for managing VM states without having to go on Azure Portal, calls Azure APIs via azurerm.

#### Ansible

Used for executing intialization scripts once the VMs are created, functions with SSH.

### On-Server Tools

#### Prometheus

Monitoring data collection tools, functions with a main Prometheus instance and multiple Prometheus Exporters that expose metrics for the main instance to pull.

#### Grafana

Dashboard and monitoring tool, used to send alerts on message application like discord. Each metric will be humain readable, on a web interface exposed.

#### Docker

Used to manage each container, that contains applications or tools. Used to host Prometheus and Grafana server.

#### Traefik

Network management and service discovery, it serves each applications and exposes it to public addresses and domaine name.

#### MySQL (8.0)

Data storage and persistance for applications throught virtual machine reboot.

## IaC Workflow

1. We have describer files in a repository, that defines the current state of servers. Each time when we need to modify the state of server (create, start, stop, etc.) we'll need to modify the describer files in this repository, then commit and push.
2. Once the commit is pushed, a GitHub Action pipeline will be launched, that contains three steps:

   1. Terraform

   Terraform manage the state of the server directly via azurerm, including create, destroy, start, stop and resize VM.

   2. Ansible

   After the VMs are created, Ansible will launch the playbook in the repo, to intialize the VMs.
