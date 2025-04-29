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