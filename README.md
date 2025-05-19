
### Deploying Application on EKS cluster using Github Actions CI/CD

Create a instance and add it as a runner, run the following commannds
```cli
sudo apt update

mkdir actions-runner && cd actions-runner

curl -o actions-runner-linux-x64-2.324.0.tar.gz -L
https://github.com/actions/runner/releases/download/v2.324.0/actions-runner-linux-x64-2.324.0.tar.gz

tar xzf ./actions-runner-linux-x64-2.324.0.tar.gz

./config.sh --url https://github.com/riasdi/Github-Actions-Project --token BFZILQI7HPPJAAXLMXF4TYTIFMKMS

./run.sh
```

create instance f or SonarQube and install docker on it

```cli
sudo apt install

sudo apt install docker.io

sudo usermod -aG docker $USER

newgrp docker

docker run -d --name sonar -p 9000:9000 SonarQube:lts-community

```

using SonarQube_ip_address:9000 open the sonaeqube page

Generate token for SonarQube and store it in secrets of GitHub 
sonar_token
sonar_host_url


Lets install Docker on runner
```cli
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo usermod -aG docker ubuntu

newgrp docker

```

store Dockerhub username and password in secrets

lets again create a instance for EKS cluster

Install AWS cli
```cli
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install
```
```cli
aws configure
```

Install Terraform

```cli
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
terraform -version
```

Install kubectl
```cli
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```
clone EKS-Terraform repo

```cli
terraform init
terraform apply --auto-approve
```

```cli
aws eks --region ap-south-1 update-kubeconfig --name name-of -cluster
```

Add .kube/config file content to secrets,
Also add aws_access_key and Secret_key to secrets


```cli
kubecctl get all
```
![Screenshot 2025-05-18 203520](https://github.com/user-attachments/assets/afa2bdc6-2179-42e2-984c-7ef6ff48277d)
![Screenshot 2025-05-18 203447](https://github.com/user-attachments/assets/71e043be-f023-41ac-abf0-f8654a1a4738)


open the external ip_address on new tab
![Screenshot 2025-05-18 203349](https://github.com/user-attachments/assets/0b7d9c79-dfce-48fd-b336-404a8804a8e0)




