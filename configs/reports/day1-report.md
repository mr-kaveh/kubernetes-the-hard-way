
### **1. Check the Existing Stack**

You need to confirm that the **CloudFormation stack** `eksctl-my-eks-cluster-cluster` exists.

You can list your CloudFormation stacks using the following AWS CLI command:

	aws cloudformation describe-stacks --region eu-central-1 

Look for the stack named `eksctl-my-eks-cluster-cluster`. If it’s still present, it needs to be deleted before you can create a new cluster.

----------

### **2. Delete the CloudFormation Stack**

If the stack `eksctl-my-eks-cluster-cluster` exists, delete it manually:

	aws cloudformation delete-stack --stack-name eksctl-my-eks-cluster-cluster --region eu-central-1

You can then verify the deletion status:

	aws cloudformation describe-stacks --stack-name eksctl-my-eks-cluster-cluster --region eu-central-1

If it returns `ResourceNotFoundException`, it means the stack is deleted.

----------

### **3. Delete Cluster Using `eksctl` (Optional)**

If you want to delete the entire cluster and any associated resources, you can also use `eksctl`:

	eksctl delete cluster --name my-eks-cluster --region eu-central-1 --wait

This will delete the **EKS cluster** and the associated resources (including the CloudFormation stack). Afterward, you can try to create the cluster again.

----------

### **4. Create the Cluster Again**

Once the stack is deleted, run:

	eksctl create cluster -f eks-cluster.yaml

This will attempt to create the cluster and resources fresh, without any conflicts from existing resources.

----------

### **5. If the Stack Is Stuck in "Delete Failed" State**

If CloudFormation is having trouble deleting the stack (e.g., if it’s stuck in a `DELETE_FAILED` state), you might need to manually clean up resources. Look for the resources listed in the stack and delete them manually, such as VPCs, subnets, security groups, IAM roles, and EC2 instances associated with the cluster.

----------

### **Summary Steps:**

1.  **Check if the stack exists** using `aws cloudformation describe-stacks`.
2.  **Delete the existing CloudFormation stack** if it's still present.
3.  If needed, delete the cluster using `eksctl delete cluster`.
4.  **Recreate the cluster** using `eksctl create cluster -f eks-cluster.yaml`.

Let me know if you need further help! 😊