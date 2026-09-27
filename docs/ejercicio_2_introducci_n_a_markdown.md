# Ejercicio 2: Introducción a Markdown
**Nombre del alumno:** Adrià Ferrando Bertomeu  
**Asignatura:** Implantación de Aplicaciones Web (IAW)

---

## 1. Estructura de Directorios del Proyecto

En nuestro repositorio local creamos la siguiente estructura de archivos y carpetas para organizar el contenido Markdown y las imágenes asociadas:

```text
mi_proyecto_md/
├── README.md
├── nuevodocumento.md
└── img/
    └── logo.png
```

```bash
mkdir mi_proyecto_md
cd mi_proyecto_md
mkdir img
touch README.md nuevodocumento.md
```

---

## 2. Sintaxis Básica de Markdown Aplicada

A continuación se detallan los elementos de sintaxis utilizados dentro de `nuevodocumento.md`:

### Encabezados
```markdown
# Encabezado de Nivel 1
## Encabezado de Nivel 2
### Encabezado de Nivel 3
```

### Formato de Texto
```markdown
Este es un texto en **negrita**, este en *cursiva* y este en ***negrita y cursiva***.
```

### Listas Ordenadas y Desordenadas
```markdown
Listas desordenadas:
- Elemento A
- Elemento B
  - Sub-elemento B1

Listas ordenadas:
1. Primer paso
2. Segundo paso
3. Tercer paso
```

### Enlaces e Imágenes
```markdown
<!-- Enlace a otro archivo del repositorio -->
Para más información, consulta el [README](README.md).

<!-- Imagen externa -->
![Logo Markdown](https://markdown-here.com/img/icon256.png)

<!-- Imagen local ubicada en la carpeta img -->
![Logo Local](img/logo.png)
```

---

## 3. Conversión de Markdown a PDF y Subida a GitHub

1. Una vez redactados y previsualizados los documentos `.md`, se utiliza una herramienta de conversión (como PDF24 o la extensión de VSCode *Markdown PDF*) para generar la versión en formato PDF (`nuevodocumento.pdf`).
2. Subimos tanto los archivos `.md`, las imágenes y los PDFs finales al repositorio de GitHub:

```bash
git add .
git commit -m "Añadidos documentos Markdown e imágenes junto con versión PDF"
git push origin main
```