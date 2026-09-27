# Práctica 2: Realización de un Pull Request
**Nombre del alumno:** Adrià Ferrando Bertomeu  
**Asignatura:** Implantación de Aplicaciones Web (IAW)

---

## 1. Concepto
Un *Pull Request* (PR) es una funcionalidad de plataformas como GitHub que permite a un desarrollador notificar a los mantenedores de un proyecto que ha realizado cambios en el código y solicita que estos sean revisados e incorporados (*merged*) al repositorio principal.

---

## 2. Pasos Realizados en la Práctica

### Paso 1: Fork del Repositorio Original
1. Navegamos al repositorio original del profesor: `https://github.com/jfelis/PractiquesIAW`.
2. Hacemos clic en el botón **Fork** (esquina superior derecha) para crear una copia exacta del proyecto dentro de nuestra propia cuenta de GitHub (`Adri547/PractiquesIAW`).

---

### Paso 2: Clonación e Implementación de Cambios Localmente
Clonamos **nuestro fork** en la máquina virtual Ubuntu para trabajar localmente:

```bash
git clone https://github.com/Adri547/PractiquesIAW.git
cd PractiquesIAW
```

Editamos el archivo `README.md` insertando nuestros datos personales (Nombre y Apellidos) en la sección correspondiente de alumnos.

```bash
nano README.md
```

---

### Paso 3: Commit y Push a Nuestro Fork
Guardamos los cambios, realizamos el commit y subimos la actualización a nuestro repositorio forkeado en GitHub:

```bash
git add README.md
git commit -m "Añadido nombre de Adrià Ferrando Bertomeu al README"
git push origin main
```

---

### Paso 4: Apertura del Pull Request
1. Accedemos a la página de nuestro repositorio en GitHub (`Adri547/PractiquesIAW`).
2. Aparecerá un aviso sugiriendo la opción **Contribute > Open pull request** (o **Compare & pull request**).
3. Verificamos la dirección de las ramas:
   - **Base repository:** `jfelis/PractiquesIAW` (main)
   - **Head repository:** `Adri547/PractiquesIAW` (main)
4. Redactamos un título claro (ej. *"Añadido alumno Adrià Ferrando"*) y una descripción explicativa de los cambios.
5. Hacemos clic en **Create pull request**.