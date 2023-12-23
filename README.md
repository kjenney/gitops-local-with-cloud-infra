# gitops-local-with-cloud-infra
Local K8S that provisions infrastructure on a cloud provider

## Chosen Tools

* Rancher Desktop
* AWS Cloud
* Crossplane
* Argo CD
* kubectx

## Requirements

* [Rancher Desktop](https://rancherdesktop.io/) already installed
* [kubectx](https://github.com/ahmetb/kubectx) already installed
* AWS credentials for Cloud Infra

## Quickstart

Run the following commands:

1. `kubectx rancher-desktop`
2. Install Argo CD. Use [Getting Started](https://argo-cd.readthedocs.io/en/stable/getting_started/).
3. Login to Argo CD UI.
4. 


## Rancher Desktop Troubleshooting

If you have issues with Rancher Desktop try the following:

1. Run `rdctl factory-reset`
2. Relaunch Rancher Desktop from your desktop
3. Ensure you are on the latest version - upgrade if necessary


## Decisions

<ol>
      <li>Rancher Desktop</li>
      <ul>
        <li>Minikube wouldn't work with my version of Virtualbox and it was too difficult to downgrade on a Mac</li>
        <li>Useful because it bundles dependencies, such as kubectl </li>
      </ul>
      <li>Crossplane</li>
      <ul>
        <li>It's CNCF and well-known</li>
        <li>I want to be able to bundle infra with services during deployment</li>
      </ul>    
      <li>Argo CD</li>
      <ul>
        <li>It's CNCF and well-known</li>
      </ul>
</ol>
