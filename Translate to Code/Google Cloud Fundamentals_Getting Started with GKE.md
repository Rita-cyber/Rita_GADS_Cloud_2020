Google Cloud Fundamentals: Getting Started with GKE

# Objectives
# In this lab, you learn how to perform the following tasks:

1.Provision a Kubernetes cluster using Kubernetes Engine.

2.Deploy and manage Docker containers using kubectl.

# Task 1: Confirm that needed APIs are enabled
      gcloud services enable container.googleapis.com 
      gcloud services enable containerregistry.googleapis.com

# Task 2: Start a Kubernetes Engine cluster

# 1.For convenience, place the zone into an environment variable called MY_ZONE.
# followed by the zone that Qwiklabs assigned to you. 
      export MY_ZONE=us-central1-a

# 2.Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
     gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

# 3.After the cluster is created, check your installed version of Kubernetes
      kubectl version

# 4.View your running nodes
      kubectl get pods

# Task 3: Run and deploy a container

# 1.launch a single instance of the nginx container. (Nginx is a popular web server.)
      kubectl create deploy nginx --image=nginx:1.17.10

# 2.View the pod running the nginx container:
      kubectl get pods

# 3.Expose the nginx container to the Internet:
      kubectl expose deployment nginx --port 80 --type LoadBalancer

# 4.View the new service:
      kubectl get services

# 5.Open a new web browser tab and paste your cluster's external IP address into the address bar. 
# The default home page of the Nginx browser is displayed.

# 6.Scale up the number of pods running on your service:
       kubectl scale deployment nginx --replicas 3

# 7.Confirm that Kubernetes has updated the number of pods:
       kubectl get pods

# 8.Confirm that your external IP address has not changed:
       kubectl get services

# 9.Return to the web browser tab in which you viewed your cluster's external IP address. 
# Refresh the page to confirm that the nginx web server is still responding.
