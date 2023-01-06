# Ansible-Lab-Automation

 <p align="left">
   <img src="https://i.imgur.com/4l9bHvG.png" alt="ansible logo" width="150" align="left" />
   <img src="https://i.imgur.com/EXNTJnA.png" alt="kubernetes home logo" width="150" align="left" />
</p>

## Operations for my home lab

_...with Ansible and Kubernetes!_ :sailboat:

[![GitHub Super-Linter](https://github.com/John-Limb/Ansible-Lab-Automation/workflows/Lint%20Code%20Base/badge.svg)](https://github.com/marketplace/actions/super-linter)
[![Datree Policy Check](https://github.com/John-Limb/Ansible-Lab-Automation/actions/workflows/datree.yml/badge.svg)](https://github.com/marketplace/actions/datree-cli)

## :closed_book: Overview

This repository contains everything I use to maintain the devices and clusters in my home, along with application deployment into my kubernetes cluster. For more
details, see the readme's in each folder.
Using Ansible-Galaxy to form the template for each roles folder structure to keep structures to a standard, Ansible semaphore is used to automate patching using templated jobs.

* [Ansible](roles/) roles for additional configuration and application installation > Top level playbooks are in the top level of this repository.
* [Apps](lab/apps/) YAML files for configuation and deployment off applications into kubernetes
* [Core-Services](roles/k3s-core-services/) Configurations for the further setup of the cluster after bootsrap
* [BootStrap](roles/k3s-boostrap/) playbooks and shell scripts to provision a HA cluster of kubernetes master nodes

## :computer: Gear  

I try to run everything bare metal with virtual machines (running on Proxmox).

| Device                  | Count | Storage                  | Purpose                                      |
|-------------------------|-------|--------------------------|----------------------------------------------|
| HP MicroServer          | 1     | 12TB RAID Z1             | Media and backup storage                     |
| Intel NUC8i3BEH         | 1     | 500GB SSD + 120GB NVMe   | Proxmox VM host one                          |
| BeeLink SER3            | 1     | 500GB SSD + 120GB NVMe   | Proxmox VM host Two                          |

## :open_file_folder: Application Services

1. Infastructure:

A. Virtual machines run ubuntu 22.04.
B. K3S cluster consists of 3 Master nodes and 2 worker nodes.
C. Block storage for Nodes is handled by Longhorn.
D. Application deployment is handled by Flux.

## :lock:&nbsp; Security/Secrets

Secrets and configmaps with private data are encrypted with [sops](https://github.com/mozilla/sops) where only myself and flux can read said secrets.

## :white_check_mark:&nbsp; linting and code scanning

Code linting is performed by [Super-Linter](https://github.com/github/super-linter).
Application YAML is also check and validated by [Datree](https://github.com/marketplace/actions/datree-cli)

## :handshake:&nbsp; Thanks and Links

I learned a lot from the people over @
[Awesome-home-kubernetes](https://github.com/k8s-at-home/awesome-home-kubernetes)
and from the [k8s@home discord channel](https://discord.gg/DNCynrJ).

* [K3Sup](https://github.com/alexellis/k3sup) - Used to bootstrap clusters.
* [Longhorn](https://longhorn.io/) - Used as CSI driver for pod persistent storage.
* [flux](https://fluxcd.io/) - Used for application creation and lifecycle management.
* [Terraform](https://www.terraform.io/) - Used to provision Virtual machines within proxmox.
* [sops](https://github.com/mozilla/sops)
