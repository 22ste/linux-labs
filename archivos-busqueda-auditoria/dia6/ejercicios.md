# Día 6: Archivos, Búsqueda y Auditoría

# Ejercicio 1: Búsqueda de archivos con find

## Comandos

find ~ -name "*.txt"


find ~ -type d


find ~ -typ* f


find ~ -size +1M


find ~ -mtim* -*

## Explicación

El comando find permite localizar archivos y directorios utilizando diferentes criterios de búsqueda.

-name busca archivos o directorios por nombre.

-type d busca únicamente directorios.

-type f busca únicamente archivos.

-size +1M busca archivos mayores a 1 MB.

-mtime -1 busca archivos modificados durante las últimas 24 horas.

## Resultado esperado

Encontrar archivos específicos por nombre.

Localizar directorios dentro del sistema.

Identificar archivos grandes.

Identificar archivos modificados recientemente.


--------------------------------------------------

# Ejercicio 2: Localización de archivos y comandos

## Comandos

locate passwd

which bash*

which grep

echo $PATH

whereis*bash


whereis grep

## Explicación

Estas herramientas permiten localizar archivos y programas instalados.

locate utiliza una base de datos indexada para realizar búsquedas rápidas.

which muestra la ubicación de un ejecutable

whereis muestra ejecutables, código fuente y páginas de manual asociadas a un programa.

echo $PAH muestra los directorios donde el sistema busca comandos ejecutables.


## Resultado esperado

Localizar archivos rápidamente.

Identificar la ruta de programas ejecutables.

Comprender cómo Linux encuentra comandos que ejecuta.


## Explicación

El comando grep permite buscar patrones de texto dentro de archivos.

grep root /etc/passwd busca todas las líneas que contienen la palabra root.

-i ignora las diferencias entre mayúsculas y minúsculas durante la búsqueda.

-v muestra únicamente las líneas que no coinciden con el patrón especificado.

-r realiza búsquedas recursivas dentro de directorios y subdirectorios.

grep es una de las herramientas más utilizadas en Linux para analizar archivos de configuración, registros del sistema y grandes volúmenes de texto.

------------------------------------------------

--------------------------------------------------

# Ejercicio 4: Visualización de archivos

## Comandos

cat /etc/passwd

less /etc/passwd

head /etc/passwd

tail /etc/passwd

head -n 5 /etc/passwd

tail -n 5 /etc/passwd


## Explicación

Estos comandos permiten visualizar archivos de diferentes maneras según la cantidad de información que se necesite consultar.

cat muestra el contenido completo de un archivo.

less permite navegar por el contenido de un archivo página por página.

head muestra las primeras líneas de un archivo.

tail muestra las últimas líneas de un archivo.

head -n 5 muestra únicamente las primeras cinco líneas del archivo.

tail -n 5 muestra únicamente las últimas cinco líneas del archivo.

Estas herramientas facilitan la revisión de archivos de configuración, registros del sistema y documentos de texto sin necesidad de abrir un editor.

--------------------------------------------------

# Ejercicio 5: Conteo y análisis de información

## Objetivo

Aprender a obtener estadísticas básicas de archivos de texto.

## Comandos

wc /etc/passwd

wc -l /etc/passwd

wc -w /etc/passwd

wc -c /etc/passwd

## Explicación

El comando wc permite obtener estadísticas sobre archivos de texto.

wc muestra la cantidad de líneas, palabras y caracteres de un archivo.

wc -l muestra únicamente el número de líneas.

wc -w muestra únicamente el número de palabras.

wc -c muestra únicamente el número de caracteres.

## Resultado esperado

Obtener la cantidad de líneas contenidas en un archivo.

Determinar el número de palabras presentes en un archivo.

Conocer el número de caracteres de un archivo.

-------------------------------------------------------------------
------------------------------------------------------------------

# Ejercicio 6: Ordenar y eliminar duplicados

## Objetivo

Aprender a organizar información y eliminar datos repetidos.

## Comandos

sort /etc/passwd

cut -d ":" -f1 /etc/passwd

cut -d ":" -f1 /etc/passwd | sort

cut -d ":" -f1 /etc/passwd | sort | uniq

## Explicación

Estos comandos permiten procesar información contenida en archivos de texto.

sort ordena información alfabéticamente.

cut extrae columnas o campos específicos de un archivo.

uniq elimina líneas repetidas.

Las tuberías (|) permiten combinar comandos para procesar información de manera más eficiente.

## Resultado esperado

Ordenar datos alfabéticamente.

Extraer campos específicos de un archivo.

Identificar y eliminar registros duplicados.

Aprendizaje obtenido

Durante este ejercicio se aprendió a combinar herramientas de procesamiento de texto para organizar y analizar información de manera eficiente.

------------------------------------------------------------------------
------------------------------------------------------------------------

# Ejercicio 7: Monitoreo de archivos en tiempo real

## Objetivo

Aprender a supervisar eventos y cambios del sistema en tiempo real.

## Comandos

tail -f /var/log/syslog

journalctl -f

## Explicación

Estos comandos permiten observar información conforme se genera en el sistema.

tail -f monitorea archivos de registro en tiempo real.

journalctl -f muestra nuevos eventos gestionados por systemd.

La opción -f significa follow (seguir), permitiendo visualizar nuevos eventos a medida que ocurren.

## Resultado esperado

Monitorear eventos del sistema en tiempo real.

Observar cambios en archivos de registro.

Detectar errores o eventos importantes conforme ocurren.

--------------------------------------------------------------
--------------------------------------------------------------

# Ejercicio 8: Auditoría básica del sistema

## Objetivo

Aprender a realizar tareas básicas de auditoría utilizando herramientas de búsqueda y análisis de registros.

## Comandos

find /var/log -name "*.log"

journalctl -b

journalctl -* 20

journalctl -p err

find ~ -mt*me -7

## Explicación

Estos comandos permiten localizar registrar importantes y analizar eventos r*cientes del sistema.

find /var*log -name "*.log" busca archivos de registro.


journalctl -b muestra eventos desde el último arranque del sistema.

journalctl -n 20muestra las últimas 20 entradas registradas.

journalctl -p err muestra únicamente mensajes clasificaos como errores.

find ~ -mtime *7 busca archivos modificados durante los últimos siete días.

## Resultado esperado

Identificar registros importantes.

Detectar errores recientes.

Verificar actividad reciente del sistema.

Identificar archivos modificados durante la última semana.


--------------------------------------------------------------------
-------------------------------------------------------------------

# Conclusión

Durante este laboratorio se practicó:


Búsqueda de archivos mediante*find y locate.

Localización de programas utilizando which y whereis.

Filtrado de información mediante grep.

Visualización de archivos utilizando cat, less, head y tail.

Conteo y análisis de información mediante wc. -Organización y procesamiento de daos utilizando sort, cut y uniq.

Monitoreo de archivos y eventos en tiempo real.

Auditoría básica del sistema mediante registros y búsquedas avanzadas.

Estos ejercicios fortalecen las habilidades relacionadas con la administración, el monitoreo, la búsqueda y el análisis de información en sistemas Linux, proporcionando herramientas fundamentales para tareas de soporte técnico, auditoría y gestión de sistemas.

