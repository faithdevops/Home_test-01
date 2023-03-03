**Exercise Description**

In this exercise, we want to deploy two containers that scale independently from one another. The first container runs code that runs a small API that returns users from a database, while the second container runs code that runs a small API that returns shifts from a database. We want to ensure that the deployment can handle rolling deployments and rollbacks and that the deployment can scale based on CPU usage.



**Solution**

Kubernetes Resources

We will use Kubernetes to deploy the two containers and their respective services. The following Kubernetes resources will be created:

users.yaml: Deployment configuration for the users container and the users-service configuration

shifts.yaml: Deployment configuration for the shifts container and the shift-service configuration

postgres.yaml: Deployment configuration for PostgreSQL database

mongo.yaml: Deployment configuration for mongodb database

pvc.yaml: PersistentVolumeClaim for the mongodb database

pvc2.yaml: PersistentVolumeClaim for the PostgreSQL database

hpa-shift.yaml: horizontal pod autoscaler for the shift deployment

hpa-users.yaml: horizontal pod autoscaler for the users deployment

ingress.yaml: ingress controller configuration



**Auto-scaling**

The deployment is set up to autoscale based on CPU usage. The horizontal pod autoscaler (HPA) will scale the deployment up and down based on the average CPU usage of the pods. When the average CPU usage is at 70%, the HPA will scale up the deployment by adding new pods.

**Rolling Deployment and Rollback**

The deployment is set up to handle rolling deployments and rollbacks. The deployment strategy is set to rolling updates, which ensures that only a certain number of pods are updated at a time. This helps to prevent downtime and ensures that the application is always available. If there are any issues with the deployment, we can easily roll back to the previous version using the kubectl rollout undo command.

**Ingress controller**

An nginx ingress controller resource will be created which will enable end user talk to the user and shift application.

**IAM Controls**

To ensure that our development team cannot run certain commands on the Kubernetes cluster, we will use Role-Based Access Control (RBAC). We will create a Role that allows the team to deploy and roll back, but not to perform other privileged actions. We will also create a RoleBinding that associates the Role with the team's Kubernetes Service Account.

**Configuring Multiple Environments**

We can configure multiple environments by creating separate Kubernetes namespaces for each environment, such as staging and production and then deploy the same resources to each namespace with different configuration values.Also, we can create a separate ConfigMaps for staging and production environments and then Modify the deployment manifest to use the ConfigMap data.


**Auto-scaling based on Network Latency**

To auto-scale the deployment based on network latency instead of CPU, we can use the Kubernetes Metrics Server and create a custom metrics API that will expose the network latency metrics and use these metrics to scale the deployment. However, this requires more advanced setup and is outside the scope of this exercise.

**Conclusion**

In this exercise, we have deployed two containers that scale independently from one another and are linked to two separate databases. We have also configured auto-scaling based on CPU usage and ensured that the deployment can handle rolling deployments and rollbacks. Finally, we have implemented IAM controls to restrict the development team's access to the Kubernetes cluster.




