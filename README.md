# Predicción de Recompra de Clientes en Retail 🛒

## 1. Contexto de Negocio
Este proyecto se desarrolla desde la perspectiva del Data Scientist principal de una empresa de retail online. El objetivo principal es **identificar a los clientes con alta probabilidad de volver a comprar** en el establecimiento. 

Con los resultados de este modelo predictivo, el equipo de negocio podrá diseñar:
* **Acciones de fidelización** para clientes con alta probabilidad de compra.
* **Acciones de retención** para clientes con baja probabilidad de repetir su compra.

---

## 2. El Dataset
El modelo utiliza el conjunto de datos **Online Retail II**, que contiene las transacciones realizadas por un comercio minorista online con sede en el Reino Unido (sin tienda física) entre el `01/12/2009` y el `09/12/2011`. 

Las variables principales incluyen el número de factura, código de producto, descripción, cantidad, fecha de la transacción, precio unitario, ID del cliente y país de residencia.

---

## 3. Metodología Aplicada

El flujo de trabajo del proyecto en el notebook abarca las siguientes fases:

### 3.1. Limpieza de Datos y Análisis Exploratorio (EDA)
* Eliminación de registros duplicados y valores nulos (sin `Customer ID`).
* Filtrado de facturas de cancelación (códigos que empiezan por "C").
* Exclusión de cantidades y precios negativos o iguales a cero.
* Creación de la variable `Revenue` (Ingresos = Cantidad * Precio).

### 3.2. Ingeniería de Características (Modelo RFM)
Se dividió el dataset utilizando una fecha de corte temporal (los últimos 6 meses del dataset) para predecir el comportamiento futuro basándonos en datos históricos:
* **Recency:** Días transcurridos desde la última compra.
* **Frequency:** Número de compras distintas realizadas.
* **Monetary:** Gasto total acumulado por el cliente.
* **Target:** Variable binaria que indica si el cliente volvió a comprar en los últimos 6 meses (1 = Sí, 0 = No).

### 3.3. Modelado Predictivo
Se entrenaron y compararon múltiples algoritmos de clasificación supervisada:
* Regresión Logística
* Random Forest Classifier
* XGBoost

### 3.4. Optimización y Evaluación
* Se eliminaron outliers extremos utilizando el percentil 99 para las variables `Monetary` y `Frequency`.
* Se optimizaron los hiperparámetros del mejor algoritmo mediante `RandomizedSearchCV`.
* La evaluación del rendimiento se realizó utilizando la métrica **AUC (Área bajo la curva ROC)** y métricas de interpretabilidad (Feature Importance).

---

## 4. Resultados Clave
Tras el entrenamiento y la optimización, el modelo **Random Forest** demostró el mejor rendimiento con un **AUC de ~0.817**, logrando una excelente capacidad de discriminación entre clientes que recompran y los que no. Las variables de comportamiento RFM demostraron ser altamente predictivas.

---

## 5. Entregables del Proyecto
* `notebook_modelo.ipynb`: Jupyter Notebook con el código completo (EDA, limpieza, modelado y evaluación).
* `Presentacion_Negocio.pdf/pptx`: Presentación ejecutiva resumida (5 slides) con los insights, gráficas descriptivas, resultados del modelo y próximos pasos sugeridos para el equipo comercial.
