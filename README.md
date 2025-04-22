
# Task CLI - Gestión de Tareas desde la Terminal

Este es un simple gestor de tareas en la terminal que permite agregar, editar, actualizar, eliminar y listar tareas de manera fácil y visualmente atractiva utilizando colores y símbolos. Las tareas se almacenan en un archivo JSON, y el script puede ser ejecutado directamente desde la línea de comandos.

## Creación del archivo

El archivo debe guardarse **sin la extensión `.py`**. Esto se hace para que el script se ejecute directamente desde la terminal como un comando, sin necesidad de invocar `python` o `python3`.

### ¿Por qué sin `.py`?
Porque el script en cuestión está diseñado para ser ejecutado como un **comando de terminal** o **script** directamente desde la línea de comandos.

Cuando se le da la extensión `.py`, el sistema operativo podría interpretarlo simplemente como un archivo Python, lo que podría requerir que se ejecutes utilizando explícitamente el comando `python` o `python3`. Por ejemplo:

```bash
python task.py
```
Sin embargo, al nombrar el archivo sin extensión (como simplemente task), lo que buscamos es que se pueda ejecutar directamente desde la terminal como un comando. Esto facilita que se pueda escribir:

```bash
task add "Nueva tarea"
```

y el sistema lo reconozca como un comando ejecutable sin necesidad de especificar python.

## Instalación

1. Guarda el archivo como task sin la extensión .py.  

2. Dale permisos de ejecución al archivo:

   ```bash
   chmod +x task
   ```

   Esto hará que el script sea ejecutable desde cualquier directorio.

3. Mueve el archivo a una carpeta que esté en tu $PATH, como `/usr/local/bin/`, para que puedas ejecutar el comando globalmente desde cualquier lugar en la terminal. Esto es importante porque al mover el archivo a `/usr/local/bin/`, el sistema 
   podrá reconocerlo como un comando ejecutable en la terminal. Para mover el archivo, puedes usar el siguiente comando:

   ```bash
   sudo mv task /usr/local/bin/
   ```
   Asegúrate de que la carpeta /usr/local/bin/ esté incluida en tu $PATH. Esto garantiza que podrás ejecutar el comando task desde cualquier directorio sin tener que especificar la ruta completa del archivo.

   El $PATH es una variable de entorno en los sistemas operativos basados en Unix (como Linux y macOS) que contiene una lista de directorios. Estos directorios son los lugares donde el sistema operativo busca archivos ejecutables cuando ejecutas 
   un comando en la terminal.

   Cuando escribes un comando en la terminal, como task add "Revisar código", el sistema busca el archivo ejecutable llamado task en los directorios que están especificados en tu $PATH. Si el archivo está en uno de esos directorios, el sistema lo 
   ejecutará. Si no está, entonces te mostrará un error diciendo que el comando no fue encontrado.

   ### ¿Cómo verificar el $PATH?
   Puedes verificar qué directorios están en tu $PATH ejecutando el siguiente comando en la terminal:

   ```bash
   echo $PATH
   ```
---

## Comandos Disponibles

### `task add <descripción> [--priority baja|media|alta]`
Agrega una nueva tarea con la descripción proporcionada y la prioridad indicada. Si no se especifica prioridad, se establecerá "media" por defecto.


Ejemplo:
```bash
task add "Revisar daily" --priority alta
```

### `task edit <id> "nueva descripción" [--priority baja|media|alta]`
Edita una tarea existente, actualizando su descripción y/o prioridad. El `id` de la tarea debe ser un número.

Ejemplo:
```bash
task edit 1 "Revisar reunión" --priority baja
```

### `task update <id> todo|in-progress|done`
Actualiza el estado de una tarea existente. Los posibles estados son: `todo`, `in-progress`, `done`.

Ejemplo:
```bash
task update 1 in-progress
```

### `task delete <id>`
Elimina una tarea por su ID.

Ejemplo:
```bash
task delete 1
```

### `task list`
Lista todas las tareas almacenadas.

Ejemplo:
```bash
task list
```

### `task list-todo`
Lista solo las tareas que están en estado `todo`.

Ejemplo:
```bash
task list-todo
```

### `task list-in-progress`
Lista solo las tareas que están en estado `in-progress`.

Ejemplo:
```bash
task list-in-progress
```

### `task list-done`
Lista solo las tareas que están en estado `done`.

Ejemplo:
```bash
task list-done
```

### `task --help`
Muestra la ayuda de los comandos disponibles.

---

## Funciones del Script

### `color(text, code)`
Esta función agrega colores al texto que se muestra en la terminal. Utiliza códigos ANSI para aplicar colores.

- `text`: El texto que quieres mostrar.
- `code`: El código de color ANSI para dar formato.

Ejemplo:
```python
color("Hola Mundo", "31")  # Muestra el texto en rojo
```

### `format_task(task)`
Formato visual para las tareas. Muestra el ID de la tarea, su estado, prioridad, fecha de creación y fecha de última actualización en colores y símbolos.

- `task`: El objeto de la tarea que contiene la información como el ID, estado, descripción, etc.

Ejemplo:
```python
task = {
    "id": 1,
    "description": "Revisar código",
    "status": "todo",
    "priority": "alta",
    "createdAt": "2025-04-20T14:00:00",
    "updatedAt": "2025-04-21T14:00:00"
}
print(format_task(task))
```

### `load_tasks()`
Carga las tareas almacenadas en el archivo JSON. Si no existe el archivo, retorna una lista vacía.

### `save_tasks(tasks)`
Guarda la lista de tareas en el archivo JSON.

### `generate_id(tasks)`
Genera un nuevo ID para la tarea a partir del máximo ID en la lista de tareas existentes. Si no existen tareas, retorna 1.

### `add_task(description, priority="medium")`
Agrega una nueva tarea con la descripción y prioridad especificadas. La prioridad por defecto es "media".

### `edit_task(task_id, new_description=None, new_priority=None)`
Edita una tarea existente. Puedes actualizar su descripción y/o prioridad.

### `list_tasks(filter_status=None)`
Lista todas las tareas o filtra las tareas según el estado proporcionado (`todo`, `in-progress`, `done`).

### `update_status(task_id, status)`
Actualiza el estado de una tarea (por ejemplo, de `todo` a `in-progress` o `done`).

### `delete_task(task_id)`
Elimina una tarea basada en su ID.

### `show_help()`
Muestra los comandos disponibles y su sintaxis.

---

## Ejemplo de Uso

Aquí tienes un ejemplo de cómo interactuar con el gestor de tareas:

1. **Agregar una tarea**:
   ```bash
   task add "Revisar el código" --priority alta
   ```

2. **Ver todas las tareas**:
   ```bash
   task list
   ```

3. **Editar una tarea**:
   ```bash
   task edit 1 "Revisar código y actualizar documentación" --priority media
   ```

4. **Actualizar el estado de una tarea**:
   ```bash
   task update 1 done
   ```

5. **Eliminar una tarea**:
   ```bash
   task delete 1
   ```

6. **Ver solo las tareas en progreso**:
   ```bash
   task list-in-progress
   ```

---

## Licencia

Este proyecto está licenciado bajo la MIT License - consulta el archivo LICENSE para más detalles.
