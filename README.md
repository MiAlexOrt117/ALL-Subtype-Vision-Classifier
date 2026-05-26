# Detección y subtipificación de leucemia linfoblástica aguda usando técnicas de inteligencia artificial

Proyecto universitario de Inteligencia Artificial aplicado a imágenes microscópicas de frotis de sangre periférica para detección y subtipificación de leucemia linfoblástica aguda (ALL).

El entregable principal es:

`Notebook_Final_Unificado_Leucemia_IA.ipynb`

Este notebook integra los cuatro notebooks originales del proyecto en una versión final, limpia, explicativa y defendible académicamente.

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

La DNN final usa variables extraídas previamente; no usa CNN, transfer learning ni autoencoders.

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

No se inventaron métricas; los valores provienen de los CSVs y salidas revisadas de los notebooks.

| Enfoque | Mejor resultado reportado |
|---|---|
| Features finales | 713 variables después de eliminar 41 constantes |
| Clasificación clásica | SVM Linear, accuracy 0.9985, F1 macro 0.9981 |
| Validación cruzada Top 100 | SVM RBF, F1 macro medio 0.9900 |
| DNN densa con handcrafted features | Accuracy 0.9939, F1 macro 0.9930 |
| PCA + clasificador | SVM RBF + PCA 180 componentes, F1 macro 0.9943 |
| Clustering | Agglomerative Ward K=4, ARI 0.6833, NMI 0.7517 |

Los métodos supervisados fueron claramente más adecuados para clasificación final que los métodos no supervisados. El aprendizaje no supervisado aportó una lectura exploratoria de la estructura latente, pero no reemplaza a los clasificadores entrenados con etiquetas.

## Estructura del repositorio

```text
.
├── EDA_leucemia_unificado_Colab.ipynb
├── Notebook_Maestro_Leucemia_Clasificacion (1).ipynb
├── Notebook_Maestro_DNN_Leucemia_Parte3 (1).ipynb
├── Parte4_NoSupervisado_Leucemia.ipynb
├── Notebook_Final_Unificado_Leucemia_IA.ipynb
├── leukemia_handcrafted_features (1).csv
├── leukemia_feature_ranking (1).csv
├── model_comparison_results (1).csv
├── requirements.txt
├── outputs/
│   └── final_notebook/
│       ├── cm_svm_linear.png
│       ├── dnn_features_accuracy_curve.png
│       ├── dnn_features_confusion_matrix.png
│       └── ...
└── unsupervised_outputs/
    ├── clustering_comparison.csv
    ├── final_comparison_all_models.csv
    ├── pca_2d_visualization.png
    ├── pca_3d_visualization.png
    └── ...
```

Los sufijos como `(1)` se conservan porque así aparecen los archivos en esta copia local. El notebook final los detecta automáticamente mediante búsqueda robusta.

## Cómo ejecutar

1. Abrir `Notebook_Final_Unificado_Leucemia_IA.ipynb` en Jupyter o Google Colab.
2. Instalar dependencias si es necesario:

```bash
pip install -r requirements.txt
```

3. Verificar que los CSVs de features y resultados estén en la carpeta del proyecto.
4. Ejecutar las celdas en orden.
5. Si se desea reentrenar la DNN, cambiar `RUN_DNN_TRAINING = True` dentro del notebook.

## Conclusión

Las características handcrafted contienen información suficiente para construir clasificadores de alto desempeño sobre este dataset. SVM y Random Forest fueron especialmente competitivos; la DNN densa fue útil como comparación neuronal sin usar imágenes crudas. En una aplicación real, el reto principal sería validar externamente con imágenes de otros hospitales, microscopios, cámaras y condiciones de tinción.
