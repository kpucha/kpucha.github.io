---
title: 'MCP (Model Context Protocol): El estándar abierto para agentes IA colaborativos'
categories:
- Desarrollo
- Spring Framework
tags:
- Inteligencia Artificial
- Spring
- Desarrollo
- Java
- Spring AI
- Optimización
- Ollama
- MCP
image: assets/img/headers/mcp-model-context-protocol.png
---

## 📌 ¿Qué es MCP?

**MCP (Model Context Protocol)** es un protocolo abierto basado en JSON que define cómo representar el contexto que se intercambia entre agentes de IA o con un modelo de lenguaje (LLM). Permite encapsular:

- El **rol** del agente
- El **objetivo** general de la tarea
- Los **datos de entrada**
- El **historial** relevante de interacción
- Las **instrucciones** precisas para el agente

A diferencia de los prompts planos, MCP ofrece estructura, trazabilidad y flexibilidad para orquestar flujos IA complejos.

---

## 🏗️ Origen de MCP: ¿Quién lo creó y por qué?

**MCP fue propuesto por [Lamini AI](https://lamini.ai)** como parte de su trabajo en modelos empresariales y sistemas multiagente. Su intención fue resolver problemas comunes en flujos IA:

- Pérdida de contexto entre pasos
- Incompatibilidad entre agentes
- Dificultad para auditar decisiones tomadas por IA
- Dificultad para componer tareas complejas

### 🧑‍🔬 ¿Quién lo usa?

- **Lamini AI**: creador y usuario principal
- **CrewAI**: framework para agentes colaborativos en Python (usa MCP como formato de paso entre agentes)
- **Proyectos personalizados**: cualquier arquitectura modular con LLMs se beneficia de MCP (por ejemplo LangGraph, Semantic Kernel…)

### 📚 Especificación

Toda la especificación es pública y está disponible en GitHub:

👉 [https://github.com/modelcontextprotocol](https://github.com/modelcontextprotocol)

---

## 🧩 Estructura de un mensaje MCP

```json
{
  "context": {
    "role": "Analista de datos",
    "objective": "Detectar anomalías en el informe mensual de ventas.",
    "input": {
      "data": "ventas_marzo.csv",
      "summary": "Informe mensual con KPIs de marzo."
    },
    "history": [
      {
        "sender": "User",
        "message": "¿Puedes revisar si hubo caídas significativas?"
      },
      {
        "sender": "Model",
        "message": "Se observó una caída del 18% en ventas del producto B."
      }
    ]
  },
  "instructions": "Resume los hallazgos clave y recomienda acciones."
}
```

---

## 🚀 Casos de uso reales

- **Flujos multiagente IA**: Redactor → Editor → Revisor → Publicador
- **Pipelines IA complejos**: extracción → análisis → visualización → resumen
- **Chatbots empresariales**: donde cada turno del agente está ligado a contexto estructurado
- **Orquestación IA modular con CrewAI, LangGraph**

---

## 🛠️ ¿Cómo implementar MCP en un backend Spring Boot?

Gracias a que MCP es simplemente JSON estructurado, puedes usarlo como un DTO estándar en tu backend Java.

---

### ✅ 1. Definir las clases MCP en Java

```java
public class MCPMessage {
    private MCPContext context;
    private String instructions;
}

public class MCPContext {
    private String role;
    private String objective;
    private Map<String, Object> input;
    private List<MCPHistory> history;
}

public class MCPHistory {
    private String sender;
    private String message;
}
```

---

### ✅ 2. Crear un endpoint REST para recibir MCP

```java
@RestController
@RequestMapping("/api/mcp")
public class MCPController {

    @PostMapping("/process")
    public ResponseEntity<String> processMCP(@RequestBody MCPMessage message) {
        String rol = message.getContext().getRole();
        String objetivo = message.getContext().getObjective();
        String instrucciones = message.getInstructions();

        // Aquí podrías procesar o delegar la tarea a un modelo
        return ResponseEntity.ok("Procesado: " + rol + " | " + objetivo + " | " + instrucciones);
    }
}
```

---

### ✅ 3. Convertir MCP a prompt para un modelo LLM

```java
public String construirPrompt(MCPMessage mcp) {
    StringBuilder prompt = new StringBuilder();
    prompt.append("Rol: ").append(mcp.getContext().getRole()).append("\n");
    prompt.append("Objetivo: ").append(mcp.getContext().getObjective()).append("\n");
    prompt.append("Instrucciones: ").append(mcp.getInstructions()).append("\n\n");

    if (mcp.getContext().getHistory() != null) {
        for (MCPHistory h : mcp.getContext().getHistory()) {
            prompt.append(h.getSender()).append(": ").append(h.getMessage()).append("\n");
        }
    }

    return prompt.toString();
}
```

---

### ✅ 4. Llamar a un modelo Ollama o OpenAI desde Spring

```java
public String enviarAPromptLLM(String prompt) {
    WebClient client = WebClient.create("http://localhost:11434"); // Ollama
    String response = client.post()
        .uri("/api/generate")
        .contentType(MediaType.APPLICATION_JSON)
        .bodyValue(Map.of("model", "llama3", "prompt", prompt))
        .retrieve()
        .bodyToMono(String.class)
        .block();

    return response;
}
```

---

## 🔐 Buenas prácticas al usar MCP

- **Validar entrada**: asegúrate de que el JSON cumple con la estructura esperada.
- **Limitar el historial**: para evitar inputs demasiado largos o costosos.
- **Persistir MCPs**: para trazabilidad, debugging o auditoría.
- **Sanitizar el input** si va a modelos sensibles (evitar inyecciones o exploits de prompt).

---

## ✅ Ventajas de MCP

| Característica | Beneficio |
|----------------|-----------|
| **Estructurado** | Fácil de validar y auditar |
| **Reutilizable** | Permite compartir tareas entre agentes |
| **Escalable** | Ideal para arquitecturas complejas |
| **Agnóstico al modelo** | Funciona con cualquier LLM |
| **Trazable** | Perfecto para sistemas empresariales o regulados |

---

## 📚 Recursos adicionales

- Repositorio oficial:  
  🔗 [https://github.com/lamini-ai/mcp](https://github.com/lamini-ai/mcp)

- Frameworks relacionados:  
  🔧 [https://docs.crewai.com](https://docs.crewai.com) (CrewAI)

---

## 🧠 Conclusión

**MCP (Model Context Protocol)** representa un paso adelante en cómo estructuramos la comunicación con agentes de IA. Si estás construyendo un sistema con múltiples modelos o pasos secuenciales (pipeline), **MCP te permitirá orquestar, auditar y escalar** tu solución de forma limpia y coherente.

Además, su integración en Spring Boot es directa y flexible, lo que lo convierte en una opción excelente para entornos empresariales robustos.

---
