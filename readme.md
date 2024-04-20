## Setup GOCD Agent on Linux using script 

Create a file and give executable permission - You may need to ask to edit file manually so do that rest will be done by script also execute this script as sudo


```bash
#!/bin/bash

# Step 1: Install keyrings and add GOCD GPG key
apt install gpg curl -y
install -m 0755 -d /etc/apt/keyrings
curl https://download.gocd.org/GOCD-GPG-KEY.asc | gpg --dearmor -o /etc/apt/keyrings/gocd.gpg
chmod a+r /etc/apt/keyrings/gocd.gpg

# Step 2: Add GOCD repository
echo "deb [signed-by=/etc/apt/keyrings/gocd.gpg] https://download.gocd.org /" | tee /etc/apt/sources.list.d/gocd.list
apt update

# Step 3: Install GOCD agent
apt-get install go-agent

# Step 4: Navigate to GOCD agent directory
cd /usr/share/go-agent
chmod -R 777 wrapper-config/

# Step 5: Edit wrapper-properties.conf
nano /usr/share/go-agent/wrapper-config/wrapper-properties.conf

# Step 6: Start the agent
systemctl start go-agent
```

