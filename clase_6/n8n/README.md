# Entorno local de n8n para la Clase 6

Esta carpeta inicia n8n `2.35.7` con Docker Compose. La versión está fijada para que los equipos trabajen con la misma interfaz durante la práctica. Utiliza la imagen oficial, guarda los datos en un volumen persistente y publica el editor solamente en la computadora local.


## Prerrequisito

Docker Desktop debe estar instalado, iniciado y probado antes del encuentro.

En Símbolo del sistema:

```console
docker --version
docker compose version
docker info
```

Instalar Docker Desktop durante el encuentro puede requerir permisos administrativos y un reinicio. Comprobá antes que Docker Desktop esté iniciado y que los comandos de verificación respondan.

## Primer inicio con Internet

Abrí una terminal en esta carpeta y ejecutá:

```console
docker compose pull
docker compose up -d
docker compose ps
```

Luego, abrí:

```text
http://127.0.0.1:5678
```

En Windows también se puede hacer doble clic en `iniciar-n8n.cmd`.

La primera vez, completá la creación del usuario propietario. Usá una contraseña individual para este entorno local y guardala de forma segura.

## Operación habitual

Para iniciar, ejecutá:

```console
docker compose up -d
```

Para ver el estado, ejecutá:

```console
docker compose ps
```

Para ver los últimos mensajes, ejecutá:

```console
docker compose logs --tail 50 n8n
```

Para detener n8n sin borrar datos, ejecutá:

```console
docker compose stop
```

En Windows se pueden usar `iniciar-n8n.cmd` y `detener-n8n.cmd`. Los scripts siempre trabajan desde esta carpeta y no modifican políticas de PowerShell.

## Persistencia

La configuración guarda `/home/node/.n8n` en el volumen nombrado `clase_n8n_data`. Allí quedan la cuenta, las configuraciones y los workflows.

```text
Estos comandos pueden borrar los datos persistentes. No los ejecutes durante la práctica:

docker compose down -v
docker volume rm clase_n8n_data
```

> Para detener el entorno sin borrar los datos, usá `docker compose stop`.

## Problemas frecuentes

- Si `docker info` no conecta, abrí Docker Desktop y esperá a que el motor esté listo.
- Si el puerto 5678 está ocupado, comprobá si ya hay otra instancia de n8n. No finalices procesos desconocidos.
- Si el contenedor se detiene, ejecutá `docker compose logs --tail 50 n8n`.
- Si la página no abre, comprobá que uses `http://127.0.0.1:5678`, sin `https`.
- Si falla la descarga, pausá la instalación y consultá las restricciones de red o la alternativa de conexión prevista para el curso.

## Configuración incluida

- Imagen: `docker.n8n.io/n8nio/n8n:2.35.7`.
- Puerto: `127.0.0.1:5678` hacia el puerto `5678` del contenedor.
- Zona horaria: `America/Argentina/Tucuman`.
- Volumen persistente: `clase_n8n_data`.

Referencia oficial: [instalar n8n con Docker Compose](https://docs.n8n.io/deploy/host-n8n/install-options/install-using-docker-compose).
