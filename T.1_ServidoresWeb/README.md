# Web Application Deployment Scripts

**Course 24/25 by Yeray Padial Boorrero**

Este repositorio contiene scripts útiles para la configuración de servidores web y el despliegue de aplicaciones en sistemas Linux. A continuación, explico cada script, cómo funciona y cómo utilizarlo.

---

## Índice

1. [Añadir Puerto de Escucha en Apache](#1-añadir-puerto-de-escucha-en-apache)
2. [Añadir Dominio e IP al Archivo Hosts](#2-añadir-dominio-e-ip-al-archivo-hosts)
3. [Crear Página Web Simple](#3-crear-página-web-simple)

---

### 1. Añadir Puerto de Escucha en Apache

Este script permite añadir un puerto de escucha al archivo de configuración de Apache. Recibe el número de puerto como argumento, verifica si el puerto ya está configurado en el archivo `/etc/apache2/ports.conf` y lo añade solo si no existe.

```bash
#!/bin/bash
# Verifica que se proporcione el puerto como argumento
if [ -z "$1" ]; then
    echo "Por favor, proporciona el puerto a añadir como argumento."
    exit 1
fi
PORT=$1
CONFIG_FILE="/etc/apache2/ports.conf"
# Comprueba si el puerto ya está en el archivo de configuración
if grep -q "Listen $PORT" "$CONFIG_FILE"; then
    echo "El puerto $PORT ya está configurado en $CONFIG_FILE."
else
    # Añade el puerto al archivo de configuración
    echo "Listen $PORT" | sudo tee -a "$CONFIG_FILE"
    echo "El puerto $PORT ha sido añadido a $CONFIG_FILE."
fi

Para usar este script, simplemente ejecutar:
./añadir_puerto.sh <PUERTO>


2. Añadir Dominio e IP al Archivo Hosts
Este script toma una IP y un nombre de dominio como argumentos y añade la entrada al archivo /etc/hosts solo si el dominio no existe ya en el archivo.
#!/bin/bash
# Verifica que se proporcionen la IP y el dominio
if [ -z "$1" ] || [ -z "$2" ]; then
    echo "Uso: $0 <IP> <DOMINIO>"
    exit 1
fi
IP=$1
DOMAIN=$2
HOSTS_FILE="/etc/hosts"
# Verifica si el dominio ya existe en el archivo hosts
if grep -q "$DOMAIN" "$HOSTS_FILE"; then
    echo "El dominio $DOMAIN ya existe en $HOSTS_FILE."
else
    # Añade la entrada al archivo hosts
    echo "$IP $DOMAIN" | sudo tee -a "$HOSTS_FILE"
    echo "La entrada $IP $DOMAIN ha sido añadida a $HOSTS_FILE."
fi

Para usar este script, simplemente ejecutar:
./añadir_host.sh <IP> <DOMINIO>


3. Crear Página Web Simple
Este script genera un archivo HTML básico con un título, una cabecera y un mensaje predeterminados. Es ideal para crear una página web estática de forma rápida.

#!/bin/bash
# Definimos el título, cabecera y mensaje
TITLE="Mi Página Web"
HEADER="Bienvenido a mi sitio"
MESSAGE="¡Esta es mi página web generada en Linux!"
# Nombre del archivo HTML a crear
HTML_FILE="index.html"
# Crear el archivo HTML
cat <<EOL > $HTML_FILE
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>$TITLE</title>
</head>
<body>
    <h1>$HEADER</h1>
    <p>$MESSAGE</p>
</body>
</html>
echo "Página web creada en $HTML_FILE."

Para usar este script, simplemente ejecutar:
./crear_pagina_web.sh
