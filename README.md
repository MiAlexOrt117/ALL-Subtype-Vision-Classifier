
<img width="1024" height="682" alt="ProyectoIA" src="https://github.com/user-attachments/assets/6b785b24-702c-48d9-9f09-4081dd63f805" />

# Detección y subtipificación de leucemia linfoblástica aguda usando técnicas de inteligencia artificial

Proyecto universitario de Inteligencia Artificial aplicado a imágenes microscópicas de frotis de sangre periférica para detección y subtipificación de leucemia linfoblástica aguda (ALL).

El entregable principal es:

`Notebook_Final_Unificado_Leucemia_IA.ipynb`

Este notebook integra los cuatro notebooks originales del proyecto en una versión final, limpia, explicativa y defendible académicamente. La versión actual **no carga CSVs generados previamente**: descarga el dataset desde Kaggle y recalcula las features y resultados durante la ejecución.

## Dataset

- Nombre: **Acute Lymphoblastic Leukemia (ALL) image dataset**
- Fuente: [Kaggle - mehradaria/leukemia](https://www.kaggle.com/datasets/mehradaria/leukemia/data?select=Segmented)
- Repositorio asociado: [MehradAria/ALL-Subtype-Classification](https://github.com/MehradAria/ALL-Subtype-Classification)
- Paper asociado: *A Fast and Efficient CNN Model for B-ALL Diagnosis and its Subtypes Classification using Peripheral Blood Smear Images*
- Tipo de datos: imágenes microscópicas de células de frotis sanguíneo, con versiones originales y segmentadas.
- Clases: `Benign`, `Early`, `Pre`, `Pro`.

En los archivos generados del proyecto se registran **3256 muestras**:

| Clase | Imágenes |
|---|---:|
| Benign | 504 |
| Early | 985 |
| Pre | 963 |
| Pro | 804 |

El diagnóstico definitivo de ALL no depende solo de imágenes; requiere integración clínica y pruebas como citometría de flujo. Este proyecto se plantea como apoyo computacional, no como reemplazo diagnóstico.

## Metodología

El pipeline final está organizado así:

1. Exploración del dataset y distribución de clases.
2. Extracción de características manuales de color, intensidad, textura, bordes, frecuencia y morfología.
3. Limpieza de variables, eliminación de constantes y ranking estadístico.
4. Clasificación supervisada clásica.
5. Red neuronal profunda densa usando features handcrafted.
6. Aprendizaje no supervisado con PCA, K-Means, DBSCAN y clustering jerárquico.
7. Comparación global y conclusiones.

La DNN final usa variables extraídas en la misma ejecución; no usa CNN, transfer learning ni autoencoders.

## Modelos usados

- Gaussian Naive Bayes
- Decision Tree
- Random Forest
- SVM lineal
- SVM RBF
- SVM polinomial
- KNN
- Logistic Regression
- DNN densa
- K-Means
- DBSCAN
- Clustering jerárquico aglomerativo

## Resultados principales

Estos son resultados de referencia obtenidos en ejecuciones previas del proyecto. Al ejecutar el notebook desde Kaggle, las métricas se recalculan desde cero y pueden variar levemente por versiones de librerías o entorno.

| Enfoque | Mejor resultado reportado |
|---|---|
| Features finales | 713 variables después de eliminar 41 constantes |
| Clasificación clásica | SVM Linear, accuracy 0.9985, F1 macro 0.9981 |
| Validación cruzada Top 100 | SVM RBF, F1 macro medio 0.9900 |
| DNN densa con handcrafted features | Accuracy 0.9939, F1 macro 0.9930 |
| PCA + clasificador | SVM RBF + PCA 180 componentes, F1 macro 0.9943 |
| Clustering | Agglomerative Ward K=4, ARI 0.6833, NMI 0.7517 |

Los métodos supervisados fueron claramente más adecuados para clasificación final que los métodos no supervisados. El aprendizaje no supervisado aportó una lectura exploratoria de la estructura latente, pero no reemplaza a los clasificadores entrenados con etiquetas.

Los archivos CSV con sufijo `(1)` quedan como resultados históricos del trabajo previo. El notebook final actual no depende de ellos.

## Cómo ejecutar

1. Abrir `Notebook_Final_Unificado_Leucemia_IA.ipynb` en Jupyter o Google Colab.
2. Instalar dependencias si es necesario:

```bash
pip install -r requirements.txt
```

3. Ejecutar las celdas en orden. El notebook descargará el dataset con `kagglehub.dataset_download("mehradaria/leukemia")`.
4. Si se desea una prueba rápida, cambiar `USE_SUBSET = True` al inicio del notebook.
5. Los resultados generados se guardan en `outputs/kaggle_run/`.

## Conclusión

Las características handcrafted contienen información suficiente para construir clasificadores de alto desempeño sobre este dataset. SVM y Random Forest fueron especialmente competitivos; la DNN densa fue útil como comparación neuronal sin usar imágenes crudas. En una aplicación real, el reto principal sería validar externamente con imágenes de otros hospitales, microscopios, cámaras y condiciones de tinción.

VIDEO: https://youtu.be/ylwaWIf1Zh4
PRESENTACIÓN: https://canva.link/jlrr52hazdr8pue
