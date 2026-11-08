# Día 6: Archivos, Búsqueda y Auditoría

## Objetivos

Comprender la organización de archivos y directorios en Linux.

Localizar archivos utilizando diferentes herramientas de búsqueda.

Filtrar y analizar información mediante comandos de texto.

Visualizar archivos de diferentes formas según la necesidad.

Monitorear registros y eventos del sistema.

Realizar auditorías básicas utilizando herramientas de búsqueda y análisis.

Interpretar información contenida en logs del sistema.

Combinar comandos para obtener información específica del sistema.

------------------------------------------


# Comandos utilizados

find → búsqueda de archivos y directorios utilizando distintos criterios.

locate → búsqueda rápida mediante una base de datos indexada.

which → localiza la ubicación de un comando ejecutable.

whereis → muestra archivos binarios, código fuente y páginas de manual.

grep → búsqueda y filtrado de texto.

cat → muestra el contenido completo de un archivo.

less → visualiza archivos grandes página por página.

more → visualiza el contenido de archivos por secciones.

head → muestra las primeras líneas de un archivo.

tail → muestra las últimas líneas de un archivo.

tail -f → monitorea archivos en tiempo real.

wc → cuenta líneas, palabras y caracteres.

sort → ordena líneas de texto.

uniq → elimina líneas duplicadas consecutivas.

cut → extrae columnas específicas de un archivo.

journalctl → consulta registros administrados por systemd.

--------------------------------------

## Explicación de búsqueda de archivos

Linux ofrece múltiples herramientas para localizar información dentro del sistema.

## find

Permite realizar búsquedas utilizando múltiples criterios:


find ~ -name "*.txt"

Puede filtrar por:

Nombre

Tamaño

Fecha de modificación

Propietario

Tipo de archivo

Ejemplos:


find ~ -type f

find ~ -type d

find ~ -size +1M

find ~ -mtime -1

## locate

Busca utilizando una base de datos indexada.


locate passwd

Es más rápido que find, pero depende de una base de datos actualizada.


Actualizar base de datos:


sudo updatedb

## which

Localiza únicamente comandos ejecutables.

which bash

which grep

Ejemplo:

/usr/bin/bash


## whereis

Muestra información relacionada con programas.


whereis bash

Ejemplo:


bash: /usr/bin/bash /usr/share/man/man1/bash.1.gz

--------------------------------------

## Explicación de procesamiento de texto

## grep
Permite buscar patrones dentro de archivos.


grep "root" /etc/passwd

Opciones comunes:


grep -i

grep -r

grep -v

## wc

Cuenta información básica:


wc archivo.txt

Permite obtener:


Líneas

Palabras

Caracteres

## sort

Ordena información alfabéticamente.

sort archivo.txt

## uniq

Elimina entradas repetidas.


sort archivo.txt | uniq

## cut

Extrae columnas específicas.


cut -d ":" -f1 /etc/passwd

Visualización de archivos

## cat

Muestra el contenido completo de un archivo.


cat archivo.txt

## less

Permite navegar archivos grandes.


less archivo.txt


Salir:


q

## head

Muestra las primeras líneas.


head archivo.txt

## tail

Muestra las últimas líneas.


tail archivo.txt

Auditoría y monitoreo

tail -f

Monitorea cambios en tiempo real.


tail -f /var/log/syslog

## journalctl

Permite consultar registros almacenados por systemd.

Ejemplos:


journalctl

journalctl -f

journalctl -b

journalctl -u servicio

---------------------------------

## Actividades realizadas

Búsqueda de archivos mediante find.

Búsqueda rápida mediante locate.

Localización de ejecutables utilizando which.

Consulta de información de programas mediante whereis.

Filtrado de información utilizando grep.

Visualización de archivos mediante cat, less, head y tail.

Procesamiento de texto utilizando wc, sort, uniq y cut.

Monitoreo de registros utilizando tail -f y journalctl.

-----------------------------------

##Evidencia

Resultados de búsquedas con find.

Resultados obtenidos mediante locate.

Ubicación de ejecutables usando which.

Información de programas utilizando whereis.

Filtrado de información mediante grep.

Visualización de contenido con cat, head y tail.

Conteo y análisis de información usando wc.

Monitoreo en tiempo real mediante tail -f.

Consulta de registros del sistema utilizando journalctl.

--------------------------------------
## Resultado esperado

Localizar archivos y directorios utilizando distintos criterios.

Encontrar rápidamente programas instalados en el sistema.

Filtrar información relevante dentro de archivos de texto.

Visualizar grandes volúmenes de información de forma eficiente.

Analizar y procesar datos utilizando herramientas de texto.

Monitorear eventos y registros del sistema.

Realizar auditorías básicas de archivos y logs.
