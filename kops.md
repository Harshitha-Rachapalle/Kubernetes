**Kubernetes Installation Using KOPS on EC2**

**Create an EC2 instance or use your personal laptop.**

Dependencies required

1.Python3

2.AWS CLI

3.kubectl

**Install dependencies**

**#kubectl**

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list

**#python3**

sudo apt-get update

sudo apt-get install -y python3-pip apt-transport-https kubectl

**#awscli**

pip3 install awscli --upgrade

export PATH="$PATH:/home/ubuntu/.local/bin/"

**Installing KOPS**

curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

chmod +x kops-linux-amd64

sudo mv kops-linux-amd64 /usr/local/bin/kops

**Provide the below permissions to your IAM user. If you are using the admin user, the below permissions are available by default**

1.AmazonEC2FullAccess

2.AmazonS3FullAccess

3.IAMFullAccess

4.AmazonVPCFullAccess

**Set up AWS CLI configuration on your EC2 Instance or Laptop.**

Run aws configure (here provide access key and secret access key)

**Kubernetes Cluster Installation**

**Create S3 bucket for storing the KOPS objects.**

aws s3api create-bucket --bucket kops-harshi-storage --region us-east-1

**Create the cluster**

kops create cluster --name=demok8scluster.k8s.local --state=s3://kops-harshi-storage --zones=us-east-1a --node-count=1 --node-size=t2.micro --master-size=t2.micro  --master-volume-size=8 --node-volume-size=8

in organizations we'll not use k8s.local instead we use amazon.com, google.com i.e **domain name.com** for production

aws route53 create-hosted-zone --name dev.example.com --caller-reference 1

**To edit cluster**

kops edit cluster demok8scluster.k8s.local

**To validate cluster**(to verify cluster is installed or not)

kops validate cluster demok8scluster.k8s.local
