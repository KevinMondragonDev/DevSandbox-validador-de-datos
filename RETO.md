# 🚀 DevSandbox — Validador de datos

**Repositorio:** `DevSandbox-validador-de-datos` · **Tipo:** biblioteca + ETL · **Tiempo:** 4–5 h · **Después de:** el gran integrador de este módulo

> Reglas, README y lista de cierre: [`NIGHTBUILDS.md`](docs/REGLAS.md). **No hay solución: el diseño es tuyo.**

## El caso

En tu DevSandbox anterior diste por hecho que el CSV venía bien. En la vida real no: montos vacíos, fechas imposibles, tipos inventados. Vas a construir una pequeña biblioteca que revisa un archivo y dice **exactamente** qué fila está mal y por qué, sin detenerse en el primer error.

Datos: `datos/transacciones_sucias.csv` (con `csv.DictReader`, sin pandas).

## Qué practicas

| Tema | Dónde aparece |
|---|---|
| Funciones | Una función pequeña por comprobación |
| Excepciones | Excepciones propias y `try/except` que no se traga errores |
| POO | Una clase por regla y una clase que las coordina |

## Hitos

**Hito 1 — Una regla como función.** `validar_monto(fila)` que lance `ValueError` con un mensaje claro si el monto está vacío, no es número o no es positivo.
*Comprueba:* pruébala a mano con 5 filas inventadas.

**Hito 2 — Excepciones propias.** `ErrorDeValidacion` (con la fila y el motivo) y subclases para monto, fecha y tipo.
*Comprueba:* puedes capturar todas con un solo `except ErrorDeValidacion`.

**Hito 3 — Reglas como clases.** Una clase base `Regla` con `validar(fila)` y una subclase por comprobación.
*Comprueba:* añadir una regla nueva no modifica las existentes.

**Hito 4 — El coordinador.** `Validador(reglas)` recorre el archivo completo, **no se detiene** en el primer error y devuelve las filas válidas y las rechazadas con su motivo.
*Comprueba:* válidas + rechazadas = filas del archivo.

**Hito 5 — ETL.** `python validar.py entrada.csv` escribe `validas.csv`, `rechazadas.csv` y un resumen por motivo en pantalla.
*Comprueba:* si el archivo no existe, termina con un mensaje claro, no con un traceback.

## Preguntas para defenderlo

- ¿Cuándo lanzas una excepción y cuándo devuelves `False`?
- ¿Qué error NO capturas a propósito y por qué?
- ¿Qué ganaste al convertir las reglas en clases? ¿Y qué complicaste?

## Súbelo de nivel

- Tests con `pytest` para cada regla (`05_ingenieria_de_datos/03_ingenieria_de_software/02_paquetes_y_pruebas/04`).
- Compáralo, cuando llegues, con la validación de Pydantic (`05_ingenieria_de_datos/06_apis_con_fastapi/01_construir/02`).
