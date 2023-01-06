# Tailscale in k8s

All credit goes to https://github.com/mvisonneau who created the following helm charts and container images
* https://github.com/mvisonneau/docker-tailscale
* https://github.com/mvisonneau/helm-charts/tree/main/charts/tailscale-relay


## The setup
I am using flux manage the CD side of this deployment. 
* Helm-repo.yaml sets flux to monitor Mvisonneau's repo for changes and updates in the charts
* Helm-release.yaml sets flux to provision nessacery resources in my cluster to connect to the tailscale network and advertise two RFC1918 subnets to the network (I could put them as secrets but they are generic to everyone so :shrug:)
* Tailscale-secret.yaml sets a setret key for emphemral nodes to auto join and approve in the tennant. This is encrypted. https://tailscale.com/kb/1111/ephemeral-nodes/ 

You can copy and paste all the files for your own usage, just change the key and advertised routes.
Renovate will soon take over for relases but other than that it will fire right up with the current versions of the chart and image. 