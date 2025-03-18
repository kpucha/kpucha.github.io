---
title: 'n8n: Automatización Gratis en local'
categories:
- Automatización
- Herramientas
tags:
- Automatización
- Herramientas
- n8n
- local
image: "/assets/img/headers/n8n-automatizacion.png"
---

[n8n](https://n8n.partnerlinks.io/hs9dwwyl9top) es una herramienta de automatización de flujos de trabajo *open source* que te permite conectar aplicaciones y servicios sin tener que escribir casi código. Con [n8n](https://n8n.partnerlinks.io/hs9dwwyl9top) puedes crear procesos automatizados (workflows) que integren distintos sistemas, lo que te ayudará a ahorrar tiempo y minimizar errores en tareas repetitivas.

---

## 1. ¿Qué es n8n?

[n8n](https://n8n.partnerlinks.io/hs9dwwyl9top) es un motor de automatización que te permite diseñar flujos de trabajo (workflows) conectando nodos. Cada nodo representa una acción (como enviar un correo o hacer una petición HTTP) o un trigger (evento que inicia el workflow). 

### Ejemplos de uso
- **Integración de aplicaciones:** Conecta tu CRM con servicios de email marketing.
- **Automatización de tareas repetitivas:** Recibe datos a través de un webhook y almacénalos en una base de datos.
- **Procesos condicionales:** Filtra información y envía notificaciones según criterios definidos.

### Tabla Comparativa: n8n vs. Zapier vs. Integromat

| Herramienta | Open Source | Personalización | Costo Inicial  |
|-------------|-------------|-----------------|----------------|
| **[n8n](https://n8n.partnerlinks.io/hs9dwwyl9top)**    | Sí          | Alta            | Gratuito       |
| Zapier      | No          | Media           | Planes pagos   |
| Integromat  | No          | Alta            | Planes pagos   |

[n8n](https://n8n.partnerlinks.io/hs9dwwyl9top) también tiene la posibilidad de adquirir una suscripción de pago para su uso online, pero a continuación veremos como realizar la instalación de forma local para poder tener workflows ilimitados gratis

---

## 2. Instalación de n8n

Existen diferentes métodos para instalar [n8n](https://n8n.partnerlinks.io/hs9dwwyl9top), según tus preferencias y entorno de trabajo. A continuación, se muestra una tabla con las opciones más comunes:

| Método | Requisitos             | Comando de instalación                                        |
|--------|------------------------|----------------------------------------------------------------|
| npm    | Tener Node.js instalado| `npm install n8n -g`                                             |
| Docker | Tener Docker instalado | `docker run -it --rm -p 5678:5678 n8nio/n8n`                     |

### Instalación vía npm
1. **Instala Node.js:** Descarga e instala Node.js desde su [sitio oficial](https://nodejs.org/).
2. **Instala n8n globalmente:** Ejecuta en la terminal:
   ```bash
   npm install n8n -g
   ```
3. **Ejecuta n8n:** Simplemente teclea `n8n` en la terminal y accede a [http://localhost:5678](http://localhost:5678).

### Instalación vía Docker 
1. **Instala Docker:** Asegúrate de tener Docker instalado en tu sistema.
2. **Ejecuta n8n:** Abre la terminal y ejecuta:
   ```bash
   docker run -it --rm -p 5678:5678 n8nio/n8n
   ```
3. **Accede a la interfaz:** Una vez iniciado, abre tu navegador y visita [http://localhost:5678](http://localhost:5678).

---

## 3. Conceptos Básicos de n8n

Antes de crear un workflow, es importante conocer algunos conceptos clave:

- **Workflow:** Es el conjunto de nodos conectados que definen un proceso automatizado.
- **Nodo:** Representa una acción (por ejemplo, enviar un email) o un trigger (por ejemplo, recibir una petición HTTP).
- **Trigger:** Nodo que inicia el workflow al detectar un evento (como un Webhook).
- **Action:** Nodo que realiza una acción (como realizar una petición a una API).

### Tabla de Nodos Comunes

| Nodo            | Función                                      |
|-----------------|----------------------------------------------|
| **Webhook**     | Recibe peticiones HTTP para disparar un flujo|
| **HTTP Request**| Realiza peticiones a APIs externas           |
| **Function**    | Permite ejecutar código JavaScript personalizado |
| **Email Send**  | Envía correos electrónicos                   |

---

## 4. Ejemplo Práctico: Creando un Workflow Sencillo

En este ejemplo crearemos un workflow que reciba una petición a través de un Webhook y, a partir de los datos recibidos, realice una petición HTTP para enviar un email.

### Paso 4.1: Configuración del Webhook

1. Arrastra un nodo **Webhook** a tu lienzo.
2. Configura el **path** (por ejemplo, `webhook-test`) y el método HTTP (POST).

### Paso 4.2: Configuración del HTTP Request

1. Añade un nodo **HTTP Request**.
2. Configura el nodo para que haga una petición POST a una API de ejemplo que simule el envío de un email.
3. Usa parámetros en formato JSON para enviar datos recibidos desde el Webhook.

### Ejemplo de JSON del Workflow

Puedes importar el siguiente JSON en [n8n](https://n8n.partnerlinks.io/hs9dwwyl9top) (menú *Import Workflow*) para replicar el ejemplo:

```json
{
  "nodes": [
    {
      "parameters": {
        "path": "webhook-test",
        "httpMethod": "POST"
      },
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "requestMethod": "POST",
        "url": "https://api.ejemplo.com/sendEmail",
        "jsonParameters": true,
        "options": {},
        "bodyParametersJson": "={\n  \"email\": {{$json[\"email\"]}},\n  \"message\": \"Recibimos tu solicitud correctamente.\"\n}"
      },
      "name": "HTTP Request",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        450,
        300
      ]
    }
  ],
  "connections": {
    "Webhook": {
      "main": [
        [
          {
            "node": "HTTP Request",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

> **Nota:** Asegúrate de cambiar la URL `https://api.ejemplo.com/sendEmail` por la de un servicio real o una API que estés utilizando. Además, revisa la sintaxis de las expresiones para que no se produzcan errores al ejecutar el workflow.

### Paso 4.3: Ejecutar y Probar el Workflow

1. **Activar el Workflow:** Guarda y activa el workflow en n8n.
2. **Realizar una prueba:** Envía una petición POST a `http://localhost:5678/webhook-test` con un cuerpo JSON similar a:
   ```json
   {
     "email": "usuario@ejemplo.com"
   }
   ```
3. **Verifica el resultado:** En el panel de ejecución de n8n, revisa que el nodo Webhook reciba la petición y que el nodo HTTP Request envíe correctamente la información.

---

## 5. Integración de IA en n8n (Opcional)

Aunque este tutorial está dirigido a principiantes, n8n también permite integrar servicios de inteligencia artificial. Por ejemplo, podrías conectar con la API de OpenAI para generar respuestas automáticas.

### Ejemplo Básico de Integración con OpenAI

1. **Añade un nodo HTTP Request.**
2. **Configura el nodo:**
   - Método: POST
   - URL: `https://api.openai.com/v1/engines/davinci-codex/completions`
   - Headers: Incluye el API Key en `Authorization: Bearer TU_API_KEY`
   - Body (JSON):
     ```json
     {
       "prompt": "Escribe un resumen sobre n8n.",
       "max_tokens": 50
     }
     ```
3. **Conecta este nodo en tu workflow** para que, tras recibir un input, puedas obtener un resumen generado por la IA.

> Recuerda que para evitar errores, es fundamental validar las respuestas de la API y gestionar posibles excepciones mediante nodos *Function* o *Error Trigger* en n8n.

---

## 6. Consejos para Controlar Errores y Depurar

- **Utiliza el panel de ejecución:** n8n muestra un historial detallado de cada ejecución, lo que facilita identificar en qué paso ocurre algún error.
- **Prueba cada nodo por separado:** Antes de conectar todos los nodos, verifica que cada uno funcione de manera independiente.
- **Manejo de errores:** Configura nodos *Error Trigger* para gestionar errores y notificarte si algo falla en el workflow.
- **Valida expresiones:** Asegúrate de que las expresiones (por ejemplo, `{{$json["email"]}}`) se resuelvan correctamente para evitar errores de sintaxis o ejecución.

---

## Conclusión

n8n es una herramienta poderosa y flexible para automatizar tareas y conectar diferentes servicios. Este post te ha mostrado desde la instalación hasta la creación de un workflow sencillo, pasando por conceptos básicos y ejemplos prácticos. Con la práctica, podrás expandir tus flujos de trabajo para integrar APIs de inteligencia artificial y muchos otros servicios.
