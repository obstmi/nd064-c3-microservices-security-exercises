# Installations
## Go
### Remove old versions:  
* sudo apt-get remove golang-go
* sudo apt-get remove --auto-remove golang-go
### Install new version:
* wget https://go.dev/dl/go1.19.linux-arm64.tar.gz
* sudo tar -C /usr/local -xzf go1.19.linux-arm64.tar.gz
### Add path:
* echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.profile
* source ~/.profile
### Test it:
* go version
* go env | grep GOENV

## Install docker-compose standalone
* sudo curl -SL https://github.com/docker/compose/releases/download/v2.12.2/docker-compose-linux-aarch64 -o /usr/local/bin/docker-compose
* sudo chmod +x /usr/local/bin/docker-compose

## Install pip
* sudo apt update
* sudo apt install python3-pip -y
+ (..consider a virtual environment)

## Install icdiff to compare two files
python3 -m pip install icdiff
python3 -m icdiff <file1> <file2>

## Install SQLite
* sudo apt update
* sudo apt install sqlite3
* sqlite3 --version

## Install Syft
* sudo curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sudo sh -s -- -b /usr/local/bin
* syft --version

## Install Grype
* curl -sSfL https://raw.githubusercontent.com/anchore/grype/main/install.sh | sudo sh -s -- -b /usr/local/bin
* grype version

## Install Trivy
* curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sudo sh -s -- -b /usr/local/bin v0.18.3
* trivy --version

## Install Docker via Provisioning:
```
  config.vm.provision "shell", inline: <<-SHELL
    # Update the system
    apt-get update
    apt-get install -y ca-certificates curl gnupg lsb-release

    # Add Docker GPG-Key & Repo
    install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
      gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    chmod a+r /etc/apt/keyrings/docker.gpg

    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
      https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) stable" | \
      tee /etc/apt/sources.list.d/docker.list > /dev/null

    # Install Docker
    apt-get update
    apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    # Add Vagrant-User to the docker-group
    usermod -aG docker vagrant
  SHELL
```
### Provision existing Vagrant machine:  
* vagrant reload --provision
### Docker commands in Vagrant machine:
* Docker build with extended DNS:  
docker build --network=host -t my-image .
* Run a Docker image with limited memory:  
docker run -it --memory 256mb opensuse/leap /bin/bash

### Other docker commands:
* Check privileged statre of the container  
docker ps --quiet --all | xargs docker inspect --format '{{ .Id }}: Privileged={{ .HostConfig.Privileged }}'

### Use Docker content trust:
* git clone https://github.com/theupdateframework/notary.git
* mkdir .docker/trust
* cd notary/
* docker trust key generate udacity_demo --dir ~/.docker/trust
* docker-compose up -d
* docker trust signer add --key ~/.docker/trust/udacity_demo.pub udacity_demo obstmi/udacitysecurity
* export DOCKER_CONTENT_TRUST_SERVER=https://notary.docker.io
* docker trust sign obstmi/udacitysecurity:hardened-v1.0  
(Signing and pushing trust data for local image obstmi/udacitysecurity:hardened-v1.0, may overwrite remote trust data
The push refers to repository [docker.io/obstmi/udacitysecurity])
* export DOCKER_CONTENT_TRUST=1
* opt.: docker push obstmi/udacitysecurity:hardened-v1.0 (already done before)
* test: docker pull obstmi/udacitysecurity:hardened-v1.0
* docker trust inspect --pretty obstmi/udacitysecurity:hardened-v1.0




