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
* AWS credentials for Cloud Infra saved in `/tmp/credentails`

## Quickstart

Run the following commands:

1. `kubectx rancher-desktop`
2. Install Argo CD. Use [Getting Started](https://argo-cd.readthedocs.io/en/stable/getting_started/).
3. Deploy Crossplane using Argo CD [here](#Deploy-CrossPlane-using-Argo-CD).
4. Deploy Kubernetes Secret with AWS Credentials [here](#Create-Kubernetes-Secret-for-AWS-Providers).
5. Deploy Crossplane's AWS Providers with Argo CD [here](#Deploy-Crossplane-AWS-Providers-using-Argo-CD).
6. Deploy Crossplane RDS Database Composite with Argo CD [here](#Deploy-RDS-Database-Composite).
7. Deploy RDS Database using Argo CD [here](#Deploy-RDS-Database).
8. Deploy Service using Argo CD [here](#Deploy-Service).

## Deploy CrossPlane using Argo CD

Run the following code:

```
kubectl create ns crossplane
argocd app create crossplane --repo https://charts.crossplane.io/stable --helm-chart crossplane --revision 1.14.5 --dest-namespace crossplane --dest-server https://kubernetes.default.svc
argocd app sync crossplane
```

## Create Kubernetes Secret for AWS Providers

Use [AWS Quickstart](https://docs.crossplane.io/latest/getting-started/provider-aws/#create-a-kubernetes-secret-for-aws). Update the namespace to use `crossplane` like so:

```
kubectl create secret generic aws-secret -n crossplane --from-file=creds=/tmp/credentials
```

## Deploy CrossPlane AWS Providers using Argo CD

```
argocd app create crossplane-aws-provider --repo https://github.com/kjenney/gitops-local-with-cloud-infra --path charts/crossplane-aws  --dest-server https://kubernetes.default.svc
argocd app sync crossplane-aws-provider
```

## Deploy RDS Database

Run the following code:

```
argocd app create rds-database --repo https://github.com/kjenney/gitops-local-with-cloud-infra --path charts/rds-database --dest-server https://kubernetes.default.svc
argocd app sync rds-database
```

## Deploy Service

Run the following code:

```
kubectl create ns smart-search
argocd app create smart-search --repo https://github.com/kjenney/gitops-local-with-cloud-infra --path charts/smart-search --dest-server https://kubernetes.default.svc
argocd app sync smart-search
```


## Rancher Desktop Troubleshooting

If you have issues with Rancher Desktop try the following:

1. Run `rdctl factory-reset`
2. Relaunch Rancher Desktop from your desktop
3. Ensure you are on the latest version - upgrade if necessary

## CrossPlane Troubleshooting

To get the latest versions of Crossplane packages, go [here](https://marketplace.upbound.io/providers/upbound/provider-family-aws)

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
