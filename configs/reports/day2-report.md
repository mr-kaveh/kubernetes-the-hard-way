### I tried today to enable SSH Access to the control-plane and the worker nodes

#### **Step 1: Create a New SSH Key Pair**

Run the following command **on your local machine**:

	aws ec2 create-key-pair --key-name MyNewKeyPair --query 'KeyMaterial' --output text > MyNewKeyPair.pem
	chmod 400 MyNewKeyPair.pem

> This creates a new key pair and saves the private key to `MyNewKeyPair.pem`.

Also create inbound rule for security group to allow ssh connection from the vm's public ip address, here is how to get 
vm public ip address:

	curl ifconfig.me
or

	dig +short myip.opendns.com @resolver1.opendns.com

 #### Correct way to login through SSH
 	ssh -i "~/.ssh/MyNewKeyPair.pem" ec2-user@ec2-3-120-16-168.eu-central-1.compute.amazonaws.com
