I’m setting up Jenkins agents on EC2.

Instead of manually creating workers, I want to use EC2-Fleet Plugin (Auto Scaling with Spot instances) so Jenkins can dynamically scale nodes.

The Jenkins controller should connect to these EC2 agents via SSH (using the ubuntu user + private key).

Currently, I can manually SSH into the agent from the master, but in Jenkins UI the node shows offline with the error "".
<img width="1427" height="296" alt="image" src="https://github.com/user-attachments/assets/52be7137-b74b-4a1d-9472-e0e31c32c551" />


So my goal is:

Bring the EC2 agent online in Jenkins (via EC2-Fleet plugin) using SSH authentication with private key.

### Steps:
#### 1.Created an EC2 instance called JenkinsWorkerNodes.
<img width="1657" height="273" alt="image" src="https://github.com/user-attachments/assets/0b7f144e-1edb-4cdd-9cdc-dd6d8371113f" />

This is the AMI created from WorkerNode Which we have created earlier.
<img width="1361" height="891" alt="image" src="https://github.com/user-attachments/assets/985743b0-dcda-4975-9cc1-e4ade1f70b49" />
Launch Template:
I have used AMI to create this Template.
<img width="1644" height="229" alt="image" src="https://github.com/user-attachments/assets/0ff5d43c-8721-41e9-9734-4ae2f02f9d8f" />




#### 2.Launched an Auto Scaling Group with all required configurations using a template named JenkinsTemplate.

<img width="1824" height="322" alt="image" src="https://github.com/user-attachments/assets/e5019769-4694-49f8-841d-8f679dd085a3" />




#### 3.Generated SSH keys to enable secure communication between Jenkins master and worker nodes.
Connect to the JenkinsMainSever name "JenkinsServerAlloi"
```
ssh-keygen -t ed25519 -f ~/.ssh/jenkins_agent_key
```
<img width="1189" height="648" alt="image" src="https://github.com/user-attachments/assets/36ba5dbb-ba0c-427a-9bf5-ad841f01049b" />

```
ssh -i ~/.ssh/jenkins_agent_key ubuntu@15.206.153.205

```
The SSH connection between your Jenkins master and agent (worker) node is successfully established using the private key.
this message is from terminal.We are facing issue with only with JenkinsUI.

#### 4.Stored the private SSH key on the Jenkins master node (user: ubuntu) and added the public key to the authorized_keys file of the Jenkins worker node.

<img width="1654" height="380" alt="image" src="https://github.com/user-attachments/assets/d7621eec-eac4-43f3-876b-9cf063503db0" />

#### 5.created a cloud EC2-Fleet in jenkins with providing ASG,SSH credentials and AWS credentials.
<img width="1856" height="968" alt="image" src="https://github.com/user-attachments/assets/4461728b-bc04-4cc9-984b-0c9a22ff8859" />

#### For checking configurations:
##### Navigate to manage jenkins > clouds >EC2-Fleet >configure 

##### Navigate to manageJenkins > nodes > EC2-fleet -i <instance id>

launch an agent you will see the error.
<img width="1856" height="452" alt="image" src="https://github.com/user-attachments/assets/2b165d7c-dd4d-41d3-8f6e-49e3dbbab375" />

#### 6.Facing an error when attempting to establish an SSH connection between the master and worker nodes in Jenkins.
<img width="1427" height="296" alt="image" src="https://github.com/user-attachments/assets/e3e90611-a0a1-43ab-8921-25bc92e51f22" />

The only Issue with cloud node EC2-Fleet Configuration.
