comandos:
---------

* vagrant plugin install vagrant-vbguest (opcional)

* Inicializar la maquina virtual.

~~~
	$ vagrant up
~~~

* Comprovar conexión SSH.

~~~
	$ vagrant ssh
	$ ssh vagrant@192.168.33.100 (opcional*)
~~~

* Instalaremos docker en la maquina virtual creada con vagrant y crearemos un enlace entre nuestro host y la maquina virtual, esto permitira ejecutar comandos de docker desde nuestro host.

> Para esto utilizaremos el driver generico de la herramienta docker-machine.

~~~
	$ docker-machine create -d generic --generic-ssh-user vagrant --generic-ssh-key config/insecure_private_key --generic-ip-address 192.168.33.100 --engine-install-url "https://get.docker.com" LocalEnvironment
~~~

> Ejemplo de mensaje de salida:

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

* Verificamos que se creo la docker-machine

~~~
	$ docker-machine ls
~~~

* Configuramos las variables de entorno para conectarnos a la docker-machine creada.

~~~
	$ eval $(docker-machine env LocalEnvironment)
~~~

* Verificamos si docker esta instalado en la maquina virtual

~~~
	$ docker info
~~~

* Para fines practicos, se tiene un archivo de tareas (docker-compose.yml)

> Con esto crearemos un contenedor que servira un servicio httpd, donde mostraremos el archivo index.html ubicado en nuestra carpeta " public/ "

~~~
	$ docker-compose build
	$ docker-compose up
~~~

* probamos en el browser

~~~
	192.168.33.100:8080
~~~

NOTA
====
La carpeta public/ esta sincronizada con la maqiuna creada en vagrant, por lo cual todos los cambios que hagamos dentro de ella se veran reflejados en nuestro servicio httpd.