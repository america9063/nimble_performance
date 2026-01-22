Las instrucciones claras. Aquí explicamos el paso del crontab que es mejor hacerlo manualmente o con cuidado.
# Nimble Streamer Performance Tuning (187GB RAM Server)

Este repositorio contiene la configuración óptima para servidores de alto rendimiento con ingesta SRT y 187GB de RAM.

## 📋 Requisitos Previos
* Interfaz de red principal identificada como `eno1` (si se llama `eth0` cámbialo en el paso de Crontab).
* Nimble Streamer ya instalado.

## 🚀 Instrucciones de Instalación

### Paso 1: Descargar y Aplicar Tuning de Sistema
Sube los archivos `nimble.conf` y `optimizar_sistema.sh` a tu servidor.

```bash
chmod +x optimizar_sistema.sh
./optimizar_sistema.sh

# Nimble Streamer Performance Tuning (187GB RAM Server)

Este repositorio contiene la configuración óptima para servidores de alto rendimiento con ingesta SRT y 187GB de RAM.

## 📋 Requisitos Previos
* Interfaz de red principal identificada como `eno1` (si se llama `eth0` cámbialo en el paso de Crontab).
* Nimble Streamer ya instalado.

## 🚀 Instrucciones de Instalación

### Paso 1: Descargar y Aplicar Tuning de Sistema
Sube los archivos `nimble.conf` y `optimizar_sistema.sh` a tu servidor.

```bash
chmod +x optimizar_sistema.sh
./optimizar_sistema.sh

Este script hará lo siguiente:

Configura el Kernel de Linux para aceptar buffers de 32MB.

Reemplaza /etc/nimble/nimble.conf con la versión optimizada.

Reinicia el servicio Nimble.

Paso 2: Configurar la Red (Crontab)
Este paso asegura que la tarjeta de red tenga la cola de transmisión (txqueuelen) ampliada en cada reinicio.

Edita el crontab:
crontab -e
Borra cualquier línea vieja referente a ifconfig o ethtool y agrega/corrige esta línea al final:
@reboot /sbin/ifconfig eno1 txqueuelen 10000
(Nota: Asegúrate de que tu interfaz se llame eno1. Si usas ifconfig y ves eth0, cambia eno1 por eth0 en la línea anterior).

3. Verificación Final
Para confirmar que todo está cargado correctamente:
Verificar Buffers del Sistema:
sysctl net.core.rmem_max
# Debe decir: 33554432

Verificar Configuración de Nimble: Revisa los logs para asegurar que no hay errores de memoria:
cat /var/log/nimble/nimble.log | grep "buffer"

