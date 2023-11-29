# AWS_ec2_based_web_page
### This project is a detailed instruction of how you can host your personal web site for cheapest price in 2023-2024.

# For my project I'll be use folowing stack of technology:
* AWS ec2 with ubuntu operating system
* ElasticIPs - statick ip which won't be changed after enstanse reboot
* Docker
* NGINX web server which will be run in docker. It allow me for creating isolated and encapsulated components that don't share resources that allow us automatically scale them up or down in future.
* www.namecheap.com for domain registration
* www.cloudflare.com for encrypting my web traffic, preventing data theft and other tampering.
* And of course HTML & CSS files, for web page itself. That I found in internet and customized to myself.
  
# AWS ec2 launching

* Sign in to AWS Console:
  - Log in to your AWS account at https://aws.amazon.com/.

* Navigate to EC2:
  - In the AWS Management Console, go to the "Services" dropdown and select "EC2" under the "Compute" section.

* Launch Instance:
  - Click on the "Instances" link in the EC2 Dashboard and then click the "Launch Instance" button.

* Choose an Amazon Machine Image (AMI):
  - Select an AMI that suits your needs, Ubuntu in our case.

* Choose an Instance Type:
  - Choose the type of instance you want to launch. We can use any free tier eligible (t3.micro) or to purchase the cheapest configuration which will cost around 6$ per month.

* Create Key Pair:
  - Press create new pair key. Type name of key. Select RSA key type and .pem format for future SSH connection.

* Network settings:
  - Select 'Create new security group' and all chek box below: allow ssh,https,http traffic.

* Add Storage:
  - You can add free space, but for our purposes it's not necessarily.

* Launch Instance:
  - Click "Launch Instances" to start your EC2 instance.

Once launched, you can connect to your EC2 instance using SSH (for Linux instances) or Remote Desktop (for Windows instances), depending on your chosen operating system.

# ElasticIPs

* Navigate to EC2:
  - In the AWS Management Console, go to the "Services" dropdown and select "EC2" under the "Compute" section.
   
* Allocate an Elastic IP:
   - In the EC2 Dashboard, click on "Elastic IPs" in the left navigation pane.
   - Click the "Allocate Elastic IP address" button.

* Allocate the Elastic IP:
    - Choose "Amazon's pool of IPv4 addresses" for the Allocation ID.
    - Click "Allocate."

* Associate Elastic IP with EC2 Instance:
  - In the Elastic IPs dashboard, select the newly created Elastic IP.
  - Click "Actions" and choose "Associate Elastic IP address."
  - In the dialog box, select the instance you want to associate the Elastic IP with.
  - Click "Associate."

* Confirm Association:
  - Once associated, you should see the Elastic IP listed in the Elastic IPs dashboard with the status "associated."

* Connecting to our AWS ec2 machine
    - Easyest way to use windowd PowerShell and next command ssh -i D:\use_your_path_to_the_key\your_keyname.pem ubuntu@Elastic_ip which we created above.

# Docker instalation and downloading NGNIX image from docker hub.

* Docker instalation
    - Use this [link](https://docs.docker.com/engine/install/ubuntu/) with instruction from official web site.
    - Execute below command
      ```bash
      sudo usermod -aG docker $USER
      ```
By adding current user to the docker group we prevent typing sudo every time during execution docker commands.

# NGNIX image and setting up
- Checking if nginx image exist
```bash
docker search nginx
```
- Downloading image
```bash
docker pull nginx
```
- Run image
```bash
docker run -d --restart unless-stopped -p 8080:80 nginx
```
  - `-d` option specifies that the container runs in detached mode: the container continues to run until stopped but does not respond to commands run on the command line.
  - `--restart` option settings for container restart `unless-stopped` always restart the container if it stops, except that when the container is stopped (manually or otherwise), it is not restarted even after Docker daemon restarts
  - `-p` option tells Docker to map the ports exposed in the container by the NGINX image (port 80) to the specified port on the Docker host. The first parameter specifies the port in the Docker host, the second parameter is mapped to the port exposed in the container
> [!important]
> Don't forget to add port 8080 or that what you invented in inbound list of rules in AWS security group.

## Seting up nginx.conf and adding our web site contetnt
  - Copying content from you machine into container
```bash
cp PATH_to_your_cintent `CONTAINER ID`:/var/www/
```

  - We need to enter into the container, for this purpose execute below command
```bash
docker ps
```
  Copy the `CONTAINER ID`
```bash
docker exec -it  CONTAINER ID /bin/bash
```


