# Testing-AWS-VPC-Connectivity

Enhancing AWS Infrastructure: A Step-by-Step Guide to My Latest Project
In this article, I'll walk you through a recent project I completed to enhance our AWS infrastructure. The project focused on improving secure SSH access, ensuring reliable server communication, and verifying internet access for our VPC. Here’s a detailed, step-by-step guide:

Step 1: Secure SSH Access with EC2 Instance Connect
Objective:
Streamline and secure SSH access to EC2 instances by eliminating the need for managing SSH keys.

Steps:
Enable EC2 Instance Connect:
Open the AWS Management Console and navigate to the EC2 dashboard.
Select the EC2 instance you want to access.
Ensure the instance is running Amazon Linux 2 or Ubuntu 16.04 and later.
Update IAM Roles and Permissions:

Navigate to the IAM service in the AWS Management Console.
Create or update an IAM role that includes the ec2-instance-connect:SendSSHPublicKey permission.
Attach this IAM role to your EC2 instance.
Modify Security Group Settings:
Go to the EC2 dashboard and select the security group associated with your Public Server.
Edit the inbound rules to allow SSH traffic from the EC2 Instance Connect service. Specifically, add a rule to permit traffic on port 22 from ec2-instance-connect IP ranges.

Access the EC2 Instance:
In the EC2 dashboard, select the instance and click on "Connect."
Choose the "EC2 Instance Connect" tab and click "Connect" to SSH into your instance using the temporary key.

Benefits:
Simplifies SSH access management.
Enhances security by using temporary, session-specific SSH keys.

Step 2: Ensuring EC2 Connectivity with Ping
Objective:
Verify that public and private EC2 instances can communicate with each other.

Steps:
Use Ping to Test Connectivity:
Open a terminal on your Public Server.
Use the ping command to send ICMP Echo Request packets to the Private Server’s IP address:
bash
Copy code
ping <private-server-ip>
Observe the responses to confirm connectivity.

Update NACL Settings:
In the AWS Management Console, navigate to the VPC dashboard.
Select the Network Access Control List (NACL) associated with your Private Server’s subnet.
Update the inbound rules to allow ICMP traffic (type 8, code 0) from the Public Server’s IP range.
Update the outbound rules to allow ICMP traffic (type 0, code 0) back to the Public Server’s IP range.

Benefits:
Ensures reliable communication between EC2 instances.
Facilitates network troubleshooting and connectivity validation.

Step 3: Verifying VPC Internet Access with Curl
Objective:
Confirm that the VPC has proper internet access by fetching data from external web servers.

Steps:
Use Curl to Test Internet Access:
Open a terminal on an EC2 instance within the VPC.
Use the curl command to fetch data from a web server:
bash
Copy code
curl http://example.com
Check the output to ensure the data is retrieved successfully.

Verify VPC Configuration:
Ensure that the VPC has an attached Internet Gateway (IGW).
Check that the route table associated with the subnet includes a route directing traffic to the IGW (destination: 0.0.0.0/0, target: igw-id).

Benefits:
Confirms that the VPC can access external resources.
Validates that the network configuration supports secure outbound internet traffic.

Conclusion
By following these steps, I was able to enhance our AWS infrastructure’s security, reliability, and connectivity. Implementing EC2 Instance Connect simplified our SSH access, while ping tests and NACL updates ensured robust server communication. Additionally, verifying VPC internet access with curl confirmed our network’s capability to interact with external resources effectively.

This project marks a significant improvement in our cloud environment, and I’m excited to see the positive impact it will have on our operations. If you have any questions or would like to discuss these techniques further, feel free to reach out!
