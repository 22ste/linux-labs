# Laboratorio Día 3: Sudo, Umask y ACLs

## Objetivo
Comprender cómo se gestionan los privilegios en Linux mediante `sudo` y el archivo `sudoers`, interpretar el efecto de la máscara de permisos `umask`, y aplicar **Listas de Control de Acceso (ACLs)** para otorgar permisos más granulares a usuarios y grupos.

## Comandos utilizados
- `sudo` → ejecutar comandos con privilegios de superusuario.
- `visudo` → editar de forma segura el archivo `/etc/sudoers`.
- `passwd` → cambiar contraseñas de usuarios.
- `cat /etc/passwd` → visualizar información básica de usuarios.
- `cat /etc/shadow` → revisar contraseñas cifradas y bloqueos.
- `umask` → mostrar o establecer la máscara de permisos por defecto.
- `ls -l` → listar permisos de archivos y directorios.
- `chmod` → modificar permisos tradicionales.
- `chown` → cambiar propietario.
- `chgrp` → cambiar grupo.
- `getfacl` → mostrar ACLs de un archivo o directorio.
- `setfacl` → añadir, modificar o eliminar ACLs.

## Explicación de umask y permisos
- **Permisos básicos**: lectura (r), escritura (w), ejecución (x).
- **Umask**: define qué permisos se eliminan al crear un archivo o directorio.  
  - Ejemplo: `umask 022` → archivos nuevos nacen con `644` (rw-r--r--), directorios con `755` (rwxr-xr-x).
- Valores comunes:
  - `022` → dueño con control total, grupo y otros solo lectura.
  - `002` → dueño y grupo con control total, otros solo lectura.
  - `027` → dueño con control total, grupo con lectura/ejecución, otros sin acceso.
  - `077` → solo el dueño tiene acceso.

## Permisos en números (octal)
Cada número representa un conjunto de permisos para **usuario (dueño), grupo y otros**:

- **7 = rwx** → lectura, escritura y ejecución.  
- **6 = rw-** → lectura y escritura.  
- **5 = r-x** → lectura y ejecución.  
- **4 = r--** → solo lectura.  
- **0 = ---** → sin permisos.  

### Ejemplo: `777`
- Usuario: `rwx`  
- Grupo: `rwx`  
- Otros: `rwx`  

## Actividades realizadas
1. Configuración de privilegios con `sudo` y edición de `/etc/sudoers`.
2. Revisión de bloqueos en `/etc/passwd` y `/etc/shadow`.
3. Práctica con `umask` y creación de archivos para observar permisos iniciales.
4. Uso de `chmod`, `chown` y `chgrp` para modificar permisos y propietarios.
5. Aplicación de ACLs:
   - Añadir permisos específicos a usuarios (`setfacl -m u:alice:rw`).
   - Quitar permisos (`setfacl -x u:alice`).
   - Configurar ACLs heredadas en directorios (`setfacl -d -m u:alice:rwx`).

## Evidencia
- Salida de `ls -l` mostrando permisos iniciales y modificados.
- Capturas de `/etc/passwd` y `/etc/shadow` con cuentas bloqueadas.
- Ejecución de `umask` y verificación de permisos en archivos nuevos.
- Salida de `getfacl` mostrando entradas adicionales para alice.
- Prueba de acceso con alice leyendo y escribiendo en archivos de bob.

## Resultado esperado
- Comprender cómo `sudo` y `sudoers` controlan privilegios administrativos.
- Identificar cómo `umask` afecta la creación de archivos y directorios.
- Aplicar ACLs para otorgar permisos específicos a usuarios adicionales.
- Verificar que los permisos heredados en directorios facilitan la colaboración.

## Qué aprendí
- La diferencia entre permisos tradicionales y ACLs.
- Cómo `umask` define la seguridad por defecto en el sistema.
- Que los privilegios y bloqueos se reflejan en `/etc/passwd` y `/etc/shadow`.
- Que ACLs permiten compartir archivos sin cambiar el dueño ni el grupo.
- Que las ACLs heredadas (`default`) simplifican el trabajo colaborativo en directorios.
