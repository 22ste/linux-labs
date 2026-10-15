
# Día 4: Procesos y Servicios

## Ejercicio 1: Visualización de procesos

Comandos

ps

ps aux

pstree

top



## Explicación


Estos comandos permiten observar los procesos activos en el sistema.


ps muestra los procesos asociados a la terminal actual.

ps aux muestra todos los procesos activos del sistema.

pstree presenta la relación jerárquica entre procesos padre e hijo.

top permite monitorear procesos en tiempo real y observar consumo de CPU y memoria.


## Resultado esperado

Identificar procesos activos.

Reconocer el PID de cada proceso.

Observar consumo de CPU y memoria.

Comprender la relación padre-hijo entre procesos.

------------------------------------------------------------

## Ejercicio 2: Procesos en segundo plano

Comandos

Shell

sleep 300 &

jobs

 

sleep 500

CTRL + Z

 

jobs

bg

fg


## Explicación


Se utilizan procesos de prueba para comprender la ejecución en foreground y background.


& envía un proceso al segundo plano.

jobs lista los trabajos asociados a la sesión actual.

CTRL + Z suspende temporalmente un proceso.

bg reanuda un proceso suspendido en segundo plano.

fg devuelve un proceso al primer plano.


## Resultado esperado


Identificar estados como:


Running

Stopped


y comprender cómo administrar tareas en segundo plano.

---------------------------------------------------------------


## Ejercicio 3: Búsqueda de procesos

Comandos

Shell

pgrep bash

 

pgrep -l bash
 

pidof bash
 

ps aux | grep bash
 

ps -p PID


## Explicación


Permiten localizar procesos específicos mediante nombre o PID.


pgrep busca procesos por nombre.

pidof devuelve el PID asociado a un programa.

grep filtra información proveniente de otros comandos.

ps -p muestra información detallada de un PID específico.


## Resultado esperado

Identificar el PID de un proceso.

Relacionar procesos con sus nombres.

Obtener información detallada de procesos específicos.

----------------------------------------------------------------

## Ejercicio 4: Finalización de procesos

Comandos


sleep 500 &
 

pgrep -l sleep
 

kill PID
 

kill -l
 

kill -9 PID
 

sleep 500 &

sleep 500 &
 

pkill sleep


## Explicación


Permite finalizar procesos utilizando señales de Linux.


kill PID envía la señal SIGTERM.

kill -9 PID envía la señal SIGKILL.

kill -l muestra todas las señales disponibles.

pkill finaliza procesos utilizando el nombre del programa.


## Resultado esperado


Comprender las diferencias entre:




SIGTERM (15)

SIGKILL (9)



y finalizar procesos correctamente.

-------------------------------------------------------


## Ejercicio 5: Estado de servicios

Comandos



systemctl list-units --type=service
 

systemctl status ssh
 

systemctl status NetworkManager
 

systemctl --type=service --state=running
 

systemctl --failed

## Explicación


Permiten consultar el estado de los servicios administrados por systemd.


## Resultado esperado


Identificar servicios:


Identificar el PID principal asociado a un servicio.


active

inactive

failed



------------------------------------------------------------------


## Ejercicio 6: Iniciar, detener y reiniciar servicios

Comandos


sudo systemctl stop servicio
 

sudo systemctl start servicio
 

sudo systemctl restart servicio
 

sudo systemctl reload servicio


## Explicación


Permite administrar servicios del sistema.


start inicia un servicio.

stop detiene un servicio.

restart reinicia un servicio.

reload recarga la configuración sin reiniciar completamente.


## Resultado esperado


Comprender las diferencias entre:



start

stop

restart

reload


y verificar el cambio de estado de los servicios.

----------------------------------------------------------


## Ejercicio 7: Servicios al arranque

Comandos


systemctl is-enabled servicio
 

sudo systemctl disable servicio
 

sudo systemctl enable servicio


## Explicación


Permiten controlar si un servicio se ejecutará automáticamente cuando Linux inicie.



## Resultado esperado


Comprender la diferencia entre:



enabled

disabled


y entre iniciar un servicio manualmente y habilitarlo para el arranque automático.



-----------------------------------------------------

## Ejercicio 8: Análisis de logs con journalctl

Comandos


journalctl
 

journalctl -n 20
 

journalctl -f
 

journalctl -u cron
 

journalctl -p err
 

journalctl -xe
 

journalctl -b


## Explicación


Estos comandos permiten consultar registros del sistema generados por systemd.


journalctl muestra todos los registros.

journalctl -n muestra las últimas entradas.

journalctl -f monitorea registros en tiempo real.

journalctl -u filtra por servicio.

journalctl -p err muestra errores.

journalctl -xe muestra eventos detallados.

journalctl -b muestra registros desde el último arranque.

Resultado esperado

Consultar registros recientes.

Monitorear eventos en tiempo real.

Filtrar registros por servicios.

Identificar errores y eventos relacionados con el arranque del sistema.

-----------------------------------------------------------

# Conclusión



Durante este laboratorio se practicó:


Visualización y monitoreo de procesos.

Administración de procesos en primer y segundo plano.

Búsqueda de procesos mediante PID y nombre.

Finalización de procesos mediante señales.

Administración de servicios utilizando systemctl.

Configuración de servicios al arranque.

Diagnóstico y monitoreo utilizando journalctl.

Estos ejercicios fortalecen las habilidades de administración de sistemas Linux y resolución de problemas relacionados con procesos y servicios.
