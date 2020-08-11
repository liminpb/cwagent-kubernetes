Step 1: Create a Namespace for CloudWatch

# kubectl apply -f cloudwatch-namespace.yaml

Step 2: Create a Service Account in the Cluster

# kubectl apply -f cwagent-serviceaccount.yaml

Step 3: Create a ConfigMap for the CloudWatch Agent

Edit the cwagent-configmap.yaml as follows 

cluster_name – In the kubernetes section, replace {{cluster-name}} with the name of your cluster. Remove the {{}} characters. Alternatively, if you're using an         Amazon EKS cluster, you can delete the "cluster_name" field and value. If you do, the CloudWatch agent detects the cluster name from the Amazon EC2 tags.

Step 4: Deploy the CloudWatch Agent as a DaemonSet

# kubectl apply -f cwagent-daemonset.yaml

Step 5: Install FluentD

>> Create a ConfigMap named cluster-info with the cluster name and the AWS Region that the logs will be sent to. Run the following command, updating the placeholders with your cluster and Region names.


"kubectl create configmap cluster-info \
--from-literal=cluster.name=cloudwatch.k8s.local \
--from-literal=logs.region=us-east-1 -n amazon-cloudwatch"


>> Deploy the FluentD DaemonSet to the cluster by running the following command.

# kubectl apply -f fluentd.yaml


>> Validate the deployment by running the following command. Each node should have one pod named fluentd-cloudwatch-*.

# kubectl get pods -n amazon-cloudwatch

