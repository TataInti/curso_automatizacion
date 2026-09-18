# IA y automatización aplicada a soporte técnico

Material de capacitación para el equipo de soporte técnico de Casinos Play. Las clases combinan conceptos, casos de trabajo y ejercicios con un modelo de lenguaje local. Los ejemplos usan datos ficticios.

## Material disponible

| Clase | Guía | Práctica |
| --- | --- | --- |
| 1 · Fundamentos de IA generativa | [Leer la guía](clase_01/clase_1_fundamentos_de_ia.md) | [Abrir el notebook](clase_01/clase_1_ejercicio.ipynb) |
| 2 · Ingeniería de prompt | [Leer la guía](clase_02/clase_2_ingenieria_de_prompt.md) | [Abrir el notebook](clase_02/clase_2_ingenieria_de_prompt.ipynb) |

Las guías explican la clase; los notebooks contienen las actividades para ejecutar y completar. La clase 2 presupone el entorno preparado para la clase 1.

## Antes de empezar

Necesitás Python 3.12, conexión a Internet para instalar los paquetes y descargar el modelo la primera vez, y Visual Studio Code con las extensiones **Python** y **Jupyter** (u otro programa que abra notebooks de Jupyter). El modelo se descarga desde Hugging Face en la primera ejecución y luego queda en la caché local. La inferencia se ejecuta en la computadora, sin usar una API paga. Reservá espacio libre y memoria para el modelo; la descarga y la primera carga pueden tardar varios minutos.

En macOS o Linux, el comando de Python puede llamarse `python3.12` en vez de `python`. Comprobá la versión antes de seguir:

```bash
python --version
```

## Instalación automática en Windows

Si no tenés experiencia preparando el entorno, usá el [instalador de Windows](scripts/setup_windows.ps1). Abrí **PowerShell** desde el menú Inicio y pegá este comando:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -Command "[Net.ServicePointManager]::SecurityProtocol=[Net.SecurityProtocolType]::Tls12; & ([scriptblock]::Create((Invoke-RestMethod 'https://raw.githubusercontent.com/TataInti/curso_automatizacion/main/scripts/setup_windows.ps1')))"
```

El instalador comprueba Git, Python 3.12 y Visual Studio Code; instala lo que falte con `winget` o desde python.org, clona este repositorio en `GitHub\curso_automatizacion` dentro de tu carpeta de usuario, crea `.venv`, instala `requirements.txt` y las extensiones de VS Code, y abre la carpeta. Necesitás Internet y acceso para instalar programas. Puede que Windows muestre solicitudes de confirmación. **No hace falta abrir PowerShell como administrador.**

Si ya descargaste el repositorio, abrí PowerShell en esa carpeta y ejecutá:

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\setup_windows.ps1
```

Si falla la instalación de `llama-cpp-python`, puede faltar un compilador de C++. El instalador mostrará el error y cómo continuar. Podés volver a ejecutarlo después de resolverlo; conserva la carpeta y el entorno existentes.

## Descargar el repositorio

En GitHub, elegí **Code → Download ZIP** y descomprimí el archivo. También podés usar Git:

```bash
git clone https://github.com/TataInti/curso_automatizacion.git
cd curso_automatizacion
```

Abrí una terminal en la carpeta descargada, donde está `requirements.txt`.

## Preparar el entorno en Windows (PowerShell)

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Si `py -3.12` no encuentra Python, instalá Python 3.12 desde [python.org](https://www.python.org/downloads/) y volvé a abrir PowerShell. No hace falta ejecutar PowerShell como administrador.

## Preparar el entorno en macOS o Linux

```bash
python3.12 -m venv .venv
.venv/bin/python -m pip install --upgrade pip
.venv/bin/python -m pip install -r requirements.txt
```

Si no tenés Python 3.12, instalalo con el gestor de paquetes de tu sistema o desde [python.org](https://www.python.org/downloads/). En algunas distribuciones de Linux también hace falta instalar el paquete `python3.12-venv`. `llama-cpp-python` puede necesitar herramientas de compilación de C/C++ si no hay un paquete precompilado para tu sistema.

## Abrir y ejecutar las prácticas

1. Abrí esta carpeta en Visual Studio Code.
2. Abrí el notebook de la clase en la tabla anterior.
3. Elegí como kernel el Python de `.venv` cuando VS Code lo solicite.
4. Ejecutá las celdas en orden. La primera descarga del modelo requiere Internet.

El notebook busca el archivo `Q4_K_M` del modelo público [`LiquidAI/LFM2.5-1.2B-Instruct-GGUF`](https://huggingface.co/LiquidAI/LFM2.5-1.2B-Instruct-GGUF). Si falla la descarga, verificá la conexión y volvé a ejecutar la celda. Si aparece `ModuleNotFoundError`, comprobá que el kernel seleccionado sea `.venv` y que la instalación de `requirements.txt` haya terminado sin errores.

Las respuestas del modelo son material para observar y discutir: pueden variar y contener errores. No ingreses credenciales, datos personales ni información real sensible en las prácticas.

## Estado del material

Actualmente están publicadas las clases 1 y 2. El contenido puede actualizarse a medida que avance el curso.

## Licencia

Este material se distribuye bajo la [licencia MIT](LICENSE).
