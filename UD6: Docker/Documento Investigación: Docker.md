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
