---
title: 'Sweeping con Kali Linux: Barriendo la Red'
categories:
- Hacking ético
- Técnicas
tags:
- Hacking
- Kali
- Linux
- sweeping
image: "/assets/img/headers/sweeping.jpg"
---

En el mundo del hacking ético, el *sweeping* es una técnica fundamental utilizada en la fase de reconocimiento y escaneo de una red. Su objetivo principal es identificar hosts activos, puertos abiertos y servicios disponibles en un rango de direcciones IP.

Kali Linux permite llevar a cabo *sweeping* de manera eficiente y precisa. En este post, exploraremos cómo ejecutar diferentes tipos de *sweeping*, las herramientas más efectivas y algunas técnicas avanzadas para maximizar los resultados. También discutiremos estrategias para prevenir estos escaneos y proteger tu red.

## 1. ¿Qué es el Sweeping y por qué es Importante?

El *sweeping* es una técnica de escaneo utilizada en pentesting para mapear una red objetivo. Se utiliza para:

- Identificar hosts activos dentro de un rango de direcciones IP.
- Detectar puertos abiertos y servicios en ejecución.
- Obtener información preliminar sobre la estructura de una red.
- Evaluar la seguridad y posibles vulnerabilidades de una infraestructura.
- Comprobar la respuesta de dispositivos de seguridad como firewalls o IDS.

Su importancia radica en que es el primer paso para planificar un ataque ético o evaluar la seguridad de una infraestructura antes de un intento de intrusión más avanzado.

## 2. Tipos de Sweeping y Cómo Realizarlos en Kali Linux

### 2.1. IP Sweeping (Network Sweeping)

Consiste en enviar solicitudes a un rango de direcciones IP para determinar cuáles están activas. Para ello, utilizamos `nmap`, `fping` o `hping3`.

#### 2.1.1. Ejemplo con Nmap

```bash
nmap -sn 192.168.1.0/24
```

**Explicación de parámetros:**
- `-sn`: Realiza un escaneo sin detección de puertos, solo verifica qué hosts están activos.
- `192.168.1.0/24`: Especifica el rango de direcciones IP a escanear.

**Respuesta esperada:**
```plaintext
Starting Nmap ...
Nmap scan report for 192.168.1.1
Host is up.
Nmap scan report for 192.168.1.10
Host is up.
...
```

#### 2.1.2. Ejemplo con Fping

```bash
fping -a -g 192.168.1.0/24 2>/dev/null
```

**Explicación de parámetros:**
- `-a`: Muestra solo los hosts que responden.
- `-g`: Genera un rango de direcciones IP para escanear.
- `2>/dev/null`: Oculta los mensajes de error.

**Respuesta esperada:**
```plaintext
192.168.1.1
192.168.1.10
192.168.1.20
```

#### 2.1.3. Ejemplo con Hping3

```bash
hping3 -S 192.168.1.1 -p 80 -c 1
```

**Explicación de parámetros:**
- `-S`: Envía paquetes SYN para verificar si el puerto está abierto.
- `-p 80`: Especifica el puerto de destino.
- `-c 1`: Envía solo un paquete.

**Respuesta esperada:**
```plaintext
len=46 ip=192.168.1.1 ttl=64 DF id=0 sport=80 flags=SA seq=0 win=64240
```

### 2.2. Port Sweeping (Escaneo de Puertos)

#### 2.2.1. Ejemplo con Nmap

```bash
nmap -p 22 192.168.1.0/24 --open
```

**Explicación de parámetros:**
- `-p 22`: Escanea solo el puerto 22 (SSH).
- `--open`: Muestra solo los puertos abiertos.

**Respuesta esperada:**
```plaintext
Nmap scan report for 192.168.1.10
22/tcp open ssh
```

#### 2.2.2. Ejemplo con Netcat

```bash
echo '' | nc -v -n -z 192.168.1.1 22
```

**Explicación de parámetros:**
- `-v`: Modo detallado (verbose).
- `-n`: No usa resolución de DNS.
- `-z`: Escaneo de puertos sin enviar datos.

**Respuesta esperada:**
```plaintext
(UNKNOWN) [192.168.1.1] 22 (ssh) open
```

### 2.3. Service Sweeping (Escaneo de Servicios)

#### 2.3.1. Ejemplo con Nmap

```bash
nmap -sV 192.168.1.0/24
```

**Explicación de parámetros:**
- `-sV`: Detecta versiones de los servicios en ejecución.

**Respuesta esperada:**
```plaintext
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
```

## 3. Cómo Prevenir el Sweeping

### 3.1. Configurar Firewalls y Filtrado de Tráfico

```bash
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```

**Explicación:** Bloquea solicitudes ICMP (ping) para evitar escaneos ICMP.

Para bloquear escaneos SYN, podemos utilizar:

```bash
iptables -A INPUT -p tcp --tcp-flags ALL SYN -j DROP
```

**Explicación:** Impide que paquetes SYN inicien conexiones no autorizadas.

### 3.2. Uso de IDS/IPS (Intrusion Detection/Prevention Systems)

Ejemplo de regla en Snort:

```plaintext
alert icmp any any -> any any (msg:"ICMP Sweep Detected"; detection_filter:track by_dst, count 5, seconds 10; sid:1000001;)
```

**Explicación:** Genera una alerta si se detectan más de 5 pings en 10 segundos al mismo destino.

### 3.3. Implementación de Honeypots

Herramientas como **Kippo**, **Cowrie** o **Dionaea** pueden ayudar a registrar intentos de barrido y escaneo de puertos y analizar patrones de ataque para mejorar la seguridad.

Otra técnica avanzada es el uso de honeypots de alta interacción para registrar actividades sospechosas y engañar a posibles atacantes, recopilando información sobre sus tácticas y herramientas utilizadas.

### 3.4. Medidas Adicionales

- **Segmentación de red**: Mantener redes internas separadas de las externas mediante VLANs y firewalls.
- **Configuración de IDS con Suricata o Snort**: Monitorizar patrones de tráfico sospechoso.
- **Uso de TCP Wrappers**: Restringir acceso a servicios basados en IPs permitidas.
- **Deshabilitación de servicios innecesarios**: Reducir la superficie de ataque eliminando servicios no utilizados.
- **Implementación de reglas en Firewalld o UFW**: Aplicar políticas restrictivas de entrada y salida en servidores y dispositivos de red.

Al aplicar estas estrategias de seguridad, reducimos las posibilidades de que un atacante realice un reconocimiento efectivo sobre nuestra infraestructura y mejoremos la postura de seguridad de la red.
