# Clase 2: De un mensaje informal a un pedido de trabajo operativo

**Capacitación en Inteligencia Artificial y Automatización Aplicada a Soporte Técnico**  
**Casinos Play**

## Objetivo general

Recuperar el ejercicio pendiente de la Clase 1 y practicar cómo transformar un mensaje desordenado recibido por teléfono o WhatsApp en un registro operativo de pedido de trabajo. La salida debe ayudar a observar, preguntar, verificar, comunicar y decidir si corresponde resolver, pedir autorización o escalar.

La Inteligencia Artificial se utiliza como apoyo para ordenar y redactar. No reemplaza la comprobación técnica ni la decisión del equipo.

## Resultados esperados

Al finalizar la clase, cada participante podrá:

- separar hechos confirmados, ambigüedades, hipótesis e información faltante;
- redactar preguntas de diagnóstico que permitan avanzar;
- proponer verificaciones iniciales no disruptivas;
- sugerir una prioridad razonada y explicar qué datos la sostienen, sin asignarla automáticamente;
- preparar una comunicación breve para quien hizo el pedido;
- indicar qué requiere autorización y cuándo corresponde escalar;
- mejorar un pedido para una herramienta de IA usando rol, contexto, objetivo, restricciones y formato;
- revisar la respuesta de una herramienta y marcar supuestos, riesgos y puntos pendientes.

## Modalidad, duración y organización

- **Duración sugerida:** 90 minutos.
- **Participantes:** 12 personas, organizadas en 6 parejas.
- **Espacio:** aula pequeña con un único TV visible para todo el grupo.
- **Herramientas:** notebook `clase_02/clase_2_pedidos_de_trabajo.ipynb`, editor de texto y una herramienta de IA que ya esté disponible para el grupo, o demostración del instructor.
- **Código:** el notebook usa únicamente Python estándar para mostrar textos y revisar una estructura. No instala paquetes, no descarga archivos, no carga modelos y no llama a servicios externos.
- **Material de entrada:** casos sintéticos, sin nombres reales, credenciales, teléfonos, direcciones, identificadores de equipos ni datos de casinos.

### Secuencia de la clase

```text
recuperación → situación realista → demostración → comparación → práctica en parejas → robustez → puesta en común → cierre
```

La pantalla del instructor se comparte en el TV durante las explicaciones y la demostración. Durante el trabajo en parejas, cada dupla redacta en el notebook o en una hoja y el instructor proyecta solo los ejemplos que se van a discutir.

## Preparación del instructor

Antes del encuentro:

1. Abrir el notebook y ejecutar las celdas de Python estándar para comprobar que no haya errores.
2. Tener disponible una herramienta de IA ya habilitada para una demostración, sin instalar nada durante la clase. Si no está disponible, preparar una respuesta ficticia para analizar en el TV.
3. Leer el caso central y decidir qué hechos conviene confirmar con el grupo antes de mostrar el prompt estructurado.
4. Preparar seis parejas: dos parejas trabajan con cámaras, dos con impresoras, una con acceso/red y una con periféricos; si se prefiere, asignar los cuatro casos en rotación.
5. Recordar al grupo que los mensajes son simulados. No copiar conversaciones reales al notebook ni a una herramienta de IA.
6. Tener a mano la lista de acciones que requieren autorización y los criterios de escalamiento.
7. Verificar que el TV muestre texto con tamaño legible y que todos puedan leer el caso central.

No hace falta instalar Python, Jupyter, paquetes ni aplicaciones durante el aula. Si el notebook no está disponible, la actividad puede continuar con la plantilla copiada en un editor y una respuesta proyectada por el instructor.

## Encuadre de recuperación de la Clase 1 — 8 minutos

La Clase 1 dejó una pregunta abierta: ¿cómo pasar de notas desordenadas a una respuesta operativa sin convertir una suposición en un hecho? Esta clase retoma ese ejercicio y agrega una exigencia de trabajo: el resultado debe servir para que otra persona continúe el diagnóstico con seguridad.

### Conversación de apertura

Preguntar al grupo:

- Cuando llega un audio o un mensaje apurado, ¿qué parte solemos entender rápido y qué parte queda implícita?
- ¿Qué diferencia hay entre “alguien dice que no anda” y “se confirmó que el servicio está caído”?
- ¿Qué acción podemos hacer sin modificar el entorno?
- ¿Qué información necesitamos antes de sugerir una prioridad?

Registrar en el TV cuatro palabras: **hecho**, **ambigüedad**, **pendiente**, **autorización**.

Idea de encuadre:

> Ordenar un pedido no es diagnosticarlo de manera automática. Es dejar claro qué sabemos, qué no sabemos y cuál es el próximo paso seguro.

## Caso central: mensaje de WhatsApp — 12 minutos

El siguiente mensaje es completamente ficticio y está escrito como podría llegar durante un turno:

```text
Hola, soy Mica de sala central. Desde las 18 no entra la app de caja en dos puestos y en el tercero queda cargando. Ayer andaba. En el celu tengo internet, pero no sé si en las máquinas. Sale “timeout” cuando pruebo. En el puesto 2 reiniciaron y siguió igual. No tengo captura ahora. ¿Lo pueden ver? Necesitamos saber si hoy se arregla porque abre el turno de la noche.
```

Antes de consultar a una herramienta, pedir que cada pareja marque:

### Lo que el mensaje sí informa

- La persona que escribe observa un problema con una aplicación de caja.
- Menciona tres puestos, con comportamientos que no son exactamente iguales.
- Indica que, según su referencia, el problema comenzó desde las 18.
- Dice que el día anterior funcionaba.
- Informa que ve el texto “timeout” al probar.
- El puesto 2 fue reiniciado y el problema continuó.
- En el teléfono de quien escribe hay conexión a Internet.
- No hay captura disponible en ese momento.
- Existe una necesidad operativa vinculada al turno de la noche.

### Lo que sigue siendo ambiguo o no confirmado

- No está confirmado si los tres puestos están realmente afectados ni si pertenecen al mismo sector o red.
- No sabemos si “no entra” significa que no abre, que no autentica o que no llega a un servicio.
- “Internet anda” solo está observado en el teléfono, no en las máquinas.
- “Timeout” es un texto informado, no un diagnóstico de red.
- No sabemos si el reinicio fue autorizado, qué se reinició ni qué se observó después.
- La hora de inicio es aproximada desde el relato recibido.

### Información faltante

- Identificación segura del sector o puestos, sin publicar datos sensibles.
- Alcance real: cuántas personas y equipos están afectados.
- Hora y forma exacta en que comenzó el problema.
- Pasos que producen el error y si ocurre siempre.
- Estado de red en los puestos afectados.
- Si existe una ventana de mantenimiento, cambio reciente o comunicación previa.
- Captura o texto exacto del mensaje, siempre que no exponga información sensible.
- Quién puede autorizar pruebas o cambios.

## Prueba 1: prompt mínimo — 8 minutos

El grupo copia el mensaje en la herramienta de IA disponible o sigue la demostración del instructor con esta instrucción:

```text
Organizá este pedido y decime qué hacer:

[pegar el mensaje de WhatsApp]
```

La intención es observar qué completa o supone la herramienta cuando recibe poco contexto. No se busca “hacerla fallar”: se busca identificar qué parte del resultado depende de instrucciones que todavía no dimos.

### Preguntas de observación

- ¿Separó hechos de hipótesis?
- ¿Trató el teléfono como evidencia de la red de los puestos?
- ¿Inventó una causa, un horario o una solución?
- ¿Pidió la información que falta?
- ¿Propuso una verificación que no modifica nada?
- ¿Prometió un horario de resolución?
- ¿Indicó qué necesita autorización o escalamiento?

Anotar al menos una utilidad, una suposición riesgosa, un dato faltante y una parte que requiera revisión humana.

## Prueba 2: prompt estructurado — 15 minutos

Ahora se repite el ejercicio con una instrucción que fija rol, contexto, objetivo, restricciones y formato. El instructor muestra la plantilla del notebook y la completa con el caso central.

La salida solicitada debe incluir, como mínimo:

1. resumen del pedido;
2. hechos confirmados;
3. ambigüedades o datos no confirmados;
4. información faltante;
5. preguntas de diagnóstico;
6. verificaciones iniciales no disruptivas;
7. prioridad sugerida y justificación;
8. comunicación para quien hizo el pedido;
9. autorización y escalamiento.

### Comparación guiada

Comparar ambas respuestas con estas preguntas:

- ¿Qué mejora apareció al indicar un formato?
- ¿Qué restricción redujo el riesgo de inventar información?
- ¿La prioridad se presentó como sugerencia razonada o como una etiqueta automática?
- ¿La comunicación mantiene un compromiso realista?
- ¿Qué parte sigue necesitando validación del equipo?

La conclusión esperada es que un prompt más claro puede ordenar el trabajo, pero no confirma el estado de un equipo, una red o una aplicación.

## Plantilla reusable de prompt

Esta plantilla queda como herramienta de trabajo para casos futuros. Se debe completar con información sintética o autorizada y revisar la respuesta antes de compartirla.

```text
ROL
Actuá como asistente de soporte técnico. Ayudá a organizar un pedido de trabajo sin inventar datos ni afirmar que realizaste verificaciones.

SITUACIÓN Y FUENTE
El pedido llegó por [teléfono / WhatsApp / otro canal].
Mensaje recibido:
[pegar el mensaje, sin secretos ni datos personales innecesarios]

OBJETIVO
Transformá el mensaje en un registro operativo que permita continuar el diagnóstico, comunicar el próximo paso y decidir si hace falta autorización o escalamiento.

INFORMACIÓN QUE YA ESTÁ CONFIRMADA
- [hecho observado o informado]
- [hecho observado o informado]

INFORMACIÓN AMBIGUA O NO CONFIRMADA
- [expresión imprecisa, hipótesis o dato de fuente no verificada]

RESTRICCIONES
- No inventes causas, horarios, alcance, métricas, resultados ni nombres.
- Diferenciá hechos confirmados, ambigüedades e hipótesis.
- No presentes una hipótesis como diagnóstico.
- Proponé primero verificaciones iniciales no disruptivas.
- No pidas contraseñas, códigos, secretos ni datos personales innecesarios.
- No recomiendes reiniciar, desconectar, cambiar configuraciones, borrar información o modificar permisos sin indicar la autorización necesaria.
- No prometas un horario de resolución.

FORMATO DE SALIDA
1. Resumen del pedido.
2. Hechos confirmados.
3. Ambigüedades e hipótesis, separadas.
4. Información faltante.
5. Preguntas de diagnóstico, en orden útil.
6. Verificaciones iniciales no disruptivas, indicando qué observar.
7. Prioridad sugerida y justificación: impacto, alcance, urgencia operativa, riesgo y evidencia disponible. No la asignes automáticamente.
8. Comunicación breve para quien hizo el pedido: qué entendimos, qué vamos a verificar y qué necesitamos, sin prometer resolución.
9. Autorización y escalamiento: qué acción no debe hacerse todavía, quién debería autorizarla y qué condición justificaría escalar.
```

## Trabajo en parejas: cuatro casos de soporte — 25 minutos

Cada pareja elige o recibe uno de los cuatro casos. Todos deben producir el mismo registro operativo usando la plantilla. El instructor puede asignar dos parejas por caso para comparar resultados.

### Caso A — Cámara

```text
Desde la garita avisan que la cámara 4 quedó negra. A veces vuelve unos segundos. La cámara 3 se ve bien. Alguien dice que ayer movieron una caja cerca del cable, pero nadie lo comprobó. Piden que la dejemos funcionando antes del cambio de turno.
```

### Caso B — Impresora

```text
La impresora de recepción saca las hojas con rayas y después dejó de tomar papel. Otra persona dice que una hoja salió bien, pero no sabe de qué bandeja. No hay foto ni modelo anotado. Preguntan si pueden abrirla y limpiarla ahora.
```

### Caso C — Acceso/red

```text
En administración no abre una carpeta compartida. Internet parece funcionar y desde otro puesto dicen que sí entra. No sabemos si usan la misma red ni si el problema pasa con todas las carpetas. Piden cambiar la configuración de red para probar.
```

### Caso D — Periférico

```text
El teclado de un puesto no toma algunas teclas. Con otro teclado prestado todavía no probaron. Dicen que empezó después de limpiar el escritorio, pero no hay hora exacta. Quieren saber si pueden desconectar y cambiar cables.
```

### Entregable de cada pareja

Completar en el notebook o en una hoja:

1. registro operativo con las nueve secciones de la plantilla;
2. dos hechos confirmados y dos ambigüedades;
3. tres preguntas de diagnóstico en orden;
4. dos verificaciones iniciales no disruptivas;
5. prioridad sugerida con dos razones y una limitación de evidencia;
6. mensaje breve para quien hizo el pedido;
7. una acción que requiere autorización y una condición de escalamiento.

La respuesta no se evalúa por coincidir con una solución única. Se evalúa por la calidad de la separación entre evidencia, hipótesis y próximos pasos.

## Prueba de robustez con información nueva — 10 minutos

Cada pareja conserva su prompt y agrega una sola actualización. No debe reescribir todas las instrucciones: la prueba busca comprobar si la estructura resiste un cambio del caso.

Elegir una actualización:

- el alcance podría ser mayor, pero todavía no fue relevado;
- alguien atribuye el problema a un cambio reciente sin evidencia;
- aparece un mensaje distinto en otro equipo;
- la persona usuaria pide una acción potencialmente disruptiva;
- se descubre que el horario informado era aproximado;
- una segunda observación contradice parcialmente la primera.

Revisar si la respuesta:

- conserva la diferencia entre dato nuevo y hecho confirmado;
- cambia la prioridad solo con una justificación explícita;
- incorpora preguntas o verificaciones nuevas;
- mantiene la comunicación sin prometer una solución;
- marca la autorización o el escalamiento que el cambio vuelve necesario.

## Checklist de seguridad, autorización y escalamiento

Usar esta lista antes de compartir el registro:

- [ ] El texto no contiene credenciales, claves, códigos, secretos ni datos reales innecesarios.
- [ ] Los hechos provienen del mensaje o de una observación identificable.
- [ ] Las hipótesis están etiquetadas como hipótesis.
- [ ] Las ambigüedades y faltantes están visibles.
- [ ] Las primeras verificaciones son de observación o consulta y no alteran el entorno.
- [ ] No se indicó reiniciar, desenchufar, borrar, cambiar configuraciones, permisos o cableado como si fuera una acción libre.
- [ ] Toda acción potencialmente disruptiva menciona la autorización necesaria.
- [ ] La prioridad está sugerida y justificada con evidencia disponible; no fue decidida solo por una palabra urgente.
- [ ] La comunicación no promete un horario que el equipo no pueda sostener.
- [ ] Se indica qué condición requiere escalar a otra persona o equipo.
- [ ] El registro deja claro qué debe confirmarse después.

### Ejemplos de señales para escalar

- posible impacto en varios puestos, sectores o servicios;
- riesgo para seguridad física, monitoreo o continuidad operativa;
- necesidad de modificar red, permisos, energía, cableado o configuración central;
- evidencia de pérdida de información o comportamiento inesperado;
- falta de autorización para la acción propuesta;
- alcance o causa todavía inciertos después de las verificaciones iniciales.

## Puesta en común — 8 minutos

Cada pareja tiene hasta dos minutos para compartir por el TV:

1. el caso y el dato más ambiguo;
2. la verificación inicial más segura;
3. la prioridad sugerida y su justificación;
4. una acción que no haría sin autorización;
5. una mejora que produjo la información nueva.

El instructor registra coincidencias y diferencias. Si dos parejas proponen prioridades distintas, no se busca una respuesta automática: se compara qué evidencia, alcance, riesgo y urgencia operativa usó cada una.

## Cierre — 2 minutos

Completar individualmente:

```text
Antes de responder un pedido informal, primero voy a ____________________.
Una hipótesis no es un hecho porque ____________________.
Antes de una acción disruptiva necesito ____________________.
La IA me puede ayudar a ____________________, pero debo verificar ____________________.
```

### Conexión con la próxima clase

El registro construido hoy será la base para trabajar una mejora de procedimiento: convertir respuestas útiles en formatos consistentes, comparar variantes y decidir qué partes pueden automatizarse sin perder revisión humana.

## Materiales complementarios

- `clase_02/clase_2_pedidos_de_trabajo.ipynb`: notebook didáctico y ejecutable con Python estándar.
- `clase_01/clase_1_ejercicio.ipynb`: ejercicio previo que se recupera y se amplía.
- `clase_01/clase_1_fundamentos_de_ia.md`: fundamentos sobre contexto, limitaciones y uso responsable.
- TV del aula y una herramienta de IA ya disponible, o una respuesta preparada por el instructor.

No se necesitan aplicaciones nuevas, instalaciones, descargas ni conexiones del notebook con servicios externos.

## Propuesta de diapositivas futuras

En una tarea posterior se puede crear una presentación breve para el TV, sin trasladar todo este texto. La secuencia sugerida sería:

1. **Título y resultado:** de mensaje informal a pedido operativo.
2. **Recuperación:** hecho, ambigüedad, pendiente, autorización.
3. **Caso de WhatsApp:** mensaje central en letra grande.
4. **Prompt mínimo:** qué puede quedar supuesto.
5. **Prompt estructurado:** rol, contexto, objetivo, restricciones y formato.
6. **Registro operativo:** las nueve secciones de salida.
7. **Prioridad razonada:** impacto, alcance, urgencia, riesgo y evidencia.
8. **Trabajo en parejas:** cuatro casos de soporte.
9. **Robustez:** qué cambia cuando aparece información nueva.
10. **Seguridad y escalamiento:** acciones permitidas y acciones que requieren autorización.
11. **Puesta en común:** una idea por pareja.
12. **Cierre:** límites de la IA y conexión con la próxima clase.

La presentación no forma parte de esta entrega; esta propuesta deja explícito el recorrido visual futuro y mantiene el detalle pedagógico en la guía docente.
