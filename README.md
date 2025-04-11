Manual Setup for Passwordless SSH Authentication (Without ssh-copy-id)
🔑 Step 1: Generate SSH Key Pair (on Control Node)
Run this command on your Ansible control node (e.g., Jenkins server):

bash
Copy
Edit
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
This generates:

Private key: ~/.ssh/id_rsa

Public key: ~/.ssh/id_rsa.pub

📥 Step 2: Copy Public Key to Target Node (Manually)
SSH into the target EC2 instance:

bash
Copy
Edit
ssh -i <path-to-your-pem-file> ubuntu@<target-instance-public-ip>
Create .ssh directory and authorized_keys file (if not present):

bash
Copy
Edit
mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys
On your control node (Jenkins), get the public key:

bash
Copy
Edit
cat ~/.ssh/id_rsa.pub
Copy the output and paste it inside authorized_keys on the target instance.

Set the correct permissions:

bash
Copy
Edit
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
✅ Step 3: Verify SSH Connection
From the control node:

bash
Copy
Edit
ssh -i ~/.ssh/id_rsa ubuntu@<target-instance-public-ip>
You should be able to connect without a password prompt.

