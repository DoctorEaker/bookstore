# Despliuegue escalable y robusto

## Proyecto 2 - Tópicos Especiales en Telemática

### Análisis y Diseño

#### Equipo

-   Luis Miguel Arroyave Quiñones - larroy13@eafit.edu.co
-   Keneth Berrio Martinez - kberriom@eafit.edu.co
-   Federico Rafael Jaramillo Franco - fjaram18@eafit.edu.co

#### Requisitos

1. Poner en marcha la versión ESCALABLE de la aplicación web en AWS Academy. Para esto,
   debe considerar los siguientes aspectos:
   a. Utilizar conceptos, así como tecnologías de virtualización y contenerización (Docker
   y Docker-compose) para la solución a desplegar.
   b. Se requiere que solicite un nombre de dominio para la versión escalable.
   c. Deberá gestionar y configurar un certificado SSL de let’s encrypt para la versión
   escalable.

2. Debe consultar e indagar con el fin de monitorear la disponibilidad de la aplicación
   BookStore. Para esto debe configurar un sistema de monitoreo de disponibilidad (ej:
   uptimerobot o similar)
3. Presupuesto y estimación del costo inicial y mensual de la operación del sistema en nube.

4. Diseño:
   a. Diseñar el sistema para 1.000 usuarios, con un nivel de concurrencia del 10%.
   b. Diseñar el sistema para un almacenamiento total de 1 TB.
   c. Implementar el sistema a escala, considerando las restricciones del

5. Diseñar e implementar conceptos de alta disponibilidad considerando al menos:
   a. Balanceadores de carga
   b. Crecimiento horizontal
   c. Alta disponibilidad en la capa de servicios
   d. Alta disponibilidad en la capa de bases de datos para el manejo de la información
   almacenada en el motor definido para esto.
   e. Sistema de backup y restore de datos, contenidos, aplicaciones, etc

6. Rendimiento
   a. Tiempos de respuesta promedio entre 1 y 2 segundos
   b. Performance tunning de la Aplicación, de la Base de datos, de los servicios del
   sistema.
   c. Diseño e implementación de CDN (content distribution network) – caché (base de
   datos) – caché archivos (locales) (priorizar cloudflare si AWS no ofrece el servicio en
   Educativo y para el DCA)
7. Seguridad:
   a. Solicitar, gestionar y utilizar un certificado SSL válido para la aplicación del grupo.
   b. Implementación de certificados SSL
   c. Política de gestión de claves de usuario (passwords)
   d. Implementar Single Sign on (SSO), o auth0, gmail, e integrarlo a la aplicación.

#### Arquitectura
![alt text](https://raw.githubusercontent.com/DoctorEaker/bookstore/main/images/arch.png)


#### Presupuesto y estimación del costo inicial y mensual de la operación del sistema
 Como base se asumen los siguientes parámetros de uso del sistema 
 
 - 1.000 usuarios, con un nivel de concurrencia del 10%
 - 1 TB de almacenamiento total
 - Tiempo de respuesta 1 segundo / Petición

Asumiendo que el sistema este disponible 24 al día con una carga maxima teórica de 1.000 usuarios pero el sistema cuenta con un porcentaje de concurrencia del 10% podemos asumir que solo 100 usuarios estarán usando el sistema de manera simultanea.  
Podemos calcular en promedio cada cuando llega una petición usando la siguiente formula conocida como la ley de little (despejando la variable λ):

    L = λ x W
Donde:
- L es el numero de peticiones promedio del sistema
- λ es la velocidad de llegada de peticiones
- W es el tiempo promedio para servir cada petición
El tiempo promedio de cada petición al sistema actualmente es de 223 ms (0.223 s)

    100 = λ x 0.223 
    λ = 100 / 0.223
    λ = 448.43 es el ritmo de llegada (usuarios / segundo)
    
La aplicación desplegada en la capa del frontend pesa aproximadamente 2.1 Mb

Por lo que cada segundo se tendrá un network throughput de 448.43 (usuarios/s) * 2.1Mb = **941.703 Mb** aproximadamente.
