# Clase 2: Ingeniería de prompt

**Capacitación en Inteligencia Artificial y Automatización Aplicada a Soporte Técnico**  
**Casinos Play**

---

## Objetivo

Vas a reconocer cómo un `system prompt` gobierna la conducta de un modelo local y vas a practicar su diseño con pedidos de trabajo sintéticos de soporte para Casinos Play.

Esta clase trabaja sobre el prompt, no sobre un procedimiento de soporte. Vas a observar el efecto de cambiar solamente el `system prompt` mientras mantenés fijos los mensajes de prueba.

## Qué vas a poder hacer

Al finalizar esta clase vas a haber:

- explicado, con palabras de soporte, qué es un prompt y qué es ingeniería de prompt;
- distinguido `system prompt` (instrucción que queda puesta) de `user prompt` (pedido de este turno);
- reconocido las cinco partes: rol, contexto, instrucción, formato y output esperado;
- ejecutado dos demos comparativas;
- completado cuatro `system prompt` para anatomía, límites, few-shot y pensamiento en pasos;
- elegido el `system prompt` que mejor controló formato y límites.

## Cómo recorre esta clase

Teoría primero, práctica después:

```text
situación → concepto breve → demostración → práctica → cierre
```

La explicación es breve y te sirve para mirar mejor las demos. El resultado observable es un `system prompt` que controla formato y límites frente a pedidos distintos.

Vas a leer este texto para aclarar la teoría. La práctica la ejecutás en el notebook `clase_2_ingenieria_de_prompt.ipynb`.

## Antes de empezar

- Ya viste la Clase 1: modelo de lenguaje, token, contexto, alucinación y uso responsable.
- Vas a usar el entorno de la Clase 1: Python, `.venv`, `llama-cpp-python` y `huggingface_hub`. Este notebook no instala paquetes.
- No se usa Colab, Gemini ni APIs de modelos comerciales.

El modelo local es `LFM2.5-1.2B-Instruct` (`unsloth`, GGUF `Q4_0`): repositorio `unsloth/LFM2.5-1.2B-Instruct-GGUF` y archivo `LFM2.5-1.2B-Instruct-Q4_0.gguf`. Se descarga desde Hugging Face en la primera ejecución.

---

## Caso inicial — un pedido informal

Leé este mensaje sintético como si llegara por WhatsApp o por teléfono durante un turno:

> Hola, soy de caja. La impresora de tickets imprime con rayas, hay gente en la fila y el supervisor pregunta qué hacemos. ¿Podés ver?

Qué pasa si eso se manda así, cada vez, a un modelo:

- a veces inventa una causa;
- a veces arma un procedimiento largo;
- a veces responde como un chat;
- casi nunca mantiene el mismo formato.

El pedido cambia a cada rato. Lo que no debería cambiar es la conducta del asistente: rol, límites, formato y qué se puede afirmar.

Eso motiva la pregunta de la clase: **¿dónde se escribe la instrucción que queda puesta, aunque cambie el pedido de este turno?**

En esta sección todavía no ejecutes demos. Primero queda clara esa pregunta.

---

## Explicación conceptual

### 1. Qué es un prompt

Un **prompt** es la instrucción que le damos al modelo en una consulta: el texto que condiciona qué tipo de respuesta puede devolver.

En el trabajo de soporte no es un hechizo ni un comando de sistema. Es el encuadre de la consulta, igual que cuando le pedimos algo a un compañero: si el pedido es vago, la respuesta también.

### 2. Qué es ingeniería de prompt

> Ingeniería de prompt es diseñar la instrucción que gobierna al modelo. En un chat local, esa instrucción persistente es el system prompt.

En lenguaje de soporte: no es “hablarle lindo a la IA”. Es **diseñar la instrucción de trabajo** para que el modelo se comporte de forma repetible: mismo rol, mismos límites, mismo formato, aunque el pedido de caja, cámaras o red sea distinto.

### 3. System prompt vs user prompt

| Pieza | Qué es | Analogía operativa |
| --- | --- | --- |
| `system prompt` | Instrucción persistente. Queda puesta para toda la consulta. | La consigna del puesto: quién sos, cómo respondés, qué no podés hacer. |
| `user prompt` | Pedido de este turno. Cambia en cada llamado. | El mensaje de WhatsApp o el llamado de ahora. |

```text
pedido informal (WhatsApp / teléfono)
                 |
                 v
   +----------------------+     +----------------------+
   | SYSTEM PROMPT        |     | USER PROMPT          |
   | instrucción que      |     | pedido de este turno |
   | queda puesta         |     |                      |
   +----------+-----------+     +----------+-----------+
              |                            |
              +-------------+--------------+
                            v
                     modelo local
                            v
                       respuesta
```

El modelo no “sabe” el turno. Solo ve esas dos piezas. Si el sistema está flojo, cada pedido improvisa. Si el sistema está bien diseñado, el pedido puede cambiar y la conducta se sostiene.

### 4. Las cinco partes

No todas hacen falta en cada frase, pero sirven para diagnosticar por qué una respuesta salió desordenada.

| Parte | Qué controla | Ejemplo corto (Casinos Play) |
| --- | --- | --- |
| Rol | Desde qué función responde | Asistente de soporte de primer nivel de Casinos Play |
| Contexto | Qué situación tiene y qué no tiene | Pedido sintético de caja; no hay acceso a sistemas reales |
| Instrucción | Qué tiene que hacer | Organizar el pedido y proponer una verificación inicial segura |
| Formato | Cómo se organiza la salida | Etiquetas: Hecho informado / Verificación inicial / Respuesta |
| Output esperado | Qué debe incluir o evitar | Breve, sin afirmar una causa no confirmada |

Ejemplo unido, todavía corto:

```text
Rol: soporte de primer nivel de Casinos Play.
Contexto: pedido de trabajo sintético; no hay herramientas reales.
Instrucción: organizar el pedido sin inventar la causa.
Formato: Hecho informado / Verificación inicial / Respuesta.
Output esperado: tres bloques breves y un próximo paso no disruptivo.
```

La parte que más se omite, y más se nota cuando falta, es el **formato**. Sin formato, el modelo elige la forma — y no siempre elige la que sirve en un turno.

### 5. Por qué el objeto de esta clase es el system prompt

Los pedidos van a seguir llegando desordenados. El `user prompt` es el pedido de este turno. El `system prompt` es lo que gobierna:

- la conducta (rol y tono);
- el formato (etiquetas, orden, extensión);
- los límites (no inventar, no diagnosticar como hecho, no salirse de soporte).

Por eso, en las demos y en los cuatro ejercicios, **solo vas a diseñar el sistema**. Los mensajes de usuario están fijos a propósito.

### 6. Qué no es esta clase

Esta clase no es:

- diagnosticar hardware ni “arreglar” la impresora, la cámara o la app;
- armar un procedimiento de autorización o de escalamiento;
- diseñar un sistema de gestión de pedidos.

El modelo local **no confirma el estado técnico real**. Una respuesta útil ordena el pedido; no reemplaza la verificación en el piso.

### Criterio profesional (para nombrar, no para practicar diagnóstico)

Aunque el objeto sea el prompt, el lenguaje de las respuestas tiene que respetar el trabajo de soporte:

| Se puede | No se puede |
| --- | --- |
| Repetir un hecho informado | Inventar una causa |
| Pedir una verificación no disruptiva | Tratar una hipótesis como diagnóstico |
| Marcar dato faltante | Completar huecos con suposiciones |
| Quedarse en el alcance de soporte | Indicar una acción riesgosa como si fuera segura |

---

## Recorrido de la práctica

Cuando la teoría esté clara, pasá al notebook. El entorno es soporte de la práctica, no el objeto de estudio.

### 1. Carga del modelo

Ejecutá, en orden:

- las celdas de carga del modelo local;
- la descarga del archivo GGUF `LFM2.5-1.2B-Instruct-Q4_0.gguf` desde `unsloth/LFM2.5-1.2B-Instruct-GGUF`;
- la función única `llamar_llm`;
- la prueba corta que imprime `Todo listo.` y consulta al modelo para obtener `Entorno preparado.`

Si la prueba no corre, resolvé el entorno antes de pasar a las demos.

El notebook no instala paquetes. Se asume el entorno preparado de la Clase 1 con `llama-cpp-python` y `huggingface_hub`.

### 2. Demostración

En esta sección no inventes prompts ni edites mensajes: las dos demos están listas para ejecutar.

**Demo A.** Vas a ver el mismo pedido de trabajo con un prompt mínimo y con un prompt que contiene rol, contexto, instrucción, formato y output esperado. Observá qué cambia al agregar las cinco partes en el `user prompt`. El pedido de trabajo es el mismo.

**Demo B.** Vas a ver el mismo mensaje de usuario con dos `system_prompt` distintos. Observá cómo cambia la conducta aunque el mensaje del usuario sea idéntico.

Después de ejecutar, volvé a esta idea:

> Ingeniería de prompt es diseñar la instrucción que gobierna al modelo. En un chat local, esa instrucción persistente es el system prompt.

Las cinco partes son rol, contexto, instrucción, formato y output esperado. El control que nos interesa para el resto de la clase está en el sistema.

### 3. Práctica: los cuatro ejercicios

En cada ejercicio vas a:

1. Completar solamente el `system_prompt` marcado con `TODO`.
2. No modificar los mensajes de prueba.
3. Ejecutar el `for` que llama a `llamar_llm(..., system_prompt=...)` e imprime cada respuesta.
4. Contestar las preguntas de observación que están debajo.

No diseñás el `user prompt`. Solo cambiás la instrucción del sistema.

#### Ejercicio 1. Anatomía

Completá las cinco partes dentro del `system_prompt`: rol, contexto, instrucción, formato y output esperado. Después ejecutá tres pedidos de trabajo fijos: una cámara sin imagen, una impresora con rayas y una app de caja que se cierra.

Observá si el modelo mantiene el formato solicitado en los tres casos aunque cambie el problema.

Preguntas de observación:

- ¿El modelo mantuvo las mismas etiquetas y el mismo orden en los tres pedidos?
- ¿Qué parte de las cinco fue más importante para sostener el formato?
- ¿Qué cambió entre los casos sin que cambiaras el `system_prompt`?

#### Ejercicio 2. Límites

Completá un `system_prompt` que indique qué no hacer. El sistema incluye como límites mínimos no inventar, no presentar un diagnóstico como hecho y no salirse del soporte técnico. Los tres mensajes fijos contienen un pedido válido, una acción riesgosa y una consulta fuera de tema.

Observá si la respuesta conserva el alcance de soporte y evita convertir una suposición o una acción riesgosa en una instrucción.

Preguntas de observación:

- ¿Evitó inventar una causa o un resultado de prueba?
- ¿Cómo respondió ante la acción riesgosa sin convertirla en una instrucción operativa?
- ¿Marcó el pedido fuera de tema y volvió al alcance de soporte?

#### Ejercicio 3. Few-shot

Primero ejecutá un `system_prompt` zero-shot sobre el mismo conjunto fijo de pedidos. Después completá otro `system_prompt` con ejemplos dentro del sistema y volvé a ejecutar exactamente el mismo conjunto. Las categorías son `hardware`, `red`, `aplicación` y `no es soporte`.

Observá si los ejemplos ayudan a sostener las categorías y el formato sin tocar los mensajes de usuario.

Preguntas de observación:

- ¿Qué diferencia viste entre zero-shot y few-shot con el mismo conjunto de mensajes?
- ¿Los ejemplos ayudaron a mantener las cuatro categorías y el formato?
- ¿Qué error de clasificación seguiría necesitando revisión humana?

#### Ejercicio 4. Chain of thought

Compará el mismo pedido fijo con un sistema sin la instrucción de pensar en pasos y otro sistema que pide revisar internamente el caso en pasos antes de responder. La respuesta final debe mostrar solo el formato solicitado, no un razonamiento privado extenso.

Observá qué cambia en la organización y consistencia de la respuesta cuando la instrucción de revisión en pasos está en el sistema.

Preguntas de observación:

- ¿Qué cambió en la organización de la respuesta al pedir una revisión interna en pasos?
- ¿El formato final se mantuvo aunque el sistema agregara esa instrucción?
- ¿Qué limitación del modelo local seguís observando?

### 4. Cierre

En la celda final del notebook, copiá el `system_prompt` que consideres más efectivo: el que mejor controló formato y límites.

---

## Si algo no sale como esperabas

| Qué puede pasar | Qué hacer |
| --- | --- |
| La carga del modelo falla o tarda | No saltes a las demos. Revisá kernel `.venv`, red y archivo `Q4_0`. |
| El modelo no respeta el formato | Es material de observación, no un fallo de la clase. Señalá qué parte del sistema estaba floja. |
| Inventa una causa o un resultado | Volvé a la tabla de hechos vs hipótesis. El sistema tiene que prohibirlo con claridad. |
| Few-shot no alcanza para las cuatro categorías | Los ejemplos ayudan, pero no reemplazan la revisión humana. |
| Dan ganas de “arreglar” el caso técnico | El objeto es la instrucción, no el diagnóstico. |

Las respuestas son experimentales: el modelo local puede equivocarse y ninguna salida se presenta como verdad operativa.

## Seguridad, autorización y alcance

- Usá solo pedidos sintéticos. No cargues credenciales, datos personales ni información real del casino.
- El asistente no autoriza cambios de configuración, no desactiva protecciones y no indica acciones disruptivas.
- Si un mensaje pide algo riesgoso o fuera de tema, el `system prompt` tiene que devolver el caso al alcance de soporte o marcarlo como fuera de alcance.
- Nada de lo que imprima el modelo se ejecuta en equipos reales durante la clase.

## Qué te llevás

La clase queda hecha si podés señalar, a partir de las ejecuciones, qué parte de una instrucción modifica el comportamiento del modelo y por qué el `system prompt` es el objeto de trabajo.

## Conexión con la siguiente clase

Cuando puedas diseñar una instrucción persistente, el paso siguiente es usarla para transformar pedidos informales (WhatsApp / teléfono) en un registro operativo consistente: hechos, datos faltantes y próximo paso, sin inventar información.

Esta clase deja el instrumento. La siguiente puede dejar el registro.
