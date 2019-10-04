Create vpc for eks using cloudformation stack file name: eks-vpc.yaml







Create eks cluster using cloudformation stack file name:eks-cluster.yaml




Create eks worker nodes(spot and on demand) using cloudformation stack file name:eks-workernodes.yaml



Create configmap.yaml file and add rolearn.





Create .kube/config file after creating cluster and add the server and certificate details in config file.

Create ALB ingress controller and change the annotations to below mentioned

annotations:
    kubernetes.io/ingress.class: alb



    NodePort

    ClusterIP (with the alb.ingress.kubernetes.io/target-type: ip annotation to put the service into IP mode)

    LoadBalancer (this creates two load balancers; one for the service, and one for the ingress)

To deploy the ALB Ingress Controller to an Amazon EKS cluster

    Tag the subnets in your VPC that you want to use for your load balancers so that the ALB Ingress Controller knows that it can use them.
Public subnets in your VPC should be tagged accordingly so that Kubernetes knows to use only those subnets for external load balancers.
Key 	                        Value
kubernetes.io/role/elb            1

Private subnets in your VPC should be tagged accordingly so that Kubernetes knows that it can use them for internal load balancers:
Key 	                        Value
kubernetes.io/role/internal-elb  1


Use templates directory to create and deploy ingress controller and use helm to create helm chart to render objects for reuse
