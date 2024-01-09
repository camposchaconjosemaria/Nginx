# Nginx configuración básica

## 1. Introducción

![image](https://github.com/camposchaconjosemaria/Nginx/assets/114906855/f8cfbb76-b004-43ed-96d0-8ae1b9ce9296)



Nginx es un servidor web de alto rendimiento, utilizado comúnmente como proxy inverso y equilibrador de carga. Destaca por su eficiencia, bajo uso de recursos y capacidad para manejar una gran cantidad de conexiones simultáneas.

Este repositorio proporciona información básica y pasos de configuración para comenzar a trabajar con Nginx. Desde la instalación hasta la gestión del servidor y la exploración de archivos clave, aquí encontrarás una guía concisa para aprovechar al máximo este servidor web versátil.

## 2.Diferencias entre Apache y Nginx

Al considerar Nginx y Apache, las diferencias fundamentales pueden influir en tu elección:

**Compatibilidad con el Sistema Operativo:**
- Ambos funcionan bien en UNIX, LINUX, y variantes.
- En Windows, Apache supera a Nginx.

**Administración y Mantenimiento:**
- Apache: Soporte comunitario global.
- Nginx: Soporte y administración centralizados por la compañía creadora.

**Rendimiento:**
- Apache: Un hilo por conexión.
- Nginx: Manejo eficiente de miles de conexiones simultáneas.

**Escalabilidad de la Arquitectura:**
- Nginx: Enfoque en eventos asíncronos para gestionar múltiples solicitudes.
- Apache: Arquitectura de subprocesos múltiples, menos escalable.

**Procesamiento de Contenido Dinámico:**
- Apache: Procesa contenido dinámico internamente.
- Nginx: Dependencia en procesos externos para contenido dinámico.


## 3. Instalación de Nginx

### Paso 1: Instalar Nginx

Para instalar Nginx desde los repositorios predeterminados de Ubuntu, ejecuta los siguientes comandos:

```bash
sudo apt update
sudo apt install nginx
```
### Paso 2: Ajustes en el Firewall

Antes de probar Nginx, es necesario realizar ajustes en el firewall para permitir el acceso al servicio. Nginx se registra automáticamente como un servicio con `ufw` tras la instalación, lo que facilita la apertura del acceso.

Para listar las configuraciones de la aplicación compatibles con `ufw`, ejecuta el siguiente comando:

```bash
sudo ufw app list
```

La salida del comando muestra las aplicaciones disponibles:

- Nginx Full
- Nginx HTTP
- Nginx HTTPS
- OpenSSH


Como se muestra en el resultado anterior, hay tres perfiles disponibles para Nginx:

- **Nginx Full:** Abre los puertos 80 (tráfico web normal, no cifrado) y 443 (tráfico TLS/SSL cifrado).
- **Nginx HTTP:** Abre solo el puerto 80 (tráfico web normal, no cifrado).
- **Nginx HTTPS:** Abre solo el puerto 443 (tráfico TLS/SSL cifrado).

Se recomienda habilitar el perfil más restrictivo. En este caso, solo necesitamos permitir el tráfico en el puerto 80. Puedes hacerlo con los siguientes comandos:

```bash
sudo ufw allow 'Nginx HTTP'
sudo ufw delete allow 'Nginx Full'
sudo ufw delete allow 'Nginx HTTPS'
sudo ufw status
```
### Paso 3: Verificar el Estado del Servidor Web

Al finalizar la instalación, Ubuntu 20.04 inicia Nginx, por lo que el servidor web debería estar activo.

Para verificar que el servicio esté en ejecución, utiliza el siguiente comando con systemd init:

```bash
systemctl status nginx
```

### Paso 4: Administrar el Proceso de Nginx

Nginx se puede gestionar utilizando varios comandos. Aquí tienes una lista útil:

```bash
# Iniciar Nginx
sudo systemctl start nginx

# Detener Nginx
sudo systemctl stop nginx

# Reiniciar Nginx
sudo systemctl restart nginx

# Recargar Configuración
sudo systemctl reload nginx

# Verificar Configuración
sudo nginx -t

# Habilitar al Inicio
sudo systemctl enable nginx

# Deshabilitar al Inicio
sudo systemctl disable nginx
```
### Paso 5: Explorar Archivos y Directorios Clave de Nginx

Ahora que tienes control sobre el servicio de Nginx, es crucial familiarizarse con algunos directorios y archivos esenciales.

**Contenido Web:**
- **/var/www/html:** Contiene el contenido web real. Por defecto, presenta la página predeterminada de Nginx. Puedes modificarlo ajustando los archivos de configuración de Nginx.

**Configuración del Servidor:**
- **/etc/nginx:** Directorio de configuración principal de Nginx, que contiene todos los archivos de configuración.
- **/etc/nginx/nginx.conf:** Archivo de configuración principal de Nginx. Modifícalo para realizar cambios en la configuración general.
- **/etc/nginx/sites-available/:** Directorio para guardar bloques de servidor por sitio. La configuración se realiza aquí y se habilita al establecer un vínculo en el directorio sites-enabled.

**Registros del Servidor:**
- **/etc/nginx/sites-enabled/:** Directorio que almacena los bloques de servidor habilitados por sitio. Se crean mediante vínculos con archivos de configuración en sites-available.
- **/etc/nginx/snippets:** Contiene fragmentos de configuración que pueden incluirse en otras partes de la configuración de Nginx.

**Registros del Servidor:**
- **/var/log/nginx/access.log:** Registra cada solicitud al servidor web.
- **/var/log/nginx/error.log:** Almacena errores de Nginx.

Estos directorios y archivos son fundamentales para entender y gestionar tu servidor Nginx.

## 4. Referencias

[DigitalOcean - Instalación de Nginx en Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04-es)

[Marketers Group - Diferencias entre Apache y Nginx](https://marketersgroup.es/diferencias-entre-apache-y-nginx/)


## 5. Licencia
