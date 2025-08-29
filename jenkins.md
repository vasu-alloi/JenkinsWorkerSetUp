I’m setting up Jenkins agents on EC2.

Instead of manually creating workers, I want to use EC2-Fleet (or Auto Scaling with Spot instances) so Jenkins can dynamically scale nodes.

The Jenkins controller should connect to these EC2 agents via SSH (using the ubuntu user + private key).

Currently, I can manually SSH into the agent from the master, but in Jenkins UI the node shows offline with the error "The selected credentials cannot be found".

So my goal is:

Bring the EC2 agent online in Jenkins (via EC2-Fleet plugin) using SSH authentication with private key.

Steps:
1.Created an EC2 instance called JenkinsWorkerNodes using an AMI to serve as the basis for an AWS Auto Scaling Group.

2.Launched an Auto Scaling Group with all required configurations using a template named JenkinsTemplate.

3.Generated SSH keys to enable secure communication between Jenkins master and worker nodes.

4.Stored the private SSH key on the Jenkins master node (user: ubuntu) and added the public key to the authorized_keys file of the Jenkins worker node.

5.Facing an error when attempting to establish an SSH connection between the master and worker nodes in Jenkins.
