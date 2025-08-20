## Telecom X – Predicción de Cancelación (Churn)

## Propósito del Análisis

El objetivo principal de este proyecto es desarrollar modelos predictivos para identificar a los clientes de Telecom X con mayor probabilidad de cancelar sus servicios (churn). Al anticipar este comportamiento, la empresa puede implementar estrategias de retención dirigidas y personalizadas, minimizando la pérdida de clientes y optimizando sus recursos. El análisis se centra en la identificación de variables clave que influyen en la decisión de un cliente de cancelar su contrato.

## Estructura del Proyecto

El proyecto se organiza de la siguiente manera:

- **`TelecomX_parte2_Latam.ipynb`**: Cuaderno principal de Jupyter/Colab que contiene todo el código del análisis, desde la carga de datos hasta la evaluación de modelos.
- **`datos_tratados.csv`**: Archivo CSV que contiene el conjunto de datos utilizado para el modelado, con las transformaciones y limpieza realizadas en etapas previas.
- **`visualizaciones/` (Opcional)**: Carpeta que podría contener gráficos generados durante el Análisis Exploratorio de Datos (EDA) si se exportaron como archivos de imagen. (En este caso, los gráficos están incrustados en el cuaderno).

## Preparación de los Datos

La preparación de los datos fue una etapa crucial para asegurar la calidad y el formato adecuado para el modelado. Los pasos clave incluyeron:

1.  **Carga del Dataset**: Se cargó el archivo `datos_tratados.csv`.
2.  **Clasificación de Variables**: Las variables fueron identificadas como categóricas (`object`) y numéricas (`int64`, `float64`).
3.  **Tratamiento de Variables Categóricas**: Las variables categóricas con más de dos categorías y aquellas binarias fueron codificadas utilizando **One-Hot Encoding** para convertirlas en un formato numérico adecuado para los modelos. La columna 'genero' fue mapeada a valores numéricos (Male: 1, Female: 0). La columna 'ID' también fue tratada con One-Hot Encoding, aunque su relevancia predictiva individual es baja.
4.  **Eliminación de Columnas Irrelevantes o Desbalanceadas**: Se eliminaron columnas como 'ID' (irrelevante para el modelado predictivo general) y 'servicio_telefonico' (presentaba un alto desbalance en sus categorías, con más del 90% en una sola). También se identificaron otras columnas con desbalance (>70% en una categoría) como 'cancelo', 'mayor_de_65', y 'tiene_dependentes', pero se mantuvieron para el análisis y modelado (excepto 'cancelo' que es la variable objetivo).
5.  **Balanceo de Clases**: Dado el desbalance en la variable objetivo `cancelo` (hay significativamente más clientes que no cancelaron que los que sí lo hicieron), se aplicó la técnica **SMOTE (Synthetic Minority Over-sampling Technique)** para crear instancias sintéticas de la clase minoritaria y equilibrar las clases para el entrenamiento del modelo.
6.  **Separación en Conjuntos de Entrenamiento y Prueba**: Los datos balanceados (`x_over`, `y_over`) se dividieron en conjuntos de entrenamiento y prueba utilizando `train_test_split` para evaluar el rendimiento de los modelos en datos no vistos.

## Modelado Predictivo

Se entrenaron y evaluaron tres modelos de clasificación para predecir el churn:

-   **Dummy Classifier**: Un modelo de línea base simple que predice la clase mayoritaria. Sirve como punto de referencia para evaluar si los modelos más complejos aportan valor.
-   **Decision Tree Classifier**: Un modelo basado en árboles de decisión que permite interpretar la importancia de las variables.
-   **Random Forest Classifier**: Un modelo de conjunto (ensemble) que combina múltiples árboles de decisión para mejorar la robustez y precisión.

La justificación para elegir estos modelos radica en su interpretabilidad (Decision Tree), su buen rendimiento general (Random Forest) y la necesidad de establecer una línea base (Dummy) para una comparación significativa.

## Análisis Exploratorio de Datos (EDA) e Insights

Durante el EDA, se obtuvieron insights clave sobre la relación entre diversas variables y la cancelación de clientes. Algunos ejemplos de gráficos relevantes y sus insights incluyen:

-   **Distribución de cancelación por tiempo de contrato**: Un histograma que muestra que los clientes con menos meses de contrato (clientes nuevos) tienen una mayor frecuencia de cancelación.
-   **Distribución de Gasto Mensual por Estado de cancelación**: Un histograma que compara los gastos mensuales de clientes que cancelaron y los que no, indicando que aquellos con gastos mensuales más altos tienden a cancelar más.
-   **Tasa de Cancelación por Tipo de Contrato**: Un gráfico de barras que evidencia que los clientes con contratos "Month-to-month" tienen una tasa de cancelación significativamente mayor en comparación con los contratos de "One year" o "Two year".
-   **Distribución de Gasto Total por Estado de cancelación**: Similar al gasto mensual, este histograma muestra que clientes con gastos totales más bajos a lo largo de su permanencia son más propensos a cancelar.

Estos análisis exploratorios ayudaron a confirmar las correlaciones identificadas previamente y a entender visualmente el comportamiento de churn en relación con variables clave.

## Cómo Ejecutar el Cuaderno

Para ejecutar el cuaderno `TelecomX_parte2_Latam.ipynb`, sigue estos pasos:

1.  Abre el cuaderno en Google Colab o en un entorno Jupyter local.
2.  Asegúrate de tener instaladas las bibliotecas necesarias. Puedes instalarlas ejecutando el siguiente código en una celda:
