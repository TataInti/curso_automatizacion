# Reglas de trabajo para las próximas clases

Este archivo es el contrato de trabajo del repositorio. Lo usan quienes arman las clases (Inti y los bots). No es material de alumno.

## Regla principal

Cada clase nueva se prepara como un **paquete de aula** con dos materiales complementarios:

1. Un documento principal en Markdown (`.md`), con el desarrollo completo de la clase.
2. Una presentación de diapositivas para la explicación presencial, legible en el TV del aula.

Las diapositivas no reemplazan al Markdown ni son una copia reducida de todo su texto. El Markdown conserva el detalle; las diapositivas ordenan y hacen visible el recorrido.

Esta regla vale para las clases nuevas. No obliga a rehacer el material existente, salvo que se decida revisarlo.

## A quién está dirigida la capacitación

El curso es para **soporte técnico de IT de oficio**, no para un grupo de desarrollo.

Los casos tienen que reflejar el trabajo real:

- mantenimiento y diagnóstico de hardware;
- tendido y verificación de cables y conexiones de red;
- cámaras y sistemas de seguridad;
- impresoras y periféricos;
- sistemas internos y aplicaciones de uso cotidiano;
- atención de incidentes y situaciones nuevas.

Separar con claridad dos cosas distintas:

- **Sí hay experiencia técnica especializada** en el oficio de soporte: hardware, red, cámaras, impresoras, sistemas internos, incidentes. Aprenden principalmente en la práctica y resuelven sobre la marcha.
- **No hay fluidez** en Python, entorno virtual, Jupyter, kernel, librerías ni prompting. Esos cimientos son básicos. No tratarlos como obvios ni como “experiencia técnica” del mismo tipo.

La formación tiene que conectar esa experiencia de oficio con una visión más integral del servicio: personas, equipos, red, sistemas, procedimientos, riesgos y comunicación. No da por sabido el stack de programación.

## Nivel de partida para diseñar

Asumir piso bajo en Python, venv, notebook y prompting. Subir de a un escalón.

Si el material da por sabido el entorno, la clase se gasta ahí y no llega al caso de trabajo.

Hasta que el grupo tenga el entorno en piloto automático, el éxito de la clase se mide por el caso resuelto, no por el stack que quedó instalado.

## Criterios para diseñar cada clase

### 1. Partir de una situación de trabajo visible

Cada clase empieza con un incidente, pedido o tarea reconocible: instalación, falla, consulta de usuario, mensaje informal, necesidad de mejorar un procedimiento.

El caso se ve: un mensaje, un pedido, una pantalla, un texto. No se empieza por pip, venv, Jupyter ni por una teoría sin un texto de trabajo delante.

La actividad lleva a observar, preguntar, verificar, proponer y comunicar; no solamente a recibir una explicación.

### 2. Conectar el trabajo físico con el razonamiento técnico

Cuando corresponda, mostrar el vínculo entre:

- lo que se instala, conecta, mide o revisa físicamente;
- lo que se observa en una red, cámara, impresora o sistema;
- las hipótesis posibles;
- las verificaciones seguras;
- la decisión de resolver, escalar o pedir autorización.

No presentar la parte práctica y la parte conceptual como mundos separados.

### 3. Práctica extrema y un solo concepto nuevo

Las clases son extremadamente prácticas.

- Un solo concepto nuevo por clase. Ese concepto se ve, se usa y se deja hecho. Recién después, otro.
- Un producto visible al final (un prompt que sale, un registro armado, un texto comparable).
- Vocabulario nuevo solo cuando el participante acaba de usarlo.
- Nada de capas apiladas en la misma hora (entorno → librería → notebook → modelo → prompt).
- No meter varios ejercicios de calentamiento antes del caso real.

### 4. Cero saltos de abstracción: entrada → acción → resultado

Cada paso muestra **entrada → acción → resultado**. Si no se ve, no se enseña.

Pasos numerados. Una acción por paso. Resultado esperado escrito.

No encadenar tres herramientas nuevas en un mismo paso.

Bajar abstracción: mostrar el mensaje, el prompt, el resultado; no explicar capas de tooling primero.

### 5. Trabajar en ciclos breves

Secuencia recomendada:

```text
situación → concepto breve → demostración → práctica → puesta en común → cierre
```

La explicación es breve y sirve para mejorar la siguiente acción. Cada clase tiene un resultado observable y una actividad en la que el grupo puede mostrarlo.

Si en 15–20 minutos no hubo un resultado concreto, el material está alto: recortar concepto, no recortar práctica.

### 6. El entorno no es el tema de la clase

No asumir venv, notebook, kernel ni librerías.

El setup no es el contenido. Si hace falta el entorno, o está listo antes de la clase, o es un único paso mecánico ya escrito.

Regla de corte: **si el venv falla y la clase se cae, el material está mal.** Antes de publicar o dictar: ¿se puede hacer el trabajo de hoy si el venv falla? Si la respuesta es no, hay que bajarlo.

No abrir con instalación de librerías, activación de venv, kernel ni “si falla ModuleNotFoundError…”.

No dar por hecho que el notebook de la clase anterior quedó funcionando en todas las máquinas.

Si hay notebook: celdas pensadas para ejecutar el caso, no para diagnosticar Python.

Tiempo de aula al caso, no a instalar.

### 7. Diseñar para ~12 personas, espacio chico, un solo TV

- Priorizar parejas o grupos pequeños.
- Evitar actividades que requieran que cada persona vea una pantalla diferente al mismo tiempo.
- Indicar con claridad cuándo observa todo el grupo y cuándo trabaja cada equipo.
- Reservar momentos para que los grupos compartan hallazgos sin extenderse.
- Incluir alternativas cuando una demostración física no pueda verse desde todos los lugares.
- Guía `.md` y diapositivas que se puedan seguir sin pelearse con el entorno.

## Requisitos del documento Markdown

El `.md` de cada clase incluye, como mínimo:

- objetivo general y resultados esperados;
- duración y modalidad de trabajo;
- conocimientos o preparación previa necesarios (sin dar por sabido Python, venv ni notebook);
- caso o situación inicial, visible desde el primer momento;
- explicación conceptual en lenguaje claro, atada al caso;
- demostración y actividad práctica paso a paso;
- cada paso con entrada, acción y resultado esperado;
- preguntas para orientar la observación;
- criterios de seguridad, autorización y escalamiento;
- casos de error o información faltante;
- puesta en común y cierre;
- conexión con la clase siguiente;
- materiales, imágenes o archivos complementarios;
- qué hacer si el entorno no está listo, sin convertir eso en el tema.

Las instrucciones detalladas, los procedimientos completos, las advertencias y las consignas de evaluación permanecen en el Markdown, aunque también se resuman visualmente en las diapositivas.

## Requisitos de las diapositivas

La presentación acompaña el mismo recorrido del Markdown y está pensada para visualización grupal en un TV:

- una idea principal por diapositiva;
- títulos breves y visibles desde el fondo del aula;
- poco texto, frases cortas y listas reducidas;
- alto contraste y tamaño de letra legible;
- diagramas, fotografías, capturas o esquemas cuando ayuden a entender;
- pasos numerados para procedimientos y diagnósticos;
- una diapositiva diferenciada para cada consigna importante;
- momentos explícitos para la demostración, la práctica y la puesta en común;
- una diapositiva final con las ideas centrales, los límites y el próximo paso.

No trasladar párrafos extensos del Markdown a las diapositivas. Si una explicación necesita mucho detalle, se presenta oralmente y el desarrollo completo queda en el documento.

## Seguridad y criterio profesional

Toda clase que incluya soporte técnico distingue con claridad:

- hechos observados;
- hipótesis;
- verificaciones pendientes;
- acciones permitidas;
- acciones que requieren autorización;
- situaciones que deben escalarse.

No usar credenciales, datos sensibles ni configuraciones reales en los ejemplos publicados. Las demostraciones tienen que poder repetirse en un entorno controlado y no inducir cambios disruptivos sin explicar antes su impacto.

## Qué priorizar y qué no meter

Priorizar:

- un caso de soporte (pedido informal, datos incompletos, hay que ordenar o responder);
- un producto visible al final de la hora;
- pasos numerados, una acción por paso, resultado esperado escrito;
- guía `.md` y diapositivas seguibles sin pelearse con el entorno;
- tiempo de aula reservado al caso.

No meter:

- abrir la clase con setup;
- teoría de prompting sin un texto de trabajo delante;
- varios ejercicios de calentamiento antes del caso real;
- instrucciones que encadenan tres herramientas nuevas en un mismo paso;
- asumir que el entorno de la clase anterior sigue vivo en todas las máquinas.

## Checklist de entrega

Antes de considerar terminada una clase nueva, verificar:

- el Markdown y las diapositivas tienen el mismo objetivo, caso y secuencia;
- el paquete es `.md` detallado + diapositivas para TV; no falta ninguno de los dos;
- los enlaces e imágenes funcionan desde la carpeta de la clase;
- la presentación se abre y se ve completa en el TV;
- el texto de las diapositivas se lee sin acercarse a la pantalla;
- las consignas y resultados esperados son observables;
- hay un solo concepto nuevo y un producto visible;
- cada paso muestra entrada → acción → resultado;
- se contemplan errores, límites, autorización y escalamiento;
- hechos e hipótesis están separados;
- no se incluyeron secretos ni datos reales sensibles;
- la clase no depende de que el venv, el kernel o las librerías funcionen; si el venv falla, el trabajo de hoy igual se puede hacer;
- el material fue revisado en conjunto antes de la clase.

La clase se considera incompleta si falta el documento Markdown o la presentación que lo acompaña, o si el entorno es condición para que la clase exista.
