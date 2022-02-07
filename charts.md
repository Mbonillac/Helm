## Charts
Como hemos comentado anteriormente, los charts los podemos buscar accediendo a la página [ArtifactHub](https://artifacthub.io/) indicando el nombre de la aplicación en el buscador, incluso podemos especificar que solo nos busque aplicaciones que estén unicamente en un cierto repositorio.

![ArticactHub-chart-WordPress](https://github.com/Mbonillac/Helm/blob/main/img/busqueda-charts.png?raw=true) 

También los podemos buscar desde la línea de comandos, por ejemplo si queremos buscar un chart relacionado con wordpress:

~~~
usuario@debian-203:~$ helm search repo wordpress

NAME                   	CHART VERSION	APP VERSION	DESCRIPTION                                       

bitnami/wordpress      	13.0.9       	5.9.0      	WordPress is the world's most popular blogging ...

bitnami/wordpress-intel	0.1.0        	5.8.3      	WordPress for Intel is the most popular bloggin...

stable/wordpress       	9.0.3        	5.3.2      	DEPRECATED Web publishing platform for building...
~~~

Si nos fijamos en la descripción web, es idéntica a la que nos muetra la linea de comandos.

### Parámetros

Todos los ficheros yaml que forman parte de un chart están parametrizados, es decir cada propiedad tiene un valor por defecto, pero a la hora de instalarlo se puede cambiar. Por ejemplo, ¿qué tipo de Service se creará al instalar el chart bitnami/wordpress? 

Por defecto, el parámetro service.type tiene como valor LoadBalancer, pero si queremos un Service de tipo NodePort, podremos redefinir este parámetro a la hora de instalar el chart.


¿Y cómo sabemos los parámetros que tiene definido cada chart y sus valores por defecto?. 

Estudiando la documentación del chart en [ArtifactHub](https://artifacthub.io/). En concreto para el chart con el que estamos trabajando, accediendo a la url https://artifacthub.io/packages/helm/bitnami/wordpress. Bajando un poco en la web podemos encontrar la lista de parametros.

![ArticactHub-chart-WordPress](https://github.com/Mbonillac/Helm/blob/main/img/parametros-wordpress.png?raw=true)

En al terminal también podemos obtener esta información ejecutando el siguiente comando:
~~~
usuario@debian-203:~$ helm show all bitnami/wordpress
~~~

Hay que tener en cuenta que al ejecutar este comando nos aparecerá una gran cantidad de datos en varias páginas. Por lo que es aconsejable usar tuberías para encontrar más rápido lo que buscamos. Por ejemplo con el servicio `LoadBalancer` antes mencionado.

~~~
usuario@debian-203:~$ helm show all bitnami/wordpress | grep "service.type"
  ## @param service.type WordPress service type
| `service.type`                     | WordPress service type                     | `LoadBalancer`           |
~~~

En el siguiente apartado procederemos a [instalar WordPress](wordpress.md).