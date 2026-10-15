# Día 4: Procesos y Servicios
## Objetivos
- Comprender qué es un proceso en Linux.

- Identificar procesos activos en el sistema.

- Administrar procesos en primer plano y segundo plano.

- Finalizar procesos utilizando distintas señales.

- Administrar servicios mediante systemctl.

- Verificar el estado de servicios críticos del sistema.

- Habilitar y deshabilitar servicios durante el arranque.

- Analizar registros del sistema mediante journalctl.

------------------------------------------

## Comandos utilizados

ps → muestra los procesos asociados a la terminal actual.

ps aux → muestra todos los procesos activos en el sistema.


pstree → muestra la jerarquía padre-hijo de los procesos.

top → monitoriza procesos en tiempo real.

jobs → muestra los trabajos asociados a la sesión actual.

bg → reanuda un proceso en segundo plano.


fg → trae un proceso al primer plano.

pgrep → busca procesos por nombre.


pidof → obtiene el PID de un proceso.

grep → filtra resultados de búsqueda.

kill → finaliza procesos mediante PID.

pkill → finaliza procesos mediante nombre.

systemctl → administra servicios del sistema.

journalctl → consulta los registros del sistema.


sleep → genera procesos de prueba para el laboratorio.


-------------------------------------------

## ¿Qué es un proceso?

Un proceso es una instancia de un programa en ejecución. Cada proceso posee:

PID (Process ID).

Usuario propietario.

Consumo de CPU.

Consumo de memoria.

Estado de ejecución.

Estados comunes de un proceso


Running (R) → proceso en ejecución.


Sleeping (S) → proceso esperando recursos o eventos.

Stopped (T) → proceso suspendido.

Zombie (Z) → proceso terminado pero no liberado por su padre.

Foreground y Background

Foreground



## Proceso que controla la terminal.



Ejemplos:



top

nano archivo.txt

sleep 500

Background



## Proceso que se ejecuta en segundo plano permitiendo seguir utilizando la terminal.



Ejemplo:



sleep 500 &

Señales de procesos



## Linux utiliza señales para interactuar con procesos.




Señales más utilizadas

SIGTERM (15) → terminación normal.

SIGKILL (9) → terminación forzada.

SIGSTOP (19) → detener proceso.


SIGCONT (18) → reanudar proceso.

Ejemplos



kill PID



## Finaliza un proceso de forma ordenada.




kill -9 PID


## Fuerza la finalización inmediata.




pkill sleep



## Finaliza todos los procesos llamados sleep.



---------------------------------------------------



## ¿Qué es un servicio?



Un servicio es un programa diseñado para ejecutarse en segundo plano de forma continua y proporcionar funcionalidades al sistema.



Ejemplos:



SSH

Cron

Bluetooth

CUPS


NetworkManager

Gestión de servicios



## Consultar estado:

systemctl status servicio



## Iniciar servicio:

sudo systemctl start servicio



## Detener servicio:


sudo systemctl stop servicio



## Reiniciar servicio:

sudo systemctl restart servicio



## Recargar configuración:

sudo systemctl reload servicio



## Servicios al arranque

Permite que el servicio inicie automáticamente con el sistema.

sudo systemctl enable servicio





## Deshabilitar servicio

Impide que el servicio se ejecute automáticamente durante el arranque.

sudo systemctl disable servicio




## Verificar estado

systemctl is-enabled servicio


Posibles resultados:

enabled

disabled


---------------------------------------------

## Explicación de journalctl


journalctl permite revisar eventos y registros almacenados por systemd.


## Comandos frecuentes




## Mostrar todos los registros:

journalctl



## Mostrar últimas 20 líneas:

journalctl -n 20


## Monitorear en tiempo real:

journalctl -f


## Ver eventos de un servicio:

journalctl -u ssh


## Mostrar errores:

journalctl -p err


## Mostrar errores detallados:

journalctl -xe


## Mostrar registros desde el último arranque:

journalctl -b


---------------------------------------


## Actividades realizadas

Visualización de procesos mediante ps, ps aux, pstree y top.

Identificación de PID de procesos activos.

Creación y administración de procesos en segundo plano mediante &, jobs, bg y fg.

Búsqueda de procesos mediante pgrep, pidof y grep.

Finalización de procesos con kill, kill -9 y pkill.

Análisis de señales utilizadas para controlar procesos.

Consulta de servicios mediante systemctl status.

Inicio, detención y reinicio de servicios.

Habilitación y deshabilitación de servicios al arranque.

Revisión de registros del sistema utilizando journalctl.


-----------------------------------------


## Evidencia

Salidas de ps, ps aux, pstree y top.

Identificación de PID de procesos específicos.

Ejecución de procesos en segundo plano con sleep.


Uso de jobs, bg y fg.

Finalización de procesos utilizando señales.

Verificación del estado de servicios con systemctl.

Habilitación y deshabilitación de servicios.

Consulta de registros mediante journalctl.

Resultado esperado

Comprender cómo Linux administra procesos mediante PID.

Diferenciar procesos en foreground y background.

Administrar procesos utilizando señales.

Identificar y solucionar procesos problemáticos.


Comprender la diferencia entre procesos y servicios.

Administrar servicios mediante systemctl.

Configurar servicios para ejecutarse automáticamente durante el arranque.

Consultar registros del sistema para tareas de monitoreo y diagnóstico.
