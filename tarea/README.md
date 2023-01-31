# UT3 - Prueba calificable 01 Seguridad y desplegado de aplicaciones con Docker

### Docker-Bench

**En la etapa de deploy nos interesa analizar el entorno. En el caso de Docker nos interesa ver cómo está todo montando, si está bien implementado y que cuenta con todos los requisitos necesarios. Para ello contamos con herramientas cómo Docker-bench, que se basa en una guía que es el CIS Docker Bench.**

1. **Utiliza docker bench y realiza un análisis previo de tu Docker.**

![WhatsApp Image 2023-01-31 at 19.27.55 (1).jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.55_(1).jpeg)

![WhatsApp Image 2023-01-31 at 19.27.56.jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.56.jpeg)

![WhatsApp Image 2023-01-31 at 19.27.55.jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.55.jpeg)

1. **Utiliza AuditD para que analice todas las pruebas de la Sección A, referente al host configuration.**

Para que funcione AuditD, he utilizado el siguiente comando:

![WhatsApp Image 2023-01-31 at 19.27.53.jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.53.jpeg)

Tras usar el comando, AuditD ha empezado a funcionar en el sistema.

![WhatsApp Image 2023-01-31 at 19.27.56 (2).jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.56_(2).jpeg)

Para que funcione bien, habrá que editar el archivo de configuración y añadir las siguientes rutas para que las analice.

![WhatsApp Image 2023-01-31 at 19.27.54.jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.54.jpeg)

Tendremos que utilizar el siguiente comando para que se apliquen los cambios.

![WhatsApp Image 2023-01-31 at 19.42.58.jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.42.58.jpeg)

Por último ejecutaremos el comando para que nos analice los archivos.

![WhatsApp Image 2023-01-31 at 19.27.54 (1).jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.54_(1).jpeg)

1. **Comenta 2 warnings que creas convenientes, y explica qué posible solución tendría.**

**Warning 1:**

```bash
Ensure that the container’s root filesystem is mounted as read only.
```

Este error nos indica, que el contenedor ha sido creado con permisos de administrador, de forma automática suele dejarse en modo lectura únicamente, pero yo le di permisos de escritura; para arreglarlo se debería cambiar los permisos del contenedor a modo lectura y esto se hace con el siguiente comando.

```bash
docker run <argumento> --read-only <ID> <Comando>
```

**Warning 2:**

```bash
Ensure that the memory usage for containers is limited.
```

Este error nos indica, que la memoria de los contenedores debería revisarse si está limitada, en mi caso, le quite el límite; para arreglarlo se debería configurar un límite de uso de memoria y esto se hace con el siguiente comando cuando se ejecuta el contenedor:

```bash
docker run --interactive --tty --memory 256m "ID" /bin/bash
```

### Análisis de archivos dockerfile

**Elegid cualquier archivo dockerfile que hayáis generado en la actividad UT3.AP00a - Afianzando el uso de Dockerfile y realiza un testeo con Trivy.**

![WhatsApp Image 2023-01-31 at 19.27.57.jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.57.jpeg)

Como se puede observar, se ha encontrado 304 vulnerabilidades de severidad bajas, 71 vulnerabilidades de severidad media, 80 vulnerabilidades de severidad alta y 14 vulnerabilidades de severidad crítica; aparte nos indica de que versión son las vulnerabilidades, en que librerías se encuentra, el CVE de la vulnerabilidad, un enlace donde nos explica en que consiste, la versión que se encuentra instalada en el momento y la versión en la que han arreglado dicha vulnerabilidad.

### Análisis de imágenes.

**Debéis escanear la imagen creada de Wordpress que hayáis generado en la actividad UT3.AP03-Docker-compose Wordpress con Trivy, Snyk o Docker Desktop. A continuación, descárgate la versión wordpress:4,6 y realiza el mismo procedimiento.**

**Haz una comparativa en cuanto estadísticas y puntos críticos de ambas.**

En esta captura de pantalla, se puede observar que la versión de debian que utiliza es la 11.6, esta imagen está actualizada a la última versión de wordpress y aun así es capaz de encontrar vulnerabilidades.

![WhatsApp Image 2023-01-31 at 19.27.57 (1).jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.57_(1).jpeg)

En esta captura de pantalla, se puede observar que la versión de debian que utiliza es la 8.6, esta imagen utiliza la versión 4.6 de wordpress y encuentra muchas más  vulnerabilidades.

![WhatsApp Image 2023-01-31 at 19.27.57 (2).jpeg](tarea/img/WhatsApp_Image_2023-01-31_at_19.27.57_(2).jpeg)

Tabla comparativa:

| Versión/Severidad | Wordpress:latest | Wordpress:4.6 |
| --- | --- | --- |
| Crítico | 11 | 269 |
| High | 90 | 1007 |
| Medio | 141 | 1005 |
| Bajo | 351 | 650 |
| Desconocido | 3 | 62 |

## Contact

[📧 danielruizraposo02@gmail.com](mailto:danielruizraposo02@mail.com)