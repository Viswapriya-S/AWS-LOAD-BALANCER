## AWS-LOAD-BALANCER
## REG NUMBER: 212225230311
## NAME: Viswapriya S
## AIM:
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## ALGORITHM:
## Step 1: Create an AMI for Auto Scaling:
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

## Step 2: Create a Target Group and Load Balancer:
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

## Step 3: Create a Launch Template and Auto Scaling Group:
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

## Step 4: Verify Load Balancing:
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

## Step 5: Test Auto Scaling:
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.

## Step 6: Terminate the Original Web Server:
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## OUTPUT:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9e5e0cb4-e06d-43bf-9525-358e104291fc" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/39c017b6-5ff3-44f9-a8d5-c55428f00b17" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2dccf4d4-99ad-4e4f-9748-ad35c31b4689" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/99fe830d-9144-421a-b9ee-e0800ca8c503" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3d1b2648-db71-442b-beb1-d29ad78b2e79" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/db636838-c783-4d10-8dad-b431f96c9b21" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/56fa0a8f-d03f-4bd0-ad50-2ed2f6528b1e" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2a713394-c443-433b-9b01-9c7a590e09e6" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ef5af9c1-9b76-48ff-be11-8cda23f7e0ed" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fb8a0a09-92c6-4269-883a-0cbdf754edf1" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a261a34b-9b47-45c0-a3ad-d36add96591c" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/de17821f-4971-44bf-89ce-458367a16d76" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3d68a396-c508-42dd-9c3a-ba8e4d2a7faa" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c74b116e-7839-496f-9dca-7a4b1ae71e9d" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/06792e3d-8fb7-4ec6-90ec-2516994d442c" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7150d080-b982-436f-818a-b9af2cfa80c5" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4ad01869-3d59-44da-a3e1-8c714cf70b6a" />
## RESULT:
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.
