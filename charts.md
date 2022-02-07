## Charts
Como hemos comentado anteriormente, los charts los podemos buscar accediendo a la página [ArtifactHub](https://artifacthub.io/) indicando el nombre de la aplicación en el buscador, incluso podemos especificar si queremos que solo nos busque aplicaciones que estén unicamente en un cierto repositorio.
![ArticactHub-chart-WordPress](https://github.com/Mbonillac/Helm/blob/main/img/busqueda-charts.png?raw=true) 

También los podemos buscar desde la línea de comandos, por ejemplo si queremos buscar un chart relacionado con wordpress:

~~~
usuario@debian-203:~$ helm search repo wordpress

NAME                   	CHART VERSION	APP VERSION	DESCRIPTION                                       

bitnami/wordpress      	13.0.9       	5.9.0      	WordPress is the world's most popular blogging ...

bitnami/wordpress-intel	0.1.0        	5.8.3      	WordPress for Intel is the most popular bloggin...

stable/wordpress       	9.0.3        	5.3.2      	DEPRECATED Web publishing platform for building...
~~~
