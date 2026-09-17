# Kubernetes-Zero-to-Hero
# How Devops Teams managing PROD 100 of clusters in kubernates 
Ans: Widely used tools is kops(k8 operations) earlier used kubeadm etc .
As a devops eng we have to deal with k8 instalations,upgrades,Modifications, Deletions of clusters all of these called as a life cycle of k8 . So to manage this life cycle we use kops , same thing can be done by Openshift, Rancher, EKS ,Argo Cd.

Creating this repo with an intent to make Kubernetes easy for begineers. This is a work-in-progress repo.

## Kubernetes Installation Using KOPS on EC2

### Create an EC2 instance or use your personal laptop.

Dependencies required 

1. Python3
2. AWS CLI
3. kubectl

Note: kubectl is needed because it is the command-line tool used to communicate with and manage a Kubernetes cluster.
                Kubernetes Cluster
                       │
                       │ API requests
                       ▼
                    kubectl
                       ▲
                       │
                       │ Commands
                       │
                  You / Admin

###  Install dependencies
aws - Run AWS CLI , sts -AWS Security Token Service, get-caller-identity - Who am I authenticated as?
ubuntu@ip-172-31-16-156:~$ aws sts get-caller-identity 
{
    "UserId": "417394243622",
    "Account": "417394243622",
    "Arn": "arn:aws:iam::417394243622:root"
}


Add the new Kubernetes repository:
```
sudo apt-get update
sudo apt-get install -y ca-certificates curl apt-transport-https

```

```
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

```

```
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

```
sudo apt-get update
sudo apt-get install -y kubectl

```

Install AWS CLI (Ubuntu 24.04 compatible):

```
sudo snap install aws-cli --classic
```
```
export PATH="$PATH:/home/ubuntu/.local/bin/"
```

### Install KOPS (our hero for today)

```
curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

chmod +x kops-linux-amd64

sudo mv kops-linux-amd64 /usr/local/bin/kops
```

### Provide the below permissions to your IAM user. If you are using the admin user, the below permissions are available by default

1. AmazonEC2FullAccess
2. AmazonS3FullAccess
3. IAMFullAccess
4. AmazonVPCFullAccess

### Set up AWS CLI configuration on your EC2 Instance or Laptop.

Run `aws configure`

## Kubernetes Cluster Installation 

Please follow the steps carefully and read each command before executing.

### Create S3 bucket for storing the KOPS objects.

```
aws s3api create-bucket --bucket kops-asitav-storage --region us-east-1
```

### Create the cluster 

```
kops create cluster --name=devk8scluster.k8s.local --state=s3://kops-asitav-storage --zones=us-east-1a --node-count=1 --node-size=t2.micro --master-size=t2.micro  --master-volume-size=8 --node-volume-size=8
```

### Important: Edit the configuration as there are multiple resources created which won't fall into the free tier.

```
kops edit cluster myfirstcluster.k8s.local
```

Step 12: Build the cluster

```
kops update cluster demok8scluster.k8s.local --yes --state=s3://kops-abhi-storage
```

This will take a few minutes to create............

After a few mins, run the below command to verify the cluster installation.

```
kops validate cluster demok8scluster.k8s.local
```

