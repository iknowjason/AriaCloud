FROM kalilinux/kali-rolling

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update && apt-get -y dist-upgrade && apt-get -y autoremove && apt-get install -y wget && apt-get clean

# Install some Kali core essentials
RUN apt-get install kali-linux-core kali-tools-top10 kali-desktop-core apt-utils -y 

# Install some miscellaneous favorites
RUN apt-get -y install net-tools python3-pip powershell smbclient socat

# Install awscli and s3cmd tools (aws, s3cmd)
RUN apt-get -y install awscli s3cmd

# Install some potential pre-requisites
RUN apt-get -y install ca-certificates curl apt-transport-https lsb-release gnupg

# Install Azure cli tool (az)
RUN apt-get install azure-cli -y

# Install Google Cloud Platform cli tool (gcloud)
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
RUN apt-get update -y && sudo apt-get install google-cloud-sdk kubectl -y

# Install ROADTools
RUN pip3 install roadrecon

# Install evil-winrm
RUN gem install evil-winrm

# Install Impacket Python libraries for interacting with AD
RUN /bin/bash -c "cd /opt;git clone https://github.com/SecureauthCorp/impacket;cd impacket;python3 ./setup.py install" 

# Install Neo4j for BloodHound
RUN apt-get install neo4j -y

# Install bloodhound tool
RUN apt-get install bloodhound -y

# Install fox-it bloodhound-python data ingestor
RUN pip3 install bloodhound

# Install WeirdAAL
RUN /bin/bash -c "cd /opt;git clone https://github.com/carnal0wnage/weirdAAL.git;cd weirdAAL;apt-get install python3-venv -y;python3 -m venv weirdAAL;source weirdAAL/bin/activate;pip3 install -r requirements.txt;python3 create_dbs.py" 

# Install Pacu
RUN /bin/bash -c "cd /opt;git clone https://github.com/RhinoSecurityLabs/pacu;cd pacu;chmod +x install.sh;./install.sh"

### By default, pacu causes an issue with default aws cli tools.
### Error: ModuleNotFoundError: No module named 'botocore.vendored
# To fix this, we run:  pip3 install --upgrade boto3 awscli
RUN pip3 install --upgrade boto3 awscli

# Install Cloud_Enum
RUN /bin/bash -c "cd /opt;git clone https://github.com/initstring/cloud_enum;cd cloud_enum;pip3 install -r ./requirements.txt"

# Install Bucket Stream
RUN /bin/bash -c "cd /opt;git clone https://github.com/eth0izzle/bucket-stream.git;cd bucket-stream;pip3 install virtualenv && virtualenv .virtualenv && source .virtualenv/bin/activate;pip3 install -r requirements.txt"

# Install Stormspotter
RUN pip3 install stormspotter==1.0.0a0

# User setup
RUN useradd -ms /bin/bash -p $(openssl passwd -1 !aria123!) aria
RUN usermod -a -G sudo aria

# Copy gitleaks
COPY ./tools/gitleaks /usr/local/bin/gitleaks

# Copy shhgit
RUN mkdir /opt/shhgit 
COPY ./tools/shhgit /usr/local/bin/shhgit
COPY ./tools/config.yaml /opt/shhgit/config.yaml

# Copy gitrob 
COPY ./tools/gitrob /usr/local/bin/gitrob

# Copy Rubeus
RUN mkdir /opt/rubeus
COPY ./tools/Rubeus.exe /opt/rubeus/Rubeus.exe
 
# Install Trufflehog
RUN pip3 install truffleHog

# Install detect-secrets
RUN pip3 install detect-secrets

# Install cloudmapper
RUN apt-get install autoconf automake libtool python3-tk python3-venv -y
RUN /bin/bash -c "cd /opt;git clone https://github.com/duo-labs/cloudmapper.git;cd cloudmapper;pip3 install -r requirements.txt"

# Install ScoutSuite
RUN pip3 install ScoutSuite

# Install Plumhound
RUN /bin/bash -c "cd /opt;git clone https://github.com/DefensiveOrigins/PlumHound;cd PlumHound;pip3 install -r requirements.txt"

# Download Mimikatz
RUN /bin/bash -c "mkdir /opt/mimikatz;cd /opt/mimikatz;wget https://github.com/gentilkiwi/mimikatz/releases/download/2.2.0-20200519/mimikatz_trunk.7z"

# Install OpenSSH Server
RUN apt-get install openssh-server -y

# Make privilege separation directory
RUN mkdir /run/sshd

CMD /usr/sbin/sshd  -D
