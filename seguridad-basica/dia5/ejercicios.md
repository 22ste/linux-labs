# Día 5: Seguridad Básica del Sistema

## Ejercicio 1: Identificar usuarios con acceso administrativo

Comandos

sudo getent group sudo

grep sudo /etc/group

## Explicación

Estos comandos permiten identificar qué usuarios pertenecen al grupo sudo y tienen permisos para ejecutar tareas administrativas.


getent group sudo consulta la información del grupo sudo desde la base de datos del sistema.

grep sudo /etc/group muestra directamente la entrada correspondiente al grupo sudo.


## Resultado esperado


Identificar los usuarios con privilegios administrativos.


Ejemplo:

sudo:x:27:labs,alice

---------------------------------------

## Ejercicio 2: Verificar cuentas bloqueadas

## Comandos


sudo cat /etc/shadow | grep '!'


o para un usuario específico:



sudo grep alice /etc/shadow

## Explicación


El archivo /etc/shadow almacena información relacionada con autenticación.


Los símbolos:


!
*
 


normalmente indican cuentas bloqueadas o sin acceso interactivo.


## Resultado esperado


Distinguir entre:


Usuarios activos.

Usuarios bloqueados.

Usuarios sin contraseña configurada.

-------------------------------------------------

## Ejercicio 3: Identificar puertos y servicios expuestos

## Comandos

sudo ss -tulnp

## Explicación


Muestra todos los puertos TCP y UDP que están en estado de escucha junto con el proceso asociado.


Opciones utilizadas:


t → conexiones TCP.

u → conexiones UDP.

l → puertos en escucha.

n → mostrar números en lugar de resolver nombres.

p → mostrar procesos asociados.

## Resultado esperado


Observar puertos abiertos y los programas que los utilizan.


 Ejemplo:



22/tcp ssh

631/tcp cups


Permite detectar servicios expuestos a la red.


----------------------------------------------------

## Ejercicio 4: Verificar actualizaciones de seguridad

## Comandos


sudo apt update
 

sudo apt list --upgradable

## Explicación


Permite actualizar la información de los repositorios y detectar paquetes que tienen nuevas versiones disponibles.


## Resultado esperado


Visualizar software con actualizaciones pendientes.


Ejemplo:



xwayland/noble-updates 2:23.2.6-1ubuntu0.8 amd64

-------------------------------------------------------


## Ejercicio 5: Verificar y habilitar UFW

## Comandos


sudo ufw status
 

sudo ufw enable

## Explicación


UFW (Uncomplicated Firewall) simplifica la administración de reglas de firewall.


Permite controlar:


Tráfico entrante.

Tráfico saliente.

Puertos abiertos.

Acceso por direcciones IP.


## Resultado esperado


Verificar el estado del firewall.


Ejemplo:



Status: active

--------------------------------------------------------------------

## Ejercicio 6: Configurar reglas de firewall

## Comandos


Permitir SSH:



sudo ufw allow ssh


Permitir un puerto específico:

sudo ufw allow 8080/tcp


Permitir acceso desde una dirección IP:



sudo ufw allow from 192.168.1.100 to any port 22


Ver reglas configuradas:



sudo ufw status numbered

## Explicación


Las reglas permiten controlar quién puede acceder a determinados servicios.


Se puede filtrar:


Por puerto.

Por protocolo.

Por dirección IP.

Por red completa.

## Resultado esperado


Visualizar una lista numerada de reglas activas.


Ejemplo:

[1] 22/tcp ALLOW IN 192.168.1.100

[2] 8080/tcp ALLOW IN Anywhere

------------------------------------------------------

## Ejercicio 7: Verificar AppArmor

## Comandos



sudo aa-status


o




apparmor_status


## Explicación


AppArmor implementa control de acceso obligatorio (MAC).


Su función es restringir acciones que las aplicaciones pueden realizar incluso si son comprometidas.


Mientras UFW protege la red, AppArmor protege aplicaciones y procesos.


## Resultado esperado


Ver perfiles activos y procesos protegidos.


Ejemplo:



apparmor module is loaded

XX profiles are loaded

XX profiles are in enforce mode

------------------------------------

## Ejercicio 8: Auditoría básica del sistema

## Parte 1: Revisar últimos accesos



last

## Explicación


Muestra los últimos inicios de sesión y reinicios registrados en el sistema.


## Resultado esperado


Visualizar usuarios conectados anteriormente y fechas de acceso.


## Parte 2: Revisar intentos fallidos



sudo lastb

## Explicación


Muestra intentos fallidos de autenticación.


Resultado esperado


Detectar posibles accesos no autorizados o intentos de fuerza bruta.


## Parte 3: Verificar permisos de archivos sensibles



ls -l /etc/shadow


## Explicación


Verifica quién puede acceder al archivo que almacena los hashes de contraseñas.


## Resultado esperado


Obtener permisos similares a:




-rw-r----- 1 root shadow


## Parte 4: Revisar usuarios con acceso interactivo


cat /etc/passwd


## Explicación


Permite identificar usuarios que pueden iniciar sesión y cuentas de sistema.


## Resultado esperado


Diferenciar entre:



/bin/bash


y



/usr/sbin/nologin


## Parte 5: Revisar servicios expuestos



sudo ss -tulnp
 

## Explicación



Auditar nuevamente los servicios escuchando en la red y validar si son necesarios.


## Resultado esperado


Identificar:


Servicios utilizados.

Puertos abiertos.

Servicios potencialmente innecesarios.


## Conclusión


Durante este laboratorio se practicó:


- Identificación de usuarios privilegiados.

- Verificación de cuentas bloqueadas.

-Revisión de puertos y servicios expuestos.

- Gestión básica de actualizaciones.

- Configuración de reglas de firewall mediante UFW.

- Verificación de perfiles de seguridad mediante AppArmor.

- Auditoría básica de accesos al sistema.

- Revisión de permisos sobre archivos críticos.


Estos ejercicios fortalecen las capacidades de administración y seguridad básica en sistemas Linux.
