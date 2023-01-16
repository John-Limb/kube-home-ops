# kube-home-ops

 <p align="left">
   <img src="https://i.imgur.com/EXNTJnA.png" alt="kubernetes home logo" width="150" align="left" />
</p>

## Operations for my home k3S cluster

[![Datree Policy Check](https://github.com/John-Limb/kube-home-ops/actions/workflows/datree.yml/badge.svg)](https://github.com/John-Limb/kube-home-ops/actions/workflows/datree.yml)
[![Lint Code Base](https://github.com/John-Limb/kube-home-ops/actions/workflows/super-linter.yml/badge.svg)](https://github.com/John-Limb/kube-home-ops/actions/workflows/super-linter.yml)

## :closed_book: Overview

This repository contains everything I use to maintain the devices and clusters in my home, along with application deployment into my kubernetes cluster. For more
details, see the readme's in each folder.
.
* [Apps](clusters/prod/Apps/) YAML files for configuration and deployment off applications into kubernetes
## :computer: Gear  

I try to run everything bare metal with virtual machines (running on Proxmox).

| Device                  | Count | Storage                  | Purpose                                      |
|-------------------------|-------|--------------------------|----------------------------------------------|
| HP MicroServer          | 1     | 12TB RAID Z1             | Media and backup storage                     |
| Intel NUC8i3BEH         | 1     | 500GB SSD + 120GB NVMe   | Proxmox VM host one                          |
| BeeLink SER3            | 1     | 500GB SSD + 120GB NVMe   | Proxmox VM host Two                          |

## :open_file_folder: Application Services

1. Infrastructure:

A. Virtual machines run ubuntu 22.04.
B. K3S cluster consists of 3 Master nodes and 2 worker nodes.
C. Block storage for Nodes is handled by Longhorn.
D. Application deployment is handled by Flux.

## :lock:&nbsp; Security/Secrets

Secrets and configmaps with private data are encrypted with [sops](https://github.com/mozilla/sops) where only myself and flux can read said secrets.

## :white_check_mark:&nbsp; linting and code scanning

Code linting is performed by [Super-Linter](https://github.com/github/super-linter).
Application YAML is also check and validated by [Datree](https://github.com/marketplace/actions/datree-cli)
## :pencil2:&nbsp; File Structure and files. 
Flux and kustomize recursively look through the folder structure in [clusters/prod](/clusters/prod/) for kustomization.yaml files. 
The top level file in the Apps subfolder tells kustomize to look at certain ks.yaml files or further subfolder. 
Ks.yaml is used when we need to tell kustomize to either do a health check when deploying or set dependencies so that resources deploy in the correct order E.G We don't want to deploy something that needs persistent storage without having Longhorn online, otherwise PVC's will fail to create. 

* [apps-kustomization.yaml](/clusters/prod/apps-kustomization.yaml) - Tells kustomize to watch the folderstructure and also decrypt files when they are encrypted with sops.
* [global-kustomization.yaml](/clusters/prod/global-kustomization.yaml) - Tells flux to bring in files in the [config](/clusters/prod/config/) folder Where further things like Secrets and variables are kept / injected into the cluster at kustomization build time. 
## :handshake:&nbsp; Thanks and Links

I learned a lot from the people over @
[Awesome-home-kubernetes](https://github.com/k8s-at-home/awesome-home-kubernetes)
and from the [k8s@home discord channel](https://discord.gg/DNCynrJ).

* [K3Sup](https://github.com/alexellis/k3sup) - Used to bootstrap clusters.
* [Longhorn](https://longhorn.io/) - Used as CSI driver for pod persistent storage.
* [flux](https://fluxcd.io/) - Used for application creation and lifecycle management.
* [Terraform](https://www.terraform.io/) - Used to provision Virtual machines within proxmox.
* [sops](https://github.com/mozilla/sops)
