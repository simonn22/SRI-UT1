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
[sites-available/default](nginx/sites-available/default)

## Cabeceras antes de ocultar la versión

![con version](evidencias/2026-10-21_09-27.png)

## Cabeceras *después* de ocultar la versión

![sin version](evidencias/2026-10-21_09-26.png)

## Respuesta de `/estado/`

![estado](evidencias/2026-10-21_09-32.png)

# Apartado 3. Sitios virtuales

## Contenido de sites-enabled

![Contenido de sites-enabled](evidencias/2026-10-21_10-01.png)
![La configuración no contiene errores](evidencias/2026-10-21_10-02.png)

## Intranet

![Intranet](evidencias/2026-10-21_10-03.png)

* Su archivo de configuración:
[intranet.conf](nginx/sites-available/intranet.conf)

## Sitio por defecto

![Sitio por defecto](evidencias/2026-10-21_10-05.png)

* Su archivo de configuración:
[default](nginx/sites-available/default)

## simon.test

![simon.test](<evidencias/Captura de pantalla_20261021_140018.png>)

* Su archivo de configuración:
[simon.conf](nginx/sites-available/simon.conf)

## blog.simon.test

![blog.simon.test](<evidencias/Captura de pantalla_20261021_140141.png>)

* Su archivo de configuración:
[blogsimon.conf](nginx/sites-available/blogsimon.conf)

## Archivo `hosts` de mi máquina local

[hosts](evidencias/hosts)

---

# Apartado 4. Ampliar Nginx con módulos

Para este apartado, instalo en el servidor los paquetes `libnginx-mod-http-fancyindexy` y `php-fpm`.

![alt text](<evidencias/Captura de pantalla_20261021_143509.png>)

También creo las carpetas y archivos necesarios para probar que todo funciona como debe:

![carpetas y archivos](<evidencias/Captura de pantalla_20261021_143352.png>)

## hora.php

Creo el archivo `/var/www/simontest/hora.php` y añado el siguiente código:

![hora.php](<evidencias/Captura de pantalla_20261021_153715.png>)

## `simon.conf` adaptado para implementar `hora.php` y `fancyindex`

[simon.conf actualizado](nginx/sites-available/simon_A4.conf)

Como explico en los comentarios:

* Para indicar a `fancyindex` que muestre un tamaño de archivo legible y no el tamaño exacto, se utiliza `fancyindex_exact_size off`
* Para decirle al servidor cómo comunivarse con php, lo indica el bloque `location ~ \.php$`

![simon.conf editado](<evidencias/Captura de pantalla_20261021_154152.png>)

## `/descargas/` con fancyindex

![/descargas/](<evidencias/Captura de pantalla_20261021_155256.png>)

## Error `403 Forbidden` en el resto de carpetas

![403 Forbidden](<evidencias/Captura de pantalla_20261021_155437.png>)

## Apartado 