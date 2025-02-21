---
title: 'Guía Completa de Kali Linux: Instalación, Comandos Básicos y Ejemplos de Ataques'
categories:
- Hacking ético
- Herramientas
tags:
- Hacking
- Kali
- Linux
- macOS
- Windows
---

Hola, en este post te ofrezco una guía completa para iniciarte en el hacking ético con Kali Linux. Te explicaré qué es Kali Linux, cuáles son sus ventajas y, lo más importante, cómo instalarlo en diferentes sistemas operativos: Windows (usando WSL2), macOS (a través de VirtualBox) y en una instalación nativa en Linux. Además, encontrarás una hoja de comandos básicos y ejemplos de ataques básicos, todo para que dispongas de una base sólida en ciberseguridad.

## 1. ¿Qué es Kali Linux?
Kali Linux es una distribución basada en Debian, diseñada específicamente para pruebas de penetración, auditorías de seguridad y análisis forense. Es la herramienta preferida tanto por profesionales como por entusiastas del hacking ético, ya que integra cientos de utilidades especializadas en seguridad informática.

### 1.1 Orígenes y Evolución
Kali Linux es el sucesor de BackTrack, una distribución que ya era muy popular en el ámbito de la ciberseguridad. Con el tiempo, Kali ha evolucionado, incorporando mejoras, nuevas herramientas y actualizaciones constantes para mantenerse al día con las últimas tendencias y amenazas.

### 1.2 Herramientas Integradas
Entre las utilidades que encontrarás en Kali destacan:

**Escaneo de Redes:** Herramientas como Nmap para detectar dispositivos, puertos abiertos y servicios activos.

**Explotación de Vulnerabilidades:** Metasploit para realizar pruebas de penetración y aprovechar fallos en sistemas.

**Análisis Forense:** Programas especializados para investigar incidentes y analizar evidencias digitales.

**Ingeniería Inversa**: Utilidades como Ghidra para analizar el funcionamiento interno de aplicaciones y binarios.
## 2. Ventajas de Usar Kali Linux
Utilizar Kali Linux te proporciona múltiples beneficios:

**Todo en Uno:** La mayoría de las herramientas necesarias ya vienen integradas, ahorrándote tiempo en instalaciones adicionales.

**Comunidad Activa:** Existen foros, documentación y tutoriales que te ayudarán a resolver dudas y estar al tanto de novedades.

**Actualizaciones Constantes:** Se mantiene actualizado con las últimas técnicas y parches de seguridad.

**Flexibilidad:** Puedes trabajar en entornos gráficos o directamente desde la terminal, adaptándolo a tus necesidades.

**Compatibilidad:** Kali Linux se adapta a diversos entornos, ya sea como instalación nativa o en entornos virtualizados en Windows, macOS o Linux.
## 3. Guía de Instalación de Kali Linux en Diferentes Sistemas Operativos
### 3.1 Instalación en Windows usando WSL2
#### Requisitos:

Windows 10 (versión 2004 o superior) o Windows 11.

#### Pasos:

##### Habilitar WSL y la Plataforma de Máquina Virtual:

Abre PowerShell como administrador y ejecuta:

```bash
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Reinicia el sistema.
##### Actualizar el Núcleo de Linux para WSL2:

Descarga e instala la última actualización del kernel de Linux para WSL desde la página oficial de Microsoft (busca “WSL2 Linux kernel update package for x64”).

##### Configurar WSL2 como Predeterminado:

En PowerShell (como administrador), ejecuta:
```bash
wsl --set-default-version 2
```
##### Instalar Kali Linux desde la Microsoft Store:

Abre Microsoft Store, busca “Kali Linux”, selecciona la aplicación oficial e instálala.
Al abrirla por primera vez, se te pedirá que configures un usuario y una contraseña.
##### Verificar la Versión:
Abre PowerShell y ejecuta:

```bash
wsl -l -v
```

Asegúrate de que en la columna “VERSION” aparezca el número 2 junto a Kali Linux.
##### Actualizar Kali Linux:

Abre el terminal de Kali Linux y ejecuta:
```bash
sudo apt-get update
sudo apt-get upgrade -y
```
### 3.2 Instalación en macOS usando VirtualBox
Como macOS no permite instalar Kali Linux de forma nativa, la opción más sencilla es usar VirtualBox.

#### Requisitos:

Descarga e instala VirtualBox.
Descarga la imagen ISO oficial de Kali Linux desde Kali Linux Downloads.
Pasos:

#### Crear una Nueva Máquina Virtual:

Abre VirtualBox y haz clic en “Nueva”.
Asigna un nombre (por ejemplo, “Kali Linux”), selecciona el tipo “Linux” y la versión “Debian (64-bit)”.
#### Configurar Recursos:

Asigna memoria RAM (recomendable al menos 2 GB, idealmente 4 GB o más).
Crea un disco duro virtual (20 GB o más) y elige VDI como formato.
#### Configurar la Máquina:

En “Configuración”, en la sección “Almacenamiento”, adjunta la imagen ISO de Kali Linux al controlador óptico.
#### Instalación:

Inicia la máquina virtual y sigue las instrucciones de instalación en pantalla (selecciona el modo gráfico, configura particiones, etc.).
#### Post-instalación:

Una vez instalado, asegúrate de instalar las Guest Additions de VirtualBox para mejorar el rendimiento y la integración.
### 3.3 Instalación en Linux (Instalación Nativa o en Máquina Virtual)
Si ya utilizas Linux y deseas instalar Kali Linux de forma nativa o en una máquina virtual, tienes dos opciones:

#### Instalación Nativa (Dual Boot):

##### Descarga la ISO de Kali Linux:

Obtén la imagen ISO desde Kali Linux Downloads.
##### Crear un USB Booteable:

Usa herramientas como Rufus (en Windows) o el comando dd (en Linux) para grabar la ISO en un USB.
##### Instalar Kali Linux:

Reinicia el sistema, arranca desde el USB y sigue las instrucciones del instalador para configurar un arranque dual o la instalación completa.
#### Instalación en Máquina Virtual:

##### Instalar VirtualBox o VMware:

Descarga e instala VirtualBox o VMware Workstation en tu sistema Linux.
##### Crear una Nueva Máquina Virtual:

Configura la máquina virtual similar a la sección de macOS (asigna recursos, adjunta la ISO, etc.).
##### Instalación y Configuración:

Inicia la máquina virtual y sigue el proceso de instalación de Kali Linux.
## 4. Hoja de Comandos Básicos
Para familiarizarte con la terminal de Kali Linux, aquí tienes una tabla con comandos esenciales. Puedes copiarla a una hoja de cálculo para consultarla siempre que lo necesites:

| Comando           | Descripción                                                         |
|-------------------|---------------------------------------------------------------------|
| `ls`              | Lista los archivos y directorios en el directorio actual.           |
| `cd`              | Cambia el directorio de trabajo.                                    |
| `pwd`             | Muestra el directorio actual.                                       |
| `mkdir`           | Crea un nuevo directorio.                                           |
| `rm`              | Elimina archivos o directorios (usa `-r` para carpetas).            |
| `cp`              | Copia archivos o directorios.                                       |
| `mv`              | Mueve o renombra archivos y directorios.                            |
| `chmod`           | Modifica los permisos de archivos o directorios.                    |
| `chown`           | Cambia el propietario de archivos o directorios.                    |
| `sudo`            | Ejecuta comandos con privilegios de superusuario.                   |
| `apt-get update`  | Actualiza la lista de paquetes disponibles.                         |
| `apt-get upgrade` | Actualiza los paquetes instalados a sus últimas versiones.          |
| `ifconfig` o `ip a`| Muestra la configuración de las interfaces de red.                  |
| `iwconfig`        | Muestra la configuración de las interfaces de red wireless.             |
| `ping`            | Comprueba la conectividad con otra máquina en la red.               |
| `nmap`            | Escanea redes para identificar dispositivos y servicios abiertos.   |
| `netstat`         | Muestra conexiones de red y tablas de enrutamiento.                 |

## 5. Ejemplos de Ataques Básicos (Spreadsheet)
A continuación, te dejo una tabla con algunos ejemplos de ataques básicos. Recuerda que estos ejemplos son exclusivamente para fines educativos y deben realizarse únicamente en entornos de laboratorio o sistemas con autorización.

| Ataque                          | Herramienta/Comando | Descripción                                                                           | Ejemplo/Notas                                                        |
|---------------------------------|---------------------|---------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| Escaneo de Puertos              | Nmap                | Identifica puertos abiertos y servicios activos en el objetivo.                       | `nmap -sS 192.168.1.1` para realizar un escaneo SYN.                 |
| Fuerza Bruta en SSH             | Hydra               | Realiza intentos de adivinar contraseñas en servicios SSH mediante fuerza bruta.       | `hydra -l usuario -P lista.txt ssh://192.168.1.1`                    |
| Sniffing de Red                 | Wireshark           | Captura y analiza el tráfico de red para detectar información sensible.                | Utiliza filtros para protocolos específicos, como HTTP o FTP.        |
| Inyección SQL                   | sqlmap              | Automatiza la detección y explotación de vulnerabilidades de inyección SQL en aplicaciones web. | `sqlmap -u "http://objetivo.com/page.php?id=1" --risk=3 --level=5`   |
| Denegación de Servicio (DoS)    | hping3              | Envía paquetes de red para saturar un servicio y hacerlo inaccesible.                  | `hping3 -S --flood 192.168.1.1` (usar con extrema precaución)        |

**Nota:** Estos ejemplos deben realizarse únicamente en entornos de prueba y con autorización expresa. El uso indebido de estas técnicas puede ser ilegal y está penado por la ley. 


## 6. Explorando el Hacking Ético
Una vez que tengas Kali Linux instalado en tu sistema, es momento de explorar el mundo del hacking ético. Algunos pasos recomendados son:

**Escaneo y Reconocimiento:** Aprende a utilizar Nmap para identificar dispositivos y servicios en una red.

**Introducción a Metasploit:** Familiarízate con este framework para detectar y explotar vulnerabilidades.

**Análisis Forense:** Investiga cómo utilizar herramientas forenses para reconstruir incidentes de seguridad.

**Proyectos Prácticos:** Configura entornos de prueba y realiza ejercicios prácticos para aplicar lo aprendido.

**Formación Continua:** La ciberseguridad es un campo en constante evolución. Mantente al día con tutoriales, foros y documentación actualizada.

Recuerda que el hacking ético se basa en la responsabilidad y el respeto a la ley. Siempre actúa con el debido consentimiento y en entornos controlados.

## 7. Conclusión
En este post tienes una guía completa para que des tus primeros pasos en el hacking ético con Kali Linux. He explicado qué es Kali Linux, sus ventajas y te has visto cómo instalarlo en Windows (usando WSL2), macOS (con VirtualBox) y en Linux (de forma nativa o virtualizada). Además, dispondrás de una hoja de comandos básicos y ejemplos de ataques que te ayudarán a comenzar a explorar el fascinante mundo de la ciberseguridad.


¡Gracias por leer y te invito a seguir explorando posts!
