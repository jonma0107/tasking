
# Task CLI - Gestión de Tareas desde la Terminal

Este es un simple gestor de tareas en la terminal que permite agregar, editar, actualizar, eliminar y listar tareas de manera fácil y visualmente atractiva utilizando colores y símbolos. Las tareas se almacenan en un archivo JSON, y el script puede ser ejecutado directamente desde la línea de comandos.

## Instalación

1. **Clonar el repositorio (si es necesario)**:

   Si aún no tienes el archivo `task.py`, simplemente clónalo o crea un archivo llamado `task.py` con el contenido proporcionado.

2. **Colocar el script en `/usr/local/bin/`**:

   Para poder ejecutar el script desde cualquier lugar del sistema, copia el archivo `task.py` en el directorio `/usr/local/bin/` y renómbralo como `task`.

   Para ello, abre una terminal y ejecuta los siguientes comandos:

   ```bash
   sudo cp task.py /usr/local/bin/task
   sudo chmod +x /usr/local/bin/task
   ```

   Esto hará que el script sea ejecutable desde cualquier directorio.

3. **Verificar que se instaló correctamente**:

   Ejecuta el siguiente comando para verificar que el script está disponible globalmente:

   ```bash
   task --help
   ```

   Deberías ver la lista de comandos disponibles.

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
