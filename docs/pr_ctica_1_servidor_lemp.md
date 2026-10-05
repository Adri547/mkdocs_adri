# Práctica 1: Instalación de un Servidor LEMP

**Alumno:** Adrià Ferrando

---

## 1. Instalación y Configuración de MariaDB

1. **Instalación de paquetes:**
   Se instala el servidor de base de datos MariaDB:
   ```bash
   sudo apt update
   sudo apt install mariadb-server -y
   ```

2. **Asegurar la instalación (Hardening):**
   Ejecución del script interactivo de seguridad:
   ```bash
   sudo mariadb-secure-installation
   ```
   * Modificación de la contraseña de `root`.
   * Eliminación de usuarios anónimos.
   * Desactivación del inicio de sesión remoto para `root`.
   * Eliminación de la base de datos de test.

3. **Creación de Base de Datos y Usuarios:**
   Acceso a la consola de MariaDB y ejecución de las sentencias SQL:
   ```sql
   CREATE DATABASE newdb;
   CREATE USER 'adri'@'localhost' IDENTIFIED BY 'tu_contraseña';
   GRANT ALL PRIVILEGES ON newdb.* TO 'adri'@'localhost';
   FLUSH PRIVILEGES;
   ```

![Captura: Creación de base de datos y asignación de permisos](images/p1_mariadb_config.png)

---

## 2. Instalación y Configuración de Nginx y PHP

1. **Instalación del servidor web y PHP-FPM:**
   ```bash
   sudo apt install nginx php php-fpm php-mysql -y
   ```

2. **Configuración de Nginx para procesar PHP:**
   Edición del archivo de sitio por defecto `/etc/nginx/sites-available/default`:
   ```nginx
   server {
       listen 80 default_server;
       listen [::]:80 default_server;

       root /var/www/html;
       index index.php index.html index.htm;

       server_name www.adria.com;

       location / {
           try_files $uri $uri/ =404;
       }

       location ~ \.php$ {
           include snippets/fastcgi-php.conf;
           fastcgi_pass unix:/run/php/php8.5-fpm.sock;
       }
   }
   ```

3. **Comprobación sintáctica y recarga:**
   ```bash
   sudo nginx -t
   sudo systemctl reload nginx
   ```

![Captura: Verificación de la sintaxis de Nginx](images/p1_nginx_test.png)

---

## 3. Verificación del Funcionamiento y Logs

1. **Script de prueba PHP:**
   Creación de `/var/www/html/info.php`:
   ```php
   <?php
   phpinfo();
   ?>
   ```

2. **Mapeo DNS Local:**
   Edición de `/etc/hosts`:
   ```text
   10.0.2.15 www.adria.com
   ```

3. **Comprobación en el navegador:**
   Navegar a `http://www.adria.com/info.php` para validar el entorno PHPinfo.

![Captura: Pantalla de phpinfo() en el navegador](images/p1_phpinfo.png)

4. **Consulta de registros (Logs):**
   ```bash
   sudo journalctl -u nginx --no-pager -n 20
   ```

![Captura: Logs del servicio Nginx](images/p1_nginx_logs.png)