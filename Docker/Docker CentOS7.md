Docker CentOS7
=======
###Prerequisites###
Docker requires a 64-bit OS and version 3.10 or higher of the Linux kernel.

Check the current kernel version to your terminal

`$ uname -r`

Result something like this

`3.10.0-327.36.3.el7.x86_64`

--

###Install with yum###

1. Log into your machine as a user with sudo or root privileges.

2. Update the yum packages

	`sudo yum update`

3. Add yum repo

	```
sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
[dockerrepo]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/centos/7/
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
EOF
```

4. Install the Docker package

	`sudo yum install docker-engine`
	
5. Enable the service

	`sudo systemctl enable docker.service`

6. Start the Docker daemon

	`sudo systemctl start docker`

7. Verify docker is installed correctly by running a test image in a container
	```
sudo docker run --rm hello-world

 Unable to find image 'hello-world:latest' locally
 latest: Pulling from library/hello-world
 c04b14da8d14: Pull complete
 Digest: sha256:0256e8a36e2070f7bf2d0b0763dbabdd67798512411de4cdcf9431a1feb60fd9
 Status: Downloaded newer image for hello-world:latest

 Hello from Docker!
 This message shows that your installation appears to be working correctly.

 To generate this message, Docker took the following steps:
  1. The Docker client contacted the Docker daemon.
  2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
  3. The Docker daemon created a new container from that image which runs the
     executable that produces the output you are currently reading.
  4. The Docker daemon streamed that output to the Docker client, which sent it
     to your terminal.

 To try something more ambitious, you can run an Ubuntu container with:
  $ docker run -it ubuntu bash

 Share images, automate workflows, and more with a free Docker Hub account:
  https://hub.docker.com

 For more examples and ideas, visit:
  https://docs.docker.com/engine/userguide/  
```

8. Start the docker daemon at boot

	`sudo systemctl enable docker`
	
--

###Uninstall###


You can uninstall the Docker software with `yum`.

1. List the installed Docker packages
	
	`$ yum list installed | grep docker`
	
	result: 
	
	`docker-engine.x86_64     1.7.1-0.1.el7@/docker-engine-1.7.1-0.1.el7.x86_64`

2. Remove the package

	`sudo yum -y remove docker-engine.x86_64`
	
	This command does not remove images, containers, volumes, or user-created configuration files on your host.
	
3. To delete all images, containers, and volumes, run the following command

	`rm -rf /var/lib/docker`
	
4. Locate and delete any user-created configuration files

5. If you want to run docker without `sudo`

	`sudo chown <username>:docker /var/run/docker.sock`
