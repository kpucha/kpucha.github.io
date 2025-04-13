---
title: Desbloquea el bootloader de tu Xiaomi sin entregar tu alma a Xiaomi
tags:
- Hacking
- Herramientas
- Windows
- Linux
- macOS
- Android
categories:
- Hacking ético
- Herramientas
image: assets/img/headers/xiaomi-flipper-zero-eater-2.png
---

---

### 🔐 **Serie: Convierto mi Xiaomi en una herramienta de hacking definitiva (más potente que un Flipper Zero)**

---

## 📌 Estructura general de la serie

| Post | Título | Contenido principal |
|------|--------|----------------------|
| 1️⃣ | **Introducción al proyecto + Preparación del entorno** | Qué vamos a construir, por qué un Xiaomi Mi Note 10 Lite, diferencias con Flipper Zero, requisitos físicos y lógicos, instalación de herramientas en el PC, conceptos básicos (ADB, fastboot, bootloader, root, etc.) |
| 2️⃣ | **Desbloquear el bootloader sin comprometer privacidad** | Qué es el bootloader, por qué desbloquearlo, cómo hacerlo paso a paso sin registrar el dispositivo con Xiaomi |
| 3️⃣ | **Instalar un recovery personalizado (TWRP) y rootear con Magisk** | Qué es un recovery, qué es Magisk, cómo instalarlo correctamente y ocultar el root del sistema |
| 4️⃣ | **Blindar el móvil: seguridad, cifrado y anonimato total** | Cifrar todo el sistema, anonimizar conexiones, bloquear rastros, usar VPN segura y DNS cifrado |
| 5️⃣ | **Instalación de Termux y herramientas de pentesting** | Qué es Termux, instalación y configuración, instalación de Nmap, Hydra, Metasploit, etc. |
| 6️⃣ | **Casos prácticos de pentesting desde el móvil** | Ejemplos reales de uso: escaneo de redes Wi-Fi, fuerza bruta, explotación de vulnerabilidades |
| 7️⃣ | **Añadir capacidades avanzadas: IR, NFC, Bluetooth hacking y sniffing** | Cómo aprovechar IR y NFC para emular tarjetas, mandos, llaves; ataques MITM, etc. |
| 8️⃣ | **Hardening final del dispositivo + consejos legales y éticos** | Protección contra ataques, backup seguro, cómo ser invisible en auditorías, marco legal en España |

---

## 🔓 **Post 2: Desbloquea el bootloader de tu Xiaomi sin entregar tu alma a Xiaomi**

---

### 📢 IMPORTANTE antes de empezar

> **Desbloquear el bootloader** borrará todo el contenido del móvil.  
> Guarda lo que necesites antes de continuar.

Además, muchas guías te hacen **crear una cuenta Xiaomi** y enviar datos personales para obtener “permiso” de desbloqueo.  
**Nosotros no haremos eso.** Vamos a hacerlo sin vincular cuentas ni entregar información.

---

## 🧠 ¿Qué es el bootloader exactamente?

El bootloader es un sistema que **controla qué se puede cargar al arrancar el teléfono**. Viene **bloqueado por defecto** para que no puedas instalar sistemas personalizados, rootearlo o modificarlo.

Desbloquearlo nos permite:

- Instalar un recovery como **TWRP**.
- Rootear el dispositivo con **Magisk**.
- Instalar herramientas de hacking reales.
- Tener control completo del sistema.

---

## 🛡️ ¿Por qué hacerlo sin usar la cuenta Xiaomi?

Usar la vía oficial:

❌ Obliga a crear una cuenta Xiaomi.  
❌ Enlaza tu identidad con el dispositivo.  
❌ Xiaomi registra la IP, la SIM y los IMEIs.  
❌ Puedes esperar hasta **7 días** para el desbloqueo.

En hacking ofensivo, **el anonimato es clave**.  
Así que usaremos otro método.

---

## 🔧 Requisitos para este paso

- Tener **ADB y Fastboot ya instalados** en el ordenador.  
- Tener activada la **depuración USB** (lo hicimos en el post anterior).  
- Tener el móvil **con batería al 100 %**.  
- Usar el cable USB original si es posible.

---

## 🧪 Paso 1: Comprobar conexión ADB

Conecta el móvil al ordenador y ejecuta en la terminal:

```bash
adb devices
```

Debe salir algo como:

```
List of devices attached
abc123456789	device
```

Si te sale “unauthorized” o nada, **revisa el móvil**: debe aparecer un aviso para **permitir depuración USB**. Acepta.

---

## 🚀 Paso 2: Reiniciar en modo Fastboot

Ejecuta:

```bash
adb reboot bootloader
```

El móvil se reiniciará en **modo Fastboot**: pantalla negra con letras pequeñas.  
Si no funciona, puedes entrar manualmente:

1. Apaga el móvil.
2. Pulsa **Volumen Abajo + Encendido** a la vez.
3. Mantenlo hasta que aparezca el logo de Fastboot.

---

## 🧰 Paso 3: Comprobar que Fastboot funciona

En la terminal:

```bash
fastboot devices
```

Debe aparecer un código de dispositivo.

---

## 🔓 Paso 4: Desbloquear el bootloader con un exploit alternativo

> ⚠️ Aquí podríamos usar métodos alternativos que **NO requieren la cuenta Xiaomi**.  
> Por seguridad, esta parte **varía según la versión del firmware** y el parche de seguridad.

### 🔐 Opción recomendada: *Unlock Bootloader vía exploit temporal (sin cuenta Xiaomi)*

Este método requiere:

✅ Firmware anterior a julio 2022  
✅ Bootloader vulnerable (verificamos ahora)  
✅ Herramienta open-source (segura y local)

---

### 🔎 Verifica si tu móvil es vulnerable

En modo fastboot, ejecuta:

```bash
fastboot getvar all
```

Busca estas líneas:

```
(bootloader) anti: 1
```

- Si dice `anti: 1`, probablemente se puede desbloquear.
- Si dice `anti: 4` o más, está parcheado. Necesitamos *downgradear* (lo veremos al final de este post por si te hace falta).

---

### ✅ Si tu móvil es vulnerable: sigue

Usaremos una herramienta llamada **XiaoMiTool V2** (pero solo **offline y sin cuenta**).

1. Descárgala desde [https://xiaomitool.com/V2/](https://xiaomitool.com/V2/)
2. Ejecuta y conecta el móvil en modo fastboot.
3. Pulsa "Advanced" > "Unlock Bootloader".
4. Elige **NO INICIAR SESIÓN** con cuenta Xiaomi.
5. Acepta los términos y espera.

> Si todo va bien, el móvil se reiniciará y verás un mensaje como:  
> **“The bootloader is unlocked”**

---

## 🧼 Paso 5: Limpieza y verificación

Al reiniciar el móvil se formateará completamente.  
Cuando arranque, **salta la configuración de WiFi y Google si quieres mantener anonimato**.

Puedes verificar que el bootloader está desbloqueado con:

```bash
adb reboot bootloader
fastboot oem device-info
```

Debe poner:

```
(bootloader) Device unlocked: true
```

---

## 🛡️ ¡Enhorabuena! Tu móvil ahora está **liberado, pero sigue virgen**.

Ya puedes instalar un recovery, rootear, cifrar y convertirlo en una máquina de guerra digital.

---

Perfecto, vamos a ampliar este mismo post incluyendo también el **downgrade seguro del firmware** para los Xiaomi con protección **anti-rollback > 3 (anti:4, anti:5, etc.)**, lo cual es muy común en modelos actualizados.

El objetivo es **bajar a una versión vulnerable del sistema**, desbloquear el bootloader sin cuenta Xiaomi, y luego poder seguir con la personalización completa.

---

## 🧨 ¿Tu Xiaomi muestra `anti: 4` o superior?

Si en el paso anterior ejecutaste:

```bash
fastboot getvar all
```

Y te apareció:

```
(bootloader) anti: 4
```

Entonces necesitas hacer un **downgrade del firmware** para poder desbloquear el bootloader de forma **segura y sin cuenta Xiaomi**.

---

## ⚠️ ¿Qué es el Anti-Rollback?

Es una protección que **impide instalar versiones anteriores** a la que trae el móvil.

Si intentas forzar una versión antigua **sin conocer el nivel anti-rollback**, puedes **brickear** el móvil para siempre.

Por eso, **vamos a usar versiones compatibles con tu nivel anti**.

---

## 🧰 Requisitos para hacer downgrade seguro

1. Conexión estable por cable USB.
2. Tener **ADB y Fastboot** instalados.
3. Un PC con **al menos 8 GB de RAM**.
4. Móvil con batería > 80 %.
5. Herramienta de flasheo **MiFlash Tool** o **XiaoMiTool V2**.
6. ROM oficial fastboot compatible (te la doy ahora).

---

## ⬇️ Paso 1: Descargar ROM Fastboot segura (anti:4 compatible)

Vamos a usar una ROM anterior a julio de 2022, que aún **permite desbloqueo del bootloader sin cuenta**.

| Modelo                | ROM segura recomendada |
|-----------------------|------------------------|
| Xiaomi Mi Note 10 Lite | [Descargar V12.5.6.0.RFNMIXM](https://xiaomifirmwareupdater.com/miui/toco/stable/V12.5.6.0.RFNMIXM/) |

> ⚠️ Asegúrate de elegir **fastboot ROM**, no “recovery”.

---

## 🧪 Paso 2: Extraer la ROM fastboot

El archivo tendrá nombre como `miui_TOCO_V12.5.6.0.RFNMIXM_xxxxxx_fastboot.zip`.  
Extrae el zip en una carpeta sin espacios, por ejemplo:

```
C:\miui_downgrade\toco
```

---

## 🛠️ Paso 3: Instala MiFlash Tool

1. Descarga MiFlash Tool: [https://xiaomiflashtool.com/](https://xiaomiflashtool.com/)
2. Instálalo y ejecútalo como administrador.
3. En el menú superior, selecciona el directorio donde extrajiste la ROM.

---

## 🔌 Paso 4: Entra en modo Fastboot

1. Apaga el móvil.
2. Pulsa **Volumen Abajo + Encendido** hasta que aparezca el conejito de Fastboot.
3. Conecta al PC por USB.

---

## 🚨 Paso 5: Flashear la ROM correctamente

En MiFlash Tool:

1. Haz clic en “Refresh”.  
   Verás el ID de tu dispositivo.

2. Abajo selecciona:  
   ✅ **clean all**  
   (¡NO elijas *clean all and lock*! Eso relockea el bootloader.)

3. Haz clic en **Flash**.

El proceso tardará unos minutos. Al finalizar verás `success`.

---

## 🔁 Paso 6: Verifica rollback y desbloquea

Una vez flasheado:

1. El móvil se reiniciará y tardará unos minutos en iniciar.
2. Ve al paso anterior y repite:

```bash
fastboot getvar all
```

Si sigue marcando `anti: 4`, está bien, ya estás en versión compatible.  
Ahora puedes usar **XiaoMiTool V2** para desbloquear el bootloader sin cuenta.

---

## 🧩 ¿Y si no funciona el desbloqueo aún?

En algunos casos Xiaomi ha cerrado incluso las ROMs antiguas, entonces toca:

- Usar herramientas como **MTK Bypass** o **EDL Test Point** (requiere abrir el móvil).
- O usar exploits como **firehose programmer + QFIL** (para usuarios avanzados).

---

## 🔜 Próximo post

> **Post 3: Instalar TWRP y Rootear con Magisk paso a paso (sin romper el móvil)**

---
