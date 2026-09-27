# Práctica 1: Git – Ramas y Uniones
**Nombre del alumno:** Adrià Ferrando Bertomeu  
**Asignatura:** Implantación de Aplicaciones Web (IAW)

---

## 1. Creación y Manejo de Ramas Básicas

Inicializamos o utilizamos un repositorio local para practicar la gestión de ramas (*branches*).

```bash
# Ver las ramas existentes
git branch

# Crear una nueva rama llamada "segunda"
git branch segunda

# Cambiar a la rama "segunda"
git checkout segunda

# Comprobar la rama activa (estará marcada con un asterisco *)
git branch
```

---

## 2. Realizar Cambios en la Nueva Rama y Fusión *Fast-Forward*

En la rama `segunda`, creamos un nuevo archivo y realizamos un commit. Posteriormente, lo uniremos a la rama principal (`main` o `master`).

```bash
# Crear un archivo en la rama 'segunda'
echo "Texto en la rama segunda" > archivo_segunda.txt
git add archivo_segunda.txt
git commit -m "Añadido archivo_segunda.txt en la rama segunda"

# Regresar a la rama principal
git checkout main

# Fusionar la rama 'segunda' en 'main' (Fusión Fast-Forward)
git merge segunda

# Borrar la rama 'segunda' una vez fusionada
git branch -d segunda
```

---

## 3. Provocar y Resolver un Conflicto de Fusión (*Merge Conflict*)

Para comprender cómo gestiona Git los conflictos, editaremos el mismo archivo en dos ramas distintas antes de fusionarlas.

### Step 1: Modificación en la rama activa
Editamos el archivo `README.md` en la rama `main`:

```bash
echo "Línea modificada desde la rama main" >> README.md
git add README.md
git commit -m "Cambio en README desde main"
```

### Step 2: Modificación en una nueva rama
Creamos la rama `conflicto-branch`, nos cambiamos a ella y modificamos la **misma línea** del archivo `README.md`:

```bash
git checkout -b conflicto-branch
echo "Línea modificada desde la rama conflicto-branch" >> README.md
git add README.md
git commit -m "Cambio en README desde conflicto-branch"
```

### Step 3: Provocar el conflicto
Volvemos a `main` e intentamos realizar la fusión:

```bash
git checkout main
git merge conflicto-branch
```
*Git notificará un conflicto de fusión en `README.md` y pausará el proceso de merge.*

### Step 4: Resolución Manual del Conflicto
Abrimos el archivo `README.md` con un editor de texto (como `nano` o `vim`). Encontraremos las marcas de conflicto:

```text
<<<<<<< HEAD
Línea modificada desde la rama main
=======
Línea modificada desde la rama conflicto-branch
>>>>>>> conflicto-branch
```

Editamos manualmente el archivo dejando el texto final deseado y eliminando las marcas de Git (`<<<<<<<`, `=======`, `>>>>>>>`).

### Step 5: Finalizar el Merge
Una vez resuelto el conflicto, guardamos el archivo y completamos la fusión:

```bash
git add README.md
git commit -m "Resolución de conflicto en README.md"
```

---

## 4. Sincronización de Ramas con el Repositorio Remoto

Para subir una rama local específica al repositorio remoto en GitHub:

```bash
# Crear la rama local
git checkout -b rama-remota

# Subir la rama al remoto origin
git push origin rama-remota
```