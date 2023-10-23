# Configuración de Docker para PrestaShop

Este README proporciona una guía para utilizar Docker y Docker Compose con la imagen de PrestaShop. 

## Requisitos

Asegúrate de tener Docker y Docker Compose instalados en tu sistema. Puedes seguir las instrucciones en [https://docs.docker.com/](https://docs.docker.com/) para la instalación.

## Configuración de Docker Compose

El siguiente archivo `docker-compose.yml` configura PrestaShop junto con una base de datos MySQL. Asegúrate de tener este archivo en un directorio local.

```yaml
version: '3'

services:

   mysql:
      # Asignas un nombre de contenedor específico ("mysql") a este servicio.
      container_name: mysql
      #  Estás utilizando la imagen Docker "mysql:5.7" para este servicio.
      image: mysql:5.7
      # Empiezas a definir las variables de entorno para el servicio MySQL contraseña y base de datos.
      environment:
         MYSQL_ROOT_PASSWORD: admin
         MYSQL_DATABASE: prestashop
      # Comienzas a definir las redes utilizadas en este servicio
      networks:
         - prestashop_network

   prestaShop:
      # Asignas un nombre de contenedor específico ("prestashop1") a este servicio.
      container_name: prestashop1
      #  Estás utilizando la imagen Docker "prestashop/prestashop:latest" para este servicio
      image: prestashop/prestashop:latest
      # Defines
      ports:
         - 8080:80
      # Empiezas a definir las variables de entorno para el servicio prestashop base de datos, nombre de la base de datos, usuario y contraseña.
      environment:
         DB_SERVER: mysql
         DB_NAME: prestashop1
         DB_USER: root
         DB_PASSWD: admin

      # defines una red igual a la anterior para conectar ambas bases de datos
      networks:
         - prestashop_network
```

## Instrucciones

Sigue estos pasos para configurar y ejecutar PrestaShop con Docker:

1. Crea un directorio en tu sistema y coloca el archivo `docker-compose.yml` dentro de él.

2. Abre una terminal y navega al directorio donde se encuentra el archivo `docker-compose.yml`.

3. Ejecuta el siguiente comando para iniciar los servicios:

   ```bash
   docker-compose up -d
   ```

   El argumento `-d` se utiliza para ejecutar los contenedores en segundo plano.


4. Una vez que los contenedores estén en funcionamiento, podrás acceder a PrestaShop a través de tu navegador web en [http://localhost:8080](http://localhost:8080). PrestaShop estará conectado a la base de datos MySQL.


5. Puedes detener los servicios en cualquier momento ejecutando el siguiente comando en el mismo directorio donde se encuentra el archivo `docker-compose.yml`:

   ```bash
   docker-compose down
   ```

## Capturas de Pantalla

A continuación, se incluyen capturas de pantalla para demostrar el funcionamiento:

- **PrestaShop en el navegador:**
- ![imagen](https://github.com/JorgeGonzalez-castelao/1erExamen_Docker/assets/113522749/1b5f4020-abce-46bc-b1bc-fd0ca755110e)


  

## Notas

- Se ha configurado una base de datos MySQL enlazada a PrestaShop a través de Docker Compose.

- PrestaShop estará disponible en el puerto 8080 de tu máquina local.

- Puedes personalizar la configuración de estos servicios según tus necesidades editando el archivo `docker-compose.yml`.

Disfruta de tu entorno de desarrollo de PrestaShop utilizando Docker Compose y una base de datos enlazada. Si tienes alguna pregunta o necesitas ayuda adicional, no dudes en consultar la documentación de Docker o ponerse en contacto con nosotros.
