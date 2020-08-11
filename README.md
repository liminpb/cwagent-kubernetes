# cwagent-kubernetes
Here is my working config:

Prepare the cluster for RABAC authentication 
command

kops edit cluster  --state s3://cw-metrics08

kops cluster spec for kubelet.

  kubelet:
    anonymousAuth: false
    authenticationTokenWebhook: true
    authorizationMode: Webhook

Then run 
# kops rolling-update cluster cloudwatch.k8s.local --state s3://cw-metrics08 --yes

Once it is finished validate the cluster

# kops validate cluster --state s3://cw-metrics08
