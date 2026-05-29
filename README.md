# Predicción de Recompra de Clientes en Retail 

## Contexto de Negocio
Este proyecto se desarrolla desde la perspectiva del Data Scientist principal de una empresa de retail online. El objetivo principal es **identificar a los clientes con alta probabilidad de volver a comprar** en el establecimiento. 

Con los resultados de este modelo predictivo, el equipo de negocio podrá diseñar:
* **Acciones de fidelización** para clientes con alta probabilidad de compra.
* **Acciones de retención** para clientes con baja probabilidad de repetir su compra.

---

## El Dataset
El modelo utiliza el conjunto de datos [**Online Retail II**](https://archive.ics.uci.edu/dataset/502/online+retail+ii) obtenido del **UCI Machine Learning Repository**. Este contiene las transacciones realizadas por un comercio minorista online con sede en el Reino Unido (sin tienda física) durante un período histórico de dos años. 

Las variables principales incluyen el número de factura, código de producto, descripción, cantidad, fecha de la transacción, precio unitario, ID del cliente y país de residencia.

---

## Metodología Aplicada

El flujo de trabajo del proyecto en el notebook abarca las siguientes fases:

### Limpieza de Datos y Análisis Exploratorio (EDA)
* Eliminación de registros duplicados y valores nulos (sin identificación del cliente).
* Filtrado de facturas de cancelación (códigos con indicador alfabético).
* Exclusión de cantidades y precios negativos o iguales a cero.
* Creación de la variable de ingresos totales por registro (Ingresos = Cantidad * Precio).

### Ingeniería de Características (Modelo RFM)
Se dividió el dataset utilizando una fecha de corte temporal basada en el segmento final del dataset para predecir el comportamiento futuro basándonos en datos históricos:
* **Recency:** Días transcurridos desde la última compra.
* **Frequency:** Número de compras distintas realizadas.
* **Monetary:** Gasto total acumulado por el cliente.
* **Target:** Variable binaria que indica si el cliente volvió a comprar en el período futuro evaluado (Afirmativo / Negativo).

### Modelado Predictivo
Se entrenaron y compararon múltiples algoritmos de clasificación supervisada:
* Regresión Logística
* Random Forest Classifier
* XGBoost

### Optimización y Evaluación
* Se eliminaron outliers extremos utilizando el percentil superior para las variables de gasto e ingresos.
* Se optimizaron los hiperparámetros del mejor algoritmo mediante una búsqueda aleatoria y validación cruzada.
* La evaluación del rendimiento se realizó utilizando la métrica **AUC (Área bajo la curva ROC)** y métricas de interpretabilidad (Importancia de las variables).

---

## Resultados Clave
Tras el entrenamiento y la optimización, el modelo **Random Forest** demostró el mejor rendimiento con un **AUC sobresaliente**, logrando una excelente capacidad de discriminación entre clientes que recompran y los que no. Las variables de comportamiento de la metodología empleada demostraron ser altamente predictivas.

---

## Referencias y Licencia

**Fuente de los Datos:**
* Chen, D. (Dos mil doce). Online Retail II [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5CG6D

**Licencia de Uso:**
Este dataset se utiliza y comparte bajo la licencia [Creative Commons Atribución Cuatro Punto Cero Internacional](https://creativecommons.org/licenses/by/4.0/deed.es).
