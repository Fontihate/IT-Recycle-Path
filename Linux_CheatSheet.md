# 🐧 Guía Maestra de Administración Linux

Este repositorio contiene una recopilación estructurada de comandos esenciales para la administración de sistemas, gestión de archivos y automatización en entornos Linux (enfocado en distribuciones Debian/Ubuntu y Red Hat).

---

## 📂 Bloque 1: Navegación y Gestión de Archivos

### Visualización de Contenido
| Comando | Función |
| :--- | :--- |
| `cat <file>` | Muestra el contenido completo (archivos cortos). |
| `tac <file>` | Muestra el contenido en orden inverso (de última a primera línea). |
| `less <file>` | Visualizador interactivo para archivos grandes. Navegación: `/` (buscar), `q` (salir). |
| `head -n <X>` | Muestra las primeras X líneas del archivo. |
| `tail -n <X>` | Muestra las últimas X líneas. Usa `-f` para seguir cambios en tiempo real (logs). |

### Manipulación de Archivos y Directorios
* **Creación:** * `touch <file>`: Crea un archivo vacío o actualiza su timestamp.
    * `mkdir <dir>`: Crea un directorio.
* **Eliminación:**
    * `rmdir <dir>`: Elimina directorio si está vacío.
    * `rm -rf <dir>`: Eliminación recursiva y forzada (usar con precaución).
    * `rm -i <file>`: Modo interactivo (pregunta antes de borrar).
* **Movimiento:**
    * `mv <origen> <destino>`: Sirve tanto para mover como para renombrar.
* **Enlaces (Links):**
    * `ln <orig> <dest>`: Hard link (mismo inodo).
    * `ln -s <orig> <dest>`: Soft/Symbolic link (acceso directo).

### Navegación Avanzada
* `pwd`: Muestra la ruta actual.
* `cd ~`: Ir al Home del usuario.
* `cd -`: Volver al directorio anterior.
* `pushd / popd`: Gestiona directorios en una pila (historial de saltos).
* `dirs`: Muestra la pila de directorios guardados.

---

## 🛠️ Bloque 2: Pipes, Redirección y Búsqueda

### Flujos Estándar y Redirección
1.  **stdin (0)**: Entrada (teclado).
2.  **stdout (1)**: Salida estándar (pantalla).
3.  **stderr (2)**: Salida de errores.

* `>` : Sobrescribe el archivo con la salida.
* `>>` : Añade la salida al final del archivo sin borrar lo anterior.
* `2>` : Redirige solo los errores.
* `&>` o `2>&1` : Une la salida estándar y los errores en un solo flujo.
* `|` (Pipe): Conecta la salida de un comando con la entrada del siguiente.

### Búsqueda y Filtrado
* **`grep`**: El estándar para filtrar texto.
* **`locate`**: Búsqueda rápida mediante base de datos indexada (usar `updatedb` para refrescar).
* **`find`**: Búsqueda potente en tiempo real.
    * `find . -name "*.py"`: Busca archivos Python.
    * `find . -size +10M`: Busca archivos mayores a 10MB.
    * `find . -mtime -1`: Archivos modificados en las últimas 24 horas.
    * `find . -type f -exec chmod 644 {} ';'` : Ejecuta una acción sobre los resultados.

---

## 📦 Bloque 3: Gestión de Paquetes (DEB vs RPM)

| Operación | Debian/Ubuntu (APT) | Red Hat/Fedora (DNF) |
| :--- | :--- | :--- |
| **Instalar** | `sudo apt install <pkg>` | `sudo dnf install <pkg>` |
| **Eliminar** | `sudo apt remove <pkg>` | `sudo dnf remove <pkg>` |
| **Actualizar Repo** | `sudo apt update` | `sudo dnf check-update` |
| **Actualizar Sistema** | `sudo apt dist-upgrade` | `sudo dnf update` |
| **Buscar paquete** | `apt-cache search <name>` | `dnf list "<name>"` |
| **Listar instalados** | `dpkg --list` | `rpm -qa` |
| **¿A quién pertenece el archivo?** | `dpkg --search <file>` | `rpm -qf <file>` |

---

## ⌨️ Comodines (Wildcards)
* `?` : Sustituye a un solo carácter.
* `*` : Sustituye a cualquier cadena de caracteres.
* `[set]` : Coincide con cualquier carácter dentro del corchete.
* `[!set]` : Coincide con cualquier carácter **fuera** del conjunto.
