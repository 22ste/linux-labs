# Ejercicios Día 1 – Usuarios y Grupos

1. Crear tres usuarios: alice, bob, prueba.
   sudo adduser alice
   sudo adduser bob
   sudo adduser prueba


2. Crear un grupo llamado developers y agregar a alice.
   sudo groupadd developers
   sudo usermod -aG developers alice


3. Verificar pertenencia de alice al grupo.
   id alice
   groups alice


4. Eliminar el usuario prueba.
   sudo deluser prueba


5. Explorar los archivos del sistema.
   cat /etc/passwd
   cat /etc/group
   cat /etc/shadow


6. Crear un archivo y modificar permisos con chmod.
   touch ejemplo.txt
   chmod 744 ejemplo.txt
   ls -l ejemplo.txt


7. Cambiar propietario y grupo de un archivo.
   sudo chown alice ejemplo.txt
   sudo chgrp developers ejemplo.txt
   ls -l ejemplo.txt
