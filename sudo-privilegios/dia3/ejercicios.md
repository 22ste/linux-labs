# Día 3 – Sudo y Privilegios
## Objetivos
•	Comprender el uso de sudo para ejecutar comandos con privilegios administrativos.
•	Configurar el archivo sudoers utilizando visudo.
•	Agregar usuarios al grupo sudo y verificar sus privilegios.
•	Limitar los comandos que determinados usuarios pueden ejecutar con sudo.
•	Comprender umask y cómo afecta los permisos de archivos y directorios nuevos.
•	Utilizar ACLs para asignar permisos específicos a usuarios.
•	Comprender cómo se reflejan los usuarios, contraseñas y bloqueos en /etc/passwd y /etc/shadow.
________________________________________

# Parte A – Sudo y Sudoers
## 1. Verificar que sudo está instalado
Comando
sudo -V
Resultado esperado
Debe mostrar información sobre la versión instalada de sudo.
¿Por qué?
sudo permite ejecutar determinados comandos con privilegios administrativos sin tener que iniciar sesión directamente como root.
El comando sudo -V permite comprobar que sudo está instalado y disponible en el sistema.
________________________________________

## 2.Agregar un usuario al grupo sudo
En este laboratorio utilizamos alice como ejemplo de usuario con privilegios administrativos completos.
Comandos
sudo usermod -aG sudo alice
groups alice
Resultado esperado
En la salida de groups alice debe aparecer el grupo:
sudo
¿Por qué?
El comando:
sudo usermod -aG sudo alice
agrega a alice al grupo sudo.
Las opciones significan:
•	usermod → modifica la configuración de un usuario.
•	-a → agrega sin eliminar los grupos existentes.
•	-G sudo → agrega al grupo sudo.
El segundo comando:
groups alice
sirve para comprobar que alice pertenece al grupo.
________________________________________
## 3. Configurar sudoers con visudo
Para modificar las reglas de sudo utilizamos:
sudo visudo
visudo es la forma recomendada de editar sudoers porque comprueba la sintaxis antes de guardar los cambios.
En el archivo encontramos una sección similar a:
# User privilege specification
root ALL=(ALL:ALL) ALL

## Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

## Allow members of group sudo to execute any command
%sudo ALL=(ALL:ALL) ALL
También podemos agregar una regla específica para un usuario.
Para alice:
alice ALL=(ALL) ALL
¿Qué significa?
alice ALL=(ALL) ALL
Significa que alice puede utilizar sudo para ejecutar cualquier comando como cualquier usuario autorizado, incluyendo root.
La estructura general es:
usuario   host=(usuario_destino)   comandos
________________________________________

## 4. Crear un usuario con privilegios restringidos
Para demostrar que sudo no necesariamente tiene que proporcionar acceso completo, utilizamos bob.
En sudoers agregamos:
bob ALL=(ALL) /bin/ls, /bin/cat
¿Qué significa?
bob solamente podrá utilizar sudo para ejecutar:
/bin/ls
/bin/cat
No significa que bob solamente pueda usar ls y `cat normalmente.
La restricción se aplica específicamente cuando utiliza sudo.
Por ejemplo:
ls
cat archivo.txt
son comandos normales de bob.
Pero:
sudo ls /etc
sudo cat /etc/passwd
utilizan los privilegios definidos en sudoers.
________________________________________

## 5. Ejecutar un comando como otro usuario
Podemos utilizar:
sudo -u bob whoami
Resultado esperado
bob
¿Por qué?
La opción -u indica que queremos ejecutar el comando como otro usuario.
En este caso:
sudo -u bob whoami
ejecuta whoami como bob.
________________________________________

## 6. Verificar los privilegios de un usuario
Para consultar los privilegios del usuario actual:
sudo -l
También podemos consultar los privilegios de un usuario específico:
sudo -l -U alice
sudo -l -U bob
¿Por qué?
Esto permite comprobar las reglas que sudo tiene configuradas para cada usuario.
En nuestro laboratorio:
•	alice tiene acceso administrativo completo.
•	bob tiene acceso restringido a determinados comandos.
________________________________________
## 7. Probar los privilegios de Alice
Entramos como alice:
su - alice
Después:
sudo whoami
Resultado esperado
root
¿Por qué?
Aunque el comando se ejecuta desde la sesión de alice, sudo permite ejecutarlo con privilegios de root.
Esto demuestra que alice tiene privilegios administrativos.
________________________________________
## 8. Probar los privilegios restringidos de Bob
Entramos como bob:
su - bob
Probamos:
sudo ls /etc
y:
sudo cat /etc/passwd
Estos comandos deben funcionar porque están incluidos en la regla de sudoers.
Después probamos:
sudo apt update
Resultado esperado
Debe ser rechazado porque apt no está incluido en los comandos autorizados para bob.
¿Por qué?
Aquí podemos observar la diferencia entre:
Usuario con privilegios completos
y:
Usuario con privilegios restringidos
Bob puede utilizar normalmente los comandos que tenga permitidos como usuario, pero sudo limita los comandos que puede ejecutar con privilegios administrativos.
________________________________________
## 9. Crear y trabajar con archivos como Bob
Durante la práctica, Bob creó:
ls -l
Resultado observado:
-rw-rw-r-- 1 bob bob 0 ... example_bob
También pudo editarlo con:
nano example_bob
¿Por qué puede hacerlo si Bob tiene sudo restringido?
Porque la restricción de sudoers no elimina los permisos normales de Bob.
Bob sigue siendo un usuario normal y puede trabajar dentro de su propio directorio /home/bob.
Por eso puede:
ls
nano example_bob
sin utilizar sudo.
La restricción aparece cuando intenta utilizar:
sudo <comando>
________________________________________

# Parte B – /etc/passwd y /etc/shadow
## 10. Revisar la información de un usuario en /etc/passwd
Podemos consultar la entrada de alice:
grep alice /etc/passwd
También:
grep bob /etc/passwd
Ejemplo
Una entrada puede verse así:
alice:x:1001:1001:Alice:/home/alice:/bin/bash
Los campos representan:
usuario
x
UID
GID
información
directorio HOME
shell
¿Por qué?
/etc/passwd contiene información básica de las cuentas del sistema.
La x indica que la información de autenticación no está almacenada directamente allí, sino que se encuentra en /etc/shadow.
________________________________________

## 11. Revisar /etc/shadow
Para consultar la información de autenticación:
sudo grep alice /etc/shadow
También podemos consultar:
sudo grep bob /etc/shadow
¿Por qué se utiliza sudo?
/etc/shadow contiene información sensible relacionada con las contraseñas y políticas de autenticación, por lo que normalmente no puede ser leído por un usuario normal.
________________________________________

## 12. Identificar una cuenta bloqueada
En /etc/shadow, el campo de contraseña permite identificar determinadas situaciones.
Por ejemplo:
bob:!:19200:0:99999:7:::
El carácter:
!
al comienzo del campo de contraseña indica que la cuenta está bloqueada.
También podemos encontrar:
!!
o:
*
dependiendo del estado de la cuenta.
Cuenta con contraseña activa
Una entrada puede contener un hash, por ejemplo:
alice:$6$....
El $6$ es un indicador del tipo de hash utilizado.
¿Por qué es importante?
Esto permite relacionar la existencia de una cuenta con su estado de autenticación.
Un usuario puede existir en:
/etc/passwd
pero tener su acceso bloqueado según el estado reflejado en:
/etc/shadow
________________________________________

# Parte C – Umask
## 13. Consultar el umask actual
Comando:
umask
Resultado esperado
Puede aparecer algo como:
0022
o:
0002
¿Qué es umask?
umask es una máscara que determina qué permisos se eliminan de los permisos iniciales cuando se crea un archivo o directorio nuevo.
No modifica archivos que ya existen.
________________________________________

## 14. Cambiar temporalmente el umask
Utilizamos:
umask 027
Después creamos un archivo:
touch archivo_umask.txt
Y comprobamos sus permisos:
ls -l archivo_umask.txt
Resultado esperado
Con umask 027, un archivo nuevo normalmente queda:
-rw-r-----
que corresponde a:
640
¿Por qué?
Los archivos parten de una base de:
666
y los directorios de:
777
El umask elimina permisos de esa base.
Por eso:
666 → archivo
027 → umask
640 → resultado
________________________________________

## 15. Permisos en números (octal)
Esta tabla sirve como referencia rápida:
7 = rwx  lectura + escritura + ejecución
6 = rw-  lectura + escritura
5 = r-x  lectura + ejecución
4 = r--  lectura
0 = ---  ningún permiso
Los tres números representan:
usuario | grupo | otros
Por ejemplo:
755
significa:
7 = rwx
5 = r-x
5 = r-x
Por lo tanto:
rwxr-xr-x
________________________________________

## Ejemplos de umask
umask 022
Archivos:
666 - 022 → 644
rw-r--r--
Directorios:
777 - 022 → 755
rwxr-xr-x
umask 027
Archivos:
666 - 027 → 640
rw-r-----
Directorios:
777 - 027 → 750
rwxr-x---
Otros valores comunes son:
022
002
027
077
El valor elegido depende del nivel de acceso que se quiera permitir por defecto.
________________________________________

# Parte D – ACLs
## 16. ¿Qué son las ACLs?
ACL significa:
Access Control List
Los permisos tradicionales de Linux trabajan principalmente con:
usuario propietario
grupo propietario
otros
Las ACL permiten agregar permisos específicos para usuarios o grupos adicionales sin cambiar el propietario del archivo.
Los comandos principales que utilizamos son:
getfacl
setfacl
________________________________________

## 17. Revisar la ACL de example_bob
El archivo utilizado en la práctica pertenece a bob.
Desde root podemos consultar:
sudo getfacl /home/bob/example_bob
Inicialmente podemos encontrar algo similar a:
# owner: bob
# group: bob
user::rw-
group::rw-
other::r--
¿Por qué?
getfacl muestra los permisos tradicionales y cualquier ACL adicional que exista.
________________________________________

## 18. Dar permisos de lectura y escritura a Alice
Agregamos una ACL específica:
setfacl -m u:alice:rw /home/bob/example_bob
Si estamos trabajando desde root, podemos utilizar:
sudo setfacl -m u:alice:rw /home/bob/example_bob
¿Qué significa?
-m
modifica la ACL.
u:alice:rw
significa:
usuario:alice
permisos: lectura + escritura
Por lo tanto, estamos diciendo:
Alice puede leer y modificar este archivo aunque no sea su propietaria.
Verificamos:
sudo getfacl /home/bob/example_bob
Ahora debe aparecer:
user:alice:rw-
________________________________________

## 19. Problema con el directorio /home/bob
Durante la práctica ocurrió algo importante.
Aunque example_bob tenía:
user:alice:rw-
Alice todavía podía recibir:
Permission denied
¿Por qué?
Porque para llegar hasta:
/home/bob/example_bob
Alice necesita permisos de ejecución x sobre el directorio:
/home/bob
En un directorio, x permite atravesarlo/acceder a los elementos que contiene.
Por eso agregamos:
sudo setfacl -m u:alice:rx /home/bob
Y verificamos:
sudo getfacl /home/bob
Debe aparecer:
user:alice:r-x
¿Qué significa el -?
r-x
se divide en:
r = lectura
- = sin escritura
x = ejecución/entrada
Por lo tanto, Alice puede acceder al directorio, pero no puede modificar su contenido directamente.
________________________________________

## 20. Probar el acceso de Alice al archivo de Bob
Cambiamos a Alice:
su - alice
Probamos lectura:
cat /home/bob/example_bob
Después escritura:
echo "Hola desde alice" >> /home/bob/example_bob
Resultado esperado
Alice puede leer y modificar example_bob.
¿Por qué?
Se combinaron dos permisos:
En el archivo:
user:alice:rw-
En el directorio:
user:alice:r-x
Alice puede llegar al archivo gracias a r-x en el directorio y puede leer/escribir el archivo gracias a rw-.
________________________________________

## 21. Quitar una ACL
Para eliminar el permiso específico de Alice:
sudo setfacl -x u:alice /home/bob/example_bob
Después podemos verificar:
sudo getfacl /home/bob/example_bob
¿Por qué?
La opción:
-x
elimina una entrada específica de la ACL.
En este caso eliminamos:
user:alice
________________________________________

# Parte E – ACLs en directorios
## 22. Crear un directorio de proyectos
Creamos un directorio dentro del HOME de Bob:
sudo mkdir /home/bob/proyectos
Podemos asignarle permisos para Alice:
sudo setfacl -m u:alice:rwx /home/bob/proyectos
Verificamos:
sudo getfacl /home/bob/proyectos
Debe aparecer:
user:alice:rwx
¿Por qué?
Ahora Alice tiene:
r = puede leer/listar
w = puede crear, modificar o eliminar elementos según el contexto
x = puede entrar al directorio
Esto permite utilizar el directorio como un espacio compartido.
________________________________________

## 23. Probar el directorio con Alice
Cambiamos a Alice:
su - alice
Entramos al directorio:
cd /home/bob/proyectos
Creamos un archivo:
touch archivo_alice.txt
Escribimos contenido:
echo "ACL en directorios" > archivo_alice.txt
Y lo comprobamos:
cat archivo_alice.txt
Resultado esperado
Alice puede crear, modificar y leer archivos dentro del directorio gracias a la ACL:
user:alice:rwx
________________________________________

# Parte F – ACLs heredadas
## 24. Crear una ACL heredada
Una ACL normal afecta al directorio actual.
Una ACL default permite establecer permisos que serán heredados por nuevos elementos creados dentro del directorio.
Primero damos permisos actuales:
sudo setfacl -m u:alice:rwx /home/bob/proyectos
Después configuramos la ACL heredada:
sudo setfacl -d -m u:alice:rwx /home/bob/proyectos
¿Qué significa -d?
La opción:
-d
indica que estamos trabajando con una ACL por defecto (default ACL).
La finalidad es que los nuevos archivos y directorios creados dentro de proyectos hereden una configuración de permisos para Alice.
________________________________________

## 25. Verificar la ACL heredada
Ejecutamos:
sudo getfacl /home/bob/proyectos
Ahora debemos observar dos tipos de información:
user:alice:rwx
y una sección:
default:
con una entrada para Alice.
¿Por qué?
La primera ACL corresponde a los permisos actuales del directorio.
La ACL default funciona como una configuración que se utilizará para los nuevos elementos creados dentro del directorio.
________________________________________

## 26. Probar la ACL heredada
Cambiamos a Alice:
su - alice
Entramos:
cd /home/bob/proyectos
Creamos un archivo:
touch archivo_alice.txt
Escribimos:
echo "ACL heredada" > archivo_alice.txt
Y comprobamos:
cat archivo_alice.txt
También podemos revisar la ACL:
getfacl archivo_alice.txt
Resultado esperado
El archivo nuevo debe tener una ACL relacionada con Alice debido a la configuración default del directorio.
¿Por qué?
La ACL heredada evita tener que configurar manualmente los permisos de Alice cada vez que se crea un archivo nuevo dentro del directorio compartido.
________________________________________

# Resumen del Día 3
En este laboratorio se practicó la administración de privilegios y permisos avanzados en Linux.
Sudo y sudoers
Aprendimos a:
sudo -V
sudo usermod -aG sudo alice
sudo visudo
sudo -l
sudo -l -U alice
sudo -l -U bob
También diferenciamos:
•	alice → usuario con privilegios administrativos completos.
•	bob → usuario con privilegios sudo restringidos.
/etc/passwd y /etc/shadow
Aprendimos que:
/etc/passwd
contiene información básica de las cuentas.
Mientras que:
/etc/shadow
contiene información relacionada con autenticación y políticas de contraseña.
También aprendimos a reconocer estados de bloqueo mediante caracteres como:
!
!!
*
en el campo correspondiente de /etc/shadow.
Umask
Aprendimos que umask controla los permisos que se eliminan de los permisos iniciales al crear nuevos archivos y directorios.
Ejemplos:
umask 022
archivo → 644
directorio → 755

umask 027
archivo → 640
directorio → 750
ACLs
Aprendimos a utilizar:
getfacl
setfacl
para asignar permisos específicos a usuarios.
Ejemplo:
setfacl -m u:alice:rw archivo
También vimos que una ACL sobre un archivo no siempre es suficiente: el usuario necesita poder atravesar los directorios que llevan hasta ese archivo.
Finalmente practicamos ACLs en directorios y ACLs heredadas mediante:
setfacl -d
________________________________________

# Comandos principales aprendidos
sudo -V
sudo usermod -aG sudo alice
groups alice
sudo visudo
sudo -u bob whoami
sudo -l
sudo -l -U alice
sudo -l -U bob

grep alice /etc/passwd
sudo grep alice /etc/shadow

umask
umask 027
touch archivo_umask.txt
ls -l archivo_umask.txt

getfacl /home/bob/example_bob
setfacl -m u:alice:rw /home/bob/example_bob
setfacl -x u:alice /home/bob/example_bob

sudo setfacl -m u:alice:rx /home/bob
sudo getfacl /home/bob

sudo mkdir /home/bob/proyectos
sudo setfacl -m u:alice:rwx /home/bob/proyectos
sudo getfacl /home/bob/proyectos

sudo setfacl -d -m u:alice:rwx /home/bob/proyectos
Conceptos clave
sudo       → ejecutar comandos con privilegios elevados
sudoers    → define qué puede hacer cada usuario mediante sudo
umask      → controla permisos por defecto de archivos/directorios nuevos
ACL        → permite permisos específicos para usuarios o grupos
getfacl    → consultar ACLs
setfacl    → modificar ACLs
passwd     → información básica de usuarios
shadow     → información sensible de autenticación

## Día 3 completado: Sudo y Privilegios.
