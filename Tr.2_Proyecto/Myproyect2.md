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



---  Ruta imagenes
<img src="Images/a1.png" alt="Texto Alternativo">


