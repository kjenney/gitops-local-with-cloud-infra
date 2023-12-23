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
3. Deploy Crossplane using Argo CD [here](#Deploy-CrossPlane-using-Argo-CD)
4. Deploy Crossplane's AWS Provider with Argo CD. Use [AWS Quickstart](https://docs.crossplane.io/latest/getting-started/provider-aws/)
5. Deploy RDS Database using Crossplane AWS Provider with Argo CD [here](#Deploy-RDS-Database)

## Deploy CrossPlane using Argo CD

Run the following code:

```
kubectl create ns crossplane
argocd app create crossplane --repo https://charts.crossplane.io/stable --helm-chart crossplane --revision 1.14.5 --dest-namespace crossplane --dest-server https://kubernetes.default.svc
argocd app sync crossplane
```

## Deploy CrossPlane AWS Provider using Argo CD

```
argocd app create crossplane-aws-provider --repo https://charts.crossplane.io/stable --helm-chart crossplane
```

## Deploy RDS Database 

Run the following code:

```
argocd app create rds-database --repo https://github.com/kjenney/gitops-local-with-cloud-infra rds-database --path rds-database --dest-server https://kubernetes.default.svc
argocd app sync rds-database 
```

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
      <li>AWS Cloud</li>
      <ul>
        <li>It's well-known</li>
        <li>I know it very well</li>
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
      <li>kubectx</li>
      <ul>
        <li>Becaus I don't feel like running more than one command if I don't have to</li>
      </ul>
</ol>
