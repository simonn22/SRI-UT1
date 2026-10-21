# Esta es la tarea del alumno Simón Jiménez del curso ASIR2, módulo SRI.

# Apartado 1. Tu red y tu instancia en AWS

### VPC:

![VPC](evidencias/a1_01_vpc.png)

### Subred pública:

![Subred publica](evidencias/a1_02_subred_publica.png)
![Route table](evidencias/a1_03_route_table.png)
![Editar rutas](evidencias/a1_04_editar_rutas.png)


### Grupo de seguridad con mínimo privilegio:

![Grupo de seguridad](evidencias/a1_05_grupo_seguridad.png)

### Instancia EC2:

![Instancia de EC2](evidencias/a1_06_instancia_ec2.png)

#### Detalles de la instancia:

![Detalles de la Instancia](evidencias/a1_07_detalles_instancia.png)

## Mapa de recursos de la VPC

![Mapa de recursos de la VPC](evidencias/a1_08_mapa_recursos_vpc.png)

## Salida de timedatectl

![timedatectl](evidencias/a1_09_timedatectl.png)

---

# Apartado 2. Instalación y configuración básica de Nginx

## Configuracion de los sitios de Nginx

* Creo la carpeta para el sitio:
![Creo la carpeta para el sitio](evidencias/a2_01_crear_carpeta_sitio.png)

* Cambio la ruta del sitio por defecto para que apunte a mi nueva carpeta:
![Cambio la ruta del sitio por defecto](evidencias/a2_02_cambiar_ruta_sitio_defecto.png)

* Creo un archivo simple index.html:
![Creo index.html](evidencias/a2_03_crear_index_html.png)

* Creo `/var/www/simon/estado/index.html` con un texto simple que indica que el servidor funciona:
![Creo /var/www/simon/estado/index.html](evidencias/a2_04_crear_estado_index_html.png)

* Modifico el archivo `/etc/nginx/nginx.conf` para ocultar la versión de Nginx en las cabeceras. Se cambia el valor de esta línea a `off`:
![server_tokens off](evidencias/a2_05_server_tokens_off.png)

* Verifico la configuración de Nginx, y siendo correcta la aplico y reinicio el servicio:
![Configuracion de nginx](evidencias/a2_06_verificar_y_reiniciar_nginx.png)

## Archivos nginx.conf y sites-available/default:

[nginx.conf](evidencias/nginx.conf)
[sites-available/default](nginx/sites-available/default)

## Cabeceras antes de ocultar la versión

![con version](evidencias/a2_07_cabeceras_con_version.png)

## Cabeceras *después* de ocultar la versión

![sin version](evidencias/a2_08_cabeceras_sin_version.png)

## Respuesta de `/estado/`

![estado](evidencias/a2_09_respuesta_estado.png)

# Apartado 3. Sitios virtuales

## Contenido de sites-enabled

![Contenido de sites-enabled](evidencias/a3_01_contenido_sites_enabled.png)
![La configuración no contiene errores](evidencias/a3_02_nginx_t_sin_errores.png)

## Intranet

![Intranet](evidencias/a3_03_intranet.png)

* Su archivo de configuración:
[intranet.conf](nginx/sites-available/intranet.conf)

## Sitio por defecto

![Sitio por defecto](evidencias/a3_04_sitio_por_defecto.png)

* Su archivo de configuración:
[default](nginx/sites-available/default)

## simon.test

![simon.test](evidencias/a3_05_simon_test.png)

* Su archivo de configuración:
[simon.conf](nginx/sites-available/simon.conf)

## blog.simon.test

![blog.simon.test](evidencias/a3_06_blog_simon_test.png)

* Su archivo de configuración:
[blogsimon.conf](nginx/sites-available/blogsimon.conf)

## Archivo `hosts` de mi máquina local

[hosts](evidencias/hosts)

---

# Apartado 4. Ampliar Nginx con módulos

Para este apartado, instalo en el servidor los paquetes `libnginx-mod-http-fancyindexy` y `php-fpm`.

![alt text](evidencias/a4_01_instalar_fancyindex_y_php_fpm.png)

También creo las carpetas y archivos necesarios para probar que todo funciona como debe:

![carpetas y archivos](evidencias/a4_02_carpetas_y_archivos_prueba.png)

## hora.php

Creo el archivo `/var/www/simontest/hora.php` y añado el siguiente código:

![hora.php](evidencias/a4_03_hora_php.png)

## `simon.conf` adaptado para implementar `hora.php` y `fancyindex`

[simon.conf actualizado](nginx/sites-available/simon_A4.conf)

Como explico en los comentarios:

* Para indicar a `fancyindex` que muestre un tamaño de archivo legible y no el tamaño exacto, se utiliza `fancyindex_exact_size off`
* Para decirle al servidor cómo comunivarse con php, lo indica el bloque `location ~ \.php$`

![simon.conf editado](evidencias/a4_04_simon_conf_editado.png)

## `/descargas/` con fancyindex

![/descargas/](evidencias/a4_05_descargas_fancyindex.png)

## Error `403 Forbidden` en el resto de carpetas

![403 Forbidden](evidencias/a4_06_error_403_forbidden.png)

---

# Apartado 5. Autenticación y control de acceso

## Instalar `apache2-utils`

![Instalar apache2-utils](evidencias/a5_01_instalar_apache2_utils.png)

### Averiguar IP pública de mi equipo

Para esto uso echo `$SSH_CLIENT` mientras estoy conectado a la máquina remota.

## Fichero para `intranet`

![Usuario simon](evidencias/a5_02_htpasswd_intranet_simon.png)

![Usuario profesor](evidencias/a5_03_htpasswd_intranet_profesor.png)

## Fichero para Admin

![Admin simon](evidencias/a5_04_htpasswd_admin_simon.png)

### Ajustar permisos de los ficheros

Para cumplir el requisito de que solo root y www-data puedan leerlos, cambio el propietario y los permisos:

![Permisos y propietario de los ficheros](evidencias/a5_05_permisos_y_propietario_ficheros.png)

## Editar el archivo `intranet.conf`

![intranet.conf actualizado](evidencias/a5_06_intranet_conf_actualizado.png)

[intranet.conf actualizado](nginx/sites-available/intranet_A5.conf)

## Configurar web principal (carpeta `/admin/`)

En este caso la configuración solo se aplica dentro del bloque location /admin/ para que solo pida autenticación ahí:

![simon.conf (/admin/)](evidencias/a5_07_simon_conf_location_admin.png)

[simon.conf actualizado](nginx/sites-available/simon_A5.conf)

## Acceso a la intranet

![Acceso a intranet](evidencias/a5_08_acceso_intranet.png)

## Acceso a /admin/ desde la IP permitida

![Acceso a /admin/ desde IP permitida](evidencias/a5_09_admin_desde_ip_permitida.png)

## Acceso a /admin/ desde el propio servidor

![Acceso a admin desde el propio servidor](evidencias/a5_10_admin_desde_el_servidor.png)

## Acceso a /admin/ desde fuera de la red

Como puede comprobarse, estando fuera de la red solicita usuario para acceder a `/admin/`.
En caso de intentar entrar como `profesor`, rechaza el acceso, pero al entrar como `simon` sí lo permite.

![Acceso a /admin/ desde fuera de la red](evidencias/a5_11_admin_desde_fuera_de_la_red.png)

---

# Apartado 6. Registros: estadísticas e incidencias

## 6.1. Un registro para cada sitio

Los siguientes cambios se añadirán bajo server_name:

### En simon.conf se añade lo siguiente

```nginx
access_log /var/log/nginx/simon.access.log;
error_log  /var/log/nginx/simon.error.log;
```

[Archivo actualizado](nginx/sites-available/simon_A6.conf)

### En blogsimon.conf se añade lo siguiente

```nginx
access_log /var/log/nginx/blog.access.log;
error_log  /var/log/nginx/blog.error.log;
```

[Archivo actualizado](nginx/sites-available/blogsimon_A6.conf)

### En intranet.conf se añade lo siguiente

```nginx
access_log /var/log/nginx/intranet.access.log;
error_log  /var/log/nginx/intranet.error.log;
```

[Archivo actualizado](nginx/sites-available/intranet_A6.conf)

## 6.2. Estadísticas desde la terminal

Se han realizado intentos variados, como accesos correctos, con usuario incorrecto, estando fuera de la red permitida para entrar a /admin/ etc.

### Para ver el numero total de peticiones

![Num total de peticiones](evidencias/a6_01_total_peticiones.png)

### Para ver las 5 IP que más peticiones hacen

![5 IP con mas peticiones](evidencias/a6_02_top5_ips.png)

### Para ver cuántas respuestas hay de cada código

![Cuantas respuestas hay de cada codigo](evidencias/a6_03_respuestas_por_codigo.png)

### Para ver qué rutas dan 404 y cuántas veces

![Errores 404](evidencias/a6_04_rutas_404.png)

### Para ver la hora del día con más peticiones

![Hora del dia con más peticiones](evidencias/a6_05_hora_con_mas_peticiones.png)

## Informe visual con GoAccess

Para instalarlo uso `sudo apt install -y goaccess`.

Para generar el informe uso `sudo goaccess /var/log/nginx/simon.access.log --log-format=COMBINED -o /var/www/intranet/informe.html`

Salida:

![alt text](evidencias/a6_06_goaccess_salida.png)