Hicimos un trabajo en grupo sobre Docker donde investigamos qué es, para qué se usa, cómo instalarlo en Ubuntu y los comandos más comunes. También tuvimos que encontrar un contenedor, instalarlo y ejecutarlo, y decidimos usar Wordpress para hacerlo.

# ¿Cómo instalar Ubuntu?
## Es importante asegurarse de que los paquetes estén actualizados.
 
_sudo apt-get update_

_sudo apt-get install ca-certificates curl_

## Añadir la Clave GPG Oficial de Docker para garantizar la autenticidad de sus paquetes.
 
_sudo install -m 0755 -d /etc/apt/keyrings_

_sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc_

_sudo chmod a+r /etc/apt/keyrings/docker.asc_

## Agregar el Repositorio de Docker a las Fuentes de Apt
 
_echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \_

sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

## Una vez configurado el repositorio, instala Docker y sus componentes relacionados.

_sudo apt-get update_

_sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin_

## Verificar la Instalación

_sudo docker run hello-world_

# ¿Cómo instalar WordPress con Docker?
## Crear un archivo docker-compose.yml con el puerto 8081:80 en Wordpress.
## Asegurar que WordPress se conecte con la BBDD

_docker exec -it wordpress_db mysql -uwordpress -p -h127.0.0.1_

## Debemos revisar los permisos en /var/www/html

_docker exec -it wordpress_app bash_

_chown -R www-data:www-data /var/www/html_

_chmod -R 755 /var/www/html_

_exit_

Y posteriormente, reiniciar los contenedores.

_docker-compose restart_

## Configurar ServerName en Apache para evitar advertencias y garantizar una conexión estable

_docker exec -it wordpress_app bash_

_echo "ServerName localhost" >> /etc/apache2/apache2.conf_

_exit_

Debemos reiniciar el servicio de Apache.

## Añadir el puerto que utiliza la BBDD en docker-compose.yml

## Iniciar los Contenedores

Hay que ejecutar el siguiente comando para comprobar el estado de los contenedores:

_sudo docker ps_

Luego debemos detener los contenedores y posteriormente, descargar las imágenes necesarias y volverlos a levantar:

_docker-compose down_

_docker-compose up -d_

## Hay que conectarse desde el contenedor de WordPress y probar si se puede acceder a MySQL.

Habrá que ingresar la contraseña que hemos escogido en **docker-compose.yml** y luego podremos acceder desde el navegador.
