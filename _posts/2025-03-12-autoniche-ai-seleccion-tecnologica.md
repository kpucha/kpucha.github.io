---
title: Autoniche AI - Selección Tecnológica
image: "/assets/img/headers/autoniche-ai-seleccion-tecnologica.png"
categories:
- Proyectos
- AutoNiche AI
tags:
- Inteligencia Artificial
- Automatización
- AutoNiche AI
- Monetización
---

## 1. Introducción

Este documento detalla el proceso de selección de tecnologías para Autoniche AI, un sistema automatizado de creación y publicación de contenido de vídeo. Se describen los componentes principales del sistema, el flujo de trabajo, las tecnologías evaluadas y las decisiones finales.

> Dado que los modelos están en continua actualización y mejora, las selecciones de este post sólo se deben tomar como referencia y los modelos que se utilizarán se decidirán cuando realmente se comience el desarrollo del módulo donde se necesiten.
{: .prompt-warning }

> Si necesitas ver que modelos hay y cual se ajusta mejor a tus necesidades puedes consultar [LLM Stats](https://llm-stats.com) o [Artificial Analysis](https://artificialanalysis.ai/).
{: .prompt-info }
## 2. Arquitectura del Sistema

* **Componentes Principales:**

    | Componente | Descripción | Tecnologías Clave |
    | :--- | :--- | :--- |
    | Entrada de Datos | Generación de ideas para contenido. | LLM local (Mixtral 8x7B, Mistral 7B, Phi-2), Google Sheets/Bases de Datos |
    | Procesamiento de Contenido | Creación de guiones, subtítulos, descripciones y síntesis de voz. | LLM (Mixtral 8x7B), NLP, F5 TTS |
    | Producción de Vídeo | Generación y edición de clips de vídeo. | Stable Video Diffusion, ModelScope, FFmpeg, Rife AI |
    | Publicación y Monetización | Detección de momentos virales, generación de shorts y publicación automática. | Whisper AI, FFmpeg, n8n, APIs (YouTube, TikTok, Instagram) |

* **Tecnologías Seleccionadas:**

    | Módulo | Tecnología / Herramienta | Justificación |
    | :--- | :--- | :--- |
    | Generación de Ideas | Mixtral 8x7B (prioridad), Mistral 7B/Phi-2 (alternativas), LLama 2 | Alto rendimiento, eficiencia, versatilidad. |
    | Generación de Guion | Mixtral 8x7B | Excelente coherencia y creatividad. |
    | Síntesis de Voz (TTS) | F5 TTS | Alta calidad de voz y personalización. |
    | Generación de Clips | Stable Video Diffusion/ModelScope | Calidad visual y adaptabilidad. |
    | Edición y Ensamblaje | FFmpeg + Rife AI | Eficiencia y mejora de calidad. |
    | Detección de Momentos Virales | Whisper AI | Precisión en la detección. |
    | Generación de Shorts | FFmpeg | Recorte automático eficiente. |
    | Publicación Automática | n8n | Automatización flexible y sin código. |
    | Bases de datos | PostgreSQL/MongoDB/ChromaDB | Almacenamiento eficiente de datos y embeddings. |
    | Gestión de modelos de IA | Ollama, LMStudio, Hugging Face | Facilidad de gestión y acceso a modelos. |

## 3. Infraestructura de Software

* **Sistema Operativo:**
    * Windows 11 (evaluar rendimiento en Linux para optimización).
* **Orquestación:**
    * n8n (automatización de flujos de trabajo).
* **Gestión de Modelos:**
    * Ollama, LMStudio, Hugging Face (administración y despliegue de modelos).
* **Bases de Datos:**
    * PostgreSQL/MongoDB (almacenamiento de datos estructurados y no estructurados).
    * ChromaDB (gestión de embeddings para LLMs).

## 4. Proceso de Evaluación

* **Criterios Clave:**
    * Rendimiento (velocidad, eficiencia).
    * Calidad (precisión, naturalidad).
    * Flexibilidad (personalización, integración).
    * Costo (licencias, hardware).
    * Comunidad y soporte.
* **Metodología:**
    * Pruebas comparativas de modelos LLM (rendimiento, calidad).
    * Evaluación de calidad de TTS (naturalidad, claridad).
    * Análisis de rendimiento de herramientas de vídeo (eficiencia, calidad).
    * Pruebas de flujos de trabajo en n8n (fiabilidad, eficiencia).

## 5. Decisiones y Justificación

* **LLM Local:**
    * Mixtral 8x7B: rendimiento superior en tareas creativas y de razonamiento.
    * Mistral 7B y Phi-2: alternativas eficientes para recursos limitados.
    * LLama 2: gran versatilidad.
* **TTS:**
    * F5 TTS: calidad de voz excepcional y opciones de personalización.
* **n8n:**
    * Automatización flexible y sin código, ideal para integrar diferentes servicios.
* **ChromaDB:**
    * Mejora significativa del rendimiento de los LLM locales mediante la gestión eficiente de embeddings.

## 6. Plan de Implementación

* **Fase 1:**
    * Configuración de infraestructura (hardware, SO, n8n).
    * Instalación y configuración de LLMs locales.
    * Integración de ChromaDB y bases de datos.
* **Fase 2:**
    * Desarrollo de flujos de trabajo en n8n.
    * Integración de TTS y herramientas de vídeo.
    * Pruebas y optimización de rendimiento.
* **Fase 3:**
    * Implementación de publicación automática y monitorización.
    * Pruebas exhaustivas y ajustes finales.

## 7. Consideraciones Finales

* Mantenimiento y actualización continua de modelos y herramientas.
* Pruebas A/B para optimización de contenido y formatos.
* Seguimiento de avances en IA y producción de vídeo para mejoras futuras.
