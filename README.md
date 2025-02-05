# Kubernetes

#**Install minikube in WSL**

**Step 1: Create the minikube directory**

In your WSL environment, use the following command to create the directory on your Windows filesystem:

mkdir -p /mnt/c/minikube

**Step 2: Download Minikube executable**

Use wget to download the latest Minikube binary from GitHub:

wget https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64 -O /mnt/c/minikube/minikube

**Step 3: Make Minikube executable**

Now, you need to make the minikube binary executable:

chmod +x /mnt/c/minikube/minikube

**Step 4: Verify the installation**

Now, check if Minikube is installed and working:

/mnt/c/minikube/minikube version



