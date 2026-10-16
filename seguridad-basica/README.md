# Día 5: Seguridad Básica del Sistema

Objetivos

* Comprender los principios básicos de seguridad en Linux.

* Identificar usuarios y cuentas con acceso privilegiado.

* Verificar el estado de bloqueo de usuarios.

* Revisar puertos y servicios expuestos.

* Administrar reglas básicas de firewall con UFW.

* Comprender el propósito de AppArmor.

* Gestionar actualizaciones de seguridad.

* Aplicar buenas prácticas de endurecimiento (hardening) del sistema.


## Comandos utilizados

getent group sudo → muestra los usuarios pertenecientes al grupo sudo.

grep → filtra información específica dentro de archivos.

cat /etc/shadow → permite revisar el estado de las cuentas y contraseñas.

ss -tulnp → muestra puertos abiertos y procesos asociados.

apt update → actualiza el índice de paquetes.

apt list --upgradable → muestra actualizaciones disponibles.

ufw status → consulta el estado del firewall.

ufw enable → habilita el firewall.

ufw allow → crea reglas de acceso.

ufw deny → bloquea tráfico específico.

ufw status numbered → muestra reglas numeradas.

aa-status → verifica el estado de AppArmor.

last → muestra los últimos inicios de sesión.

lastb → muestra intentos fallidos de acceso.

ls -l /etc/shadow → verifica permisos de archivos sensibles.

-------------------------------------------------------


## Explicación de UFW

UFW (Uncomplicated Firewall) es una herramienta que simplifica la administración del firewall de Linux.


Su función principal es controlar:

- Qué conexiones pueden ingresar al sistema.

- Qué puertos permanecen abiertos.

- Qué direcciones IP pueden acceder a determinados servicios.

## Comandos básicos


## Verificar estado:

sudo ufw status


## Habilitar firewall:



sudo ufw enable


## Permitir SSH:


sudo ufw allow ssh


## Permitir un puerto específico:



sudo ufw allow 8080/tcp


## Bloquear una dirección IP:

sudo ufw deny from 192.168.1.100


## Permitir acceso desde una IP específica:


sudo ufw allow from 192.168.1.100 to any port 22

## Ejemplo práctico

sudo ufw allow from 192.168.1.100 to any port 22


Permite conexiones SSH únicamente desde la dirección IP indicada.

-----------------------------------------------

## Explicación de AppArmor


AppArmor es un sistema de control de acceso obligatorio (MAC) utilizado por Ubuntu para restringir las acciones que pueden realizar las aplicaciones.


Mientras que UFW protege el sistema a nivel de red, AppArmor protege el sistema limitando lo que puede hacer cada proceso.

## Funciones principales

Restringir acceso a archivos y directorios.

Limitar operaciones permitidas a programas específicos.

Reducir el impacto de aplicaciones comprometidas.

## Verificar estado

sudo aa-status

## Modos de operación

Enforce



El perfil se aplica y las acciones prohibidas son bloqueadas.


Complain


El perfil registra las acciones que deberían bloquearse, pero no las impide.


## Comparación entre UFW y AppArmor

Característica	UFW	AppArmorControla red	Sí	No

Controla aplicaciones	No	Sí

Filtra puertos	Sí	No

Limita acciones de procesos	No	Sí

Firewall	Sí	No

Actividades realizadas

Identificación de usuarios con privilegios administrativos.

Revisión de cuentas bloqueadas mediante /etc/shadow.

Consulta de puertos y servicios expuestos utilizando ss -tulnp.

Verificación de actualizaciones disponibles del sistema.

Revisión y habilitación del firewall UFW.

Creación de reglas de acceso mediante puertos y direcciones IP.

Verificación del estado y funcionamiento de AppArmor.

Revisión de registros de inicio de sesión e intentos fallidos de autenticación.

Verificación de permisos sobre archivos sensibles del sistema.

## Evidencia

Salida de getent group sudo.

Salida de ss -tulnp mostrando puertos abiertos.

Salida de apt list --upgradable.

Estado del firewall mediante ufw status.

Reglas configuradas con ufw status numbered.

Estado de AppArmor mediante aa-status.

Registros de acceso obtenidos con last.

Registros de accesos fallidos obtenidos con lastb.

Permisos del archivo /etc/shadow.

## Resultado esperado

Identificar correctamente usuarios con privilegios administrativos.

Detectar cuentas bloqueadas en el sistema.

Reconocer servicios y puertos expuestos.

Comprender el uso básico de UFW para proteger servicios.

Comprender el uso de AppArmor para restringir aplicaciones.

Mantener el sistema actualizado.

Auditar accesos recientes e intentos fallidos.

Verificar la protección de archivos críticos del sistema.

