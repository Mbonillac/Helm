#  Instalación de WordPress

## Instalación parametrizada

Para instalar el chart de WordPress ejecutamos la siguiente instrucción, en la que además estaremos asignándole un nombre interno y parametrizando:
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


## Obtener Información

Para poder obtener la información de cualquier chart desplegado tendremos que utilizar el siguiente comando:

~~~
usuario@debian-203:~$ helm status miwordpress
~~~


## Acceso a la aplicación

Si queremos acceder a la aplicación desde el exterior debemos ejecutar los comandos:
- minikube ip:  para obtener la ip de nuestro cluster.
- kubectl get all:  para obtener el puerto asignado al Service NodePort.

Trás obtener los datos necesarios los introduciremos en el navegador y accederemos a wordpress.

![acceso-WordPress](https://github.com/Mbonillac/Helm/blob/main/img/wordpress.png?raw=true)


Como hemos indicado, a través de parámetros, el usuario administrador y su contraseña podemos entrar en la zona de administración de WordPress y editarlo a nuestro gusto, por ejemplo creando una entrada nueva.

![nueva_entrada_WordPress](https://github.com/Mbonillac/Helm/blob/main/img/nueva_entrada_wordpress.png?raw=true)  

## Listar deployments y elementos
Para poder listar los deployments que hemos desplegado con Helm utilizaremos:
~~~
usuario@debian-203:~$ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
miwordpress     default         1               2022-02-07 18:14:24.7697074 +0100 CET   deployed        wordpress-13.0.9        5.9.0 
~~~

Y para listar todos los elementos creados y desplegados usaremos el comando:
~~~
usuario@debian-203:~$ kubectl get all,cm,secret,pv,pvc
NAME                               READY   STATUS    RESTARTS   AGE
pod/miwordpress-566d76d684-nqkr4   0/1     Running   0          25s
pod/miwordpress-mariadb-0          0/1     Running   0          25s

NAME                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
service/kubernetes            ClusterIP   10.96.0.1       <none>        443/TCP                      52d
service/miwordpress           NodePort    10.109.90.172   <none>        80:30624/TCP,443:31593/TCP   25s
service/miwordpress-mariadb   ClusterIP   10.111.52.129   <none>        3306/TCP                     25s

NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/miwordpress   0/1     1            0           25s

NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/miwordpress-566d76d684   1         1         0       25s

NAME                                   READY   AGE
statefulset.apps/miwordpress-mariadb   0/1     25s

NAME                            DATA   AGE
configmap/kube-root-ca.crt      1      52d
configmap/miwordpress-mariadb   1      25s

NAME                                       TYPE                                  DATA   AGE
secret/default-token-6m5x4                 kubernetes.io/service-account-token   3      52d
secret/miwordpress                         Opaque                                1      25s
secret/miwordpress-mariadb                 Opaque                                2      25s
secret/miwordpress-mariadb-token-jdcx2     kubernetes.io/service-account-token   3      25s
secret/sh.helm.release.v1.miwordpress.v1   helm.sh/release.v1                    1      25s

NAME                                                        CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                                STORAGECLASS   REASON   AGE
persistentvolume/pvc-22b83b6a-7838-4024-a571-8b57ebb213a7   10Gi       RWO            Delete           Bound    default/miwordpress                  standard                25s
persistentvolume/pvc-b4886e89-c6c5-40ab-8f51-9e6fea8ee55e   8Gi        RWO            Delete           Bound    default/data-miwordpress-mariadb-0   standard                25s

NAME                                               STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/data-miwordpress-mariadb-0   Bound    pvc-b4886e89-c6c5-40ab-8f51-9e6fea8ee55e   8Gi        RWO            standard       25s
persistentvolumeclaim/miwordpress                  Bound    pvc-22b83b6a-7838-4024-a571-8b57ebb213a7   10Gi       RWO            standard       25s
~~~
## Desinstalar aplicaciones

Para poder desinstalar una aplicación :
~~~
usuario@debian-203:~$ helm delete miwordpress
release "miwordpress" uninstalled
~~~
Hay que tener en cuenta que, si estamos trabajando con minikube, al eleminar una aplicación es probable que el PVC no sea eliminado y tengamos que hacerlo me manera manual.
~~~
usuario@debian-203:~$ kubectl delete persistentvolumeclaim/data-miwordpress-mariadb-0
persistentvolumeclaim "data-miwordpress-mariadb-0" deleted
~~~