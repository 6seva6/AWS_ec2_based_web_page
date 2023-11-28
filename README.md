# AWS_ec2_based_web_page
### This project is a detailed instruction of how you can host your personal web site for cheapest price in 2023-2024.

# For my project I'll be use folowing steck of technology:
* AWS ec2 with ubuntu operating system
* ElasticIPs - statick ip which won't be changed after enstanse reboot
* Docker
* NGINX web server which will be run in docker. It allow me for creating isolated and encapsulated components that don't share resources that allow us automatically scale them up or down in future.
* www.namecheap.com for domain registration
* www.cloudflare.com for encrypting my web traffic, preventing data theft and other tampering.
* And of course HTML & CSS files, for web page itself. That I found in internet and customized to myself.
  
# AWS ec2 launching

* Sign in to AWS Console:
> Log in to your AWS account at https://aws.amazon.com/.

* Navigate to EC2:
In the AWS Management Console, go to the "Services" dropdown and select "EC2" under the "Compute" section.

* Launch Instance:
Click on the "Instances" link in the EC2 Dashboard and then click the "Launch Instance" button.

* Choose an Amazon Machine Image (AMI):
Select an AMI that suits your needs, Ubuntu in our case.

* Choose an Instance Type:
Choose the type of instance you want to launch. We can use any free tier eligible (t3.micro) or to purchase the cheapest configuration which will cost around 6$ per month.

* Create Key Pair:
Press create new pair key. Type name of key. Select RSA key type and .pem format for future SSH connection.

* Network settings:
Select 'Create new security group' and all chek box below: allow ssh,https,http traffic.

* Add Storage:
You can add free space, but for our purposes it's not necessarily.

* Launch Instance:
Click "Launch Instances" to start your EC2 instance.

Once launched, you can connect to your EC2 instance using SSH (for Linux instances) or Remote Desktop (for Windows instances), depending on your chosen operating system.
