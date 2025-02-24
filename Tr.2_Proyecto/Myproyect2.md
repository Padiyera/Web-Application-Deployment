# Configuración de Servidor Web Apache en EC2 con EFS y RDS  

## Introducción  

Este manual tiene como objetivo configurar un servidor web Apache en una instancia EC2 con Debian o Ubuntu. La infraestructura incluirá:  

- **Almacenamiento**: Sistema de archivos en **EFS**.  
- **Base de datos**: Gestionada por **RDS** en una subred privada.  
- **Red**: Un **VPC** con dos subredes públicas y dos privadas.  

## Estructura de la Red  

Para la implementación, configuraremos:  

1. **VPC** con cuatro subredes:  
   - **Dos públicas**: Permitirán la creación de un balanceador de carga para distribuir el tráfico según la carga de los servidores.  
   - **Dos privadas**: Alojarán la base de datos en **RDS** y otros recursos internos.  

2. **Balanceador de Carga**: Mejorará la distribución de tráfico y la disponibilidad del servicio.  

## Creación de las Subredes  

Para crear dos subredes públicas y dos privadas, primero de todo en servicios, nos dirigimos a VPC.
Aqui creamos una VPC con estas subredes.

<img src="Images/a1.png" alt="Texto Alternativo">

Una vez clickado accedemos a VPC
<img src="Images/a2.png" alt="Texto Alternativo">
<img src="Images/a3.png" alt="Texto Alternativo">
Procedemos con la creación de estos VPC, le damos a crear y tendremos que tener encuenta los siguientes parametros:
Nombre del VPC: wordpress-vpc.(Por ejemplo).
Bloque CIDR IPv4: 10.0.0.0/16(Por ejemplo).
Bloque CIDR IPv6: no lo necesitamos.
Por tanto quedaría asi:
<img src="Images/a4.png" alt="Texto Alternativo">

Posteriomente a configurar nuestro VPC, creamos sus subredes.En primer lugar las públicas
<img src="Images/a5.png" alt="Texto Alternativo">
Al clickar, le damos a crear subred.
<img src="Images/a6.png" alt="Texto Alternativo">
Posteriormente configurarla, tal que así:
Nombre de la subred: subred-publica-1.
VPC:Selecciona wordpress-vpc.
Zona de disponibilidad (AZ): Selecciona una AZ, por ejemplo, us-east-1a.
Bloque CIDR IPv4: 10.0.1.0/24.
<img src="Images/a7.png" alt="Texto Alternativo">


