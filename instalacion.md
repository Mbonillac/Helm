## Instalación

Esta guía muestra cómo instalar HelmCLI. Helm se puede instalar desde la fuente o desde versiones binarias preconstruidas.

Cada lanzamiento de Helm proporciona binarios de lanzamiento para una variedad de sistemas operativos. Estas versiones binarias se pueden descargar e instalar manualmente.

1. [Aquí](https://github.com/helm/helm/releases) podemos descargar la versión más adecuada para nuestro sistema.

2. Desempaquetar con tar el paquete descargado.
~~~
tar -zxvf helm-v3.8.0-linux-amd64.tar.gz 
~~~

3. Mueve el directorio desempaquetado a /usr/local/bin/helm.
~~~
mv linux-amd64/helm /usr/local/bin/helm
~~~

Para conocer otras maneras de instalar Helm, consultar su [web oficial](https://helm.sh/es/docs/intro/install/).

Una vez instalado podemos ver la versión de Helm que tenemos instalada:
~~~
usuario@debian-203:~$ helm version

version.BuildInfo{Version:"v3.8.0", GitCommit:"d14138609b01886f544b2025f5000351c9eb092e", GitTreeState:"clean", GoVersion:"go1.17.5"}

~~~
