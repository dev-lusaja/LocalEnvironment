requirements:
-------------

* vagrant
* docker-tools (docker - machine - compose)

commands:
---------

* download the vagrantbox

~~~
 	$ vagrant box add Centos7 https://github.com/CommanderK5/packer-centos-template/releases/download/0.7.1/vagrant-centos-7.1.box
~~~

* started the virtual machine.

~~~
	$ vagrant up
~~~

* verify ssh conectivity.

~~~
	$ vagrant ssh
	$ ssh vagrant@192.168.33.100 (opcional*)
~~~

* create a docker-machine and install docker engine into virtual machine.

> this is posible using the generic driver from docker-machine.

~~~
	$ docker-machine create -d generic --generic-ssh-user vagrant --generic-ssh-key config/insecure_private_key --generic-ip-address 192.168.33.100 --engine-install-url "https://get.docker.com" LocalEnvironment
~~~

> output example:

~~~
	ll-url "https://get.docker.com" LocalEnvironment
	Running pre-create checks...
	Creating machine...
	(LocalEnvironment) Importing SSH key...
	Waiting for machine to be running, this may take a few minutes...
	Detecting operating system of created instance...
	Waiting for SSH to be available...
	Detecting the provisioner...
	Provisioning with centos...
~~~

* verify that docker-machine exists

~~~
	$ docker-machine ls
~~~

* setting the environment variables for docker-machine.

~~~
	$ eval $(docker-machine env LocalEnvironment)
~~~

* verify that docker engine is installed

~~~
	$ docker info
~~~

* creating a service http container for testing

> this service uses the index.html file into path public/

~~~
	$ docker-compose build
	$ docker-compose up
~~~

* go to the browser

Note: the IP is referential, there you must put the ip that was assigned to your virtual machine.

~~~
	http://192.168.33.100
~~~

NOTE
====

The folder public / is synchronized with the machine set up in vagrant, so any changes you make in it will be reflected in our httpd service.