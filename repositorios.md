## Repositorios

Una vez que tengamos instalado Helm, lo siguiente es indicar un repositorio para que podamos empezar a trabajar; para ello a traves del propio comando helm.

### Añadir
La sintaxis sería:
helm repo add "nombre_que_le_damos" "URL_del_repositorio" --force-update
~~~
usuario@debian-203:~$ helm repo add "stable" "https://charts.helm.sh/stable" --force-update
~~~

### Comprobar
Una vez que hemos añadido el repositorio a Helm, podemos comprobarlo con un comando que nos muestra una lsita con todos los repositorios que tenemos añadidos.

~~~
usuario@debian-203:~$ helm repo list
NAME   	URL                               
stable 	https://charts.helm.sh/stable
~~~

### Eliminar
Para eliminar un repositorio.
~~~
usuario@debian-203:~$ helm repo remove stable
"stable" has been removed from your repositories
~~~