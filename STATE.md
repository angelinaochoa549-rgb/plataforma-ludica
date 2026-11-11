## Estado actual
Repositorio publicado en GitHub con el CI en verde.
Página de inicio, /salud y /docs funcionando en https://plataforma-ludica-pyw7.onrender.com.
Agregado GET /api/version, que devuelve la versión definida en app/proyecto.py.
Prueba del endpoint añadida; las 7 pruebas pasan y Ruff no reporta problemas.
Pendiente comprobar /api/version en https://plataforma-ludica-pyw7.onrender.com/api/version.

## Decisiones
| Fecha | Decisión | Motivo |
| --- | --- | --- |
| 2026-11-11 | Usar la plantilla del curso con FastAPI | Es el stack definido para el proyecto |
| 2026-11-11 | GET /api/version devuelve {"version": proyecto.VERSION} | Mantener una única fuente para la versión y verificar el contrato con una prueba |

## Siguiente paso
Crear el servicio de la mecánica Memoria de parejas del curso Matemáticas en app/servicios/, con su prueba.
