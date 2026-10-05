# Práctica 3: Configuración de Web Segura (HTTPS / SSL)

**Alumno:** Adrià Ferrando

---

## 1. Preparación del Dominio Local y Directorio Web

1. **Resolución de dominio:**
   Añadir entrada en `/etc/hosts`:
   ```text
   10.0.2.15 intranet.local
   ```

2. **Estructura del sitio:**
   Crear el directorio y archivo inicial en `/var/www/segur/index.html`:
   ```bash
   sudo mkdir -p /var/www/segur
   ```

![Captura: Creación de estructura web y hosts](images/p3_estructura.png)

---

## 2. Generación del Certificado SSL Autofirmado

1. **Creación de clave y certificado con OpenSSL:**
   ```bash
   sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
     -keyout /etc/ssl/private/nginx-selfsigned.key \
     -out /etc/ssl/certs/nginx-selfsigned.crt
   ```

2. **Comprobación de metadatos del certificado:**
   ```bash
   openssl x509 -noout -subject -dates -in /etc/ssl/certs/nginx-selfsigned.crt
   ```

![Captura: Generación e inspección del certificado OpenSSL](images/p3_openssl.png)

---

## 3. Configuración de Nginx (HTTPS y Redirección 301)

1. **Configuración del bloque de servidor:**
   Archivo `/etc/nginx/sites-available/intranet.local`:
   ```nginx
   # Servidor HTTPS
   server {
       listen 443 ssl;
       server_name intranet.local;

       ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
       ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;

       root /var/www/segur;
       index index.html;

       location / {
           try_files $uri $uri/ =404;
       }
   }

   # Redirección HTTP a HTTPS
   server {
       listen 80;
       server_name intranet.local;

       return 301 https://intranet.local$request_uri;
   }
   ```

2. **Activación y prueba:**
   ```bash
   sudo ln -s /etc/nginx/sites-available/intranet.local /etc/nginx/sites-enabled/
   sudo nginx -t
   sudo systemctl reload nginx
   ```

![Captura: Configuración Nginx y reinicio del servicio](images/p3_nginx_ssl.png)

---

## 4. Verificación de Seguridad en Navegador

1. Probar la redirección introduciendo `http://intranet.local` (debe redirigir a `https://`).
2. Aceptar la advertencia del certificado autofirmado en el navegador.

![Captura: Advertencia de certificado autofirmado](images/p3_cert_warning.png)
![Captura: Acceso correcto por HTTPS](images/p3_https_success.png)