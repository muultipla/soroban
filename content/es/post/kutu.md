{
   "date": "2020-06-12",
   "title": "Kutu: actualizando el entorno k8s",
   "weight": 10,
   "image": "kutu.png",
   "authors": [ "mcabrerizo" ],
   "branches": [ "tech" ],
   "tags": [ "dev", "golang", "kubernetes", "cli", "utils" ]
}

Aquí en **Muultipla** nos encanta Kubernetes, y nos encantan herramientas como kubectl, minikube, skaffold y kustomize.

Algunos de nosotros usamos Linux y nos gusta descargar la última versión de estas herramientas de la página de releases de sus repositorios de GitHub. 

Esas herramientas cambian con frecuencia así que hemos creado un sencillo binario escrito en Go que comprueba si esas herramientas tienen nuevas versiones disponibles y las actualiza si es necesario. Claro, existen otras formas de hacer esto como utilizar **brew** pero nos gusta desarrollar nuestras propias aplicaciones y funciona muy bien.

Esta herramienta se llama Kutu y puedes visitar nuestro [repositorio en Github](https://github.com/muultipla/kutu) si quieres probar nuestras versiones [pre-release para Linux y Mac](https://github.com/muultipla/kutu/releases). Cualquier comentario es bienvenido.

¡Gracias!
