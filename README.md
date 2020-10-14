# Aria Cloud Overview
Aria Cloud Penetration Testing Tools Container.  **Aria Cloud** is a Docker Container ideal for remote pentesting over SSH or RDP, with a primary emphasis on cloud security tools and secondary on Active Directory tools.  Use it for an assumed breach pentest where remote access is necessary via RDP or SSH, or for simple AD lab testing.  It is built for use cases where one needs to remote into a container using SSH or RDP, and then run their security workflows (i.e., Cloud environments).  This repo also included an automated Terraform template + Ansible Playbook to deploy Aria Cloud as a container running on an Ubuntu Linux VM, with remote access over RDP. 

Medium Blog:  https://medium.com/bugbountywriteup/pentesting-in-the-clouds-introducing-ariacloud-58cb5cc1c50d


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
* Cloud_Enum (https://github.com/initstring/cloud_enum)
* cloudmapper (https://github.com/duo-labs/cloudmapper)
* Bucket Stream (https://github.com/eth0izzle/bucket-stream)
* Pacu (https://github.com/RhinoSecurityLabs/pacu)
* WeirdAAL (https://github.com/carnal0wnage/weirdAAL)
* evil-winrm (https://github.com/Hackplayers/evil-winrm)
* Impacket Python library and tools (https://github.com/SecureAuthCorp/impacket)
* Neo4j (https://neo4j.com/)
* Bloodhound (https://github.com/BloodHoundAD/BloodHound)
* Plumhound (https://github.com/DefensiveOrigins/PlumHound)
* Fox-IT Bloodhound-python data ingestor (https://github.com/fox-it/BloodHound.py)
* gitleaks (https://github.com/zricethezav/gitleaks)
* shhgit (https://github.com/eth0izzle/shhgit)
* gitrob (https://github.com/michenriksen/gitrob)
* Trufflehog (https://github.com/dxa4481/truffleHog)
* detect-secrets (https://github.com/Yelp/detect-secrets)
* Rubeus (https://github.com/GhostPack/Rubeus)
* Mimikatz (https://github.com/gentilkiwi/mimikatz)

# Terraform Automated Deployment

This repo now includes a Terraform template and Ansible Playbook that automatically deploys Aria Cloud into an Azure VM with remote access over RDP.  For more information, navigate into the **terraform-azure** directory and see the README.


# Default Credentials

**Username:**  aria

**Password:**  !aria123!

**Default Tools Directory** Most special tools are installed into **/opt** directory if they aren't in the default /usr/local/bin/ path

# 3 Docker Containers:  3 Potential Use Cases
**Use Case #1:**  aria-base:  Attach to /bin/bash local console, and do your thing.

**Use Case #2:**  aria-rdp:  Use an RDP client to remotely access the container.  Best for running Bloodhound and other tools that require Neo4j GUI.

**Use Case #3:**  aria-ssh:  Use an SSH client to remotely access the container.

# Base Image Use Case:  Build or Pull, and then Run 

**Pre-requisite:** Install docker for your system

**Quickly run it with docker pull:** 

```
docker pull iknowjason/aria-base:latest
```
Run it!
```
docker run -ti iknowjason/aria-base:latest
```

You can get the IMAGE_ID with **docker images** command

**Build & Run It** 

Clone this repo:

```
git clone https://github.com/iknowjason/AriaCloud.git
cd AriaCloud
```
Build:
```
docker build -f Dockerfile.base -t aria .
```
Run:
```
docker run -ti aria
```

# RDP Container Use Case:  Build or Pull, and then Run 

**Quickly run it with docker pull:** 

```
docker pull iknowjason/aria-rdp:latest
```

Bind the RDP ports from the docker container to expose them on the LAN interface of the host computer

```
docker run -d --name myname -p 3389:3389 iknowjason/aria-rdp:latest
```

You can get the IMAGE_ID with **docker images** command

Verify ports:
```
docker port myname
```
Now RDP to your Host computer's IP address on port 3389.

**Build & Run It** 

Clone this repo:
```
git clone https://github.com/iknowjason/AriaCloud.git
cd AriaCloud
```
Build:
```
docker build -f Dockerfile.rdp -t aria .
```
Run:
```
docker run -d --name myname -p 3389:3389 aria
```

# SSH Container Use Case:  Build or Pull, and then Run 

**Quickly run it with docker pull:** 
```
docker pull iknowjason/aria-ssh:latest
```
Bind the SSH ports from the docker container to expose them on the LAN interface of the host computer
```
docker run -d --name myname -p 22:22 iknowjason/aria-ssh:latest
```
You can get the IMAGE_ID with **docker images** command

Verify ports:
```
docker port myname
```
Now SSH to your Host computer's IP address on port 22.

**Build & Run It** 

Clone this repo:
```
git clone https://github.com/iknowjason/AriaCloud.git
cd AriaCloud
```
Build:
```
docker build -f Dockerfile.ssh -t aria .
```
Run:
```
docker run -d --name myname -p 22:22 aria
```

# To Do
* Fix small errors after RDP connection and auth success
* Fix MacOS RDP client black screen
* Terraform template deployment for AWS
* K8s tools

# Hat Tips
* Offensive Security team for Kali
* All the other tool authors listed above
