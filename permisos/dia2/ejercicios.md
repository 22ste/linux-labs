# Ejercicios Día 2 – Permisos Especiales

## Ejercicio 1: Quitar permisos a grupo y otros

chmod g-r ejemplo.txt

chmod o= ejemplo.txt


Explicación:

g-r quita el permiso de lectura al grupo.

o= elimina todos los permisos para “otros”.


Resultado esperado:  
El archivo ya no puede ser leído ni accedido por usuarios fuera del propietario.

---------------------------------------------

## Ejercicio 2: Dar permisos específicos

chmod o+r ejemplo.txt

chmod o+x ejemplo.txt



Explicación:

o+r da permiso de lectura a otros.

o+x permite ejecución a otros.



Resultado esperado:  
El archivo puede ser leído y ejecutado por cualquier usuario, pero no modificado.

----------------------------------------------

## Ejercicio 3: Cambiar propietario y grupo

sudo chown alice:developers ejemplo.txt
ls -l ejemplo.txt



Explicación:

chown alice:developers asigna a alice como propietaria y al grupo developers.

ls -l muestra el cambio en la columna de propietario y grupo.


Resultado esperado:  
El archivo pertenece a alice y al grupo developers.

-------------------------------------------------

## Ejercicio 4: Setuid
chmod u+s script_uid.sh

ls -l script_uid.sh

Explicación:  

El bit SUID hace que el script se ejecute con los permisos del propietario, no del usuario que lo corre.


Resultado esperado:  

El permiso aparece como -rwsr-xr-x (la s en lugar de la x del propietario).

-------------------------------------------------

## Ejercicio 5: Setgid
mkdir grupo_demo

chmod g+s grupo_demo

ls -ld grupo_demo

Explicación:  

El bit SGID en un directorio hace que los archivos creados dentro hereden el grupo del directorio.


Resultado esperado:  

El permiso aparece como drwxr-sr-x.

Al crear un archivo dentro, su grupo será automáticamente developers.

--------------------------------------------------------

## Ejercicio 6: Sticky Bit
mkdir sticky_demo

chmod 777 sticky_demo

chmod +t sticky_demo

ls -ld sticky_demo

Explicación:  

El Sticky Bit evita que un usuario borre archivos de otros dentro de un directorio compartido.


Resultado esperado:  

El permiso aparece como drwxrwxrwt.

Solo el propietario de un archivo puede borrarlo, aunque otros tengan permisos de escritura.

---------------------------------------------

## Ejercicio 7: Prueba con usuarios distintos
cd sticky_demo

touch archivo_labs.txt


su bob

cd /ruta/a/sticky_demo

touch archivo_bob.txt

rm archivo_labs.txt   # “Operation not permitted”

Explicación:  

El usuario bob puede crear su propio archivo, pero no puede borrar el archivo creado por labs.




Resultado esperado:  

El sistema devuelve el error:

Code
rm: cannot remove 'archivo_labs.txt': Operation not permitted

-------------------------------------------

## Ejercicio dia 2 Completado
