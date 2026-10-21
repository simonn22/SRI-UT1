Esta es la tarea del alumno Simón Jiménez del curso ASIR2, módulo SRI.

# Apartado 1

### VPC:

![VPC](<evidencias/Captura de pantalla_20261019_175731.png>)

### Subred pública:

![Subred publica](<evidencias/Captura de pantalla_20261019_180020.png>)
![Route table](<evidencias/Captura de pantalla_20261019_180233.png>)
![Editar rutas](<evidencias/Captura de pantalla_20261019_182337.png>)


### Grupo de seguridad con mínimo privilegio:

![Grupo de seguridad](<evidencias/Captura de pantalla_20261019_182702.png>)

### Instancia EC2:

![Instancia de EC2](<evidencias/Captura de pantalla_20261019_190803.png>)

#### Detalles de la instancia:

![Detalles de la Instancia](<evidencias/Captura de pantalla_20261019_192117.png>)

## Mapa de recursos de la VPC

![Mapa de recursos de la VPC](<evidencias/Captura de pantalla_20261019_183921.png>)

## Salida de timedatectl

![timedatectl](<evidencias/Captura de pantalla_20261019_192503.png>)

---

# Apartado 2. Instalación y configuración básica de Nginx

## Configuracion de los sitios de Nginx

* Creo la carpeta para el sitio:
![Creo la carpeta para el sitio](evidencias/2026-10-21_08-59.png)

* Cambio la ruta del sitio por defecto para que apunte a mi nueva carpeta:
![Cambio la ruta del sitio por defecto](evidencias/2026-10-21_09-01.png)

* Creo un archivo simple index.html:
![Creo index.html](evidencias/2026-10-21_09-03.png)

* Creo `/var/www/simon/estado/index.html` con un texto simple que indica que el servidor funciona:
![Creo /var/www/simon/estado/index.html](evidencias/2026-10-21_09-06.png)

* Modifico el archivo `/etc/nginx/nginx.conf` para ocultar la versión de Nginx en las cabeceras. Se cambia el valor de esta línea a `off`:
![server_tokens off](evidencias/2026-10-21_09-12.png)

* Verifico la configuración de Nginx, y siendo correcta la aplico y reinicio el servicio:
![Configuracion de nginx](evidencias/2026-10-21_09-14.png)

## Archivos nginx.conf y sites-available/default:

[nginx.conf](evidencias/nginx.conf)
[sites-available/default](evidencias/default)

## Cabeceras antes de ocultar la versión

![con version](evidencias/2026-10-21_09-27.png)

## Cabeceras *después* de ocultar la versión

![sin version](evidencias/2026-10-21_09-26.png)

## Respuesta de `/estado/`

![alt text](evidencias/2026-10-21_09-32.png)

# Apartado 3. Sitios virtuales

## Contenido de sites-enabled

![Contenido de sites-enabled](evidencias/2026-10-21_10-01.png)
![La configuración no contiene errores](evidencias/2026-10-21_10-02.png)

## Intranet

![Intranet](evidencias/2026-10-21_10-03.png)

## Sitio por defecto

![Sitio por defecto](evidencias/2026-10-21_10-05.png)

AÑADIR CAPTURAS DE LOS OTROS SITIOS Y SUBIR EL ARCHIVO HOSTS Y LOS FICHEROS DE CONFIGURACION DE LOS TRES SITIOS