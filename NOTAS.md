# Notas de operación

## Comandos frecuentes

| Comando | Función |
|---|---|
| `docker compose up -d` | Levanta el entorno en segundo plano |
| `docker compose ps` | Estado de los servicios |
| `docker compose logs -f wordpress` | Logs de WordPress en tiempo real |
| `docker compose logs -f db` | Logs de MySQL en tiempo real |
| `docker compose down` | Detiene y elimina contenedores y red (conserva datos) |
| `docker compose down -v` | Detiene y **elimina también los volúmenes** |
| `docker volume ls` | Lista los volúmenes existentes |

## Problemas encontrados y solución

**El puerto 8080 está ocupado.** Cambiar el valor de `WORDPRESS_PORT` en el
archivo `.env` y volver a levantar el entorno. No es necesario modificar el
`docker-compose.yml`, ya que el puerto está externalizado.

**WordPress muestra error de conexión a la base de datos.** Verificar con
`docker compose ps` que el servicio `db` aparezca como `healthy`. Si el
healthcheck aún no ha pasado, esperar unos segundos. Si persiste, comprobar que
las variables de `.env` coincidan entre ambos servicios.

**Se quiere reiniciar la instalación de WordPress desde cero.** Ejecutar
`docker compose down -v` para eliminar los volúmenes y levantar de nuevo. Esto
borra todo el contenido publicado.

## Restauración del entorno en otro equipo

1. Clonar el repositorio.
2. Copiar `.env.example` a `.env` y completar los valores.
3. Ejecutar `docker compose up -d`.
4. Completar el asistente de instalación en `http://localhost:8080`.