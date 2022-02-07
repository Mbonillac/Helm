## Instalación de chart - WordPress

Para instalar el chart de WordPress ejecutamos la siguiente instrucción, en la que además estaremos asignandole un nombre interno y parametrizando:
 - Tipo de servicio.
 - Nombre del blog.
 - Nombre del usuario.
 - Contraseña de usuario.

~~~
usuario@debian-203:~$  helm install miwordpress bitnami/wordpress --set service.type=NodePort --set wordpressBlogName="Blog de Manuel" --set wordpressUsername="manuel" --set wordpressPassword="manuel"
NAME: miwordpress
LAST DEPLOYED: Mon Feb  7 18:14:24 2022
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: wordpress
CHART VERSION: 13.0.9
APP VERSION: 5.9.0

** Please be patient while the chart is being deployed **

Your WordPress site can be accessed through the following DNS name from within your cluster:

    miwordpress.default.svc.cluster.local (port 80)

To access your WordPress site from outside the cluster follow the steps below:

1. Get the WordPress URL by running these commands:

   export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services miwordpress)
   export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
   echo "WordPress URL: http://$NODE_IP:$NODE_PORT/"
   echo "WordPress Admin URL: http://$NODE_IP:$NODE_PORT/admin"

2. Open a browser and access WordPress using the obtained URL.

3. Login with the following credentials below to see your blog:

  echo Username: manuel
  echo Password: $(kubectl get secret --namespace default miwordpress -o jsonpath="{.data.wordpress-password}" | base64 --decode)
~~~
Para poder obtener la información de cualquier chart desplegado tendremos que utilizar el siguiente comando:

~~~
usuario@debian-203:~$ helm status miwordpress
~~~

Si queremos acceder a la aplicación desde el exterior debemos ejecutar las instrucciones:
- minikube ip:  que nos muestran la ip de nuestro cluster.
- kubectl get all:  para ver el puerto asignado al Service NodePort.

Trás obtener los datos necesarios los introduciremos en el navegador y accederemos a wordpress.

![acceso-WordPress](https://github.com/Mbonillac/Helm/blob/main/img/wordpress.png?raw=true)


Como hemos indicado, a través de parámetros, el usuario administrador y su contraseña podemos entrar en la zona de administración de WordPress y editarlo a nuestro gusto, por ejemplo creando una entrada nueva.

![nueva_entrada_WordPress](https://github.com/Mbonillac/Helm/blob/main/img/nueva_entrada_wordpress.png?raw=true)


Para poder listar los deployments que hemos realizado con Helm utilizaremos:
~~~
usuario@debian-203:~$ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
miwordpress     default         1               2022-02-07 18:14:24.7697074 +0100 CET   deployed        wordpress-13.0.9        5.9.0 
~~~