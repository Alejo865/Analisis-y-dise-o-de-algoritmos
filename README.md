# Nivora

Aplicacion Flask para aprender Python.

## Desarrollo

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
$env:NIVORA_SECRET_KEY = "clave-local-de-desarrollo"
flask --app app run --debug
```

## Pruebas

```powershell
python -m pytest -q
```

Las pruebas crean una base SQLite temporal independiente por instancia de la aplicación; no modifican `database/nivora.db`.

## Laboratorio de algoritmos

Desde **Practicar** puedes entrar al Laboratorio. Incluye actividades interactivas de Merge Sort, programación dinámica y Backtracking, además de contenido educativo de Kruskal, Prim y Union-Find. La recomendación Voraz utiliza los resultados guardados de los quizzes.

## Producción

Configura `NIVORA_SECRET_KEY` con una clave aleatoria larga, `NIVORA_DATABASE_PATH` con la ruta de la base de datos y `NIVORA_COOKIE_SECURE=1` cuando se use HTTPS. Ejecuta `deploy.sh` en un entorno Linux con Gunicorn. No actives `FLASK_DEBUG` en producción.
## Recomendación Voraz (Fase 5)

Al evaluar un quiz, Nivora registra por pregunta el último estado, el total de
intentos, los aciertos y los errores en `PROGRESO_EJERCICIO`. La sección
`Practicar` recomienda una pregunta pendiente con esta prioridad:

1. Mayor cantidad de respuestas incorrectas acumuladas.
2. Menor dificultad (`basico`, `intermedio`, `avanzado`).
3. Menor posición dentro de la lección.

Es una heurística voraz local; no pretende calcular una ruta de aprendizaje
óptima. En el esquema actual `USUARIO.id_persona` es su clave primaria, por lo
que ese identificador se guarda en `PROGRESO_EJERCICIO.id_usuario`.
