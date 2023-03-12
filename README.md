### Create AWS EKS cluster with a Node Group manually

### Technologies Used:

Kubernetes, AWS EKS, Nginx

### Project Description:

1- Configure necessary IAM Roles

2- Create VPC with Cloudformation Template for Worker Nodes

3- Create EKS cluster (Control Plane Nodes)

4- Create Node Group for Worker Nodes and attach to EKS cluster

5- Configure Auto-Scaling of worker nodes

6- Deploy a sample application to EKS cluster

### Instructions:

###### Step 1: Create AWS IAM role for EKS cluster

![image](/images/Screenshot%202023-03-12%20at%208.03.22%20pm.png)

###### Step 2: Create customized VPC for K8s Worker nodes by AWS cloudformation

![image](/images/Screenshot%202023-03-12%20at%208.08.34%20pm.png)

###### Step 3: Create EKS cluster and connect it to created VPC

![image](/images/Screenshot%202023-03-12%20at%201.09.20%20pm.png)
![image](/images/Screenshot%202023-03-12%20at%201.11.58%20pm.png)

###### Step 4: Configure kubectl to AWS EKS cluster

```
aws configure list
```

```
aws eks update-kubeconfig --name eks-cluster-nginx
```

```
kubectl get ns
```

```
kubectl cluster-info
```

###### Step 5: Create a role for NodeGroup worker nodes

![image](/images/Screenshot%202023-03-12%20at%208.15.05%20pm.png)

###### Step 6: Create nodegroup to eks cluster and attach the role to nodegroup

![image](/images/Screenshot%202023-03-12%20at%202.19.19%20pm.png)
![image](/images/Screenshot%202023-03-12%20at%202.21.29%20pm.png)

###### Step 7: Create and configure ec2 instances on nodegroup

![image](/images/Screenshot%202023-03-12%20at%202.24.05%20pm.png)
![image](/images/Screenshot%202023-03-12%20at%202.24.21%20pm.png)
![image](/images/Screenshot%202023-03-12%20at%202.26.45%20pm.png)

###### Step 8: Create a auto-scale policy for node-group and attach it to eks-worker-node-role

![image](/images/Screenshot%202023-03-12%20at%208.25.30%20pm.png)
![image](/images/Screenshot%202023-03-12%20at%205.32.20%20pm.png)
![image](/images/Screenshot%202023-03-12%20at%205.32.54%20pm.png)

###### Step 9: Create cluster-autoscaler for node-group

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml
```

```
kubectl edit deployment -n kube-system cluster-autoscaler
```

###### Step 10:deploy a nginx app into eks cluster

```
kubectl apply -f nginx.yaml
```
