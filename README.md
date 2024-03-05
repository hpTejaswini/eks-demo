**Step 1: Create an Amazon EKS Cluster**


a.Install and configure the AWS CLI. Ensure that it's configured with the necessary IAM permissions.

b.Create an EKS cluster in the AWS by using manually.

c. I followed this document to create the cluster [https://docs.aws.amazon.com/eks/latest/userguide/create-cluster.html](url)

d. connect to the cluster by using the **aws eks update-kubeconfig --region region-code --name my-cluster ( give your region code and cluster name)
**

**Step 2: Create Dockerfiles and Push into the Docker Hub**

a. Build Docker images for each microservice and push them to a docker hub registry 

b. Login to Docker Hub by **docker login** command

c. Before pushing the images, you need to tag them appropriately with your Docker Hub username and the repository name

d. For example docker tag <your-local-image>:latest your-docker-hub-username/product-microservice:latest

e. Push Images to Docker Hub **docker push your-docker-hub-username/product-microservice:latest**

**Step 3: Deploy manifestFiles and Services into the EKS**

a. write the yaml manifest files and services for each microservices.

b. Depoy the each yaml by using the **kubectl apply -f product-microservice.yaml**, Please repeat for all yaml files 

c. Now verify the deployment.

d. kubectl get pods, kubectl get services ,  kubectl get deployments and kubectl get all 

e. <img width="539" alt="image" src="https://github.com/hpTejaswini/eks-demo/assets/162014688/3a084547-e5bd-4f29-98c8-5f78ca35c5a5">

f. <img width="910" alt="image" src="https://github.com/hpTejaswini/eks-demo/assets/162014688/3bb92579-dc88-4aa2-b207-99b0eb3f52be">

g. Take external IP of the node and node port of an microservice , you can acccess form the browser.

h. <img width="388" alt="image" src="https://github.com/hpTejaswini/eks-demo/assets/162014688/cba431df-81cd-4664-92ea-bb836c81aebd">

i. Repeat for all micro services and you shoule able to get it.

**Step 3: Service Mesh implementation by Istio**

a. Please follow the steps provided in the **Istio.yaml** in the above

b. <img width="468" alt="image" src="https://github.com/hpTejaswini/eks-demo/assets/162014688/f7868797-257f-4a88-936b-9308800e6424">

**Step 4: Horizontal Pod AutoScaling**

a. Horizontal Pod Autoscaler (HPA) in Kubernetes is a resource that automatically adjusts the number of replicas in a deployment or replica set based on observed metrics. It helps in scaling the number of pods in a deployment up or down to meet the desired metric values, such as CPU utilization or custom metrics

b. kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.5.0/components.yaml

c. This command will download and apply the necessary CRDs from the Metrics Server release. The Metrics Server is commonly used with Horizontal Pod Autoscaler

d. If you CPU utilization is goes above 70% , it will automatically scale up the pods.

**Step 5: Implement CRD and Pod Disruption Budgets**

a. CRDs allow you to extend the Kubernetes API and define custom resources with specific behaviors and properties

b. Custom resources act as a higher-level abstraction for your application, encapsulating configurations, behaviors, and metadata specific to your use case.

c. PDBs are used to limit the number of simultaneously disrupted pods during voluntary disruptions (e.g., scaling down, rolling updates, node draining).

d. They ensure that a specified number of pods are always available, helping maintain the reliability and availability of the application.

**Step 6: Multi Cluster and Security Measures**

a. Implementing failover for applications in a Kubernetes cluster involves designing for high availability and resilience. Kubernetes itself is designed to handle node failures and maintain the desired state of your applications

b. Use Kubernetes ReplicaSets or Deployments to ensure that multiple replicas of your application are running across nodes

c. Implement Chaos Engineering practices to proactively test and validate the resilience of your system under controlled failure scenarios.

d. For high availability across regions, consider multi-region deployments and global load balancing.

e. As I am using the AWS free-tier limits, I am not implemented the Multi Cluster.

f. Role-Based Access Control (RBAC) is a crucial security measure in Kubernetes that helps in controlling access to resources and operations within the cluster

g. <img width="353" alt="image" src="https://github.com/hpTejaswini/eks-demo/assets/162014688/9f8550d9-fc40-4a2f-8727-dc83537a8a48">


**Step 6: Monitoring , Logging and Chaos Engineering**

a. If enabling full-fledged monitoring and logging solutions is not feasible due to cost constraints in AWS free-tier account.

b. Use kubectl logs to view container logs. Redirecting logs to standard output/error and using log aggregation in the container runtime can help centralize logs.

c. Clearly define the objectives of your Chaos Engineering experiments. Identify the areas of your Kubernetes infrastructure or applications that you want to test for resilience.

d.  <img width="778" alt="image" src="https://github.com/hpTejaswini/eks-demo/assets/162014688/8c368dee-0380-43f0-ae94-6f5c8bfd4d31"> getting error in this one.







