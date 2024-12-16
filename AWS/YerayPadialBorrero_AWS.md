# 1. Configuración necesaria de AWS

## Enciendo el laboratorio de AWS
<img src="imagenes/Im1.png" alt="Texto Alternativo">


1. Una vez listo vemos la pantalla principal
<img src="imagenes/Im2.png" alt="Texto Alternativo">

2. Entramos en instancias 
<img src="imagenes/Im3.png" alt="Texto Alternativo">

3. Lanzamos una nueva instancia
<img src="imagenes/Im4.png" alt="Texto Alternativo">
Aplicamos una configuración segun nuestras necesidades, en mi caso la siguiente:
<img src="imagenes/Im5.png" alt="Texto Alternativo">
<img src="imagenes/Im6.png" alt="Texto Alternativo">
<img src="imagenes/Im7.png" alt="Texto Alternativo">

El resultado sería el siguiente:
<img src="imagenes/Im8.png" alt="Texto Alternativo">

4. Ahora nos conectamos a la instancia desde SSH. Tal que así: 
<img src="imagenes/Im9.png" alt="Texto Alternativo">
Antes de seguir, es necesario, descargarnos nuestro .pem que se instala. Para ello le damos a "Download Key Pair" y se descargará.

Ahora entramos en el directorio donde esté el .pem y ponemos lo siguiente:
<img src="imagenes/Im10.png" alt="Texto Alternativo">
Y ya estamos conectados a la maquina virtual de AWS.

# 2. Activar la autenticación con MySql
1. Primero de todo actualizamos los paquetes con 
```bash
sudo apt update
```

2. Instalamos apache
   <img src="imagenes/Im11.png" alt="Texto Alternativo">

3. Inicia y habilita el servicio Apache:
  <img src="imagenes/Im12.png" alt="Texto Alternativo">

4.  Activar la autenticación con MySQL
    Instala mysql:
    <img src="imagenes/Im13.png" alt="Texto Alternativo">

    Ejecutamos el script de seguridad:
   <img src="imagenes/Im14.png" alt="Texto Alternativo">
   
5. Crea un usuario y una base de datos para la autenticación:
<img src="imagenes/Im15.png" alt="Texto Alternativo">

6. Configura la autenticación en Apache:

Instala el módulo de autenticación para MySQL:

<img src="imagenes/Im16.png" alt="Texto Alternativo">

Habilita los módulos de Apache necesarios y reinicia apache:
<img src="imagenes/Im17.png" alt="Texto Alternativo">

Entra al archivo de configuracion de apache:
```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```
Agrega las siguientes directivas para configurar la autenticación:

<img src="imagenes/Im18.png" alt="Texto Alternativo">

7. Crear la base de datos y la tabla de usuarios
<img src="imagenes/Im19.png" alt="Texto Alternativo">

Inserta un usuario. he utilizado bscrypt para encriptar la contraseña
<img src="imagenes/Im20.png" alt="Texto Alternativo">

Y reiniciamos Apache.

# Crear un certificado autofirmado y activar el módulo SSL

1.  Instalar OpenSSL y habilitar el módulo SSL

  ```bash
sudo apt install openssl -y

  ```

  ```bash
sudo a2enmod ssl
  ```

2. Generar un certificado autofirmado. <br>
Creamos un directorio para almacenar el certificado y la clave privada y generamos el certificado y la clave privada:
<img src="imagenes/Im21.png" alt="Texto Alternativo">

Esto generará dos archivos:
/etc/ssl/certificados/servidor.key (clave privada).
/etc/ssl/certificados/servidor.crt (certificado).

3. Configurar Apache para usar el certificado SSL
Habilitar el archivo de configuración para SSL:
<img src="imagenes/Im22.png" alt="Texto Alternativo">

Edita el archivo de configuración del sitio SSL:
<img src="imagenes/Im23.png" alt="Texto Alternativo">
Cerramos apache y es necesarios guardar para terminar.
 




