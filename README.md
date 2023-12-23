# gitops-local-with-cloud-infra
Local K8S that provisions infrastructure on a cloud provider

## Chosen Tools

* Rancher Desktop
* AWS Cloud
* Crossplane
* ArgoCD
* kubectx

## Requirements

* [Rancher Desktop](https://rancherdesktop.io/) already installed
* [kubectx](https://github.com/ahmetb/kubectx) already installed
* AWS credentials for Cloud Infra

## Quickstart

Run the following commands:

1. `kubectx rancher-desktop`
2. 


## Rancher Desktop Troubleshooting

If you have issues with Rancher Desktop try the following:

1. Run `rdctl factory-reset`
2. Relaunch Rancher Desktop from your desktop
3. Ensure you are on the latest version - upgrade if necessary


## Decisions

1. Rancher Desktop - because Minikube wouldn't work with my version of Virtualbox and it was too difficult to downgrade on a Mac

