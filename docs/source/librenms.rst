.. _installation:

LibreNMS 
+++++++++

Installation Document : Docker
==============================

Prerequisites:
--------------

OS Requirement:
````````````````
To install Docker Engine, you need the 64-bit version of one of these Ubuntu versions: 

 * Ubuntu Kinetic 22.10 

 * Ubuntu Jammy 22.04 (LTS) 

 * Ubuntu Focal 20.04 (LTS) 

 * Ubuntu Bionic 18.04 (LTS) 

Docker Engine is compatible with *x86_64* (or *amd64*), *armhf, arm64,* and *s390x* architectures.

.. figure:: /images/ubuntu.jpg
   :alt: ubuntu
   :align: center
   :scale: 70%



Uninstall old versions 
```````````````````````

Older versions of Docker went by the names of *docker, docker.io,* or *docker-engine*. Uninstall any such older versions before attempting to install a new version: 

   **$ sudo apt-get remove docker docker-engine docker.io containerd runc**

It’s OK if *apt-get* reports that none of these packages are installed. 

Images, containers, volumes, and networks stored in */var/lib/docker/* aren’t automatically removed when you uninstall Docker. 
If you want to start with a clean installation, and prefer to clean up any existing data, refer to the :ref:`Uninstall Docker Engine<uninstall_doc_eng>` section.


Install using the repository
````````````````````````````` 

Before installing Docker Engine for the first time on a new host machine, we need to set up the Docker repository. Afterward, we can install and update Docker from the repository. 


Set up the repository
........................

1. we need to update the apt package index and install packages to allow apt to use a repository over HTTPS: 

 	**$ sudo apt-get update**


 	**$ sudo apt-get install \\**

 	**ca-certificates \\**

 	**curl \\**

 	**gnupg \\**

 	**lsb-release**

2. Add Docker’s official GPG key: 

	**$ sudo mkdir -p /etc/apt/keyrings**

	**$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg**

3. Use the following command to set up the repository: 

	**$ echo \\**

	  **"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \\**

  	  **$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null**



Install Docker Engine
......................

1. Update the apt package index: 

    **$ sudo apt-get update**

.. admonition:: Receiving a GPG error when running *apt-get update?*
   
   If our default umask incorrectly configured, it may be preventrd detection of the repository public key file. 
   We need to try granting read permission for the Docker public key file before updating the package index: 
   
	**$ sudo chmod a+r /etc/apt/keyrings/docker.gpg**
	
	**$ sudo apt-get update**

2. Install Docker Engine, containerd, and Docker Compose. 

	* Latest 
	* Specific version 

   To install the latest version, run: 

	**$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin**


3. Verify that the Docker Engine installation is successful by running the hello-world image: 

	**$ sudo docker run hello-world**

   This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits. 
   You have now successfully installed and started Docker Engine. The docker user group exists but contains no users, which is why you’re required to use sudo to run Docker commands. 
   Continue to Linux post-install to allow non-privileged users to run Docker commands and for other optional configuration steps. 



.. _uninstall_doc_eng:

Uninstall Docker Engine 
========================

Uninstall the Docker Engine, CLI, containerd, and Docker Compose packages: 

 **$ sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin**

Images, containers, volumes, or custom configuration files on your host aren’t automatically removed. To delete all images, containers, and volumes: 

 **$ sudo rm -rf /var/lib/docker**

 **$ sudo rm -rf /var/lib/containerd**

You must delete any edited configuration files manually.  
..

