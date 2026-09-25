# Clase 3: Visual Studio Code, GitHub Copilot, agentes y skills

**Capacitación en Inteligencia Artificial y Automatización Aplicada a Soporte Técnico**

**Casinos Play**

> **Estado del material:** guía conceptual y consigna del ejercicio integrador. Durante la práctica, cada equipo creará y probará una app de Streamlit conectada al modelo local del curso.

---

## Objetivo general

Aprender a usar Visual Studio Code como un espacio de trabajo técnico asistido por inteligencia artificial y comprender cómo pasar de una conversación ocasional con GitHub Copilot a formas de trabajo repetibles mediante agentes personalizados y skills compartidas.

## Resultados esperados de la clase

Al finalizar este recorrido vas a poder:

- reconocer las zonas principales de Visual Studio Code y explicar para qué sirve cada una;
- entender qué carpeta o repositorio está usando Copilot como contexto;
- pedirle a Copilot una descripción del workspace y contrastarla con los archivos y configuraciones visibles;
- elegir entre los modos **Preguntar (Ask)**, **Plan (Plan)** y **Agente (Agent)** según la tarea;
- distinguir una respuesta informativa, un plan y una acción que modifica el proyecto;
- explicar qué es un agente personalizado y qué decisiones contiene;
- explicar qué es una skill y cuándo conviene crear una;
- diferenciar agentes, skills e instrucciones permanentes del repositorio;
- decidir si una personalización debe ser personal, propia de un repositorio o compartida por el equipo;
- crear con Copilot una app mínima de chat en Streamlit que consulte el modelo local con `llama-cpp-python`;
- reconocer acciones permitidas, acciones que requieren autorización y situaciones que deben escalarse.

## Duración y modalidad

- **Duración total prevista de la clase completa:** 120 minutos.
- **Parte teórica desarrollada en este documento:** 65 minutos.
- **Ejercicio integrador:** 45 minutos.
- **Puesta en común y cierre:** 10 minutos.
- **Grupo:** 12 personas.
- **Organización:** cuatro equipos de tres integrantes.
- **Pantallas:** una computadora por equipo y un TV compartido.

Durante la explicación, todos observan el mismo VS Code en el TV. En el ejercicio, cada equipo rotará estas funciones:

| Función | Responsabilidad |
| --- | --- |
| Operador/a | Usa VS Code y conversa con Copilot. |
| Observador/a | Controla el contexto, los archivos y las acciones propuestas. |
| Relator/a | Registra decisiones, resultados y dudas para la puesta en común. |

## Preparación previa

Antes de la clase se necesita:

- Visual Studio Code actualizado;
- acceso a GitHub Copilot habilitado con una cuenta personal o de la organización;
- una carpeta de práctica abierta en VS Code;
- el entorno virtual del curso preparado con `llama-cpp-python` y el modelo GGUF local ya disponible;
- Streamlit instalado en el mismo entorno virtual;
- Git instalado si se van a compartir archivos mediante un repositorio;
- permiso para usar el modo Agente, ya que una organización puede deshabilitarlo;
- un entorno de práctica sin credenciales, datos reales ni acceso a sistemas de producción.

No hace falta saber programar para comprender esta clase. Sí conviene recordar lo trabajado en las clases anteriores sobre prompts, contexto, alucinaciones y validación humana.

---

## 1. Situación inicial: de una consulta aislada a una forma de trabajo

Imaginá que llega una tarea de soporte compleja. No alcanza con escribir una única pregunta: hay que leer varios archivos, entender un procedimiento existente, identificar información faltante, proponer pasos, generar o modificar materiales y comprobar el resultado.

Antes de empezar aparecen cuatro decisiones:

1. ¿Queremos **entender** algo sin cambiar archivos?
2. ¿Necesitamos **planificar** antes de actuar?
3. ¿Estamos autorizados a que la IA **modifique o ejecute** elementos del proyecto?
4. Si este trabajo se repite, ¿conviene conservar un **rol especializado** o un **procedimiento reutilizable**?

Esas cuatro preguntas organizan toda la clase.

> El ejercicio usa una carpeta de práctica y datos sintéticos. Primero se confirma qué puede saber Copilot sobre el workspace; después se construye una app local pequeña y se revisa antes de ejecutarla.

---

## 2. Visual Studio Code como espacio de trabajo

Visual Studio Code no es solamente un editor de texto. Reúne en una misma ventana los archivos del proyecto, la búsqueda, el control de versiones, la terminal, los errores detectados, las extensiones y el chat con IA.

### 2.1 Carpeta, proyecto y workspace

Cuando abrís una carpeta, VS Code la toma como el espacio de trabajo o **workspace**. Esa carpeta le da un límite visible al trabajo:

- el Explorador muestra sus archivos y subcarpetas;
- la búsqueda puede recorrer todo el contenido;
- la terminal integrada suele abrirse en esa ubicación;
- Git puede mostrar qué cambió dentro del repositorio;
- Copilot puede buscar contexto dentro del proyecto, según el modo y los permisos disponibles.

Abrir un archivo suelto no equivale a abrir el proyecto. Para trabajar con un agente conviene abrir la carpeta correcta y comprobar su nombre antes de pedir cualquier acción.

### 2.2 Las zonas que necesitás reconocer

| Zona | Para qué sirve | Qué conviene mirar |
| --- | --- | --- |
| Explorador | Navegar, crear, renombrar y organizar archivos. | Qué carpeta está abierta y dónde se guardará cada cambio. |
| Editor | Leer y modificar el archivo activo. | Pestaña, lenguaje detectado, cambios sin guardar. |
| Búsqueda | Encontrar texto en todo el proyecto. | Coincidencias, archivos afectados y reemplazos. |
| Control de código fuente | Ver cambios de Git. | Archivos nuevos, modificados o eliminados y su diff. |
| Panel de Problemas | Reunir errores y advertencias detectados. | Archivo, línea, gravedad y origen del diagnóstico. |
| Terminal integrada | Ejecutar comandos dentro del proyecto. | Carpeta actual, comando exacto y resultado. |
| Extensiones | Incorporar soporte para lenguajes y herramientas. | Editor, versión, permisos y procedencia de la extensión. |
| Chat | Preguntar, planificar o delegar tareas a la IA. | Modo, modelo, contexto, herramientas y permisos. |

### 2.3 La Paleta de comandos

La Paleta de comandos permite buscar acciones por su nombre sin memorizar dónde está cada botón.

- Windows/Linux: `Ctrl+Shift+P`
- macOS: `Cmd+Shift+P`

Ejemplos de acciones que se pueden buscar:

- `Terminal: Create New Terminal`;
- `Chat: Open Chat`;
- `Chat: Open Customizations`;
- `Workspaces: Manage Workspace Trust`.

Los nombres y la posición de algunos botones pueden cambiar entre versiones. La Paleta de comandos es una referencia más estable que una captura de pantalla.

### 2.4 Atajos mínimos para orientarse

| Acción | Windows/Linux | macOS |
| --- | --- | --- |
| Abrir la Paleta de comandos | `Ctrl+Shift+P` | `Cmd+Shift+P` |
| Buscar un archivo por nombre | `Ctrl+P` | `Cmd+P` |
| Buscar texto en todo el proyecto | `Ctrl+Shift+F` | `Cmd+Shift+F` |
| Abrir Control de código fuente | `Ctrl+Shift+G` | `Ctrl+Shift+G` |
| Mostrar u ocultar la terminal | `` Ctrl+` `` | `` Ctrl+` `` |
| Abrir la vista de Chat | `Ctrl+Alt+I` | `Ctrl+Cmd+I` |
| Guardar el archivo activo | `Ctrl+S` | `Cmd+S` |

No hace falta memorizar todos los atajos. La prioridad es reconocer la zona de trabajo y poder encontrar la acción desde la Paleta de comandos.

### 2.5 Confianza del workspace

VS Code puede abrir carpetas desconocidas en **Modo restringido**. Esto reduce la ejecución automática de tareas, extensiones o configuraciones potencialmente peligrosas.

Confiar en un workspace no significa que “seguro va a funcionar”. Significa que confiás en el origen de sus archivos lo suficiente como para permitir funciones que pueden ejecutar código. Si el repositorio es desconocido, primero se inspecciona; no se lo marca como confiable por costumbre.

### 2.6 Tres comprobaciones antes de usar IA

Antes de conversar con Copilot, verificá:

1. **Dónde estoy:** nombre y ruta de la carpeta abierta.
2. **Qué estado tiene:** archivos modificados en Control de código fuente.
3. **Qué puede ejecutarse:** confianza del workspace y permisos del agente.

---

## 3. Qué controla una sesión de Copilot

En el área de chat pueden aparecer varios controles. No significan lo mismo:

- **Objetivo de sesión o session target:** determina qué entorno de agente atiende la conversación y dónde trabaja.
- **Modo o rol:** define si la conversación pregunta, planifica o actúa.
- **Modelo:** es el modelo de IA que razona y genera la respuesta.
- **Herramientas:** permiten leer archivos, buscar, editar, usar la terminal o conectarse con otros servicios.
- **Permisos y aprobaciones:** determinan qué acciones requieren confirmación humana.
- **Contexto:** incluye el prompt, la conversación, los archivos adjuntos, el archivo activo y la información que el agente puede recuperar del workspace.

Un modelo potente no reemplaza una mala elección de contexto o permisos. La primera habilidad profesional es saber **qué le estamos permitiendo ver y hacer**.

---

## 4. Los tres modos de GitHub Copilot

GitHub documenta tres modos de Copilot Chat en el IDE: **Ask**, **Plan** y **Agent**. En una interfaz en español pueden aparecer como **Preguntar**, **Plan** y **Agente**.

Una forma sencilla de recordarlos es:

```text
PREGUNTAR              PLANIFICAR                 ACTUAR
    Ask        →           Plan          →          Agent
 comprender          decidir el camino        ejecutar y verificar
```

No siempre es necesario usar los tres. El nivel de autonomía debe ser proporcional a la tarea, al riesgo y a la claridad del pedido.

### 4.1 Modo Preguntar (Ask)

**Para qué sirve:** entender código, archivos, errores, conceptos u opciones sin delegar la implementación.

**Qué hace normalmente:**

- responde preguntas;
- explica fragmentos o relaciones entre archivos;
- propone ejemplos o alternativas;
- ayuda a identificar qué información falta.

**Cuándo elegirlo:**

- todavía no entendés el problema;
- querés explorar sin modificar el proyecto;
- necesitás comparar opciones;
- querés preparar mejores preguntas antes de avanzar.

**Ejemplo:**

> Revisá el procedimiento de diagnóstico de este repositorio. Explicame qué comprueba cada etapa, qué supuestos hace y qué información falta. No modifiques archivos.

**Resultado observable:** una explicación que el equipo puede contrastar con los archivos citados.

**Límite:** una explicación convincente puede ser incorrecta o incompleta. Hay que revisar las referencias y distinguir lo leído de lo inferido.

### 4.2 Modo Plan (Plan)

**Para qué sirve:** investigar el proyecto y construir un plan de implementación antes de cambiar archivos.

**Qué hace normalmente:**

- analiza el resultado pedido y las restricciones;
- busca los archivos y patrones relevantes;
- formula preguntas de aclaración;
- identifica decisiones, riesgos y dependencias;
- propone pasos de implementación y verificación.

**Cuándo elegirlo:**

- la tarea afecta varios archivos o componentes;
- existen distintas soluciones posibles;
- un error podría tener impacto operativo;
- todavía faltan decisiones del responsable;
- querés revisar el alcance antes de gastar tiempo implementando.

**Ejemplo:**

> Prepará un plan para incorporar este nuevo procedimiento sin alterar los diagnósticos existentes. Identificá archivos afectados, información faltante, riesgos, autorizaciones necesarias y pruebas. No implementes nada.

Un buen plan no es una lista genérica. Debe indicar:

- qué resultado se busca;
- qué evidencia del repositorio utilizó;
- qué archivos o áreas podrían cambiar;
- qué decisiones siguen abiertas;
- cómo se verificará el resultado;
- qué queda explícitamente fuera de alcance.

**Resultado observable:** un plan revisable. Aprobar el plan y aprobar la ejecución de herramientas son decisiones diferentes.

### 4.3 Modo Agente (Agent)

**Para qué sirve:** delegar una tarea concreta que puede requerir varios pasos, edición de archivos, uso de herramientas, ejecución de comandos e iteración sobre errores.

**Qué puede hacer, según las herramientas y permisos habilitados:**

- decidir qué archivos necesita leer;
- modificar uno o varios archivos;
- ejecutar comandos en la terminal;
- observar errores o pruebas fallidas;
- corregir su trabajo y volver a verificar.

**Cuándo elegirlo:**

- el resultado y el alcance ya están claros;
- el equipo conoce qué acciones están permitidas;
- existe una forma observable de comprobar el trabajo;
- se revisarán los cambios antes de aceptarlos o compartirlos.

**Ejemplo:**

> Implementá el plan aprobado. Limitá los cambios a los archivos enumerados, no uses datos reales, ejecutá únicamente las verificaciones indicadas y al final informá qué cambiaste, qué comprobaste y qué no pudiste verificar.

**Resultado observable:** archivos modificados, comandos ejecutados, resultados de verificación y un resumen de límites.

**Riesgo principal:** el agente puede actuar sobre el sistema. Leer una respuesta no tiene el mismo impacto que aceptar una edición, ejecutar un script, instalar software o conectarse a un servicio.

### 4.4 Cómo elegir el modo

| Necesidad | Modo recomendado | Señal de que podés avanzar |
| --- | --- | --- |
| Entender un archivo o error | Preguntar | Podés explicar el problema con evidencia. |
| Explorar soluciones | Preguntar o Plan | Conocés opciones, límites y datos faltantes. |
| Diseñar un cambio complejo | Plan | Hay un plan específico y verificable. |
| Modificar varios archivos | Agente | Alcance y permisos están aprobados. |
| Ejecutar comandos | Agente | Conocés el comando, el impacto y la recuperación posible. |
| Repetir un rol especializado | Agente personalizado | El rol, las herramientas y la salida esperada son estables. |
| Repetir un procedimiento | Skill | El flujo puede escribirse paso a paso y comprobarse. |

### 4.5 Un flujo profesional

```text
1. Explorar       2. Planificar       3. Autorizar       4. Ejecutar       5. Revisar
   Preguntar   →     Plan          →     persona       →    Agente      →   diff + pruebas
```

La revisión no se delega por completo. El agente puede ejecutar pruebas, pero el equipo debe comprobar que esas pruebas realmente demuestran el resultado esperado.

---

## 5. Qué es un agente personalizado

Los modos incorporados son generales. Un **agente personalizado** es una configuración reutilizable para un rol específico, por ejemplo:

- investigador de un repositorio;
- analista de incidentes;
- revisor de seguridad;
- implementador;
- revisor de documentación.

Un agente personalizado combina principalmente:

1. **Rol:** qué responsabilidad asume.
2. **Objetivo:** qué resultado debe producir.
3. **Instrucciones:** cómo debe razonar y trabajar.
4. **Herramientas:** qué puede leer, editar o ejecutar.
5. **Límites:** qué no debe hacer y cuándo tiene que detenerse.
6. **Formato de salida:** cómo comunica evidencia, dudas y resultados.
7. **Modelo opcional:** qué modelo se prefiere para ese rol.

### 5.1 Un agente no es “una persona digital”

El nombre del rol ayuda a orientar el comportamiento, pero no garantiza que las reglas se cumplan de manera perfecta. “Sos un auditor que no modifica nada” es una intención; restringir las herramientas de edición y terminal es un control más concreto.

Siempre se revisan:

- las instrucciones generadas;
- la lista de herramientas;
- el alcance de los archivos;
- las acciones solicitadas;
- la salida real obtenida.

### 5.2 Estructura conceptual de un agente

En un repositorio, VS Code reconoce agentes guardados en `.github/agents/`. Los archivos usan Markdown y, habitualmente, la extensión `.agent.md`.

```text
proyecto/
└── .github/
    └── agents/
        └── analista-incidentes.agent.md
```

Ejemplo conceptual para leer y discutir —la lista de herramientas se debe reemplazar por nombres verificados en el entorno del aula antes de usar el archivo—:

```markdown
---
name: Analista de incidentes
description: Investiga incidentes documentados y separa hechos, hipótesis y datos faltantes.
tools: [herramientas-de-lectura-verificadas]
---

Analizá únicamente la evidencia disponible en el repositorio.

Entregá:
1. hechos observados;
2. hipótesis, indicando su evidencia;
3. información faltante;
4. verificaciones seguras sugeridas;
5. acciones que requieren autorización o escalamiento.

No modifiques archivos ni ejecutes comandos.
```

Los nombres exactos de las herramientas disponibles dependen del entorno o **agent harness** seleccionado. Por eso no se copia una lista de herramientas sin verificarla en el VS Code que se usará.

### 5.3 Crear un agente con ayuda de la IA

VS Code permite abrir el editor de personalizaciones desde el engranaje del Chat o mediante `Chat: Open Customizations` en la Paleta de comandos. Desde allí se puede pedir a la IA que genere un agente de workspace.

El flujo recomendado es:

1. describir el rol y el resultado esperado;
2. indicar si es personal o propio del workspace;
3. responder las preguntas aclaratorias;
4. revisar el archivo `.agent.md` generado;
5. comprobar herramientas y límites;
6. probarlo con un caso controlado;
7. corregir sus instrucciones con base en resultados observables.

No alcanza con que el archivo sea válido: el agente tiene que comportarse bien frente a un caso normal, uno ambiguo y uno que debe rechazar o escalar.

> Algunas opciones rápidas, como `/create-agent`, dependen del objetivo de sesión seleccionado. El editor de personalizaciones permite ver el alcance y el archivo que se está creando con mayor claridad.

---

## 6. Qué es una skill

Una **Agent Skill** es una carpeta que enseña a un agente a realizar una tarea especializada y repetible. Puede contener instrucciones, scripts, plantillas, ejemplos y otros recursos.

La idea central es:

> Un agente define **quién actúa, con qué herramientas y con qué límites**. Una skill define **cómo se realiza un procedimiento concreto**.

Ejemplos posibles para soporte técnico:

- validar la documentación de un incidente;
- preparar una lista de comprobaciones no disruptivas;
- normalizar un informe técnico;
- revisar que un procedimiento incluya autorización y escalamiento;
- generar un paquete de evidencias sin datos sensibles.

### 6.1 Estructura de una skill

Una skill vive dentro de una carpeta y su archivo principal debe llamarse `SKILL.md`.

```text
proyecto/
└── .github/
    └── skills/
        └── validar-diagnostico/
            ├── SKILL.md
            ├── examples/
            ├── templates/
            └── scripts/
```

No todas las carpetas adicionales son obligatorias. Solo se agregan si aportan recursos reales al procedimiento.

Un encabezado mínimo tiene esta forma:

```markdown
---
name: validar-diagnostico
description: Revisa un diagnóstico técnico cuando se necesita comprobar evidencia, riesgos, autorizaciones y criterios de escalamiento.
---

# Validar un diagnóstico

## Procedimiento

1. Identificar el resultado que se esperaba.
2. Separar hechos observados de hipótesis.
3. Enumerar información faltante.
4. Revisar verificaciones realizadas y su evidencia.
5. Identificar acciones no autorizadas o riesgosas.
6. Informar qué puede concluirse y qué debe escalarse.
```

El `name` debe coincidir con el nombre de la carpeta. La `description` debe explicar tanto **qué hace** como **cuándo usarla**, porque Copilot usa esa descripción para decidir si la skill es relevante.

### 6.2 Carga progresiva

Las skills están pensadas para cargar contexto de forma progresiva:

1. Copilot descubre el nombre y la descripción.
2. Si la tarea coincide, carga las instrucciones de `SKILL.md`.
3. Accede a plantillas, ejemplos o scripts solo cuando las instrucciones los referencian y los necesita.

Esto permite conservar procedimientos completos sin incluir todo su contenido en cada conversación.

### 6.3 Crear una skill con ayuda de la IA

El editor de personalizaciones permite crear una skill para el usuario o para el workspace. También puede generarse desde el chat con `/create-skill` cuando esa función está disponible.

El proceso recomendado es:

1. partir de una tarea que realmente se repite;
2. describir entradas, pasos, decisiones, salidas y errores esperables;
3. pedir a la IA que proponga la estructura;
4. revisar `name`, `description` e instrucciones;
5. comprobar cada script o plantilla incluida;
6. probar invocación explícita y selección automática;
7. ajustar la descripción si se activa cuando no corresponde o no se activa cuando debería.

Una skill puede aparecer como comando `/nombre-de-la-skill`. Según su configuración, también puede ser seleccionada automáticamente por el agente cuando la tarea coincide.

---

## 7. Agente, skill o instrucciones: cómo decidir

| Necesidad | Recurso | Pregunta que responde | Ejemplo |
| --- | --- | --- | --- |
| Mantener reglas generales del proyecto | Instrucciones del repositorio | “¿Qué reglas se aplican siempre acá?” | No usar datos reales; ejecutar una validación determinada. |
| Definir un especialista | Agente personalizado | “¿Quién debe encargarse y con qué herramientas?” | Revisor que solo lee y reporta hallazgos. |
| Enseñar un procedimiento repetible | Skill | “¿Cómo se realiza esta tarea?” | Validar un diagnóstico en seis pasos. |
| Guardar una solicitud puntual | Archivo de prompt | “¿Qué pedido quiero ejecutar a demanda?” | Generar un resumen con un formato fijo. |

También pueden combinarse:

```text
instrucciones del repositorio
        ↓
agente analista ── usa ──> skill validar-diagnostico
        ↓
informe con hechos, hipótesis, pendientes y escalamiento
```

No conviene crear una personalización para cada prompt. Primero se resuelve la tarea, se observa qué parte se repite y recién entonces se convierte ese conocimiento en instrucciones, agente o skill.

---

## 8. Alcance y trabajo en equipo

### 8.1 Personal

Una personalización personal sirve para preferencias o procedimientos que una persona usa en distintos proyectos.

Ubicaciones habituales:

- agentes personales de Copilot: `~/.copilot/agents/`;
- skills personales de Copilot: `~/.copilot/skills/`.

No se comparte automáticamente con el resto del equipo.

### 8.2 Repositorio o workspace

Cuando un agente o una skill refleja la arquitectura, las herramientas o el procedimiento propio de un proyecto, debe vivir dentro del repositorio:

```text
.github/
├── agents/
│   └── nombre.agent.md
└── skills/
    └── nombre-de-skill/
        └── SKILL.md
```

Al versionar esos archivos con Git:

- todos reciben la misma definición;
- los cambios pueden revisarse mediante un diff;
- el equipo puede proponer mejoras por pull request;
- existe historial de quién cambió qué y por qué;
- la personalización evoluciona junto con el proyecto.

### 8.3 Compartir en varios repositorios

Copiar una skill manualmente en muchos repositorios crea versiones divergentes. Si la capacidad es común a varios equipos, hace falta una estrategia de distribución y mantenimiento.

Según el alcance, se puede:

- mantener una versión por repositorio cuando necesita adaptación local;
- conservar una fuente común y definir un proceso de actualización;
- distribuir un conjunto de personalizaciones mediante un plugin de agentes;
- usar agentes definidos a nivel de organización cuando esa función esté habilitada por GitHub y por la organización.

Las skills del repositorio sí se comparten con quienes clonan ese repositorio. No se debe asumir que una skill colocada en un proyecto aparecerá automáticamente en todos los demás.

### 8.4 Revisión antes de compartir

Antes de incorporar un agente o una skill al repositorio, el equipo debe revisar:

- propósito y momento de uso;
- herramientas permitidas;
- comandos o scripts incluidos;
- datos a los que podría acceder;
- supuestos sobre sistema operativo y dependencias;
- resultado esperado y método de verificación;
- situaciones de rechazo, autorización y escalamiento;
- responsable de mantenerlo actualizado.

Una skill descargada de Internet se trata como código de terceros: se inspecciona antes de usarla, especialmente si contiene scripts o propone ejecutar comandos.

---

## 9. Ejercicio: explorar el workspace y crear un chatbot local

### Situación y resultado esperado

Antes de construir una herramienta, el equipo necesita entender qué proyecto tiene abierto y qué recursos puede reutilizar. Primero Copilot describirá el workspace con evidencia. Después, ayudará a crear un chatbot sencillo para consultas de soporte técnico: una app de Streamlit que use el modelo local del curso mediante `llama-cpp-python`.

Al terminar, cada equipo debe poder mostrar:

- una descripción contrastada con archivos y configuraciones visibles;
- una app que recibe un mensaje y muestra una respuesta del modelo local;
- una revisión breve de los cambios, el comando de ejecución y los límites de la prueba.

```text
workspace abierto → descripción con evidencia → plan revisable → app local → prueba → revisión
```

### Organización y tiempo

Trabajá en los cuatro equipos de tres integrantes. Una persona opera VS Code, otra controla el contexto y los límites, y otra registra hallazgos. Roten las funciones entre las dos partes.

| Parte | Tiempo | Modo o herramienta |
| --- | ---: | --- |
| Confirmar carpeta y estado inicial | 3 min | VS Code y Git |
| Pedir una descripción del entorno | 7 min | Preguntar (Ask) |
| Revisar datos y preparar el plan | 7 min | Plan |
| Crear la app en una carpeta nueva | 15 min | Agente (Agent) |
| Ejecutar y probar localmente | 8 min | Terminal y navegador local |
| Registrar el resultado y lo pendiente | 5 min | Revisión del equipo |

Durante la consigna inicial, todos siguen el mismo VS Code en el TV. Después, los cuatro equipos trabajan en una computadora cada uno. En el cierre, cada equipo comparte su pantalla por turno; si no se puede conectar una computadora al TV, el relator lee el prompt y la evidencia que el equipo revisó.

### Parte A. Pedirle a Copilot que describa el entorno

1. Abrí la carpeta de práctica completa en VS Code; no trabajes desde un archivo suelto.
2. Mirá el nombre de la carpeta raíz y el estado inicial de Control de código fuente. Si hay cambios previos, registralos antes de empezar.
3. En el modo **Preguntar (Ask)**, enviá este pedido:

   > Describime el entorno de trabajo que está abierto en VS Code. Revisá la estructura del workspace, los lenguajes y dependencias que puedas confirmar, los archivos que indican cómo se prepara o ejecuta el proyecto y el código existente que carga el modelo local. Separá hechos observados, inferencias e información faltante. Para cada hecho, nombrá el archivo o evidencia que lo respalda. No modifiques archivos, no ejecutes comandos, no busques fuera de este workspace y no supongas una ruta del modelo ni la disponibilidad de datos que no puedas confirmar.

4. Contrastá al menos dos afirmaciones con el Explorador, el archivo citado o la configuración visible. Marcá cualquier afirmación que no tenga evidencia.
5. Anotá qué sabe Copilot sobre el proyecto y qué necesita preguntarle a una persona. Una descripción convincente no demuestra que la IA haya inspeccionado o entendido correctamente el entorno.

### Parte B. Planificar el chatbot

En el modo **Plan**, pedile que revise el código existente de las prácticas y proponga cómo crear el chatbot. Usá esta consigna:

> Prepará un plan para crear una app mínima de chatbot con Streamlit dentro de `clase_03/practica_chatbot/`. Usá Python y `llama-cpp-python` para llamar al mismo modelo GGUF local que ya está disponible en este entorno. Revisá el código del curso para encontrar la forma de carga y el formato de conversación existentes. No propongas otro modelo, una API en la nube ni una descarga. No inventes el nombre ni la ruta del GGUF: si no podés confirmar cuál archivo usar, preguntame y esperá. No edites todavía. Indicá qué archivos crearías, qué dependencias requiere la app, cómo conservarías el historial entre mensajes y qué comando local se usaría para probarla.

Antes de pasar a Agente, revisá que el plan:

- use `llama-cpp-python` en el entorno virtual del curso;
- identifique el GGUF solo si pudo confirmarlo;
- se detenga y pregunte si no encuentra el modelo o la ruta;
- limite los cambios a `clase_03/practica_chatbot/`;
- no incluya instalaciones, descargas ni servicios externos no solicitados.

### Parte C. Construir la app con Copilot

Si el plan respeta el alcance, cambiá al modo **Agente (Agent)** y pedí la implementación:

> Implementá el plan aprobado únicamente dentro de `clase_03/practica_chatbot/`. Creá una app pequeña de Streamlit con un título, una entrada de chat, respuestas del modelo local y el historial visible durante la sesión. Reutilizá `llama-cpp-python` y el GGUF existente que confirmé; cargá el modelo una sola vez por proceso. Para cada turno, enviá al modelo los mensajes necesarios para conservar el contexto de la conversación. El chatbot debe responder como asistente de soporte técnico: distinguir hechos de hipótesis, pedir los datos que faltan y no recomendar cambios disruptivos ni acciones sin autorización. Mostrá un mensaje claro si falta una dependencia o la ruta del modelo no está configurada. No descargues modelos, no instales paquetes, no cambies archivos fuera de esa carpeta y no expongas el servidor en la red. Antes de ejecutar cualquier comando, mostrá el comando para revisarlo.

Copilot puede crear `app.py` y, si hace falta, un `README.md` breve para esa práctica. Revisá la lista de cambios antes de aceptarlos. No agregues rutas personales, credenciales ni información real al repositorio.

### Parte D. Ejecutar y comprobar

1. Revisá el diff y comprobá que Copilot solo haya creado o cambiado archivos dentro de `clase_03/practica_chatbot/`.
2. Confirmá que Streamlit está instalado en el `.venv`. Si falta, detené la ejecución y registrá la dependencia pendiente para preparar el entorno; no instales paquetes sin autorización.
3. Leé el comando propuesto y confirmá que usa el Python del entorno virtual y abre la app solo para verla localmente. Con el `.venv` activado, la forma general es:

   ```bash
   python -m streamlit run clase_03/practica_chatbot/app.py
   ```

4. En la interfaz local, probá con este caso sintético:

   > La impresora del puesto 12 imprime tickets con rayas. No sé desde cuándo empezó ni si pasa con todos los tickets.

5. En un segundo mensaje, agregá un dato nuevo, por ejemplo: “La impresora de al lado sale bien”. Observá si el chatbot conserva el contexto y separa la observación de las hipótesis.
6. Si la app falla, registrá el mensaje exacto. No cambies la ruta ni ejecutes instalaciones hasta entender qué dato o permiso falta.

### Seguridad, autorización y escalamiento

- Usá una carpeta de práctica, datos sintéticos y un workspace que puedas revisar.
- En la primera parte, Copilot observa. En la planificación todavía no modifica. En la implementación puede escribir únicamente dentro de la carpeta acordada.
- Antes de ejecutar, revisá el diff, el comando, el directorio actual y cualquier acceso solicitado. Rechazá cambios fuera del alcance.
- El modelo debe cargarse desde el GGUF local confirmado. No uses credenciales, datos personales, registros reales ni configuración de producción.
- La app corre localmente para la práctica. No la publiques ni la expongas a otros equipos o redes.
- Si Copilot no puede confirmar una ruta, dependencia, permiso o comportamiento, registrá la pregunta pendiente y consultá antes de seguir.

### Entregable y puesta en común

Cada equipo registra en pocas líneas:

1. un hecho sobre el workspace que verificó en un archivo;
2. una inferencia de Copilot que necesitó corregir o dejar como duda;
3. los archivos creados y el comando usado para abrir la app;
4. qué mostró la prueba y qué no llegó a validar;
5. qué acción habría requerido autorización adicional.

En los diez minutos de puesta en común y cierre, cada equipo comparte un hallazgo en un minuto mientras los demás comparan las respuestas con sus propias verificaciones. Usá el tiempo restante para registrar una limitación común y una comprobación que les resultó útil.

## 10. Errores frecuentes y cómo interpretarlos

| Situación | Causa posible | Qué revisar o hacer |
| --- | --- | --- |
| Copilot describe archivos que no existen | Workspace equivocado o afirmación inventada. | Comparar con Explorador y citas; corregir la descripción. |
| No puede confirmar qué modelo usar | La ruta o el GGUF no están visibles en el workspace. | Proporcionar la ruta exacta del modelo existente; no pedirle que busque en todo el equipo ni que descargue otro. |
| El plan propone instalar dependencias | Streamlit no está preparado en el entorno. | Detenerse y registrar la preparación pendiente antes de instalar. |
| `ModuleNotFoundError` al iniciar | Se ejecutó otro Python o falta Streamlit en `.venv`. | Revisar el intérprete seleccionado y la dependencia; no tocar el entorno global. |
| El modelo no carga | Ruta incorrecta, archivo inexistente o memoria insuficiente. | Confirmar el GGUF y el mensaje de error; no cambiar de modelo por cuenta propia. |
| El chat olvida el mensaje anterior | La app no conserva o no reenvía el historial de sesión. | Revisar `st.session_state` y los mensajes enviados a `create_chat_completion`. |
| La app tarda o se cierra | El equipo no tiene recursos suficientes o hubo un error de ejecución. | Registrar el tiempo y el mensaje; detenerse antes de reducir controles o cambiar el modelo. |
| El agente edita fuera de la carpeta | El alcance quedó poco claro o se aceptó una acción amplia. | Rechazarla, revisar Git y limitar cambios a la ruta acordada. |

## 11. Preguntas para orientar la observación

Durante el ejercicio, respondé:

1. ¿Qué evidencia usó Copilot para describir el workspace?
2. ¿Qué afirmó como hecho y qué presentó como inferencia?
3. ¿Qué información del modelo ya existía en los archivos y qué tuviste que confirmar?
4. ¿Qué cambió al pasar de Preguntar a Plan y de Plan a Agente?
5. ¿El historial permitió que la segunda respuesta entendiera el dato nuevo?
6. ¿Qué parte de la respuesta del chatbot necesitó revisión humana?
7. ¿Qué archivos se modificaron y qué comando se ejecutó?
8. ¿Qué limitación o dato faltante quedó registrado?

## 12. Síntesis para el cierre

- VS Code reúne archivos, terminal, control de versiones, diagnósticos e IA dentro de un workspace.
- **Preguntar** ayudó a describir lo visible; **Plan** convirtió el objetivo en pasos revisables; **Agente** creó una app dentro del alcance acordado.
- La descripción de Copilot se contrastó con archivos y configuraciones; no se tomó como evidencia por sí sola.
- La app usó el modelo local con `llama-cpp-python`; no necesitó una API comercial ni un modelo nuevo.
- El chatbot sirve para practicar una interfaz y observar respuestas. Sus sugerencias no autorizan cambios técnicos ni reemplazan la validación del equipo.
- Los diffs, los comandos y los errores también forman parte del resultado y se revisan antes de dar la tarea por terminada.

## 13. Conexión con la clase siguiente

El chatbot deja una app pequeña que puede ampliarse en otra clase con un caso de soporte más completo. Antes de agregar funciones, primero se conserva lo aprendido aquí: describir el proyecto con evidencia, planificar los cambios y verificar cada resultado.