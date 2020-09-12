Google Cloud Fundamentals: Getting Started with Compute Engine

# Objectives
# In this lab, you will learn how to perform the following tasks:

1.Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

2.Create a Compute Engine virtual machine using the gcloud command-line interface.

3.Connect between the two instances.

# Task 1: Create a virtual machine my-vm-1

# 1.To display a list of all the zones in the region to which Qwiklabs assigned you 
    gcloud compute zones list | grep us-central1

# 2.Choose a zone from that list to which Qwiklabs assigned you
    gcloud config set compute/zone us-central1-a

# 3.To create a VM instance called my-vm-1 in that zone, execute this command:

    gcloud compute instances create "my-vm-1" \
    --machine-type "n1-standard-1" \
    --image-project "debian-cloud" \
    --image "debian-9-stretch-v20190213" \
    --subnet "default"

# Task 2: Create a virtual machine my-vm-2

# 1.To display a list of all the zones in the region to which Qwiklabs assigned you 
    gcloud compute zones list | grep followed by the region your instructor or Qwiklab assigned you.
    gcloud compute zones list | grep us-central1

# 2.Choose another zone from that list to which Qwiklabs assigned you

# 3.To set your default zone to the one you just chose, enter this partial command gcloud config set compute/zone followed by the zone you chose.
    gcloud config set compute/zone us-central1-b

# 3.To create a VM instance called my-vm-2 in that zone, execute this command:

    gcloud compute instances create "my-vm-2" \
    --machine-type "n1-standard-1" \
    --image-project "debian-cloud" \
    --image "debian-9-stretch-v20190213" \
    --subnet "default"

# Task 3: Connect between VM instances
# 1.Verify both instances created;you should be able to see all instances created 
    gcloud compute instances list
# 2.Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
    ping my-vm-1
# 3.Use the ssh command to open a command prompt on my-vm-1:
    ssh my-vm-1
# 4.At the command prompt on my-vm-1, install the Nginx web server:
    sudo apt-get install nginx-light -y

# 5.Use the nano text editor to add a custom message to the home page of the web server:
    sudo nano /var/www/html/index.nginx-debian.html

# 6.Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
# Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.
# Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
     curl http://localhost/
# To exit the command prompt on my-vm-1, execute this command:
      exit
# To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
     curl http://my-vm-1/
# 