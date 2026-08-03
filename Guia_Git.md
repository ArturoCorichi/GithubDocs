# Guía práctica de Git Bash

> Un mapa visual para entender Git, trabajar con confianza y dominar los comandos más importantes de forma práctica.

## Tabla de contenido

- [Introducción](#introducción)
- [Inicio rápido](#inicio-rápido)
- [Conceptos básicos](#conceptos-básicos)
- [Configuración básica de un repositorio para una persona](#configuración-básica-de-un-repositorio-para-una-persona)
- [Configuración básica de un repositorio para un equipo de desarrollo](#configuración-básica-de-un-repositorio-para-un-equipo-de-desarrollo)
- [Flujos clásicos de trabajo](#flujos-clásicos-de-trabajo)
- [Flujos prácticos adicionales](#flujos-prácticos-adicionales)
- [Flujo diario de trabajo](#flujo-diario-de-trabajo)
- [Glosario completo de comandos de Git Bash](#glosario-completo-de-comandos-de-git-bash)
  - [Configuración y entorno](#configuración-y-entorno)
  - [Repositorios y clonación](#repositorios-y-clonación)
  - [Estado y cambios](#estado-y-cambios)
  - [Historial y revisión](#historial-y-revisión)
  - [Ramas y fusiones](#ramas-y-fusiones)
  - [Remotos y sincronización](#remotos-y-sincronización)
  - [Herramientas avanzadas](#herramientas-avanzadas)
- [Errores comunes](#errores-comunes)
- [Ejemplos prácticos de conflictos de Git](#ejemplos-prácticos-de-conflictos-de-git)
- [Consejos finales](#consejos-finales)

---

## Introducción

> Descripción: presenta Git como una herramienta esencial para guardar, organizar y compartir cambios con orden y seguridad.

Git es mucho más que un sistema de control de versiones: es una forma de pensar en el trabajo colaborativo, la trazabilidad y la evolución de un proyecto. Permite registrar cada cambio, volver a estados anteriores, trabajar en paralelo con otras personas y mantener un historial claro del progreso. Git Bash convierte esa lógica en comandos precisos y repetibles.

Esta guía combina una introducción práctica, ejemplos de flujo de trabajo y un glosario útil para aprender y recordar los comandos más importantes.

---

## Inicio rápido

> Descripción: ofrece una vista inmediata de los comandos que más se utilizan al empezar a trabajar con Git.

Si solo recuerdas unos pocos comandos, empieza con este flujo básico:

```bash
git status
git add .
git commit -m "Descripción del cambio"
git push
```

### Mini guía de uso diario

- `git status`: revisa qué ha cambiado.
- `git add .`: prepara los cambios para guardar.
- `git commit -m "..."`: crea un punto de control con un mensaje claro.
- `git push`: sube los cambios al repositorio remoto.

### Inicio rápido para un nuevo repositorio

```bash
git init
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git status
git add .
git commit -m "Primer commit"
```

---

## Conceptos básicos

> Descripción: explica los pilares de Git para que los comandos tengan sentido.

Antes de memorizar comandos, conviene entender algunos conceptos clave:

- **Working directory**: es la carpeta donde trabajas y editas archivos.
- **Área de preparación o staging**: es el lugar donde eliges qué cambios quieres guardar.
- **Commit**: es un punto de control del historial.
- **Rama**: es una línea de desarrollo independiente.
- **Repositorio remoto**: es la copia del proyecto alojada en GitHub u otro servidor.

Una forma sencilla de imaginarlo es esta:

```text
Archivos en tu carpeta -> git add -> commit -> rama -> push -> GitHub
```

Comprender esto facilita mucho el uso de los comandos posteriores.

---

## Configuración básica de un repositorio para una persona

> Descripción: ideal para proyectos personales, aprendizajes, portafolios o tareas individuales.

### Escenario

Una persona necesita crear un repositorio local y luego compartirlo en GitHub.

### Pasos recomendados

```bash
git init
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git status
git add .
git commit -m "Primer commit"
```

### Subir a GitHub

```bash
git branch -M main
git remote add origin https://github.com/TU_USUARIO/TU_REPOSITORIO.git
git push -u origin main
```

### Resumen visual

- Crear proyecto
- Inicializar Git
- Guardar cambios
- Publicar en GitHub

Este flujo es perfecto para quien empieza a trabajar solo y quiere mantener un historial claro de sus avances.

---

## Configuración básica de un repositorio para un equipo de desarrollo

> Descripción: orientada a equipos pequeños que comparten un proyecto y necesitan trabajar de forma ordenada.

### Escenario

Un equipo necesita un repositorio compartido donde cada miembro trabaje en ramas independientes y luego integre cambios mediante revisiones.

### Pasos recomendados

```bash
git clone https://github.com/ORG/REPO.git
cd REPO
git checkout -b feature/nombre-tarea
git status
git add .
git commit -m "Agregar nueva funcionalidad"
git push -u origin feature/nombre-tarea
```

### Buenas prácticas del equipo

- Crear una rama por tarea o corrección.
- Mantener `main` estable y protegida.
- Usar Pull Requests para revisar cambios.
- Hacer `git pull` antes de empezar a trabajar.

### Resumen visual

- Clonar repo
- Crear rama
- Desarrollar
- Revisar y fusionar

Este modelo reduce conflictos y mejora la colaboración.

---

## Flujos clásicos de trabajo

> Descripción: reúne los modelos más comunes para organizar el trabajo con Git según la complejidad del proyecto.

### 1. GitHub Flow

Es el flujo más simple y recomendado para equipos pequeños o proyectos ágiles.

```text
main -> rama de trabajo -> PR -> merge
```

#### Características

- Ramas cortas y temporales.
- Un Pull Request por cambio.
- Integración continua y despliegues frecuentes.

### 2. Git Flow

Es más estructurado y útil cuando el proyecto requiere versiones, lanzamientos y mantenimiento.

```text
main
  └── develop
        └── feature/*
        └── release/*
        └── hotfix/*
```

#### Características

- Separa desarrollo, liberación y mantenimiento.
- Adecuado para proyectos grandes.
- Requiere más disciplina y organización.

### 3. Trunk-Based Development

Es un modelo más ágil y moderno, ideal para equipos que integran cambios con frecuencia.

```text
main -> cambios pequeños -> integración continua
```

#### Características

- Cambios pequeños y frecuentes.
- Menos tiempo en ramas largas.
- Requiere automatización y buena disciplina.

---

## Flujos prácticos adicionales

> Descripción: recoge escenarios muy comunes en Git para corregir errores, revisar cambios y trabajar con estructuras más complejas.

### 1. Cambio de comentarios de un commit

Cuando un commit ya fue creado y se desea corregir el mensaje:

```bash
git commit --amend -m "Nuevo mensaje de commit"
```

Si el commit ya fue enviado a GitHub y otros colaboradores lo han visto, conviene usar con cuidado.

### 2. Cambio de archivos de un commit

Si se necesita modificar el último commit para incluir o quitar archivos:

```bash
git add archivo_modificado.txt
git commit --amend --no-edit
```

Esto reemplaza el commit anterior por uno nuevo con los cambios ajustados.

### 3. Visualización de diferencias

Para ver lo que cambió entre versiones o archivos:

```bash
git diff
git diff --staged
git diff HEAD~1 HEAD
```

Estas órdenes ayudan a revisar cambios antes de confirmar o fusionar.

### 4. Retorno a una versión previa

Si se necesita volver a un commit anterior:

```bash
git checkout <commit>
```

O de forma más segura en una rama actual:

```bash
git restore --source=<commit> -- <archivo>
```

Para regresar al estado anterior de toda la rama:

```bash
git reset --hard <commit>
```

### 5. Fusión de una rama con la rama principal

Para trabajar en una rama y luego integrar cambios con `main`:

```bash
git checkout main
git pull
git checkout -b feature/nueva-funcion
git merge main
```

Este flujo evita que una rama se quede desactualizada respecto a la rama principal.

### 6. Conflictos de fusión

Cuando dos ramas cambian el mismo archivo, puede aparecer un conflicto:

```bash
git merge feature/rama
```

Si ocurre, se editan los archivos marcados por Git, se resuelven y luego se marcan como listos:

```bash
git add .
git commit -m "Resolver conflicto de merge"
```

Si se desea cancelar:

```bash
git merge --abort
```

### 7. Uso de `stash` como ramas temporales

`stash` sirve para guardar cambios temporales sin hacer commit:

```bash
git stash
git stash list
git stash pop
```

Esto es útil cuando se necesita cambiar de rama o dejar de trabajar un momento sin perder cambios.

### 8. Uso de submodules

Los submodules permiten incluir repositorios dentro de otros repositorios:

```bash
git submodule add https://github.com/usuario/repositorio.git
```

Para inicializar o actualizar:

```bash
git submodule update --init --recursive
```

Este enfoque es útil cuando un proyecto depende de otro proyecto independiente.

---

## Flujo diario de trabajo

> Descripción: muestra el ciclo básico que suele repetirse cada día en un proyecto con Git.

Un flujo básico de trabajo en Git suele seguir este patrón:

```bash
git status
git pull
git add .
git commit -m "Descripción del cambio"
git push
```

Este ciclo representa la lógica central de Git:

- revisar el estado,
- actualizar la base de trabajo,
- preparar los cambios,
- guardar un punto de control,
- compartir el avance con el equipo.

La práctica constante de este flujo convierte a Git en una herramienta natural y esencial para cualquier persona que trabaje con código o archivos versionados.

---

## Glosario completo de comandos de Git Bash

> Descripción: reúne los comandos más importantes, organizados por función para facilitar su consulta.

### Configuración y entorno

| Comando | Descripción |
|---|---|
| `git config --global user.name "Tu Nombre"` | Define el nombre que aparecerá en tus commits. |
| `git config --global user.email "tu@email.com"` | Define el correo asociado a tus commits. |
| `git config --list` | Muestra la configuración actual de Git. |
| `git help <comando>` | Abre la ayuda oficial de Git sobre un comando específico. |
| `git version` | Muestra la versión instalada de Git. |

### Repositorios y clonación

| Comando | Descripción |
|---|---|
| `git init` | Inicializa un nuevo repositorio Git en la carpeta actual. |
| `git clone <url>` | Copia un repositorio remoto a tu máquina local. |
| `git clone <url> <carpeta>` | Clona el repositorio en una carpeta específica. |

### Estado y cambios

| Comando | Descripción |
|---|---|
| `git status` | Muestra el estado de los archivos: modificados, preparados o sin seguimiento. |
| `git add <archivo>` | Agrega un archivo concreto al área de preparación. |
| `git add .` | Agrega todos los cambios de la carpeta actual. |
| `git add -A` | Agrega todos los cambios, incluidas eliminaciones y renombrados. |
| `git commit -m "mensaje"` | Guarda los cambios preparados con un mensaje descriptivo. |
| `git commit --amend` | Modifica el último commit. |
| `git rm <archivo>` | Elimina un archivo del repositorio y del sistema. |
| `git mv <archivo> <nuevo>` | Renombra o mueve un archivo y lo registra en Git. |
| `git restore <archivo>` | Restaura un archivo a su estado anterior. |
| `git restore --staged <archivo>` | Quita un archivo del área de preparación. |
| `git reset <archivo>` | Deshace el seguimiento de un archivo sin eliminarlo físicamente. |
| `git reset --soft HEAD~1` | Deshace el último commit manteniendo los cambios en preparación. |
| `git reset --mixed HEAD~1` | Deshace el último commit y deja los cambios sin preparar. |
| `git reset --hard HEAD~1` | Deshace el último commit y elimina los cambios del trabajo actual. |

### Historial y revisión

| Comando | Descripción |
|---|---|
| `git log` | Muestra el historial de commits. |
| `git log --oneline` | Muestra el historial en una forma más compacta. |
| `git log --graph --decorate --all` | Muestra el historial con un gráfico visual de ramas. |
| `git show <commit>` | Muestra los cambios de un commit concreto. |
| `git diff` | Muestra las diferencias entre cambios no guardados. |
| `git diff --staged` | Muestra las diferencias entre los cambios ya preparados. |
| `git blame <archivo>` | Muestra quién modificó cada línea de un archivo. |
| `git reflog` | Registra cambios de referencia recientes, útil para recuperar commits perdidos. |
| `git shortlog` | Resume los commits por autor. |
| `git grep <texto>` | Busca texto dentro de los archivos del repositorio. |

### Ramas y fusiones

| Comando | Descripción |
|---|---|
| `git branch` | Lista las ramas existentes. |
| `git branch <nombre>` | Crea una nueva rama. |
| `git branch -d <nombre>` | Elimina una rama si ya está fusionada. |
| `git branch -D <nombre>` | Fuerza la eliminación de una rama. |
| `git checkout <nombre>` | Cambia a una rama o commit existente. |
| `git checkout -b <nombre>` | Crea una nueva rama y cambia a ella. |
| `git switch <nombre>` | Cambia a otra rama de manera más clara. |
| `git switch -c <nombre>` | Crea una nueva rama y cambia a ella. |
| `git merge <rama>` | Fusiona los cambios de otra rama en la rama actual. |
| `git merge --abort` | Cancela una fusión en curso. |
| `git rebase <rama>` | Reorganiza los commits aplicándolos sobre otra rama. |
| `git rebase --abort` | Cancela un rebase en curso. |
| `git cherry-pick <commit>` | Aplica un commit específico en otra rama. |
| `git tag` | Lista las etiquetas del repositorio. |
| `git tag <nombre>` | Crea una etiqueta sencilla. |
| `git tag -a <nombre> -m "mensaje"` | Crea una etiqueta anotada. |

### Remotos y sincronización

| Comando | Descripción |
|---|---|
| `git remote -v` | Muestra los remotos configurados y sus URLs. |
| `git remote add origin <url>` | Agrega un repositorio remoto con el nombre `origin`. |
| `git remote rename <viejo> <nuevo>` | Renombra un remoto. |
| `git remote remove <nombre>` | Elimina un remoto. |
| `git remote set-url <nombre> <url>` | Cambia la URL de un remoto. |
| `git fetch` | Descarga cambios del remoto sin fusionarlos. |
| `git pull` | Descarga cambios y los integra en la rama actual. |
| `git pull --rebase` | Actualiza usando rebase en lugar de merge. |
| `git push` | Sube los cambios locales al remoto. |
| `git push -u origin <rama>` | Sube una rama y la configura como seguimiento. |
| `git push --force-with-lease` | Fuerza la subida de cambios cuando se reescriben commits. |

### Herramientas avanzadas

| Comando | Descripción |
|---|---|
| `git stash` | Guarda cambios temporales sin hacer commit. |
| `git stash list` | Muestra los cambios guardados en stash. |
| `git stash apply` | Recupera cambios del stash. |
| `git stash pop` | Recupera cambios y los elimina del stash. |
| `git stash drop` | Elimina un elemento del stash. |
| `git worktree add <ruta> <rama>` | Crea un árbol de trabajo adicional para otra rama. |
| `git submodule add <url>` | Agrega un repositorio dentro de otro como submódulo. |
| `git submodule update --init --recursive` | Inicializa y actualiza submódulos. |
| `git bisect start` | Inicia una búsqueda binaria para encontrar el commit que introdujo un error. |
| `git bisect good` | Marca un commit como bueno durante una búsqueda binaria. |
| `git bisect bad` | Marca un commit como malo durante una búsqueda binaria. |
| `git bisect reset` | Finaliza la búsqueda binaria. |
| `git notes add -m "mensaje"` | Agrega notas a un commit. |
| `git archive --format=zip HEAD` | Crea un archivo comprimido con el estado actual del repositorio. |
| `git clean -fd` | Elimina archivos no rastreados y directorios vacíos. |
| `git fsck` | Verifica la integridad de la base de datos de Git. |
| `git gc` | Optimiza el repositorio limpiando objetos innecesarios. |

---

## Errores comunes

> Descripción: ayuda a identificar problemas frecuentes y a resolverlos con rapidez.

### 1. `fatal: not a git repository`

Se produjo porque la carpeta actual no está inicializada como repositorio.

```bash
git init
```

### 2. `nothing to commit`

Indica que no hay cambios nuevos para guardar.

```bash
git status
```

### 3. `origin already exists`

Ya existe un remoto con ese nombre. Se puede cambiar o eliminar.

```bash
git remote -v
git remote remove origin
```

### 4. `failed to push some refs`

Suele pasar cuando la rama remota tiene cambios que tu copia local no tiene.

```bash
git pull --rebase
git push
```

### 5. Conflicto al hacer merge o pull

Se resuelve editando los archivos marcados por Git, dejando la versión correcta y luego:

```bash
git add .
git commit -m "Resolver conflicto"
```

---

## Ejemplos prácticos de conflictos de Git

> Descripción: presenta ejemplos reales, ordenados del más fácil al más complejo, para generar conflictos y resolverlos con Git de forma práctica.

### 1. Cambio simple en un archivo sin conflicto

#### Generación

```bash
git checkout main
echo "Primera línea" > archivo.txt
git add archivo.txt
git commit -m "Agregar archivo base"
git push origin main
```

#### Resolución

No hay conflicto. Solo basta con confirmar y sincronizar:

```bash
git status
git push origin main
```

### 2. Cambio local y cambio remoto sobre el mismo archivo

#### Generación

```bash
git checkout main
echo "Cambio local" > archivo.txt
git add archivo.txt
git commit -m "Cambio local"
```

En otra copia o desde GitHub, realiza un cambio diferente en el mismo archivo y súbelo.

#### Resolución

```bash
git pull origin main
```

Si aparece un conflicto, edita el archivo, deja el contenido deseado y luego:

```bash
git add archivo.txt
git commit -m "Resolver conflicto de sincronización"
git push origin main
```

### 3. Conflicto al hacer merge entre `main` y una rama

#### Generación

```bash
git checkout main
git checkout -b feature/ejemplo
# Edita archivo.txt en esta rama
git add archivo.txt
git commit -m "Cambio en feature"
git checkout main
# Edita el mismo archivo.txt en main
git add archivo.txt
git commit -m "Cambio en main"
git merge feature/ejemplo
```

#### Resolución

Git mostrará el conflicto. Abre el archivo y elimina los marcadores:

```text
<<<<<<< HEAD
=======
>>>>>>> feature/ejemplo
```

Luego:

```bash
git add archivo.txt
git commit -m "Resolver conflicto de merge"
```

### 4. Conflicto al hacer `pull`

#### Generación

```bash
git checkout main
# Haz un cambio local en archivo.txt
git add archivo.txt
git commit -m "Cambio local"
# En GitHub o en otra copia, cambia el mismo archivo y súbelo
```

#### Resolución

```bash
git pull origin main
```

Si aparece conflicto, resuélvelo manualmente y luego:

```bash
git add archivo.txt
git commit -m "Resolver conflicto al hacer pull"
git push origin main
```

### 5. Conflicto en la misma línea de un archivo

#### Generación

```bash
git checkout main
echo "Versión uno" > archivo.txt
git add archivo.txt
git commit -m "Versión uno"
git checkout -b feature/linea
# Cambia la misma línea a otra versión
git add archivo.txt
git commit -m "Versión dos"
git checkout main
# Cambia la misma línea a una tercera versión
git add archivo.txt
git commit -m "Versión tres"
git merge feature/linea
```

#### Resolución

Edita el archivo conflictivo y deja la versión final deseada. Después:

```bash
git add archivo.txt
git commit -m "Resolver conflicto de línea"
```

### 6. Conflicto con rebase

#### Generación

```bash
git checkout feature/rebase
git rebase main
```

Si ambas ramas modificaron el mismo archivo, Git mostrará un conflicto.

#### Resolución

```bash
git status
git add archivo.txt
git rebase --continue
```

Si deseas cancelar el proceso:

```bash
git rebase --abort
```

### 7. Conflicto por archivo eliminado y modificado

#### Generación

```bash
git checkout main
rm archivo.txt
git add -A
git commit -m "Eliminar archivo"
git checkout -b feature/archivo
# Modifica archivo.txt en esta rama
git add archivo.txt
git commit -m "Modificar archivo"
git checkout main
git merge feature/archivo
```

#### Resolución

Git marcará el conflicto. Decide si conservar el archivo o eliminarlo y luego:

```bash
git add -A
git commit -m "Resolver conflicto por archivo eliminado"
```

### 8. Conflicto avanzado con submodulos o estructuras complejas

#### Generación

```bash
git submodule add https://github.com/usuario/otro-repo.git
```

Luego modifica el submódulo en dos ramas distintas.

#### Resolución

```bash
git status
git submodule update --init --recursive
```

Y resuelve los cambios del submódulo manualmente o con el flujo normal de merge.

### Recomendación de orden para practicar

1. Cambio simple en un archivo sin conflicto
2. Cambio local y cambio remoto sobre el mismo archivo
3. Conflicto al hacer merge entre `main` y una rama
4. Conflicto al hacer `pull`
5. Conflicto en la misma línea de un archivo
6. Conflicto con rebase
7. Conflicto por archivo eliminado y modificado
8. Conflicto avanzado con submodulos

---

## Consejos finales

> Descripción: ofrece recomendaciones para convertir el aprendizaje en una práctica estable y segura.

Aprender Git no consiste solo en memorizar comandos, sino en comprender su lógica. Cada comando representa una decisión: guardar, revisar, mover, fusionar, sincronizar o recuperar. Con la práctica, estos comandos dejan de verse como instrucciones aisladas y se convierten en una forma natural de trabajar con proyectos, equipos y cambios continuos.

La mejor manera de dominar Git es usarlo de forma constante, experimentar con ramas y commits, revisar el historial y preferir flujos claros y fáciles de seguir. En ese sentido, Git Bash no es solo una herramienta técnica: es una disciplina de organización, colaboración y control de cambios.

---

## Cierre

Git Bash transforma el control de versiones en una práctica accesible, potente y esencial. Dominar sus comandos no solo mejora la productividad, sino que también fortalece la capacidad de trabajar con proyectos reales, profesionales y de alto impacto.
