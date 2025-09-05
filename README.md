# 🚗 Modelo de Predicción de Precios de Vehículos 🚗

Este repositorio contiene un modelo de machine learning para predecir el precio de vehículos de segunda mano. El modelo utiliza un enfoque de regresión por cuantiles para no solo estimar el precio más probable (mediana), sino también para proporcionar un rango de precios (percentiles 10 y 90), ofreciendo una visión más completa de la valoración.

---

##  **Visión General del Proyecto**

El objetivo es proporcionar una herramienta robusta y precisa para la tasación de vehículos usados. A partir de características como la marca, el modelo, el año, el kilometraje y el tamaño del motor, el modelo predice un rango de precios de venta realista. Este enfoque es especialmente útil para:

* **Vendedores**: Para fijar precios competitivos.
* **Compradores**: Para evaluar si una oferta es justa.
* **Empresas del sector automotriz**: Para la gestión de inventario y la valoración de activos.

---

## 🛠️ **Detalles del Modelo**

* **Algoritmo**: Se utiliza un `GradientBoostingRegressor` de Scikit-learn, entrenado para predecir tres cuantiles diferentes:
    * **P10**: Un precio optimista para una venta rápida.
    * **P50**: La estimación de precio más probable (mediana).
    * **P90**: Un precio de venta inicial más alto.

* **Características Principales**: Las predicciones se basan en las siguientes características del vehículo:
    * Kilometraje (`Mileage`)
    * Año de fabricación (`Year of manufacture`)
    * Tamaño del motor (`Engine size`)
    * Antigüedad del vehículo (`Age`)
    * Modelo (`Model`)
    * Fabricante (`Manufacturer`)
    * Tipo de combustible (`Fuel type`)

* **Validación**: El modelo fue evaluado utilizando una estrategia de validación cruzada `GroupKFold` para garantizar que las predicciones sean generalizables a vehículos no vistos durante el entrenamiento, evitando el sobreajuste.

---

## 📈 **Rendimiento del Modelo**

El modelo ha demostrado un rendimiento sólido y es considerado apto para su despliegue en producción.

| Métrica                         | Valor Promedio (Validación Cruzada) | Interpretación                                                              |
| :------------------------------ | :---------------------------------: | :-------------------------------------------------------------------------- |
| **MAE (Error Absoluto Medio)** |               ~$1,174               | La predicción se desvía, en promedio, esta cantidad del precio real.      |
| **MAPE (Error % Absoluto Medio)** |               **~9.4%** | El error promedio es inferior al 10% del precio del vehículo, lo cual es un resultado excelente. |
| **Cobertura del Rango [P10-P90]** |                 ~80%                  | El rango de precios predicho contiene el precio real el 80% de las veces.   |

La importancia de las características, analizada mediante permutación, confirma que el **kilometraje** y la **antigüedad** son los predictores más fuertes, lo que se alinea con la lógica del mercado.



---

##  **Cómo Empezar**

Los artefactos del modelo se encuentran en:

1.  **Modelos Entrenados**:
    * `q10.pkl`: Modelo para el percentil 10.
    * `q50.pkl`: Modelo para el percentil 50 (mediana).
    * `q90.pkl`: Modelo para el percentil 90.

2.  **Reporte y Anomalías**:
    * `report.json`: Contiene las métricas de rendimiento detalladas del conjunto de prueba.
    * `anomalies_top.csv`: Un CSV con los vehículos que el modelo identificó como anómalos o con los mayores errores de predicción.
  
3. **Data set**:
   * `car_sales_data`: Mohsen Behdani en Kaggle https://www.kaggle.com/datasets/msnbehdani/mock-dataset-of-second-hand-car-sales?resource=download
     

