# Clase 6 — Primeros pasos con n8n

**Duración:** 90 minutos  
**Nivel:** inicial, sin conocimientos previos de n8n  
**Modalidad:** instalación guiada, explicación breve, observación y construcción manual  
**Producto:** n8n funcionando localmente y un primer workflow construido desde un canvas vacío

## Idea central

Una automatización recibe datos, realiza una secuencia de tareas y entrega un resultado. En esta primera clase los estudiantes construirán cada nodo y cada campo a mano para observar cómo cambia la información paso a paso.

El caso será registrar y confirmar la inscripción de una persona a un taller:

```text
Inicio manual
  → Cargar inscripción
  → Completar registro
  → Preparar confirmación
```

No se utilizarán bifurcaciones, servicios externos ni decisiones automáticas. El foco estará en el canvas, los nodos, JSON, los items y las vistas INPUT y OUTPUT.

## Objetivos de aprendizaje

Al finalizar la clase, cada estudiante podrá:

- iniciar y detener n8n con Docker Compose sin borrar sus datos;
- comprobar que la cuenta y los workflows persisten;
- explicar qué problema resuelve una automatización sencilla;
- reconocer un workflow, un nodo, una conexión y un trigger;
- ejecutar un workflow manualmente;
- leer y escribir un objeto JSON sencillo;
- distinguir strings, números, booleanos, `null` y arrays;
- reconocer que n8n transporta información mediante items;
- inspeccionar INPUT y OUTPUT;
- crear campos de distintos tipos con Edit Fields;
- recuperar un valor del item mediante una expresión sencilla;
- describir el contrato de datos entre nodos.

## Materiales

Dentro de la carpeta `n8n/`:

- [`compose.yaml`](n8n/compose.yaml): configuración local de n8n.
- [`iniciar-n8n.cmd`](n8n/iniciar-n8n.cmd) y [`detener-n8n.cmd`](n8n/detener-n8n.cmd): accesos simples para Windows.
- [`README.md`](n8n/README.md): guía breve de instalación y operación.
- [`Clase 6 - Contrato y ejemplos de inscripciones.json`](n8n/Clase%206%20-%20Contrato%20y%20ejemplos%20de%20inscripciones.json): material documental para leer y copiar datos.

El archivo de ejemplos es una referencia documental. En esta clase el workflow se crea manualmente desde un canvas vacío.

## Preparación del entorno n8n

Docker Desktop es un **prerrequisito técnico**. Debe estar instalado e iniciado antes del encuentro.

Descarga: https://www.docker.com/products/docker-desktop/

Antes de la clase:

1. Comprobá que Docker Desktop funciona en tu computadora.
2. En una terminal o PowerShell, ejecutá `docker --version`, `docker compose version` y `docker info`.



## Agenda

| Tiempo | Momento | Propósito |
|---:|---|---|
| 0–20 min | Iniciar n8n con Docker Compose | Comprobar el entorno, crear el owner y verificar persistencia |
| 20–30 min | Automatización e interfaz | Reconocer problema, canvas, workflow, nodos y trigger |
| 30–48 min | JSON desde cero | Comprender la forma y los tipos de los datos |
| 48–58 min | Items y contratos | Seguir datos entre INPUT y OUTPUT |
| 58–82 min | Primer workflow | Construir manualmente los cuatro nodos lineales |
| 82–88 min | Predicción y segunda prueba | Modificar valores y anticipar la salida |
| 88–90 min | Cierre | Recuperar las ideas principales |

Si el encuentro dura 70 minutos, el entorno debe quedar listo antes: imagen descargada, contenedor iniciado y cuenta owner creada. Reservá cinco minutos para comprobar el acceso y continuá con el resto del recorrido.

---

## 1. Iniciar n8n con Docker Compose

### 1.1 Configuración inicial

Copiá la carpeta `n8n/` en tu computadora. Contiene la base del entorno local de n8n con Docker.

> Ubicá la carpeta en un disco con permisos de lectura y escritura. **Evitá carpetas sincronizadas** con servicios de nube, repositorios Git o recursos de red.

La carpeta `n8n/` contiene este entorno:

```text
Docker Desktop
  → compose.yaml
  → imagen oficial docker.n8n.io/n8nio/n8n:2.35.7
  → volumen persistente clase_n8n_data
  → http://127.0.0.1:5678
```

La configuración:

- fija la versión de n8n para que todo el curso use la misma interfaz;
- guarda la cuenta y los workflows en un volumen nombrado;
- enlaza el puerto solamente con `127.0.0.1`;
- configura `America/Argentina/Tucuman` como zona horaria.

La práctica usa n8n `2.35.7` para que los equipos trabajen con la misma interfaz. La documentación oficial vigente puede mostrar otra versión y llamar **Include in Output** a la opción que esta guía identifica como **Include Other Input Fields**. En cada paso, seguí el resultado esperado: conservar los campos recibidos o dejar solo los campos configurados.

### 1.2 Comprobar Docker

En Windows, abrí Docker Desktop y esperá hasta que el motor esté iniciado. Después, abrí Símbolo del sistema y ejecutá:

```console
docker --version
docker compose version
docker info
```

Los primeros dos comandos deben mostrar sus versiones. `docker info` debe responder sin indicar que no puede conectarse al motor.

> En macOS o Linux, realizá las mismas comprobaciones desde una terminal.


### 1.3 Abrir la carpeta e iniciar

Ubicate desde la terminal en la carpeta `n8n/`.
- *En Windows, escribí `cd`, dejá un espacio, arrastrá la carpeta a Símbolo del sistema y presioná Enter.*

Con Internet disponible, ejecutá estos comandos para descargar la imagen y levantar el contenedor:

```console
docker compose pull
docker compose up -d
docker compose ps
```

También podés hacer doble clic en `iniciar-n8n.cmd`.

Abrí en el navegador:

```text
http://127.0.0.1:5678
```

Usá `http`, no `https`.

### 1.4 Crear el owner

La primera vez, n8n solicita crear la cuenta propietaria u owner.

1. Completá tu nombre y apellido.
2. Ingresá una dirección de correo para identificar la cuenta local.
3. Creá una contraseña individual y guardala de forma segura.
4. Completá la pantalla inicial hasta llegar al espacio de trabajo.

### 1.5 Comprobar persistencia

1. Creá un workflow vacío llamado **Prueba de persistencia**.
2. Guardalo.
3. Volvé a la terminal y ejecutá:

```console
docker compose stop
```

4. Comprobá que la página deja de responder.
5. Volvé a iniciar n8n:

```console
docker compose up -d
```

6. Recargá `http://127.0.0.1:5678`.
7. Confirmá que la cuenta y **Prueba de persistencia** siguen disponibles.

También podés usar `detener-n8n.cmd` e `iniciar-n8n.cmd`.

Los datos se conservan en el volumen `clase_n8n_data`. No ejecutes `docker compose down -v` ni `docker volume rm clase_n8n_data`: esos comandos pueden borrar los datos persistentes.

### 1.6 Operación cotidiana

```console
docker compose up -d
docker compose ps
docker compose logs --tail 50 n8n
docker compose stop
```

Después de `up -d` podés cerrar la terminal porque el contenedor queda en segundo plano. Docker Desktop debe permanecer iniciado.

### 1.7 Problemas frecuentes

| Problema | Comprobación | Acción segura |
|---|---|---|
| `docker` no se reconoce | `docker --version` | Confirmá que Docker Desktop esté instalado y abrí una terminal nueva. |
| Docker no responde | `docker info` | Abrí Docker Desktop y esperá a que el motor esté listo. |
| Descarga lenta o error de red | Observar `docker compose pull` | Esperá y comprobá la red. Si la descarga no se completa, seguí la alternativa de conexión acordada para el curso. |
| Puerto 5678 ocupado | El mensaje indica que la dirección ya está en uso | Comprobá si ya hay otra instancia local. No finalices procesos desconocidos. |
| El contenedor se detiene | `docker compose ps` | Revisá `docker compose logs --tail 50 n8n`. |
| El navegador no conecta | El contenedor figura iniciado | Abrí exactamente `http://127.0.0.1:5678` y revisá el firewall institucional. |


---

## 2. ¿Qué vamos a automatizar? (5 min)

Leé esta situación:

> Cada vez que una persona se inscribe a un taller, alguien registra sus datos, marca el estado de la inscripción y prepara un mensaje de confirmación.

Respondé estas preguntas:

- ¿Qué datos entrega la persona?
- ¿Qué tareas se repiten?
- ¿Qué resultado se espera?

Completá esta tabla con tus respuestas:

| Entrada | Tareas | Resultado |
|---|---|---|
| Datos de inscripción | Conservar datos, agregar estado y redactar mensaje | Confirmación estructurada |

Definición de trabajo:

> Una automatización es una secuencia de pasos que procesa datos para obtener un resultado.

### Vocabulario mínimo de la interfaz

**Canvas:** espacio en el que ubicamos y conectamos nodos.  
**Workflow:** proceso completo representado en el canvas.  
**Nodo:** un paso que recibe datos, realiza una tarea y entrega datos.  
**Conexión:** línea que indica hacia dónde viajan los datos.  
**Trigger:** nodo que inicia una ejecución.  
**Ejecución:** una corrida concreta del workflow.

En esta práctica se usa Manual Trigger. El workflow comenzará cuando seleccionemos **Execute workflow**.

Crear ahora un workflow nuevo, vacío, y nombrarlo:

```text
Clase 6 - Registro de inscripciones
```

No agregar todavía los demás nodos.

---

## 3. JSON desde cero (15 min)

JSON es un formato de texto para representar datos estructurados. El archivo documental de la clase contiene contratos y ejemplos escritos en este formato.

### 3.1 Objeto, claves y valores

```json
{
  "inscripcion_id": "INS-001",
  "nombre": "Lucía Gómez",
  "cantidad_asistentes": 1,
  "confirmada": true
}
```

Un objeto comienza con `{` y termina con `}`. Dentro hay pares de clave y valor:

```text
"nombre": "Lucía Gómez"
   clave : valor
```

Reglas visuales:

- las claves llevan comillas dobles;
- los dos puntos separan clave y valor;
- las comas separan un par del siguiente;
- el último par no lleva coma final;
- las llaves contienen el objeto.

### 3.2 Tipos de valores

**String**

```json
"modalidad": "presencial"
```

El texto lleva comillas dobles. Si más adelante se guarda una fecha en JSON, normalmente se representará como string, por ejemplo `"2026-09-15"`.

**Número**

```json
"cantidad_asistentes": 2
```

Los números no llevan comillas.

**Booleano**

```json
"confirmada": true
```

Puede ser `true` o `false`, sin comillas.

**Null**

```json
"observaciones": null
```

`null` expresa ausencia de valor. No es lo mismo que el string `"null"`.

**Array: primera aproximación**

```json
"intereses": ["automatización", "datos"]
```

Un array es una lista ordenada entre corchetes. En esta clase solo necesitamos reconocerlo.

-=-=-=-=-=-=-=-=-==-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-==-=-=-=-=-=-=-=-=-=-=-

---

## 4. Items, INPUT, OUTPUT y contrato de datos (10 min)

n8n procesa información mediante **items**. En esta clase una inscripción será un item y su contenido será un objeto JSON.

Representación conceptual:

```json
[
  {
    "json": {
      "inscripcion_id": "INS-001",
      "nombre": "Lucía Gómez"
    }
  }
]
```

Los corchetes exteriores indican una lista de items. Hoy trabajaremos con uno.

Cada nodo puede observarse así:

```text
INPUT → tarea del nodo → OUTPUT
```

- INPUT muestra los datos recibidos.
- OUTPUT muestra los datos entregados.

### Contrato de entrada

| Campo | Tipo | Obligatorio | Ejemplo |
|---|---|---:|---|
| `inscripcion_id` | string | sí | `"INS-001"` |
| `nombre` | string | sí | `"Lucía Gómez"` |
| `email` | string | sí | `"lucia@example.com"` |
| `taller` | string | sí | `"Introducción a n8n"` |
| `modalidad` | string | sí | `"presencial"` |
| `cantidad_asistentes` | number | sí | `1` |
| `confirmada` | boolean | sí | `true` |

Un contrato de datos acuerda el nombre, tipo, obligatoriedad y ejemplo de cada campo. `inscripcion_id` e `Inscripcion_ID` serían nombres diferentes; `true` y `"true"` tendrían tipos diferentes.

---

## 5. Práctica guiada: construir el workflow (25 min)

Realizá todos los pasos manualmente en el canvas. Usá el archivo documental solo para leer o copiar valores de ejemplo.

### Paso 1 — Manual Trigger

1. En el workflow vacío, agregá **Manual Trigger**.
2. Renombralo **Inicio manual**.
3. Guardá el workflow.

Este nodo inicia la ejecución, pero todavía no produce los datos de la inscripción.

### Paso 2 — Cargar inscripción

1. Agregá **Edit Fields**.
2. Conectalo desde **Inicio manual**.
3. Renombralo **Cargar inscripción**.
4. Creá a mano estos campos y seleccioná el tipo indicado:

| Campo | Tipo en Edit Fields | Valor fijo |
|---|---|---|
| `inscripcion_id` | String | `INS-001` |
| `nombre` | String | `Lucía Gómez` |
| `email` | String | `lucia@example.com` |
| `taller` | String | `Introducción a n8n` |
| `modalidad` | String | `presencial` |
| `cantidad_asistentes` | Number | `1` |
| `confirmada` | Boolean | `true` |

Antes de ejecutar el nodo, predecí:

- ¿Cuántos campos tendrá el OUTPUT?
- ¿Cuál será número?
- ¿Cuál será booleano?

Ejecutá el nodo y observá el OUTPUT en vista JSON.

### Paso 3 — Completar registro

1. Agregá otro **Edit Fields**.
2. Conectalo desde **Cargar inscripción**.
3. Renombralo **Completar registro**.
4. Activá **Include Other Input Fields** para conservar todos los datos recibidos.
5. Agregá `estado`, tipo String, con el valor fijo `registrada`.
6. Agregá `mensaje`, tipo String.
7. Cambiá `mensaje` al modo **Expression** y escribí:

```text
=Hola {{ $json.nombre }}, tu inscripción fue registrada.
```

> `$json.nombre` recupera el valor del campo `nombre` del item actual.



Ejecutá el nodo y compará INPUT con OUTPUT.

### Paso 4 — Preparar confirmación

1. Agregá un tercer **Edit Fields**.
2. Conectalo desde **Completar registro**.
3. Renombralo **Preparar confirmación**.
4. Dejá desactivado **Include Other Input Fields** para producir solamente el contrato final.
5. Creá los campos siguientes. Cada valor se obtiene desde el item actual con una expresión.

| Campo final | Tipo | Expresión |
|---|---|---|
| `inscripcion_id` | String | `{{ $json.inscripcion_id }}` |
| `estado` | String | `{{ $json.estado }}` |
| `taller` | String | `{{ $json.taller }}` |
| `modalidad` | String | `{{ $json.modalidad }}` |
| `cantidad_asistentes` | Number | `{{ $json.cantidad_asistentes }}` |
| `confirmada` | Boolean | `{{ $json.confirmada }}` |
| `mensaje` | String | `{{ $json.mensaje }}` |

### Paso 5 — Ejecutar y observar

Antes de seleccionar **Execute workflow**, escribí cómo esperás que se vea el JSON final.

Ejecutá el workflow completo y abrí los nodos en orden:

1. Inicio manual.
2. Cargar inscripción.
3. Completar registro.
4. Preparar confirmación.

Salida esperada:

```json
{
  "inscripcion_id": "INS-001",
  "estado": "registrada",
  "taller": "Introducción a n8n",
  "modalidad": "presencial",
  "cantidad_asistentes": 1,
  "confirmada": true,
  "mensaje": "Hola Lucía Gómez, tu inscripción fue registrada."
}
```

Revisá cada paso y respondé:

- ¿Cuántos items entraron y salieron?
- ¿Qué campos se conservaron?
- ¿Qué campos aparecieron?
- ¿El tipo de cada valor coincide con el contrato?


---

## 6. Cierre 

Completá oralmente:

1. Un nodo recibe ______ y entrega ______.
2. En JSON, clave y valor se separan con ______.
3. La diferencia entre `2` y `"2"` es ______.
4. `$json.nombre` permite ______.
5. INPUT y OUTPUT sirven para ______.
6. Los datos locales persisten gracias a ______.

Idea final:

> Antes de automatizar decisiones, necesitamos saber qué datos existen, qué forma tienen y qué espera recibir cada paso.



## Conexión con la próxima clase

En el próximo encuentro vas a trabajar con decisiones y errores dentro de un flujo. Lo que practicás hoy —seguir los datos y comparar cada INPUT con su OUTPUT— te va a ayudar a reconocer cuándo falta información, cuándo un valor no cumple lo esperado y cuándo hace falta una revisión humana.

## Referencias 

- [Instalar n8n con Docker Compose](https://docs.n8n.io/deploy/host-n8n/install-options/install-using-docker-compose)
- [Crear y ejecutar workflows](https://docs.n8n.io/build/understand-workflows/create-and-run-workflows)
- [Trabajar con nodos](https://docs.n8n.io/build/understand-workflows/workflow-components/work-with-nodes)
- [Estructura de datos](https://docs.n8n.io/build/work-with-data/understand-n8ns-data-structure)
- [Nodo Edit Fields](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.set)
