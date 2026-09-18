# Clase 2: Ingeniería de prompt

## Objetivo

Reconocer cómo un `system prompt` gobierna la conducta de un modelo local y practicar su diseño con pedidos de trabajo sintéticos de soporte para Casinos Play.

La clase trabaja sobre el prompt, no sobre un procedimiento de soporte. El alumno observa el efecto de cambiar solamente el `system prompt` mientras mantiene fijos los mensajes de prueba.

## Duración

90 minutos como máximo.

## Resultado esperado

Al finalizar, cada alumno habrá:

- ejecutado dos demos comparativas sobre la diferencia entre `user prompt` y `system prompt`;
- completado cuatro `system prompt` para trabajar anatomía, límites, few-shot y pensamiento en pasos;
- comparado respuestas del mismo modelo con mensajes de usuario fijos;
- elegido el `system prompt` que mejor controló formato y límites.

## Definición operativa

> Ingeniería de prompt es diseñar la instrucción que gobierna al modelo. En un chat local, esa instrucción persistente es el system prompt.

## Secuencia de la clase

### 0. Carga del modelo — 10 a 15 minutos

Qué proyectar:

- Las celdas de carga del modelo local.
- La selección automática del archivo GGUF `Q4_K_M` desde `LiquidAI/LFM2.5-1.2B-Instruct-GGUF`.
- La función única `llamar_llm`.
- La prueba corta que imprime `Todo listo.` y consulta al modelo para obtener `Entorno preparado.`

Punto docente: si la prueba no corre, detenerse en el entorno. No seguir con la actividad hasta comprobar que el modelo local responde.

El notebook no instala paquetes. Se asume el entorno preparado de la Clase 1 con `llama-cpp-python` y `huggingface_hub`.

### 1. Qué es ingeniería de prompt — 20 minutos

Qué proyectar:

- Demo A completa: el mismo pedido de trabajo con un prompt mínimo y con un prompt que contiene rol, contexto, instrucción, formato y output esperado.
- Demo B completa: el mismo mensaje de usuario con dos `system_prompt` distintos.
- La definición operativa de esta guía y del notebook.

Qué observar con el grupo:

- En Demo A, qué cambia al agregar las cinco partes.
- En Demo B, cómo cambia la conducta aunque el mensaje del usuario sea idéntico.
- La diferencia entre el `system prompt`, que contiene la instrucción persistente, y el `user prompt`, que contiene el pedido puntual que se consulta.

No hay que inventar prompts ni editar mensajes en esta sección: las dos demos están listas para ejecutar.

Cierre conceptual de la sección: las cinco partes son rol, contexto, instrucción, formato y output esperado. No agregar otra actividad.

### 2. Los cuatro ejercicios — 50 a 55 minutos

Esta es la única actividad del alumno. En los cuatro ejercicios se conserva la misma mecánica:

1. Completar solamente el `system_prompt` marcado con `TODO`.
2. No modificar los mensajes de prueba.
3. Ejecutar el `for` que llama a `llamar_llm(..., system_prompt=...)` e imprime cada respuesta.
4. Contestar las preguntas de observación que están debajo.

El alumno no diseña el `user prompt`. Solo cambia la instrucción del sistema.

#### Ejercicio 1. Anatomía

El alumno completa las cinco partes dentro del `system_prompt`: rol, contexto, instrucción, formato y output esperado. Luego ejecuta tres pedidos de trabajo fijos: una cámara sin imagen, una impresora con rayas y una app de caja que se cierra.

Qué mirar: si el modelo mantiene el formato solicitado en los tres casos aunque cambie el problema.

#### Ejercicio 2. Límites

El alumno completa un `system_prompt` que debe indicar qué no hacer. El sistema incluye como límites mínimos no inventar, no presentar un diagnóstico como hecho y no salirse del soporte técnico. Los tres mensajes fijos contienen un pedido válido, una acción riesgosa y una consulta fuera de tema.

Qué mirar: si la respuesta conserva el alcance de soporte y evita convertir una suposición o una acción riesgosa en una instrucción.

#### Ejercicio 3. Few-shot

Primero se ejecuta un `system_prompt` zero-shot sobre el mismo conjunto fijo de pedidos. Después se completa otro `system_prompt` con ejemplos dentro del sistema y se vuelve a ejecutar exactamente el mismo conjunto. Las categorías son `hardware`, `red`, `aplicación` y `no es soporte`.

Qué mirar: si los ejemplos ayudan a sostener las categorías y el formato sin tocar los mensajes de usuario.

#### Ejercicio 4. Chain of thought

Se compara el mismo pedido fijo con un sistema sin la instrucción de pensar en pasos y otro sistema que pide revisar internamente el caso en pasos antes de responder. La respuesta final debe mostrar solo el formato solicitado, no un razonamiento privado extenso.

Qué mirar: qué cambia en la organización y consistencia de la respuesta cuando la instrucción de revisión en pasos está en el sistema.

### 3. Cierre breve — 5 minutos

Qué proyectar:

- La celda final del notebook.
- El `system_prompt` que cada alumno considera más efectivo.

Qué completa el alumno:

- Copiar en la celda final el mejor sistema del día: el que mejor controló formato y límites.
- No se agrega una ronda oral ni una plantilla adicional de soporte.

## Criterio de cierre docente

La clase queda alineada si el alumno puede señalar, a partir de las ejecuciones, qué parte de una instrucción modifica el comportamiento del modelo y por qué el `system prompt` es el objeto de trabajo de la clase. Las respuestas son experimentales: el modelo local puede equivocarse y no se presenta ninguna salida como verdad operativa.
