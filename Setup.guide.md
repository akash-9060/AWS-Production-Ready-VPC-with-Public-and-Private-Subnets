Project Implementation
=
Here are Following list of steps that are used to implement this project.
=
Step1: First we should have the AWS account created or with IAM User you can login.
=
<img width="1920" height="949" alt="Screenshot (11)" src="https://github.com/user-attachments/assets/fb7c1be8-0e0b-4aba-960a-a02d622ec559" />

Step2: Create a VPC.
=
1.On VPC settings, click on VPC and more
<img width="1903" height="910" alt="Screenshot 2025-09-29 110500" src="https://github.com/user-attachments/assets/e79602a6-12da-498a-9fd4-a703fcbaa9d0" />
<img width="1879" height="910" alt="Screenshot 2025-09-29 110616" src="https://github.com/user-attachments/assets/ffa916f0-38c5-457b-a767-09910a875cf3" />
<img width="778" height="873" alt="Screenshot 2025-09-29 110736" src="https://github.com/user-attachments/assets/08b7dbb5-5c0d-455c-8a93-8c779e2585ec" />

2. Now VPC has been created successfully

<img width="1894" height="908" alt="Screenshot 2025-09-29 110914" src="https://github.com/user-attachments/assets/216a37ce-62ed-4e9c-bf22-fa378c3fbcb3" />
<img width="1887" height="911" alt="Screenshot 2025-09-29 111004" src="https://github.com/user-attachments/assets/38381717-d7b4-4d81-aaf9-15525821879a" />

Step3: Creation of an Auto-scaling group:
=
 
1. Click on EC2 and select the autoscaling option

<img width="1889" height="917" alt="Screenshot 2025-09-29 111912" src="https://github.com/user-attachments/assets/e3753d59-2955-4a09-bf91-112db9f482e3" />

2. Click on launch template. Autoscaling in AWS cannot be created directly. For this, you can use the launch template. You can use that template in multiple autoscaling groups, and it acts as a reference

<img width="1901" height="915" alt="Screenshot 2025-09-29 113535" src="https://github.com/user-attachments/assets/5458eb2c-39b9-4046-8ea8-63825c9277d6" />
<img width="1891" height="918" alt="Screenshot 2025-09-29 113554" src="https://github.com/user-attachments/assets/1eeab453-0c58-4292-9c78-06936d916cf7" />
Setting the Inbound rules for the application:

 The port that we are using for accessing the application is port 8000, and adding the SSH rule on port 22, and setting the source type 

<img width="1886" height="916" alt="Screenshot 2025-09-29 113856" src="https://github.com/user-attachments/assets/6dab65d3-43d3-4363-a638-11c3001a1f0a" />
<img width="1895" height="909" alt="Screenshot 2025-09-29 114001" src="https://github.com/user-attachments/assets/adff0780-0b3b-4b77-92b1-edee29158acd" />

3. Launch template is create.
<img width="1890" height="820" alt="Screenshot 2025-09-29 114018" src="https://github.com/user-attachments/assets/d9374fee-fe04-4919-888d-4834424daa56" />

4. Choose a launch template.
<img width="1879" height="908" alt="Screenshot 2025-09-29 114133" src="https://github.com/user-attachments/assets/0a1f512e-cce7-4dbd-bb88-84a93172fa38" />

5.  Choose the VPC that we have created,the availability zones as private subnets.
<img width="1888" height="910" alt="Screenshot 2025-09-29 114157" src="https://github.com/user-attachments/assets/d6e62f7f-be43-4678-b2f8-0a0fdf6e1d26" />

6. Click on No Load Balancer, we will create the load balancer in the public subnet.
<img width="1870" height="556" alt="Screenshot 2025-09-29 114214" src="https://github.com/user-attachments/assets/68dff4ad-f376-4b5a-9912-4121df53dfb1" />

7.  Select the group capacity.
<img width="1877" height="915" alt="Screenshot 2025-09-29 114242" src="https://github.com/user-attachments/assets/8f5ed829-8de3-4d8b-a385-1f1484a09a28" />

8. Now the autoscaling group has been launched successfully.
<img width="1889" height="613" alt="Screenshot 2025-09-29 114416" src="https://github.com/user-attachments/assets/6d85e023-c151-415d-8c27-89be6bcf4477" />

Two instances of EC2 were created successfully, and two instances were created in different availability zones.


<img width="1888" height="749" alt="Screenshot 2025-09-29 114452" src="https://github.com/user-attachments/assets/d16a4c4c-666f-492a-8e73-2e9427ce816a" />

Step4: Creating the Bastion Host:
=
1. In EC2, click on Launch Instance and give it a name and choose ubuntu as an image
<img width="1894" height="908" alt="Screenshot 2025-09-29 114530" src="https://github.com/user-attachments/assets/3df19896-7e43-4230-b6d4-d20ee73f3a84" />
<img width="1247" height="856" alt="Screenshot 2025-09-29 114626" src="https://github.com/user-attachments/assets/a38c47a3-59ce-468c-acea-82e8af5988cd" />

2. Make sure to add a security group that has access to SSH, and make sure that the bastion host is created in the same VPC and enable the Auto-assign public IP
<img width="1887" height="819" alt="Screenshot 2025-09-29 114801" src="https://github.com/user-attachments/assets/d5e3a726-c471-4f1a-96d3-1b421b648dc7" />

3. Now launch the instance, and you will see bastion-host has been created successfully
<img width="1888" height="481" alt="Screenshot 2025-09-29 114902" src="https://github.com/user-attachments/assets/9fdeb14e-d89d-487f-a370-73bc58284ef5" />

SSH into private subnet using bastion host:

4. First, let's do the secure copy. The command transfers the file devops-demo.pem (private key file) from the local system to the /home/ubuntu directory on the remote server.

This is commonly done to:

• Share the file for further use on the remote server.

• Prepare the remote environment for SSH-based operations.

• Now you can see that the .pem file is available in the bastion host.

• and you can ssh to bastion

5. When you do ls, you can see your.pem file in the bastion EC2.

With this setup, I will proceed to deploy a straightforward application on one of the instances we created within the private subnet.

To accomplish this, we will establish an SSH connection to one of the instances, utilizing the same terminal environment for seamless access and control.

6. Take the private IP address of any of the instances and SSH into it, In my case, I am taking 10.0.145.101

7. Give 600 permissions to .pem file

8. Now we are login to private EC2 as well

9. Now we will install a simple Python application in it
     First, create an HTML file and look for a simple HTML code from google(W3.school)

10.  Now run the Python server by using the following command: python3 -m http.server 8000

Step5: Application Load Balancer:
=

Now we will try to create a load balancer and attach private subnet instances as a target group that will be our final stage.
=

1. Go to AWS and search for load balancer, and click on create load balancer
 In our use case, go with an application load balancer, which is the L7 load balancer. The Application Load Balancer distributes incoming HTTP and HTTPS traffic across multiple targets such as Amazon EC2 instances, microservices, and containers, based on request attributes. When the load balancer receives a connection request, it evaluates the listener rules in priority order to determine which rule to apply, and if applicable, it selects a target from the target group for the rule action.
<img width="1911" height="920" alt="Screenshot 2025-09-29 120550" src="https://github.com/user-attachments/assets/b9ccd61b-979e-44ce-9cbf-77252b2d7a98" />
<img width="1878" height="914" alt="Screenshot 2025-09-29 120647" src="https://github.com/user-attachments/assets/2a31ac2d-14c9-43dc-badb-6053a6caeb75" />
<img width="1911" height="370" alt="Screenshot 2025-09-29 120750" src="https://github.com/user-attachments/assets/7d564494-88c1-4309-bb61-6850a85bad5e" />

2. Create a target group whose instances should be accessible. For this, click on the target group
<img width="1887" height="716" alt="Screenshot 2025-09-29 120827" src="https://github.com/user-attachments/assets/1ccfd8dc-5149-42dc-ae0a-73498f09dc50" />

3. Select the instances of private subnet. One has the application and the other doesn’t and click on create target group.
<img width="1887" height="912" alt="Screenshot 2025-09-29 120920" src="https://github.com/user-attachments/assets/6d0a68a3-e6b1-489d-8551-fff42393658d" />

4. Adding target group to the load balancer:

Now create target group.
<img width="1889" height="918" alt="Screenshot 2025-09-29 120942" src="https://github.com/user-attachments/assets/b89220cf-221c-4e78-bfd6-8ee7ac5ef9f9" />

5. Click on create load balancer and add the target group and port 80 which is default and make it 8000
<img width="1885" height="905" alt="Screenshot 2025-09-29 120958" src="https://github.com/user-attachments/assets/666bfd46-fdd5-4f57-9882-da6e0d806482" />

 Now load balancer with the attached target group has been created successfully


Accessing the application from outside world:
=
Let’s try to access the load balancer and you will see that the load balancer is not accessible because the subnet that you attached to the load balancer does not expose port 80 so we have to explicitly add the rule

Now we create the Load Balancer
<img width="1886" height="908" alt="Screenshot 2025-09-29 121434" src="https://github.com/user-attachments/assets/9fa7a9c9-2cb5-4a78-9192-ac59bec89fe7" />

Now we will try to access the load balancer. You will see that it is not accessible because the subenet doesn’t has port 80

To make it accessible, go to the security group. Edit inbound rule

And there allow HTTP rule from anywhere and then save rule

When you will check load balancer then you will notice the error has gone

Now you will see our application is accessible successfully!


