# Laboratorio Día 1: Usuarios y Grupos

## Objetivo
Aprender a crear, modificar y eliminar usuarios y grupos en Linux, y entender la diferencia entre grupo primario y grupos secundarios.

## Comandos utilizados
- `id`, `groups`, `users`
- `cat /etc/passwd`, `cat /etc/group`, `cat /etc/shadow`
- `adduser`, `deluser`
- `usermod`, `groupadd`, `groupdel`
- `passwd`, `chsh`

## Actividades realizadas
1. Exploración de archivos del sistema:
   - `/etc/passwd`: información básica de usuarios.
   - `/etc/group`: grupos existentes.
   - `/etc/shadow`: contraseñas encriptadas y políticas de expiración.
2. Creación y eliminación de usuarios (`prueba`, `alice`, `bob`).
3. Creación de grupo `developers` y prueba de pertenencia.
4. Verificación de grupo primario en archivos creados (`ls -l prueba.txt`).
5. Observación de grupos secundarios tras reiniciar sesión.
6. Agregar usuario `alice` al grupo `developers`.

## Evidencia
### Usuarios creados en /etc/passwd


## Resultado esperado
- Los archivos creados pertenecen al grupo primario del usuario.
- Los grupos secundarios otorgan permisos adicionales, visibles tras reiniciar sesión.
- El usuario `alice` pertenece al grupo `developers`.

## Qué aprendí
- El grupo primario se asigna automáticamente a los archivos creados.
- Los grupos secundarios permiten ampliar permisos sin cambiar el grupo principal.
- Los archivos `/etc/passwd`, `/etc/group` y `/etc/shadow` son críticos para la administración de usuarios.
