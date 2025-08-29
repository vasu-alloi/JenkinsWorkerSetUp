I’m setting up Jenkins agents on EC2.

Instead of manually creating workers, I want to use EC2-Fleet (or Auto Scaling with Spot instances) so Jenkins can dynamically scale nodes.

The Jenkins controller should connect to these EC2 agents via SSH (using the ubuntu user + private key).

Currently, I can manually SSH into the agent from the master, but in Jenkins UI the node shows offline with the error "The selected credentials cannot be found".

So my goal is:

Bring the EC2 agent online in Jenkins (via EC2-Fleet plugin) using SSH authentication with private key.

### Steps:
#### 1.Created an EC2 instance called JenkinsWorkerNodes using an AMI to serve as the basis for an AWS Auto Scaling Group.
<img width="1361" height="891" alt="image" src="https://github.com/user-attachments/assets/985743b0-dcda-4975-9cc1-e4ade1f70b49" />

<img width="1662" height="257" alt="Pasted image (2)" src="https://github.com/user-attachments/assets/f13cdd29-e698-4537-b4a4-5d09a5440661" />


#### 2.Launched an Auto Scaling Group with all required configurations using a template named JenkinsTemplate.
<img width="1644" height="229" alt="image" src="https://github.com/user-attachments/assets/0ff5d43c-8721-41e9-9734-4ae2f02f9d8f" />





#### 3.Generated SSH keys to enable secure communication between Jenkins master and worker nodes.

#### 4.Stored the private SSH key on the Jenkins master node (user: ubuntu) and added the public key to the authorized_keys file of the Jenkins worker node.

#### 5.Facing an error when attempting to establish an SSH connection between the master and worker nodes in Jenkins.
