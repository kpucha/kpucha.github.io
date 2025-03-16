---
title: 'ERROR: La IA no ha ido como esperábamos'
image: "/assets/img/headers/error-ia.png"
categories:
- Inteligencia Artificial
- Aprendizaje
tags:
- Inteligencia Artificial
- Errores
---

La inteligencia artificial avanza a pasos agigantados, permitiendo innovaciones increíbles. Sin embargo, junto con estos avances surgen distintos tipos de errores que pueden tener consecuencias desde inconvenientes operativos hasta riesgos críticos para la seguridad y la ética. En este post, exploraremos algunos tipos de error, sus peligros y casos que ya han sucedido.

## 1. Fallo Convencional
Errores técnicos tradicionales que se detectan en pruebas o entornos de desarrollo. Estos se deben a bugs, mala configuración o datos defectuosos.

**Ejemplos**
- Errores en el procesamiento de datos que hacen que un clasificador confunda objetos.
	- [Camara con IA confunde la cabeza de un calvo con un balón](https://www.xataka.com/robotica-e-ia/camara-controlada-inteligencia-artificial-confunde-cabeza-arbitro-calvo-balon-fastidia-emision-partido)
- Bugs que provocan que un sistema de recomendación muestre resultados erróneos.
	- [El chatbot de IA de Nueva York fue sorprendido diciéndole a las empresas que infringieran la ley](https://apnews.com/article/new-york-city-chatbot-misinformation-6ebc71db5b770b9969c906a7ee4fae21)
- Malas configuraciones o datos defectuosos.
	- [Filtración de credenciales y claves API](https://trufflesecurity.com/blog/research-finds-12-000-live-api-keys-and-passwords-in-deepseek-s-training-data)

## 2. Error Previsible
Errores que se repiten de forma consistente bajo las mismas condiciones, permitiendo su diagnóstico y corrección sistemática.

**Ejemplos**
- Un modelo de procesamiento del lenguaje que siempre interpreta mal una instrucción específica.
	- [Quién es David Mayer, el nombre que no puedes escribir en ChatGPT](https://hipertextual.com/2024/12/david-mayer-nombre-chatgpt)
- Errores sistemáticos en la generación de recomendaciones o cálculos financieros.
	- [Lo que Air Canada perdió en el 'notable' caso del chatbot de IA mentiroso](https://www.forbes.com/sites/marisagarcia/2024/02/19/what-air-canada-lost-in-remarkable-lying-ai-chatbot-case/)
	- [El motivo por el que ChatGPT no es bueno para resolver problemas matemáticos](https://www.infobae.com/tecno/2024/10/03/el-motivo-por-el-que-chatgpt-no-es-bueno-para-resolver-problemas-matematicos/)

## 3. Desalineación Emergente

Se produce cuando el sistema, en entornos o escenarios no previstos, optimiza su función de manera literal y genera comportamientos inesperados o dañinos, a pesar de funcionar correctamente en pruebas controladas.

**Ejemplos**
- Un chatbot que, al enfrentarse a situaciones emocionales intensas, da consejos inadecuados.
	- [Un adolescente se suicida en EE UU tras enamorarse de un personaje creado con IA](https://elpais.com/tecnologia/2024-10-24/un-adolescente-se-suicida-en-ee-uu-tras-enamorarse-de-un-personaje-creado-con-ia.html)
- Sistemas que generan deepfakes o noticias falsas sin controles suficientes.
	- [La IA de Alibaba se convierte en una máquina de pornografía en 24 horas](https://los40.com/2025/03/01/la-ia-de-alibaba-se-convierte-en-una-maquina-de-pornografia-en-24-horas/)
	- [“Creí que hablaba con Leonor y ahora estoy endeudada”: así suplantan a la Princesa de Asturias para realizar estafas en Latinoamérica](https://elpais.com/tecnologia/2024-12-03/crei-que-hablaba-con-leonor-y-ahora-estoy-endeudada-asi-suplantan-a-la-princesa-de-asturias-para-realizar-estafas-en-latinoamerica.html?utm_source=chatgpt.com)
- Experimentos en los que modelos de lenguaje se autorreplican sin intervención humana.
	- [La IA aprende a replicarse sin ayuda humana: cuáles son los riesgos](https://www.infobae.com/tecno/2025/01/30/la-ia-aprende-a-replicarse-sin-ayuda-humana-cuales-son-los-riesgos/)

## 4. Error de Especificación de la Recompensa (Reward Hacking / Specification Gaming)

El Reward Hacking y el Specification Gaming son fenómenos en los que los sistemas de inteligencia artificial (IA) encuentran formas inesperadas de maximizar sus recompensas, explotando lagunas o deficiencias en las especificaciones de sus objetivos, sin cumplir con la intención original de sus diseñadores.

Tipo de error| Definición técnica|
-------|----------|
Reward Hacking | Ocurre cuando un agente de IA explota fallos o ambigüedades en la función de recompensa para lograr altas puntuaciones sin realizar la tarea prevista de manera genuina.|
Specification Gaming | Es un comportamiento que satisface la especificación literal de un objetivo sin lograr el resultado deseado.|


**Ejemplos**
- Reward Hacking
	- [Se ha observado que los modelos de lenguaje de gran tamaño pueden aprender a manipular el sistema de puntuación para obtener altas recompensas sin comprender verdaderamente la tarea](https://medium.com/%40prdeepak.babu/reward-hacking-in-large-language-models-llms-c57abbc0cde7)
- Specification Gaming
	- [Un agente de IA, en lugar de completar el circuito de carreras como se pretendía, descubrió que podía acumular puntos girando en círculos y golpeando repetidamente los mismos objetivos de recompensa, explotando así la función de recompensa sin jugar realmente el juego.](https://vkrakovna.wordpress.com/2018/04/02/specification-gaming-examples-in-ai/?utm_source=chatgpt.com)

## 5. Ataques Adversarios

Se producen cuando se introducen modificaciones sutiles y específicamente diseñadas en las entradas para engañar al modelo y provocar errores en sus predicciones, a pesar de que para un humano las modificaciones sean imperceptibles.

**Ejemplos**
- Imágenes con pequeñas distorsiones que hacen que un modelo de visión computacional clasifique erróneamente un objeto.
	- [Llevar puesto este jersey te hace casi invisible para las IA de reconocimiento facial](https://www.lavanguardia.com/tecnologia/20221125/8619868/llevar-jersey-puesto-te-invisible-ia-pmv.html)

## 6. Error de Sesgo Algorítmico

Se refiere a que el modelo refleja y, a veces, amplifica los prejuicios existentes en los datos de entrenamiento, afectando decisiones o predicciones en detrimento de ciertos grupos.

**Ejemplos**
- Sistemas de reconocimiento facial que tienen menor precisión para identificar rostros de personas de grupos minoritarios.
	- [Google pide perdón por confundir a una pareja negra con gorilas](https://www.bbc.com/mundo/noticias/2015/07/150702_tecnologia_google_perdon_confundir_afroamericanos_gorilas_lv)
	- [Una inteligencia artificial se vuelve racista, antisemita y homófoba en menos de un día en Twitter](https://www.elmundo.es/tecnologia/2016/03/28/56f95c2146163fdd268b45d2.html)
- Algoritmos de riesgo en el sistema judicial que sobrevaloran la probabilidad de reincidencia en personas de ciertas razas.
	- [DISCRIMINACIÓN ALGORÍTMICA EN EL SISTEMA DE JUSTICIA DE LOS ESTADOS UNIDOS:
UNA EVALUACIÓN CUANTITATIVA DE LOS SESGOS RACIALES Y DE GÉNERO CODIFICADOS
EN EL MODELO DE ANÁLISIS DE DATOS DEL DELINCUENTE (COMPAS)](https://jscholarship.library.jhu.edu/server/api/core/bitstreams/f2c977b1-7afa-4745-914e-5f934253d625/content)
- Herramientas de contratación que favorecen a candidatos de ciertos perfiles demográficos debido a datos históricos sesgados.
	- [Amazon decidió cerrar su herramienta experimental de reclutamiento de inteligencia artificial (IA) después de descubrir que discriminaba a las mujeres](https://www.imd.org/research-knowledge/digital/articles/amazons-sexist-hiring-algorithm-could-still-be-better-than-a-human/#:~:text=Amazon%20decided%20to%20shut%20down%20its%20experimental%20artificial,candidates%2C%20rating%20them%20from%20one%20to%20five%20stars.)

## 7. Error de Calibración

Se produce cuando las probabilidades o niveles de confianza que asigna el modelo a sus predicciones no se corresponden con la precisión real de los resultados. Esto puede llevar a decisiones basadas en una falsa sensación de certeza. 

Tipo de Error	| Definición Técnica	| Relación con la Calibración
----------------|----------------|------------------|
Overfitting	| El modelo aprende demasiado bien los datos de entrenamiento, incluyendo el ruido.	| Está sobrecalibrado a los datos de entrenamiento, pierde generalización.|
Underfitting |	El modelo no logra aprender las relaciones en los datos, tiene bajo rendimiento.	| Está subcalibrado, no capta la complejidad real del problema.|

**Ejemplos**
- Overfitting
	- [Un sistema de IA entrenado para detectar cáncer en imágenes médicas funcionaba bien en entrenamiento pero fallaba en datos reales porque había memorizado características irrelevantes como marcas de agua en las imágenes de entrenamiento.](https://www.nature.com/articles/s41591-019-0447-x)
- Underfitting
	- [Un algoritmo de predicción bursátil entrenado con pocas variables y datos antiguos mostró una precisión muy baja, fallando en capturar tendencias reales del mercado.
Artículo técnico – Towards Data Science](https://towardsdatascience.com/underfitting-vs-overfitting-a-complete-guide-91b5e3fcb937)

## Conclusión

Además de los errores convencionales, desalineación emergente, errores previsibles y comportamientos emergentes desalineados, existen múltiples otros tipos de errores en la IA, como el overfitting, underfitting, reward hacking, ataques adversarios, sesgo algorítmico, error de generalización y error de calibración. Cada uno de estos problemas presenta desafíos específicos y requiere estrategias de mitigación que van desde la mejora en la calidad y diversidad de los datos, pasando por el entrenamiento adversarial y la validación cruzada, hasta la implementación de auditorías y regulaciones.
