# Examen Aplicado de Machine Learning I

Análisis exploratorio, no supervisado y supervisado del dataset Bike Sharing, desarrollado como parte del Examen Aplicado de Machine Learning I.

## Dataset

* **Nombre:** Bike Sharing Dataset
* **Fuente:** UCI Machine Learning Repository
* **URL:** https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset
* **Archivo utilizado:** `day.csv`
* **Número de observaciones:** 731
* **Número de variables:** 16
* **Variable objetivo:** `cnt` (cantidad total diaria de arriendos de bicicletas)
* **Tipo de tarea:** regresión

El objetivo del análisis es estudiar los patrones asociados con la demanda diaria de bicicletas y construir un modelo capaz de predecir la cantidad total de arriendos.

## Metodología

El trabajo se desarrolló mediante las siguientes etapas:

1. Análisis exploratorio de datos, incluyendo estructura, tipos de variables, estadísticas descriptivas, valores faltantes, valores extremos y distribución de la variable objetivo.
2. Análisis de correlaciones y evaluación de multicolinealidad entre los predictores.
3. División de los datos en conjuntos de entrenamiento y prueba antes de aplicar transformaciones.
4. Preprocesamiento mediante `ColumnTransformer`, utilizando imputación, estandarización, codificación nominal y codificación ordinal.
5. Reducción de dimensionalidad mediante análisis de componentes principales (PCA).
6. Segmentación no supervisada mediante K-Means y caracterización de los clusters obtenidos.
7. Entrenamiento y ajuste mediante validación cruzada de los modelos Ridge y Random Forest.
8. Evaluación sobre el conjunto de prueba mediante RMSE, MAE, R² y MAPE.
9. Análisis de importancia de variables, residuales y observaciones con mayor error.

Para evitar fuga de información, las variables `instant` (identificador del registro), `dteday` (fecha), `casual` (usuarios casuales) y `registered` (usuarios registrados) fueron excluidas de los predictores. Las dos últimas variables forman directamente la variable objetivo, dado que `cnt = casual + registered`.

## Resultados del mejor modelo

Random Forest fue seleccionado como el mejor modelo debido a que presentó el menor RMSE y MAE y el mayor R² sobre el conjunto de prueba.

| Modelo        |     RMSE |      MAE |     R² |       MAPE | Tiempo de entrenamiento | Tiempo de inferencia |
| ------------- | -------: | -------: | -----: | ---------: | ----------------------: | -------------------: |
| Random Forest | 690,5600 | 439,0709 | 0,8811 | 148,0535 % |                0,1052 s |             0,0294 s |

Los mejores hiperparámetros encontrados mediante validación cruzada fueron:

* `n_estimators = 100`
* `max_depth = 20`
* `min_samples_split = 5`

Las variables más importantes fueron la temperatura, la sensación térmica, el año de observación y la humedad. El modelo presentó cierto grado de sobreajuste, pero mantuvo un desempeño superior a Ridge en el conjunto de prueba.

## Análisis no supervisado

PCA permitió conservar el 80,62 % de la varianza mediante ocho componentes principales. Posteriormente, K-Means identificó dos perfiles generales:

* **Cluster 0:** días más cálidos y demanda promedio aproximada de 5.603 arriendos.
* **Cluster 1:** días más fríos y demanda promedio aproximada de 3.453 arriendos.

El Silhouette Score fue de 0,2498, por lo que los grupos deben interpretarse como perfiles generales y no como segmentos completamente separados.

## Estructura del repositorio

* `day.csv`: dataset utilizado.
* `examen_bike_sharing.ipynb`: notebook ejecutado con el análisis completo.
* `comparacion_modelos.csv`: tabla comparativa de los modelos.
* `requirements.txt`: bibliotecas y versiones necesarias.
* `figures/`: gráficos generados durante el análisis.
* `README.md`: descripción general e instrucciones del proyecto.

## Reproducción del análisis

Clonar el repositorio:

```bash
git clone https://github.com/frachavez1990-prog/ML1_ExamenAplicado_Chavez_Francisco.git
cd ML1_ExamenAplicado_Chavez_Francisco
```

Crear y activar un entorno virtual en Windows:

```powershell
python -m venv .venv
.venv\Scripts\activate
```

Instalar las dependencias:

```powershell
pip install -r requirements.txt
```

Abrir el notebook `examen_bike_sharing.ipynb` en VS Code o Jupyter y ejecutar todas las celdas en orden.

## Video de presentación

**Enlace:** [Ver video de presentación](https://drive.google.com/file/d/1Qh8Vqkya4Ud2TzXBeAn4WNK0nrV69Lt-/view?usp=sharing)

## Declaración de uso de inteligencia artificial

Se utilizó ChatGPT como herramienta de apoyo para estructurar el flujo de trabajo, aclarar dudas, proponer y revisar fragmentos de código, contrastar la interpretación de los resultados y corregir errores de redacción en el notebook y el README. El autor ejecutó el código, comprobó los resultados obtenidos, realizó las interpretaciones iniciales y revisó las decisiones finales incorporadas en el trabajo.

## Autor

Francisco Chávez
