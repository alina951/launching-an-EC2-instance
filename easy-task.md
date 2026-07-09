# Easy Task
### Deploy Nginx WebServer on an EC2 instance, Make sure it serves a basic html and css website rather than the basic welcome page (use ai to create this).

# Step 1
![Create EC2](/images/easys1.png)
First you want to create your EC2 instance, Make sure to create a linux based OS so either UBuntu or Amazon Linux 2023 to install nginx. 

Settings:
1. Instance type: t2.micro or t3.micro
2. Key pair: Use Existing
3. Network settings: Allow SSH and HTTP
4. Launch EC2

# Step 2
![Connect EC2](/images/easys2.png)

Once the EC2 is running you want to connect to the instance through the SSH client
# Step 3
![GIT BASH connect ec2](/images/easys3.png)

Open your personal terimnal (In this case i use GITBASH) and make sure to go into .ssh folder where your private key is stored. Finally execute the command that amazon provides in Step 2. 
# Step 4
![Update/Upgrade Ubuntu](/images/easys4.png)
![Install Nginx](/images/easys5.png)

For ubuntu Linux you want to run the above commands to successfully upgrade and update the system package repository, then install nginx. After this you can run 

```terminal
sudo systemctl start nginx
sudo systemctl enable nginx
```

to start and enable nginx to run automatically on system boot

# Step 5
![Nginx basic page](/images/easys6.png)
Once finished you can then access your website going to your personal browser and typing http://ec2publicipaddress. you should be able to see a base tempalte for your website. 

>NOTE:  make sure you start with http not https as we only allowed access to port 80 in the network settings when creating the EC2 instance. 
# Step 6
To customise the page further we want to go into the fodler where the base template is located in var/www/html using the command below: 

![Change to html directory](/images/easys9.png)

You should be able to see a base template html file which you can access.
# Step 7
using ```sudo nano [filename].html``` we can access the file and edit it. 
![edit html file using sudo nano](/images/easys7.png)

Using AI i created a base a cool html page to copy and paste in. 

>!NOTE: Make sure to use sudo before the nano command to make sure you have editing/saving permissions. 

# Step 8
Finally i refreshed the page to display the end product. 

![Finished html page](/images/easys8.png)
