# Mini-aplicación de práctica: Generador de contraseñas

## Versión A

**Objetivo:** construir la mini-aplicación con un prompt de una línea.

**Herramienta y modelo:** Copilot con el modelo Auto (gpt-6-luna).

**Prompt:**

```
Haz una app web que genere contraseñas con FastAPI.
```

**Resultado:** el agente creó una aplicación que arranca y funciona en el navegador, con `main.py` en la raíz, `static/index.html`, `README.md` y `tests/test_main.py`. Pruebas de aceptación aprobadas: 0 de 7 (ModuleNotFoundError: No module named 'app'). Errores de Ruff: 2 (I001, imports sin ordenar).

## Versión B

**Objetivo:** construir la misma aplicación con un prompt estructurado, AGENTS.md y pruebas de aceptación.

**Herramienta y modelo:** Copilot con el modelo Auto (gpt-6-luna).

**Prompt:**

```
## Rol
Actúa como desarrollador backend con experiencia en FastAPI, Jinja2 y pruebas con pytest.

## Objetivo
Construir la mini-aplicación web Generador de contraseñas con estos requisitos:
1. GET / muestra un formulario para elegir la longitud y si se incluyen números y símbolos, un botón para generar y un botón para copiar la contraseña.
2. GET /api/contrasena recibe los parámetros longitud, numeros y simbolos, y devuelve {"contrasena": texto, "longitud": número}. Valores por defecto: longitud 12, numeros true y simbolos false.
3. La contraseña siempre incluye letras minúsculas y mayúsculas. Si numeros es true, incluye al menos un número; si es false, no incluye ninguno. Si simbolos es true, incluye al menos un símbolo de este grupo: !@#$%&*?-_ ; si es false, no incluye ninguno.
4. La longitud debe estar entre 8 y 64; fuera de ese rango responde con el código 422.
5. La contraseña se genera con el módulo secrets de Python, no con random.

## Contexto
Lee AGENTS.md. El contrato de la API está en tests/test_aceptacion.py: las rutas, los nombres de los campos y los códigos de estado deben coincidir con esas pruebas.

## Restricciones
- Usa solo las dependencias de requirements.txt.
- Define las rutas en app/main.py y la lógica en app/servicios.py, sin importar FastAPI en servicios.
- Guarda los datos en memoria, sin base de datos ni archivos.
- No modifiques tests/test_aceptacion.py.
- La página usa HTML, CSS y JavaScript sin librerías externas.

## Formato de salida
Antes de escribir código, muestra el plan con las rutas completas de los archivos que vas a crear y espera mi aprobación. Al terminar, resume en una línea qué hace cada archivo.

## Ejemplo
GET /api/contrasena?longitud=16&numeros=true&simbolos=true devuelve:
{"contrasena": "q7G!mR2-xW9a#Lp4", "longitud": 16}

## Criterio de éxito
python -m pytest -v pasa todas las pruebas y ruff check . no reporta errores. Si después de 3 intentos las pruebas no pasan, detente y explica el problema.
```

**Resultado:** el agente creó `app/main.py` (rutas), `app/servicios.py` (lógica) y `app/templates/index.html` (página), con las rutas y la lógica separadas. Intentos necesarios: [1]. Pruebas de aceptación aprobadas: 7 de 7. Ruff reportaba I001 en el archivo de pruebas de la guía, que no se puede modificar; se resolvió con un `ruff.toml` que ignora esa regla solo en `tests/`. Errores de Ruff finales: 0.

## Mejora

**Objetivo:** agregar el campo fuerza a GET /api/contrasena y mostrarlo con color en la página.

**Herramienta y modelo:** Copilot con el modelo Auto (gpt-6-luna).

**Prompt:**

```
## Rol
Actúa como desarrollador backend con experiencia en FastAPI, Jinja2 y pruebas con pytest.

## Objetivo
Agregar el campo "fuerza" a la respuesta de GET /api/contrasena, que pasa a devolver {"contrasena": texto, "longitud": número, "fuerza": "fuerte" | "media" | "débil"}. Reglas, evaluadas en este orden: "débil" si la longitud es menor que 12 o si la contraseña le falta números o símbolos (basta con que falte uno); "fuerte" si la longitud es 16 o más e incluye números y símbolos; "media" en los demás casos. La página principal debe mostrar la fuerza con un color: rojo para débil, amarillo para media y verde para fuerte.

## Contexto
Lee AGENTS.md, app/main.py, app/servicios.py y app/templates/index.html. Las pruebas de tests/test_aceptacion.py deben seguir pasando.

## Restricciones
- No modifiques tests/test_aceptacion.py.
- No agregues dependencias.
- Mantén las rutas en app/main.py y la lógica en app/servicios.py, sin importar FastAPI en servicios.
- La página usa HTML, CSS y JavaScript sin librerías externas.
- Crea la prueba nueva en tests/test_mejora.py.

## Formato de salida
Antes de escribir código, muestra el plan con las rutas completas de los archivos y espera mi aprobación. Al terminar, resume en una línea qué cambió en cada archivo.

## Ejemplo
GET /api/contrasena?longitud=16&numeros=true&simbolos=true devuelve:
{"contrasena": "q7G!mR2-xW9a#Lp4", "longitud": 16, "fuerza": "fuerte"}
GET /api/contrasena?longitud=8 devuelve fuerza "débil".

## Criterio de éxito
tests/test_mejora.py comprueba el valor del campo fuerza (no solo el código de estado) en los tres niveles, y python -m pytest -v pasa todas las pruebas y ruff check . no reporta errores. Si después de 3 intentos no pasan, detente y explica el problema.
```

**Resultado:** el agente modificó `app/servicios.py`, `app/main.py` y `app/templates/index.html`, y creó `tests/test_mejora.py` con 5 casos que comprueban el valor de fuerza en los tres niveles. Pruebas aprobadas: 12 de 12 (7 de aceptación y 5 de la mejora), con Ruff sin errores. En el prompt se fijó que "débil" significa que le falta números o símbolos (basta con uno). Correcciones necesarias: [ninguna].

## Comparación

| Criterio | Versión A | Versión B |
|---|---|---|
| Modelo usado | Auto (gpt-6-luna) | Auto (gpt-6-luna) |
| Mensajes enviados al agente | [1] | [2] |
| La aplicación arranca | Sí | Sí |
| Requisitos del anexo que cumple | [X de 5] | [X de 5] |
| Pruebas de aceptación aprobadas | 0 de 7 | 7 de 7 |
| Errores de Ruff | 2 | 0 |
| Separa rutas y lógica | No | Sí |

**Conclusión:** la mayor diferencia la produjeron las pruebas de aceptación junto con el AGENTS.md. Como el agente conocía desde el inicio el contrato (`app.main`, las rutas, los campos y los códigos de estado) y la estructura de carpetas, la versión B pasó 7 de 7 pruebas y separó rutas y lógica, mientras que la versión A pasó 0 de 7 porque puso `main.py` en la raíz y no en `app/`. En la versión A el agente decidió por su cuenta la estructura de carpetas, el uso de `static/index.html`, archivos que nadie pidió (README y `test_main.py`) y valores distintos a los del anexo, como el mínimo de longitud en 4 en lugar de 8. La próxima vez daré desde el principio el contrato, la estructura del proyecto y las restricciones, y pediré el plan antes de escribir código para corregirlo antes de que construya.