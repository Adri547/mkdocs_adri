# Práctica 2: Servir Múltiples Dominios (Virtual Hosting)

**Alumno:** Adrià Ferrando

---

## 1. Estructura de Directorios y Archivos Web

1. **Creación de directorios para los sitios:**
   ```bash
   sudo mkdir -p /var/www/pagina1
   sudo mkdir -p /var/www/pagina2
   ```

2. **Creación de archivos HTML de prueba:**
   * Archivo `/var/www/pagina1/index1.html`:
     ```html
     <!DOCTYPE html>
     <html>
     <head><title>Página 1</title></head>
     <body><h1>Bienvenido a Página 1</h1></body>
     </html>
     ```
   * Archivo `/var/www/pagina2/index2.html`:
     ```html
     <!DOCTYPE html>
     <html>
     <head><title>Página 2</title></head>
     <body><h1>Bienvenido a Página 2</h1></body>
     </html>
     ```

![Captura: Creación de directorios e índices HTML](images/p2_directorios.png)

---

## 2. Configuración de Bloques de Servidor en Nginx

1. **Creación del VirtualHost para `pagina1.com`:**
   Archivo `/etc/nginx/sites-available/pagina1.com`:
   ```nginx
   server {
       listen 80;
       root /var/www/pagina1;
       index index1.html index.html;
       server_name www.pagina1.com;

       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```

2. **Creación del VirtualHost para `pagina2.com`:**
   Archivo `/etc/nginx/sites-available/pagina2.com`:
   ```nginx
   server {
       listen 80;
       root /var/www/pagina2;
       index index2.html index.html;
       server_name www.pagina2.com;

       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```

3. **Habilitación de los sitios:**
   ```bash
   sudo ln -s /etc/nginx/sites-available/pagina1.com /etc/nginx/sites-enabled/
   sudo ln -s /etc/nginx/sites-available/pagina2.com /etc/nginx/sites-enabled/
   ```

4. **Validación de configuración y reinicio:**
   ```bash
   sudo nginx -t
   sudo systemctl reload nginx
   ```

![Captura: Enlaces simbólicos y prueba de sintaxis Nginx](images/p2_nginx_symlinks.png)

---

## 3. Resolución Local y Comprobación

1. **Edición del archivo de hosts local (`/etc/hosts`):**
   ```text
   10.0.2.15 www.pagina1.com
   10.0.2.15 www.pagina2.com
   ```

2. **Prueba de acceso:**
   * Abrir en el navegador `http://www.pagina1.com`
   * Abrir en el navegador `http://www.pagina2.com`

![Captura: Verificación de acceso a Página 1](images/p2_resultado_pag1.png)
![Captura: Verificación de acceso a Página 2](images/p2_resultado_pag2.png)