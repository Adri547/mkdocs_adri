# Ejercicio 1: Introducción a Git y GitHub
**Nombre del alumno:** Adrià Ferrando Bertomeu  
**Asignatura:** Implantación de Aplicaciones Web (IAW)

---

## 1. Generar un Token de Acceso Personal (PAT) en GitHub

Como primera medida de seguridad en GitHub, es necesario generar un Token de Acceso Personal para autenticarnos desde la línea de comandos en lugar de usar la contraseña habitual.

1. Accedemos a la configuración de nuestra cuenta en GitHub: **Settings > Developer Settings > Personal Access Tokens > Tokens (classic)**.
2. Hacemos clic en **Generate new token (classic)**.
3. Asignamos un nombre al token (por ejemplo, `Token_Ubuntu`), seleccionamos los permisos requeridos (mínimo `repo`) y guardamos el token generado de forma segura.

---

## 2. Creación de un Repositorio en GitHub (`prova_adri`)

1. Desde el perfil de GitHub, creamos un nuevo repositorio público denominado **`prova_adri`**.
2. Marcamos la opción de inicializarlo con un archivo **README.md**.

---

## 3. Instalación y Configuración de Git en Ubuntu

En la terminal de la máquina virtual Ubuntu, ejecutamos los siguientes comandos para instalar y configurar Git con nuestras credenciales:

```bash
# Instalación de Git
sudo apt update
sudo apt install git -y

# Configuración del usuario y correo electrónico
git config --global user.name "Adri547"
git config --global user.email "tu_correo@ejemplo.com"

# Verificación de la configuración
git config --list
```

---

## 4. Clonar el Repositorio Remoto

Procedemos a clonar el repositorio `prova_adri` en nuestro entorno local:

```bash
git clone https://github.com/Adri547/prova_adri.git
cd prova_adri
```

---

## 5. Trabajo con Archivos: Añadir, Subir y Modificar

### 5.1 Crear y Subir un Nuevo Archivo
Creamos un archivo llamado `fichero.txt`, lo añadimos al área de preparación (*staging*), realizamos el *commit* y subimos los cambios al servidor remoto.

```bash
echo "Hola, este es un archivo de prueba" > fichero.txt
git status
git add fichero.txt
git commit -m "Añadido el archivo fichero.txt"
git push origin main
```

### 5.2 Modificar un Archivo Existente
Editamos `fichero.txt` agregando nueva información y subimos la actualización a GitHub:

```bash
echo "Añadiendo una nueva línea de contenido" >> fichero.txt
git add fichero.txt
git commit -m "Modificado contenido de fichero.txt"
git push origin main
```

---

## 6. Renombrar y Borrar Archivos en Git

### 6.1 Renombrar un Archivo
Cambiamos el nombre de `fichero.txt` a `nuevo_fichero.txt` utilizando el comando propio de Git:

```bash
git mv fichero.txt nuevo_fichero.txt
git commit -m "Renombrado fichero.txt a nuevo_fichero.txt"
git push origin main
```

### 6.2 Eliminar un Archivo
Eliminamos el archivo del repositorio local y remoto:

```bash
git rm nuevo_fichero.txt
git commit -m "Eliminado el archivo nuevo_fichero.txt"
git push origin main
```

---

## 7. Crear un Repositorio Local e Impulsarlo a GitHub (`prova2_adri`)

En este paso realizamos el proceso inverso: creamos un proyecto en local y posteriormente lo vinculamos a un nuevo repositorio remoto en GitHub llamado `prova2_adri`.

1. **Creación en GitHub:** Creamos el repositorio vacío `prova2_adri` en GitHub (sin README).
2. **Inicialización Local:**

```bash
mkdir prova2_adri
cd prova2_adri
git init
echo "# Repositorio Prova2" > README.md
git add README.md
git commit -m "Initial commit"
```

3. **Vinculación Remota y Subida:**

```bash
git branch -M main
git remote add origin https://github.com/Adri547/prova2_adri.git
git push -u origin main
```