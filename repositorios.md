## Repositorios

Una vez que tengamos instalado Helm, lo siguiente es indicar un repositorio para que podamos empezar a trabajar; para ello a traves del propio comando helm.

### Añadir
La sintaxis sería:
helm repo add "nombre_que_le_damos" "URL_del_repositorio" --force-update
~~~
usuario@debian-203:~$ helm repo add "stable" "https://charts.helm.sh/stable" --force-update
~~~
Es recomendable tener más de un repositorio instalado, así que  vamos a instalar el repositorio de bitnami por ejemplo.

~~~
usuario@debian-203:~$ helm repo add bitnami https://charts.bitnami.com/bitnami

"bitnami" has been added to your repositories


~~~

### Comprobar
Una vez que hemos añadido los repositorios a Helm, podemos comprobarlos con un comando que nos muestra una lista con todos los repositorios que tenemos añadidos.

~~~
usuario@debian-203:~$ helm repo list
NAME   	URL                               
stable 	https://charts.helm.sh/stable     
bitnami	https://charts.bitnami.com/bitnami


~~~

### Actualizar los repositoriso
Para actualizar la lista de charts ofrecidos por los repositorios.

~~~
usuario@debian-203:~$ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "stable" chart repository
...Successfully got an update from the "bitnami" chart repository
Update Complete. ⎈Happy Helming!⎈
~~~

### Eliminar
Para eliminar un repositorio.
~~~
usuario@debian-203:~$ helm repo remove stable
"stable" has been removed from your repositories
~~~