![Logo-helm](https://github.com/Mbonillac/Helm/blob/main/img/helm-logo.jpg?raw=true)
![Logo-artifacthub](https://github.com/Mbonillac/Helm/blob/main/img/artifacthub-logo.jpg?raw=true)
# Definición Helm y charts

## ¿Qué es Helm?
  
 Una aplicación real completa se compone de un conjunto amplio de objetos que definen Deployments, ConfigMaps, Services, etc. La API de Kubernetes no nos ofrece un "superobjeto" que defina una aplicación completa.
Necesitamos herramientas para gestionar la aplicación completa: empaquetado, instaladores, control de la aplicación en producción, etc.

En este repositorio vamos a conocer **Helm**, que es un software que nos permite empaquetar aplicaciones completas y gestionar el ciclo completo de despliegue de dicha aplicación.


## ¿Qué son los charts?

**Helm** usa un formato de empaquetado llamado charts. Un chart es una colección de archivos que describen un conjunto de recursos que nos permite desplegar una aplicación en Kubernetes.
Los charts son distribuidos en distintos repositorios, que podremos dar de alta en nuestra instalación de Helm. Para buscar los distintos charts y los repositorios desde los que se distribuyen podemos usar la página [ArtifactHub](https://artifacthub.io/).


