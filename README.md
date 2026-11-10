
# Práctica de Transformers: atención y Transformer básico sobre una serie de temperatura

Trabajo individual de la Especialización en Inteligencia Artificial, Universidad de Cundinamarca.

**Autor:** Juan Camilo Cruz Beltran

## Descripción

En esta práctica se implementan, con **PyTorch**, un **mecanismo de atención** y un **Transformer básico** (codificador) para predecir la temperatura mínima del día siguiente a partir de los 30 días anteriores. Los resultados se comparan con dos líneas base sin aprendizaje (persistencia y media móvil de 7 días).

## Datos

- **Conjunto:** temperaturas mínimas diarias en Melbourne, Australia (1981-1990), 3650 observaciones.
- **Fuente:** [jbrownlee/Datasets](https://github.com/jbrownlee/Datasets) (`daily-min-temperatures.csv`).
- El notebook descarga el archivo automáticamente, no hay que subirlo.

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `Practica_Transformers_Temperatura.ipynb` | Notebook con todo el flujo: datos, modelos, entrenamiento, evaluación y gráficas |

## Metodología

1. **Preparación:** división cronológica 70 % / 15 % / 15 % (entrenamiento, validación, prueba), normalización con estadísticas del entrenamiento y ventanas deslizantes de 30 días.
2. **Modelo A, atención simple:** proyección a 32 dimensiones, codificación posicional y atención de una cabeza (Q, K, V) con la consulta del último día.
3. **Modelo B, Transformer básico:** 2 bloques de codificador con 4 cabezas de atención, red feed-forward, conexiones residuales, normalización de capa y dropout.
4. **Entrenamiento:** Adam (lr = 0,002), pérdida MSE, lotes de 64, parada temprana (paciencia de 8) y semilla 42.

## Resultados (conjunto de prueba)

| Modelo | MAE (°C) | RMSE (°C) | R² |
|---|---|---|---|
| Persistencia (ayer) | 2,036 | 2,572 | 0,565 |
| Media móvil 7 días | 1,968 | 2,540 | 0,576 |
| Atención simple | 1,756 | 2,270 | 0,661 |
| Transformer básico | 1,736 | 2,229 | 0,673 |

Los modelos con atención superan a las líneas base. El Transformer solo mejora de forma marginal a la atención simple en este problema. Los valores pueden variar ligeramente según el hardware.

## Referencias

- Vaswani, A., et al. (2017). *Attention is all you need*. https://arxiv.org/abs/1706.03762
- Doshi, K. (2021). *Transformers explained visually (Part 1): Overview of functionality*. Towards Data Science.
- Brownlee, J. (s. f.). *Daily minimum temperatures in Melbourne* [Conjunto de datos]. GitHub.
