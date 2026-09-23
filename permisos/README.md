# Laboratorio Día 2: Permisos

## Objetivo
Aprender a visualizar, interpretar y modificar los permisos de archivos y directorios en Linux, comprendiendo el significado de lectura, escritura y ejecución para usuarios, grupos y otros, además de conocer los permisos especiales (setuid, setgid y sticky bit).

## Comandos utilizados
- `ls -l`
- `chmod`
- `chown`
- `chgrp`
- `nano` (para crear scripts)

## Actividades realizadas
1. Creación de archivo `grupo.txt` y verificación de permisos iniciales.
2. Modificación de permisos con `chmod`:
   - `chmod g=r grupo.txt` → quitar escritura al grupo.
   - `chmod o= grupo.txt` → quitar todos los permisos a otros.
   - `chmod o+r grupo.txt` → devolver lectura a otros.
   - `chmod o+x grupo.txt` → dar ejecución a otros.
3. Cambio de grupo con `chgrp compartido grupo.txt`.
4. Cambio de propietario y grupo con `chown alice:compartido grupo.txt`.
5. **Creación de scripts básicos:**
   - Abrir editor: `nano script.sh`.
   - Escribir contenido:
     ```bash
     #!/bin/bash
     echo "Hola desde el script"
     ```
   - Guardar y salir.
   - Dar permisos de ejecución: `chmod u+x script.sh`.
   - Ejecutar: `./script.sh`.
6. **Creación de scripts con variables:**
   - Abrir editor: `nano variables.sh`.
   - Escribir contenido:
     ```bash
     #!/bin/bash
     # Ejemplo de uso de variables en un script

     nombre="Usuario"
     edad=25

     echo "Hola $nombre"
     echo "Tu edad es $edad años"
     ```
   - Guardar y salir.
   - Dar permisos de ejecución: `chmod u+x variables.sh`.
   - Ejecutar: `./variables.sh`.
   - Resultado esperado:
     ```
     Hola Usuario
     Tu edad es 25 años
     ```
7. Exploración de permisos especiales:
   - **Setuid**: `ls -l /usr/bin/passwd` → muestra `-rwsr-xr-x`, permitiendo ejecutar con privilegios del propietario.
   - **Setgid**: `chmod g+s carpeta` → los archivos creados heredan el grupo del directorio.
   - **Sticky bit**: `ls -ld /tmp` → muestra `drwxrwxrwt`, lo que impide que un usuario borre archivos de otro en directorios compartidos.

## Evidencia
- Salida de `ls -l grupo.txt` mostrando cambios de permisos.
- Ejecución de `script.sh`, `saludo.sh`, `saludo_auto.sh` y `variables.sh`.
- Captura de `/usr/bin/passwd` con bit `s`.
- Captura de directorio con `g+s`.
- Captura de `/tmp` mostrando el bit `t`.

## Resultado esperado
- Los permisos definen claramente quién puede leer, escribir o ejecutar un archivo.
- Los permisos especiales permiten ampliar la funcionalidad y seguridad en el sistema.
- Los scripts se ejecutan correctamente tras asignarles permisos de ejecución.
- Los scripts con variables permiten almacenar y reutilizar información dentro del código.

## Qué aprendí
- `chmod` permite ajustar permisos de forma granular para usuario, grupo y otros.
- `chown` y `chgrp` controlan propietario y grupo de archivos.
- Los permisos especiales (`setuid`, `setgid`, `sticky`) son fundamentales para la seguridad en Linux.
- El sticky bit es clave en directorios compartidos como `/tmp`, porque protege los archivos de cada usuario.
- Los scripts requieren permisos de ejecución para poder correr directamente.
- Las variables hacen que los scripts sean dinámicos y más útiles en tareas repetitivas.
