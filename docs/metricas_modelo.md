# Métricas del modelo

Este archivo almacenará los resultados de evaluación del modelo.

Inicialmente se encuentra vacío porque el modelo todavía no ha sido entrenado ni evaluado.

Después de ejecutar el script:

```text
src/evaluar_modelo.py
```

este archivo será actualizado automáticamente con las métricas principales.

## Experimento controlado

### Rama creada
experimento-hiperparametro

### Cambio realizado
Se modificaron los hiperparámetros del modelo LogisticRegression:

- C = 0.5
- max_iter = 500
- random_state = 42

### Archivo modificado
src/entrenar_modelo.py

### Resultado obtenido
El modelo fue reentrenado y evaluado correctamente utilizando los nuevos hiperparámetros.

### Interpretación
El experimento demuestra que es posible ajustar hiperparámetros del modelo manteniendo el flujo completo de entrenamiento, evaluación y versionado mediante Git.