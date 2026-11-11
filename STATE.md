## Estado actual
Repositorio publicado en GitHub con el CI en verde.
Página de inicio, /salud y /docs funcionando en https://plataforma-ludica-pyw7.onrender.com.
Agregado GET /api/version, que devuelve la versión definida en app/proyecto.py.
Prueba del endpoint añadida; las 7 pruebas pasan y Ruff no reporta problemas.

## Decisiones
| Fecha | Decisión | Motivo |
| --- | --- | --- |
| 2026-11-11 | Usar la plantilla del curso con FastAPI | Es el stack definido para el proyecto |
| 2026-11-11 | GET /api/version devuelve {"version": proyecto.VERSION} | Mantener una única fuente para la versión y verificar el contrato con una prueba |

## Siguiente paso
Verificar en Render que GET /api/version responde correctamente.
