# Práctica 3: Despliegue de Documentación con MkDocs y GitHub Pages
**Nombre del alumno:** Adrià Ferrando Bertomeu  
**Asignatura:** Implantación de Aplicaciones Web (IAW)

---

## 1. Configuración del Entorno Virtual e Instalación de MkDocs

Para aislar las dependencias de Python del sistema, creamos y activamos un entorno virtual (`venv`):

```bash
# Crear entorno virtual
python3 -m venv venv

# Activar el entorno virtual
source venv/bin/activate

# Instalar MkDocs y el tema Material
pip install mkdocs mkdocs-material
```

---

## 2. Creación del Sitio con MkDocs

Inicializamos el proyecto MkDocs y verificamos su estructura general:

```bash
mkdocs new mi_sitio_mkdocs
cd mi_sitio_mkdocs
```

Estructura generada:
```text
mi_sitio_mkdocs/
├── docs/
│   └── index.md
└── mkdocs.yml
```

---

## 3. Configuración del Archivo `mkdocs.yml`

Editamos el archivo de configuración `mkdocs.yml` para definir el título del sitio, los temas visuales y la estructura de navegación:

```yaml
site_name: Documentación IAW - Adrià Ferrando
site_url: https://Adri547.github.io/mi_sitio_mkdocs/

theme:
  name: material
  palette:
    primary: indigo
    accent: blue

nav:
  - Inicio: index.md
  - Prácticas:
    - Práctica 1: practica1.md
    - Práctica 2: practica2.md
```

---

## 4. Ajuste del Archivo `.gitignore`

Es fundamental evitar subir al repositorio el entorno virtual y los archivos estáticos compilados que genera MkDocs al construir el sitio.

Creamos o editamos el archivo `.gitignore`:

```text
# Entorno virtual
venv/

# Sitio estático generado por MkDocs
site/
```

---

## 5. Previsualización en Local

Probamos el sitio localmente mediante el servidor de desarrollo integrado en MkDocs:

```bash
mkdocs serve
```
Accedemos a la dirección `http://127.0.0.1:8000/` en el navegador para comprobar los cambios en tiempo real.

---

## 6. Despliegue Automático en GitHub Pages

Utilizamos el comando interno de MkDocs para publicar el sitio automáticamente en la rama `gh-pages` de GitHub:

```bash
# Inicializar repositorio Git en caso de ser necesario
git init
git remote add origin https://github.com/Adri547/mi_sitio_mkdocs.git

# Publicar en GitHub Pages
mkdocs gh-deploy
```

El sitio queda publicado y accesible públicamente en la URL asignada por GitHub Pages (ejemplo: `https://Adri547.github.io/mi_sitio_mkdocs/`).