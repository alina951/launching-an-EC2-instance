# Deploying MongoDB on an AWS EC2 Instance

## Objective

The objective of this project was to deploy a MongoDB database on an Amazon EC2 virtual machine running Ubuntu Linux. The database was configured to allow remote connections while restricting access using AWS Security Groups and SSH key authentication. The deployment was tested by connecting from MongoDB Compass on a local machine.

---

# Technologies Used

- Amazon Web Services (AWS)
- Amazon EC2
- Ubuntu Linux
- MongoDB Community Edition
- MongoDB Compass
- SSH
- Terminal / PowerShell

---

# Architecture

```
                 Internet
                     │
                     │
        +--------------------------+
        |   EC2 Public IP Address  |
        +--------------------------+
                     │
          SSH (Port 22)
                     │
             Ubuntu EC2 Instance
                     │
              MongoDB Server
                     │
         MongoDB Port 27017
                     │
             MongoDB Compass
              (My Laptop)
```

---

# Step 1 - Launch an EC2 Instance

An Ubuntu EC2 instance was launched using the AWS Management Console.

Configuration included:

- Ubuntu Server
- t2.micro instance
- Security Group
- RSA Key Pair
- Public IP address enabled

---

# Step 2 - Create a Key Pair

A new RSA key pair was created to enable secure SSH authentication.

Example:

```
<YOUR-KEY-PAIR>
```

Each key pair consists of:

- A **public key**, which is stored by AWS.
- A **private key (.pem)**, which is downloaded once and stored securely on the local machine.

The private key is required whenever connecting to the EC2 instance.

---

# Step 3 - Connect to the EC2 Instance

The EC2 instance was accessed securely using SSH.

Example command:

```bash
ssh -i <YOUR-KEY>.pem ubuntu@<EC2-PUBLIC-IP>
```

A successful connection confirmed that the EC2 instance was accessible.

---

# Step 4 - Update Ubuntu

Before installing MongoDB, the operating system was updated.

```bash
sudo apt update
sudo apt upgrade -y
```

Updating the system ensures that the latest security patches and software updates are installed.

---

# Step 5 - Install MongoDB

MongoDB Community Edition was installed after adding the official MongoDB repository.

Installed packages included:

- mongodb-org
- mongod

---

# Step 6 - Start the MongoDB Service

Start MongoDB:

```bash
sudo systemctl start mongod
```

Enable MongoDB to start automatically whenever the server boots:

```bash
sudo systemctl enable mongod
```

Verify that MongoDB is running:

```bash
sudo systemctl status mongod
```

Expected output:

```
Active: active (running)
```

---

# Step 7 - Configure MongoDB

The MongoDB configuration file was edited.

```
/etc/mongod.conf
```

The bind IP was changed from:

```
127.0.0.1
```

to:

```
0.0.0.0
```

This allows MongoDB to accept remote connections.

MongoDB was then restarted to apply the configuration.

```bash
sudo systemctl restart mongod
```

> **Note:** Although MongoDB was configured to accept remote connections, access was restricted using AWS Security Groups so that only my own public IP address could connect.

---

# Step 8 - Configure the Security Group

The EC2 Security Group inbound rules were configured as follows:

| Type | Port | Source |
|------|------|--------|
| SSH | 22 | My IP |
| Custom TCP | 27017 | My IP |

Restricting access to **My IP** reduces the attack surface by preventing connections from other internet users.

---

# Step 9 - Test MongoDB

MongoDB Shell was used to verify that the server was running correctly.

Launch the shell:

```bash
mongosh
```

Display available databases:

```javascript
show dbs
```

Successful execution confirmed that MongoDB had been deployed correctly.

---

# Step 10 - Connect Using MongoDB Compass

MongoDB Compass was installed on the local machine.

Example connection string:

```
mongodb://<EC2-PUBLIC-IP>:27017
```

MongoDB Compass successfully connected to the MongoDB server running on the EC2 instance.

---

#<img width="2842" height="1670" alt="Screenshot 2026-07-09 111043" src="https://github.com/user-attachments/assets/68cdeea1-c20e-440c-a34f-6972447ac6e9" />


# Authentication Process

```
Laptop
    │
    │ Private Key (.pem)
    ▼
Internet
    │
    ▼
EC2 Public IP
    │
    ▼
Ubuntu EC2 Instance
    │
    ▼
MongoDB Server
```

SSH uses the private key stored on the local machine to authenticate access to the EC2 instance.

- SSH communicates over **Port 22**.
- MongoDB listens on **Port 27017**.

---

# Security Considerations

This deployment followed several security best practices:

- SSH key authentication was used instead of passwords.
- The private `.pem` key was stored locally and never uploaded to GitHub.
- SSH access (Port 22) was restricted to **My IP**.
- MongoDB access (Port 27017) was restricted to **My IP**.
- Sensitive information such as AWS Account IDs, public IP addresses, usernames, and key names has been removed from this documentation.

> **Note:** For this learning exercise, access was restricted using AWS Security Groups. In a production environment, MongoDB authentication, TLS encryption, and additional hardening should also be implemented.

---

# Advantages of Deploying MongoDB on EC2

- Cloud-hosted database accessible remotely.
- Full administrative control over the server.
- Easy to scale as requirements increase.
- Flexible configuration of networking and security.
- Suitable for development, testing, and production workloads.

---

# Challenges Encountered

During the deployment, several challenges were encountered:

- Connecting securely to the EC2 instance using SSH.
- Configuring Ubuntu and installing MongoDB.
- Editing the MongoDB configuration file.
- Configuring AWS Security Groups correctly.
- Restarting services after configuration changes.
- Connecting remotely using MongoDB Compass.

---

# What I Learned

Through this project I gained practical experience in:

- Launching Amazon EC2 instances.
- Creating and managing SSH key pairs.
- Connecting securely to Linux servers.
- Installing MongoDB on Ubuntu.
- Managing Linux services with `systemctl`.
- Configuring AWS Security Groups.
- Enabling remote database access.
- Connecting remotely using MongoDB Compass.
- Understanding basic cloud networking and security.

---

# Conclusion

MongoDB was successfully deployed on an AWS EC2 instance running Ubuntu Linux. The server was configured to allow remote access while restricting connectivity through AWS Security Groups and SSH key authentication. This project provided valuable hands-on experience with cloud infrastructure, Linux administration, networking, and NoSQL database deployment.
