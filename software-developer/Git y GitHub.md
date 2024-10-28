
## **Comandos básicos en Git**

### **¿Qué es el staging?**

Es el `area de prepracion` es un espacio intermedio entre el directorio de trabajo y el repositorio de `git` Es el lugar donde se preparan los cambios y puedes revisarlos antes de confirmar definitivamente el commit `git commit`

Los cambio que se hacen en tu directorio de trabajo, Git no los registra automáticamente se tiene que ejecutar el comando `git add` para registrar los cambios en el área de preparación, siendo esta una lista de cambios que estarán incluidos en el próximo commit

Si ejecutas el siguiente comando, estarás confirmando tus cambios hacia el repositorio remoto

```bash
git commit -m "pasando de **staging a repositorio remoto**"
```

Al hacer `commit` creas una nueva versión del archivo, para traer todos loa cambios del archivo hechos por otro desarrollador solo debes ejecutar 

```bash
git checkout
```

![[Untitled.png]]

### **¿Qué es branch (rama) y cómo funciona un Merge en Git?**

Una `branch` en una versión separada del proyecto en la cual puedes modificar o experimentar sin afectar el proyecto el resto

**Branch (Rama):**

- Creación de una rama:
    
    Generalmente en un proyecto se crean las ramas de
    
    - `main`: la rama principal utilizado para producción
    - `development`: la rama de desarrollo
    - `hotfix`: la rama de bugs
    
    ```bash
    git branch <nombre de la rama>
    ```
    
- Cambiar ramas o navegar entre ramas
    
    ```bash
    git checkout <nombre rama>
    ```
    

**Merge (Combinación):**

Un merge es básicamente la unión de una rama con otra, por decir desde la rama de `desarrollo` una vez culminado todo el trabajo se hace un merge hacia la rama principal `main`

### **Pasos para realizar un Merge:**

1. **Cambiar a la Rama Destino**: Primero, te mueves a la rama donde deseas aplicar los cambios con **`git checkout rama-destino`**.
2. **Merge de la Otra Rama**: Luego, ejecutas **`git merge rama-a-mergear`** para fusionar los cambios de la rama **`rama-a-mergear`** en la rama actual.
3. **Resolver Conflictos (si los hay)**: En caso de conflictos, Git te pedirá resolverlos manualmente antes de completar el merge.
4. **Commit del Merge**: Después de resolver los conflictos (si los hubiera), realizas un commit para aplicar el merge.

### **Volver en el tiempo en nuestro repositorio utilizando `reset` y `checkout`**

`git reset` te permite deshacer o revertir los cambios en el repositorio de git, es decir volver al pasado sin la posibilidad de volver al futuro

![[Untitled 1.png]]

- **`Soft Reset`**: Borra el historial y los registros de Git de commits anteriores, pero guarda los cambios en Staging para aplicar las últimas actualizaciones a un nuevo commit.
    
    ```bash
    **git reset --soft <commit>**
    ```
    
- **`Mixed Reset`: Borra todo, exactamente todo. Toda la información de los commits y del área de staging se elimina del historial.**
    
    ```bash
    **git reset --mixed <commit>**
    ```
    
- **`Hard Reset`**: Deshace todo, absolutamente todo. Toda la información de los commits y del área de staging se elimina del historial.
    
    ```bash
    **git reset --hard <commit>**
    ```
    

`git checkout` te permite moverte a diferentes `ramas` o `commits`, es decir como un viajero del tiempo que pasea por diferentes líneas de tiempo (ir, mirar, pasear y volver)

- **Cambiar de Rama:**
    
    ```bash
    **git checkout <nombre-de-la-rama>**
    ```
    
- **Moverte a un Commit :**
    
    ```bash
    **git checkout <commit-hash>**
    ```
    

### **¿Qué es git reset HEAD?**

`git reset HEAD` es un comando que nos permite revertir los cambios ya preparados para subir al repositorio

### Git rm

`git rm` es un comando que nos ayuda a eliminar archivos de Git sin eliminar su historial del sistema de versiones

- `git rm —cached`: Elimina archivos del repositorio local y del área de `staging`
- `git rm —force` : Elimina los archivos de Git y del disco duro

### **¿Cuál es la diferencia entre** `git rm` **y** `git reset` **Head?**

La diferencia principal entre `git rm` y `git reset HEAD` radica en que `git rm` elimina archivos del repositorio y de la historia del proyecto, mientras que `git reset` saca los cambios del área de preparación y los mueve del espacio de trabajo, sin afectar la historia del repositorio.

![[Untitled 2.png]]

### **¿Cuándo utilizar `git reset` en lugar de `git revert`?**

Para reescribir la historia del repositorio y eliminar confirmaciones anteriores, se utiliza `git reset`. Para deshacer cambios de confirmaciones anteriores de forma segura sin modificar la historia del repositorio, se emplea `git revert`.

![[Untitled 3.png]]


`git log`

1. `git log --oneline` - Te muestra el id commit y el título del commit.
2. `git log --decorate`- Te muestra donde se encuentra el head point en el log.
3. `git log --stat` - Explica el número de líneas que se cambiaron brevemente.
4. `git log -p`- Explica el número de líneas que se cambiaron y te muestra que se cambió en el contenido.
5. `git shortlog` - Indica que commits ha realizado un usuario, mostrando el usuario y el titulo de sus commits.
    1. `git log --graph --oneline --decorate` 
    - **`--graph`**: Agrega una representación gráfica del historial de commits, mostrando las ramificaciones y fusiones.
    - **`--oneline`**: Presenta cada commit en una única línea, lo que hace que la salida sea más concisa y fácil de leer.
    - **`--decorate`**: Muestra referencias como nombres de ramas (**`branch names`**) o etiquetas (**`tags`**) junto a los commits correspondientes.
6. `git log --pretty=format:"%cn hizo un commit %h el dia %cd"` - Muestra mensajes personalizados de los commits.
7. `git log -3` - Limitamos el número de commits.
8. `git log --after=“2018-1-2”` ,
9. `git log --after=“today”` y
10. `git log --after=“2018-1-2” --before=“today”` - Commits para localizar por fechas.
11. `git log --author=“Name Author”` - Commits realizados por autor que cumplan exactamente con el nombre.
12. `git log --grep=“INVIE”` - Busca los commits que cumplan tal cual está escrito entre las comillas.
13. `git log --grep=“INVIE” –i` - Busca los commits que cumplan sin importar mayúsculas o minúsculas.
14. `git log – index.html` - Busca los commits en un archivo en específico.
15. `git log -S “Por contenido”`- Buscar los commits con el contenido dentro del archivo.
16. `git log > log.txt` - guardar los logs en un archivo txt

## **Flujo de trabajo básico en Git**

### **Flujo de trabajo básico con un repositorio remoto**