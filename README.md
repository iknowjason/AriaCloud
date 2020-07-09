# Aria Cloud Overview
Aria Cloud Penetration Testing Tools.  **Aria Cloud** is a Docker Container for remote pentesting over SSH or RDP, with a primary emphasis on cloud security tools and secondary on AD tools.  Use it for an assumed breach pentest where remote access is necessary, or for simple AD lab testing.

# Summary of Tools
* Image built on Kali Linux rolling
* Metapackages:  kali-linux-core, kali-linux-top10, kali-desktop-core
* xRDP and SSH (for remote access)
* socat, powershell 7, smbclient
* AWS cli tools (aws, s3cmd)
* Azure cli tools (az)
* Google Cloud Platform cli tool (gcloud, kubectl)
* ROADTools
* Stormspotter
* ScoutSuite
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

# 3 Docker Containers / Use Cases:
1.  aria-base:  Attach to /bin/bash local console, and do your thing.
2.  aria-rdp:  Use an RDP client to remotely access the container.  Best for running Bloodhound and other tools that use Neo4j GUI.
3.  aria-ssh:  Use an SSH client to remotely access the container.

# Base Image:  Build or Pull, and then Run 

**Step 1:** Install Terraform and Ansible on your Linux system

Download and install Terraform for your platform --> https://www.terraform.io/downloads.html

Install Ansible
```
$ sudo apt-get install ansible
```

# Tools Detailed

# To Do

# Credits
