# Ejercicios Día 2 – Permisos Especiales

## chmod avanzado
1. Quitar permisos a grupo y otros:

   chmod g-r ejemplo.txt

   chmod o= ejemplo.txt
   

2. Dar permisos específicos:

   chmod o+r ejemplo.txt

   chmod o+x ejemplo.txt

   chown y chgrp


3. Cambiar propietario y grupo:

   sudo chown alice:developers ejemplo.txt

   ls -l ejemplo.txt


4. Setuid
Crear un script y activar setuid:

   chmod u+s script_uid.sh

   ls -l script_uid.sh


5. Setgid
Crear directorio grupo_demo y activar setgid:

   mkdir grupo_demo

   chmod g+s grupo_demo

   ls -ld grupo_demo


6. Crear archivo dentro y verificar grupo:
cd grupo_demo
touch archivo.txt
ls -l archivo.txt


10. Sticky Bit
Crear directorio sticky_demo y activar sticky bit:
   mkdir sticky_demo
   chmod 777 sticky_demo
   chmod +t sticky_demo
   ls -ld sticky_demo


11. Probar con usuarios distintos (labs y bob):
   cd sticky_demo
   touch archivo_labs.txt

   su bob
   cd /ruta/a/sticky_demo
   touch archivo_bob.txt
   rm archivo_labs.txt   # “Operation not permitted”
