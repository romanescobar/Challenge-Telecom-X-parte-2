# Análisis y Predicción de la Evasión de Clientes (Churn) en Telecom X

Este repositorio contiene el análisis completo y el desarrollo de modelos predictivos para identificar y comprender los factores que influyen en la evasión de clientes (Churn) en una empresa de telecomunicaciones ficticia, "Telecom X". El objetivo es proporcionar insights accionables para estrategias de retención de clientes.

---

## 📄 Tabla de Contenidos

1.  [Descripción del Proyecto](#-descripción-del-proyecto)
2.  [Objetivos del Proyecto](#-objetivos-del-proyecto)
3.  [Conjunto de Datos](#-conjunto-de-datos)
4.  [Metodología](#-metodología)
5.  [Resultados y Modelos](#-resultados-y-modelos)
6.  [Factores Clave de Churn](#-factores-clave-de-churn)
7.  [Estrategias de Retención Propuestas](#-estrategias-de-retención-propuestas)
8.  [Tecnologías Utilizadas](#-tecnologías-utilizadas)
9. [Contacto](#-contacto)

---

## 🚀 Descripción del Proyecto

En el competitivo sector de las telecomunicaciones, la retención de clientes es un desafío crucial. Este proyecto aborda el problema del Churn (tasa de abandono de clientes) mediante el análisis de datos históricos y la creación de modelos de Machine Learning. El proceso incluye la limpieza de datos, el análisis exploratorio para descubrir patrones, la estandarización y balanceo de datos, el entrenamiento y evaluación de modelos, y la interpretación de los resultados para derivar recomendaciones estratégicas.

---

## 🎯 Objetivos del Proyecto

* Identificar los principales factores que influyen en la evasión de clientes.
* Desarrollar y evaluar modelos de clasificación que predigan la probabilidad de Churn de un cliente.
* Proporcionar insights accionables y recomendaciones estratégicas para mitigar la tasa de Churn.

---

## 📊 Conjunto de Datos

El análisis se basa en un conjunto de datos ficticio de clientes de telecomunicaciones, `datos_tratados.csv`. Este dataset contiene información sobre diversos atributos del cliente, incluyendo:

* **Información Demográfica:** Género, edad, si tienen pareja o dependientes.
* **Servicios Contratados:** Servicios de teléfono, internet (DSL, fibra óptica), seguridad online, backup online, protección de dispositivo, soporte técnico, streaming de TV y películas, múltiples líneas.
* **Información de Cuenta:** Duración del contrato (`tenure`), método de pago, facturación mensual, facturación total, tipo de contrato.
* **Variable Objetivo:** `Churn` (Sí/No) - indica si el cliente canceló el servicio.

---

## 🛠️ Metodología

El proceso de análisis y modelado siguió los siguientes pasos:

1.  **Limpieza y Preprocesamiento de Datos:**
    * Carga y verificación del dataset.
    * Eliminación de columnas irrelevantes.
    * Codificación de variables categóricas (One-Hot Encoding).
    * Manejo de valores nulos y duplicados.
    * Creación de nuevas características (`Cuentas_Diarias`, `Num_Services`).
    * Detección y tratamiento del desbalance de clases en la variable `Churn` (26.58% Churn).
    * Estandarización de variables numéricas (`StandardScaler`).
2.  **Análisis Exploratorio de Datos (EDA):**
    * Análisis de la distribución de `Churn`.
    * Visualización de la relación entre variables categóricas y `Churn`.
    * Análisis de correlación para identificar relaciones entre variables numéricas y con `Churn`.
    * Análisis dirigido de variables clave (`tenure`, `Charges.Monthly`, `Charges.Total`) vs. `Churn` utilizando boxplots y scatter plots.
3.  **Preparación para el Modelado:**
    * División del dataset en conjuntos de entrenamiento (80%) y prueba (20%) con estratificación para mantener la proporción de `Churn`.
    * Aplicación de **SMOTE** (Synthetic Minority Over-sampling Technique) al conjunto de entrenamiento para abordar el desbalance de clases, resultando en un set de entrenamiento balanceado (50/50 Churn/No Churn).
4.  **Creación y Entrenamiento de Modelos Predictivos:**
    * Se entrenaron dos modelos de clasificación:
        * **Regresión Logística:** Modelo lineal, sensible a la escala de datos (beneficiado por la estandarización previa).
        * **Random Forest Classifier:** Modelo basado en árboles, no sensible a la escala de datos.
5.  **Evaluación de Modelos:**
    * Se evaluó el rendimiento de ambos modelos en el conjunto de prueba (no balanceado) utilizando métricas clave para clasificación y desbalance de clases: Exactitud (Accuracy), Precisión, Recall, F1-score y Matriz de Confusión.
6.  **Análisis de Importancia de Variables:**
    * Para Regresión Logística: Análisis de los coeficientes del modelo.
    * Para Random Forest: Utilización de las `feature_importances_` del modelo.
7.  **Conclusiones y Recomendaciones:**
    * Síntesis de los hallazgos clave.
    * Propuesta de estrategias de retención basadas en los insights obtenidos.

---

## 📈 Resultados y Modelos

Después de la evaluación, el **Modelo de Regresión Logística** demostró un desempeño ligeramente superior en métricas clave para la detección de Churn:

| Métrica                  | Regresión Logística | Random Forest Classifier |
| :----------------------- | :------------------ | :----------------------- |
| **Exactitud (Accuracy)** | 0.7676              | 0.7740                   |
| **Precisión (Precision)**| 0.5449              | 0.5667                   |
| **Recall**               | **0.7620**          | 0.6364                   |
| **F1-score**             | **0.6355**          | 0.5995                   |

La **Regresión Logística** fue el modelo preferido debido a su **mayor `Recall` (0.7620)**, lo que indica una mejor capacidad para identificar a los clientes que realmente evaden (minimizando los Falsos Negativos), lo cual es crucial para la implementación de estrategias de retención proactivas. Su `F1-score` también fue superior, indicando un mejor balance general.

---

## 🔍 Factores Clave de Churn

El análisis de importancia de variables reveló los siguientes factores críticos que influyen en la evasión:

* **Antigüedad del Cliente (`tenure`):** El factor más influyente. Los clientes con poca antigüedad son significativamente más propensos a evadir.
* **Servicios Adicionales:** La presencia de servicios como **Soporte Técnico**, **Seguridad Online**, **Backup Online** y **Protección de Dispositivo** actúan como "factores de retención", disminuyendo la probabilidad de Churn.
* **Tipo de Contrato:** Los clientes con **contratos de dos años** tienen una probabilidad mucho menor de evadir.
* **Gasto Mensual (`Charges.Monthly`) y Número de Servicios (`Num_Services`):** Un mayor gasto mensual y un mayor número de servicios contratados están asociados con una mayor probabilidad de Churn. Esto podría indicar que una cartera de servicios excesivamente compleja o costosa puede ser un detonante.
* **Servicio de Fibra Óptica y Método de Pago Electrónico:** Se identificaron como factores asociados con una mayor propensión al Churn.

---

## 💡 Estrategias de Retención Propuestas

Basadas en los hallazgos del análisis, se recomiendan las siguientes estrategias:

1.  **Mejorar el Onboarding para Nuevos Clientes:** Implementar programas robustos en los primeros meses de servicio para clientes con baja `tenure` (alta probabilidad de Churn), ofreciendo soporte proactivo y encuestas de satisfacción.
2.  **Promover Servicios de Valor Añadido:** Incentivar la contratación de servicios como soporte técnico, seguridad y protección de dispositivos, ya que actúan como "anclas" de lealtad.
3.  **Fomentar Contratos a Largo Plazo:** Ofrecer incentivos para que los clientes elijan contratos de dos años, reduciendo la flexibilidad de cancelación.
4.  **Optimizar Ofertas y Precios:** Revisar las ofertas para clientes con alto gasto mensual y múltiples servicios, buscando simplificar o ajustar precios para evitar la sobrecarga percibida.
5.  **Monitoreo Dirigido:** Establecer seguimiento y campañas de retención específicas para clientes de fibra óptica y aquellos que usan pago electrónico, dado su mayor riesgo de Churn.
6.  **Sistema de Alerta Temprana:** Utilizar el modelo de Regresión Logística para identificar proactivamente a los clientes con alta probabilidad de Churn y permitir intervenciones personalizadas del equipo de retención.

---

## 💻 Tecnologías Utilizadas

* Python (3.x)
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Seaborn
* Imbalanced-learn (para SMOTE)

---

## 📞 Contacto

Para cualquier pregunta o sugerencia, no dudes en contactarme:

* **Tu Nombre:** Román Ignacio Escobar Pizarro
* **Email:** roman.escobar.p@gmail.com


---

**¡Gracias por visitar este repositorio!**
