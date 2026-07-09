# launching-an-EC2-instance
launching an EC2 instance, connecting via SSH, installing MongoDB, and connecting from your laptop
# Deploying MongoDB on an AWS EC2 Instance

## Objective

The purpose of this task was to deploy a MongoDB database on an Amazon EC2 virtual machine running Ubuntu Linux. The database was configured to allow secure remote connections using SSH and MongoDB Compass.

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

An Ubuntu EC2 instance was launched from the AWS Management Console.

Configuration included:

- Ubuntu Server
- t2.micro instance
- Security Group
- Key Pair (.pem)
- Public IP enabled

---

# Step 2 - Create a Key Pair

A new RSA key pair was created.

Example:

```
se-alina-key-pair.pem
```

The key pair consists of:

- Public Key (stored by AWS)
- Private Key (.pem) downloaded to my computer

The private key is required whenever connecting to the EC2 instance.

---

# Step 3 - Connect to EC2 using SSH

The EC2 instance was accessed securely using SSH.

Example command:

```bash
ssh -i se-alina-key-pair.pem ubuntu@<EC2-Public-IP>
```

Successful login confirmed access to the Ubuntu server.

---

# Step 4 - Update Ubuntu

Before installing software the operating system was updated.

```bash
sudo apt update
sudo apt upgrade -y
```

This installs the latest security patches.

---

# Step 5 - Install MongoDB

MongoDB Community Edition was installed.

The MongoDB repository was added before installation.

Packages installed included:

- mongodb-org
- mongod

---

# Step 6 - Start MongoDB

MongoDB service was started.

```bash
sudo systemctl start mongod
```

Enable MongoDB to start automatically after reboot.

```bash
sudo systemctl enable mongod
```

Verify status.

```bash
sudo systemctl status mongod
```

Expected result:

```
Active: active (running)
```

---

# Step 7 - Configure MongoDB

The MongoDB configuration file was edited.

```
/etc/mongod.conf
```

The bind IP was changed from

```
127.0.0.1
```

to

```
0.0.0.0
```

This allows remote connections.

MongoDB was restarted afterwards.

```bash
sudo systemctl restart mongod
```

---

# Step 8 - Configure Security Group

The EC2 Security Group was updated.

Inbound Rules:

| Type | Port | Source |
|------|------|--------|
| SSH | 22 | My IP |
| Custom TCP | 27017 | My IP |

Only my IP address was allowed for security.

---

# Step 9 - Test MongoDB

MongoDB shell was used to confirm the database was working.

```bash
mongosh
```

Example:

```javascript
show dbs
```

---

# Step 10 - Connect from MongoDB Compass

MongoDB Compass was installed on my laptop.

Connection string:

```
mongodb://<EC2-Public-IP>:27017
```

Compass successfully connected to the MongoDB database running on the EC2 instance.

---

# How Authentication Works

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
Ubuntu Server
    │
    ▼
MongoDB
```

The SSH private key authenticates access to the EC2 server.

MongoDB listens on port **27017**.

SSH communicates over port **22**.

---

# Advantages of Deploying MongoDB on EC2

- Accessible from anywhere
- Runs continuously in the cloud
- Easy to scale
- Full control over the operating system
- Can host multiple databases

---

# Challenges Encountered

- Configuring SSH permissions
- Opening the correct Security Group ports
- Editing the MongoDB configuration file
- Restarting the MongoDB service after configuration changes
- Connecting remotely from MongoDB Compass

---

# What I Learned

Through this task I learned how to:

- Launch an EC2 instance
- Create and use SSH key pairs
- Connect securely to a Linux server
- Install MongoDB on Ubuntu
- Configure MongoDB for remote access
- Manage Linux services using systemctl
- Configure AWS Security Groups
- Connect remotely using MongoDB Compass

---

# Conclusion

MongoDB was successfully deployed on an AWS EC2 instance. The server was configured for secure remote access using SSH and MongoDB Compass. This exercise provided practical experience with Linux server administration, AWS cloud infrastructure, networking, and NoSQL database deployment.
