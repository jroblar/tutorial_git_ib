## 🔧 Git vs. GitHub: ¿Cuál es la diferencia?

| Característica              | Git                                         | GitHub                                                   |
| --------------------------- | ------------------------------------------- | -------------------------------------------------------- |
| **¿Qué es?**                | Un *sistema de control de versiones*        | Una *plataforma en la nube* para alojar repositorios Git |
| **Dónde se ejecuta**        | En tu **computadora local**                 | En la **web (GitHub.com)**                               |
| **Propósito**               | Rastrear los cambios en proyectos de código | Colaborar, compartir y respaldar código                  |
| **¿Funciona sin internet?** | Sí                                          | No                                                       |
| **Creado por**              | Linus Torvalds (2005)                       | Ahora propiedad de Microsoft (fundada en 2008)           |

> Git gestiona el historial de versiones de tu proyecto. GitHub almacena tus repositorios Git en línea para que puedas colaborar con otros.

---

## Enlaces útiles

* Guía de inicio rápido: [https://docs.github.com/es/get-started/quickstart](https://docs.github.com/es/get-started/quickstart)
* Installacion de git: [https://git-scm.com/book/en/v2/Getting-Started-Installing-Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* Configura tus credenciales de Git y GitHub: [https://docs.github.com/es/get-started/getting-started-with-git/setting-your-username-in-git](https://docs.github.com/es/get-started/getting-started-with-git/setting-your-username-in-git)
* GitHub CLI para autenticación: [https://docs.github.com/es/github-cli/github-cli/about-github-cli](https://docs.github.com/es/github-cli/github-cli/about-github-cli)
* Comandos de autenticación de GitHub CLI: [https://cli.github.com/manual/gh\_auth](https://cli.github.com/manual/gh_auth)

---

## Instrucciones de instalación

* Primero, asegúrate de tener Git instalado y luego configura tus credenciales de Git (nombre de usuario y correo).
* Para interactuar con GitHub desde la línea de comandos, instala GitHub CLI.
* Después de instalarlo, ejecuta `gh auth login` para autenticarte.

---

## 🧰 Comandos comunes de Git

### 🔁 Configuración inicial

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```

### 📦 Crear un repositorio

```bash
git init                      # Inicializar un nuevo repositorio Git
git clone <url-repo>          # Clonar un repositorio de GitHub a tu computadora
```

### 💾 Guardar cambios

```bash
git status                    # Ver archivos en estado modificado, no rastreados, etc.
git add <archivo>             # Añadir un archivo específico al staging
git add .                     # Añadir todos los cambios
git commit -m "Tu mensaje"    # Guardar los cambios añadidos en el repositorio
```

### 🔍 Ver historial

```bash
git log                       # Mostrar historial de commits
git diff                      # Mostrar diferencias en archivos rastreados
```

### 🔄 Trabajar con repositorios remotos

```bash
git remote -v                 # Mostrar los repositorios remotos vinculados
git fetch                     # Obtener los últimos cambios del remoto **sin** fusionar
git pull                      # Traer y fusionar los cambios del remoto
git push                      # Subir tus commits a GitHub
```

### 🌿 Trabajando con ramas

```bash
git branch                    # Listar ramas
git branch <nombre-rama>      # Crear una nueva rama
git checkout <nombre-rama>    # Cambiar de rama (método tradicional)
git checkout -b <nombre>      # Crear y cambiar de rama
git switch <nombre-rama>      # Nueva forma de cambiar de rama
git switch -c <nombre>        # Crear y cambiar de rama (alternativa a `checkout -b`)
git merge <nombre-rama>       # Fusionar otra rama con la rama actual
```

---

## 🧳 Trabajando con cambios temporales

A veces quieres **guardar cambios temporalmente** sin hacer commit. Usa `stash`:

```bash
git stash                     # Guardar cambios y limpiar el directorio de trabajo
git stash list                # Ver los cambios guardados (stashed)
git stash pop                 # Reaplicar el último stash y eliminarlo de la lista
git stash apply               # Reaplicar sin eliminarlo del stash
```

> Usa stash si necesitas cambiar de rama o actualizar el repositorio sin perder tu trabajo en progreso.

---

## ⚔️ Conflictos de fusión: Resolviendo diferencias entre versiones de archivos

Cuando ejecutas `git merge <nombre-rama>`, Git puede encontrar **conflictos** si la misma parte de un archivo fue modificada en ambas ramas.

### Ejemplo de marcadores de conflicto:

```
<<<<<<< HEAD
Esta es tu versión del archivo
=======
Esta es la versión que viene de la otra rama
>>>>>>> feature-branch
```

### Pasos para resolver:

1. **Abre el archivo** en tu editor de código.
2. **Elige qué versión** conservar:

   * La tuya (`HEAD`)
   * La de ellos (`feature-branch`)
   * O combina ambas manualmente
3. **Elimina los marcadores de conflicto** (`<<<<<<<`, `=======`, `>>>>>>>`)
4. **Guarda el archivo**
5. Añade y haz commit para finalizar la resolución:

```bash
git add <archivo>
git commit -m "Resuelto conflicto de merge"
```

---

## ✅ Un flujo típico de trabajo con Git

1. `git clone <url-repo>`
2. Crear o cambiar de rama: `git switch -c mi-feature`
3. Haz tus cambios
4. `git add .`
5. `git commit -m "Describe tus cambios"`
6. `git pull origin main` *(resuelve conflictos si aparecen)*
7. `git push origin mi-feature`
8. Abre un Pull Request en GitHub

---

## 🚫 Dejar de rastrear archivos o carpetas en Git

### 1. **Eliminar un archivo o carpeta rastreada**

Si Git está rastreando un archivo o carpeta que ya no quieres rastrear:

```bash
git rm --cached <ruta-al-archivo-o-carpeta>
```

Ejemplo:

```bash
git rm --cached data/output.csv
git rm --cached -r logs/  # Para carpetas
```

### 2. **Agrega a `.gitignore`**

Evita que Git los rastree en el futuro:

```bash
echo "logs/" >> .gitignore
echo "*.csv" >> .gitignore
```

Luego haz commit del cambio:

```bash
git add .gitignore
git commit -m "Dejar de rastrear archivos especificados"
```

---

## 🔄 Cambiar la conexión remota

### 1. **Ver la URL remota actual**

```bash
git remote -v
```

### 2. **Configura una nueva URL**

```bash
git remote set-url origin <nueva-url-repo>
```

Ejemplo:

```bash
git remote set-url origin https://github.com/tuusuario/nuevo-repo.git
```

### 3. **Verifica el cambio**

```bash
git remote -v
```

---

## 🚀 **Cómo copiar un repositorio de GitHub como nuevo proyecto (con o sin historial de commits)**

A veces quieres comenzar un nuevo proyecto basado en otro repo—ya sea **desde cero (sin historial)** o **con todo el historial de commits**. Así puedes hacerlo:

---

### **Opción 1: Comenzar desde cero (sin historial)**

1. **Copia el repo localmente**

   * Clona, descarga o copia la carpeta del proyecto original.

2. **Elimina el historial de Git anterior**

   ```bash
   rm -rf .git
   ```

3. **Inicializa un nuevo repositorio Git**

   ```bash
   git init
   ```

4. **Agrega todos los archivos**

   ```bash
   git add .
   ```

5. **Haz commit de tus archivos**

   ```bash
   git commit -m "Primer commit"
   ```

6. **Crea un nuevo repositorio en GitHub**

   * Ve a [github.com/new](https://github.com/new), ponle nombre y créalo.
   * No añadas README, .gitignore ni licencia todavía (puedes hacerlo después).

7. **Agrega el remoto y haz push**

   ```bash
   git remote add origin https://github.com/TU_USUARIO/NUEVO_REPO.git
   git branch -M main
   git push -u origin main
   ```

---

### **Opción 2: Mantener todo el historial de commits**

1. **Clona el repositorio original**

   ```bash
   git clone https://github.com/USUARIO_ORIGINAL/REPO_ORIGINAL.git
   cd REPO_ORIGINAL
   ```

2. **Elimina el remoto anterior**

   ```bash
   git remote remove origin
   ```

3. **Crea un nuevo repositorio en GitHub**

   * Ve a [github.com/new](https://github.com/new) y crea el nuevo repo.

4. **Agrega el nuevo remoto**

   ```bash
   git remote add origin https://github.com/TU_USUARIO/NUEVO_REPO.git
   ```

5. **Haz push de todo el historial**

   ```bash
   git push -u origin main  # o 'master', según tu rama
   ```

---

### **Tabla resumen**

|               | Mantiene historial | Pasos                        |
| ------------- | ------------------ | ---------------------------- |
| Desde cero    | ❌                  | Elimina .git, git init, push |
| Con historial | ✅                  | Cambia el remoto, push       |

---

**Tip:**
Si sólo quieres parte del historial (por ejemplo, una subcarpeta), busca la herramienta [git filter-repo](https://github.com/newren/git-filter-repo).
