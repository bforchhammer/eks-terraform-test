# Setup EKS test cluster

Based on https://github.com/terraform-providers/terraform-provider-aws/tree/master/examples/eks-getting-started

## Pre-requisites

* terraform
* kubectl
* https://github.com/kubernetes-sigs/aws-iam-authenticator

## Setup

Setup EKS cluster in us-west-2 (can take up to 10 minutes):

```
terraform apply
```

Configure kubectl:

```
terraform output kubeconfig > kubeconfig
export KUBECONFIG=$(pwd)/kubeconfig
terraform output config_map_aws_auth > config-map-aws-auth.yaml
kubectl apply -f config-map-aws-auth.yaml
```

Now you should be able to see your nodes:

```
kubectl get nodes

NAME                                       STATUS    ROLES     AGE       VERSION
ip-10-0-0-242.us-west-2.compute.internal   Ready     <none>    53s       v1.10.3
ip-10-0-1-25.us-west-2.compute.internal    Ready     <none>    50s       v1.10.3
```

## Dashboard

Follow this guide: https://docs.aws.amazon.com/eks/latest/userguide/dashboard-tutorial.html

Start `kube proxy`, and then open: http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/
