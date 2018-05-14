# Mis apuntes sobre Docker

## Sources
* [Enough Docker to be Dangerous - A Minimal Tutorial](http://seankross.com/2017/09/17/Enough-Docker-to-be-Dangerous.html)
* [Instalación en Windows 10](https://docs.docker.com/docker-for-windows/install/)

##Notas

Imágenes:: una imágen es como una plantilla, es parecido a una snapshot de una máquina virtual, pero más ligero. Puede contener por ejemplo, un Ubuntu con Apache... Hay muchas imágenes públicas con elementos básicos: Java, Ubuntu, ... que se pueden descargar y usar. Se identifican con un ID y un par nombre-version.

Contenedores: son instancias en ejecución de una imágen.

Podemos "traernos" una imagen, por ejemplo de Ubuntu con:

```
docker pull ubuntu:14.04
```

Podemos ver todas las imágenes que nos hemos traido y que por tanto tenemos disponibles:

```
docker images
```

Una vez descargada una imágen, podemos iniciar un primer contenedor:

```
docker run -it ubuntu:14.04
```

Para ver los contenedores que están corriendo actualmente en nuestra máquina, ejecutamos desde otra terminal:

```
docker ps
```

Si añadimos ```docker ps -a``` con la etiqueta -a nos mostrará todos los contenedores, incluidos los que no están corriendo.

Con exit salimos y para reiniciar: 
```
docker start -ai 4321591dd568f #el ID del contenedor, obtenemos del docker ps
```








