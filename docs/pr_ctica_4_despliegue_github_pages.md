# Práctica 4: Despliegue en GitHub Pages con MkDocs

**Alumno:** Adrià Ferrando

---

## 1. Estructura y Configuración del Proyecto MkDocs

1. **Instalación de MkDocs y tema Material:**
   ```bash
   pip install mkdocs mkdocs-material
   ```

2. **Configuración en `mkdocs.yml`:**
   ```yaml
   site_name: Documentación de Prácticas
   theme:
     name: material
   
   nav:
     - Inicio: index.md
   ```

3. **Contenido de la documentación (`docs/index.md`):**
   Redacción de las páginas en formato Markdown.

![Captura: Estructura de archivos de MkDocs](images/p4_mkdocs_structure.png)

---

## 2. Automatización CI/CD con GitHub Actions

1. **Creación del workflow:**
   Archivo `.github/workflows/deploy.yml`:
   ```yaml
   name: deploy-docs
   on:
     push:
       branches:
         - master
         - main

   permissions:
     contents: write

   jobs:
     deploy:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v3

         - name: Configure Python
           uses: actions/setup-python@v4
           with:
             python-version: 3.x

         - run: pip install mkdocs mkdocs-material

         - run: mkdocs gh-deploy --force
   ```

![Captura: Configuración del archivo deploy.yml](images/p4_workflow_yaml.png)

---

## 3. Publicación y Despliegue Automático

1. **Configuración en GitHub:**
   En las opciones del repositorio (*Settings -> Pages*), asegurarse de que la fuente esté configurada en **Deploy from a branch** (rama `gh-pages`).

2. **Envío de cambios:**
   ```bash
   git add .
   git commit -m "Actualización de documentación"
   git push origin master
   ```

3. **Verificación:**
   Comprobar en la pestaña **Actions** la correcta ejecución del pipeline y acceder a la URL pública asignada por GitHub Pages.

![Captura: Ejecución del Workflow en GitHub Actions](images/p4_github_actions_run.png)
![Captura: Sitio publicado en GitHub Pages](images/p4_site_live.png)