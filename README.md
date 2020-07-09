# Aria Cloud Overview
Aria Cloud Penetration Testing Tools Container.  **Aria Cloud** is a Docker Container for remote pentesting over SSH or RDP, with a primary emphasis on cloud security tools and secondary on AD tools.  Use it for an assumed breach pentest where remote access is necessary via RDP or SSH, or for simple AD lab testing.  

# Summary of Tools (Image Built on Kali Linux Rolling)
* Metapackages:  kali-linux-core, kali-linux-top10, kali-desktop-core
* xRDP and SSH (for remote access)
* socat, powershell 7, smbclient
* AWS cli tools (aws, s3cmd)
* Azure cli tools (az)
* Google Cloud Platform cli tool (gcloud, kubectl)
* ROADTools (https://github.com/dirkjanm/ROADtools)
* Stormspotter (https://github.com/Azure/Stormspotter)
* ScoutSuite (https://github.com/nccgroup/ScoutSuite)
* Cloud_Enum
* cloudmapper
* Bucket Stream
* Pacu
* WeirdAAL
* evil-winrm
* Impacket Python libraries and sample tools
* Neo4j
* Bloodhound
* Plumhound
* Fox-IT Bloodhound-python data ingestor
* gitleaks
* shhgit
* gitrob
* Trufflehog
* detect-secrets
* Rubeus
* Mimikatz

# Default Credentials
Username:  aria
Password:  !aria123!

Most special tools are installed into /opt directory if they aren't in the default /usr/local/bin/ path

# 3 Docker Containers:  3 Potential Use Cases:
1.  aria-base:  Attach to /bin/bash local console, and do your thing.
2.  aria-rdp:  Use an RDP client to remotely access the container.  Best for running Bloodhound and other tools that require Neo4j GUI.
3.  aria-ssh:  Use an SSH client to remotely access the container.

# Base Image Use Case:  Build or Pull, and then Run 

**Pre-requisite:** Install docker for your system

**Quickly run it with docker pull:** 
```
docker pull iknowjason/aira-base:latest
```
Run it!
```
docker run -ti <IMAGE_ID>
```
You can get the IMAGE_ID with **docker images** command
**Build It** 
Clone this repo:
```
https://github.com/iknowjason/AriaCloud.git
cd AriaCloud
```
Build it:
```
docker build -f Dockerfile.base -t aria .
```
Run it:
```
docker run -ti aria
```

# RDP Container Use Case:  Build or Pull, and then Run 

**Quickly run it with docker pull:** 
```
docker pull iknowjason/aira-rdp:latest
```
Bind the RDP ports from the docker container to expose them on the LAN interface of the host computer
```
docker run -d --name myname -p 3389:3389 <IMAGE_ID>
```
You can get the IMAGE_ID with **docker images** command
Verify ports:
```
docker port myname
```
Now RDP to your Host computer's IP address on port 3389.

**Build It** 
Clone this repo:
```
https://github.com/iknowjason/AriaCloud.git
cd AriaCloud
```
Build it:
```
docker build -f Dockerfile.rdp -t aria .
```
Run it:
```
docker run -d --name myname -p 3389:3389 aria
```

# SSH Container Use Case:  Build or Pull, and then Run 

**Quickly run it with docker pull:** 
```
docker pull iknowjason/aira-ssh:latest
```
Bind the SSH ports from the docker container to expose them on the LAN interface of the host computer
```
docker run -d --name myname -p 22:22 <IMAGE_ID>
```
You can get the IMAGE_ID with **docker images** command
Verify ports:
```
docker port myname
```
Now SSH to your Host computer's IP address on port 22.

**Build It** 
Clone this repo:
```
https://github.com/iknowjason/AriaCloud.git
cd AriaCloud
```
Build it:
```
docker build -f Dockerfile.ssh -t aria .
```
Run it:
```
docker run -d --name myname -p 22:22 aria
```

# To Do
* Integration into AD Pentest CyberRange for automated deployment using Terraform template + Ansible Playbook
* k8s tools

# Hat Tips
* Offensive Security team for Kali
* All the other tool authors listed above
