# Diagnóstico de marca empleadora con NLP

**Autor:** Alejandro Nortes del Rio-Hortega

Análisis de reseñas de Glassdoor para identificar fortalezas y áreas de mejora de **Deutsche Bank**, comparándolo con **J.P. Morgan, Barclays, Citi y HSBC**.

El objetivo es orientar las prioridades de Recursos Humanos mediante un análisis descriptivo de las valoraciones y los textos. No se busca predecir la salida de empleados.

## Datos

El proyecto utiliza el archivo `glassdoor_reviews_hr.parquet`, preparado por el profesor a partir de los datasets **Glassdoor Job Reviews 1 y 2**, de David Gauthier.

- **55.152 reseñas** de los cinco bancos para el análisis exploratorio.
- Periodo observado: **julio de 2018 a abril de 2023**, con años extremos parciales.
- Muestra para NLP: **2.000 reseñas por banco**, con reparto proporcional por año y semilla fija.
- Variables principales: empresa, fecha, situación laboral, antigüedad, rating, recomendación, pros y cons.

## Metodología

1. **Preparación y EDA:** revisión de nulos y duplicados, transformación de variables y comparación de ratings, recomendaciones y evolución temporal.
2. **Sentimiento con DistilBERT:** clasificación de pros y cons como control de calidad, con revisión manual de casos discordantes.
3. **Temas con BERTopic:** un modelo conjunto para los pros y otro para los cons de todos los bancos. Revisión y agrupación de temas en categorías comprensibles para RRHH.
4. **Comparación con competidores:** porcentajes por categoría, balance neto y diferencias frente a la media de los peers.
5. **Análisis complementario:** comparación entre empleados actuales y antiguos y evolución temporal de las categorías.
6. **Priorización:** matriz que combina el peso de cada categoría en los cons con su desventaja frente a los competidores.

**Balance neto:** porcentaje en pros − porcentaje en cons.  
**Gap:** balance de Deutsche Bank − balance medio de sus competidores, dando igual peso a cada banco.

## Principales hallazgos

- Deutsche Bank obtiene un **rating medio de 3,73 sobre 5**, aunque mejora de **3,40 en 2018 a 3,87 en 2023**.
- La **conciliación y carga de trabajo** destaca como fortaleza relativa frente a los competidores.
- **Compensación y beneficios** y **carrera y desarrollo** presentan las principales desventajas relativas.
- Estas desventajas no se traducen siempre en ratings inferiores. Los resultados orientan asuntos que investigar, sin demostrar causas de insatisfacción o salida.

## Recomendaciones para RRHH

- Revisar la competitividad de salarios y beneficios por puesto y mercado.
- Hacer más claros los criterios de promoción y las oportunidades de movilidad interna.
- Priorizar mejoras en herramientas de trabajo, validando las necesidades con los equipos afectados.

## Tecnologías

Python, pandas, NumPy, Matplotlib, Seaborn, Transformers, PyTorch, Sentence Transformers, BERTopic, UMAP y HDBSCAN.

## Ejecución

Se recomienda utilizar **Python 3.11** y un entorno virtual.

```bash
pip install -r requirements.txt
```

Coloca `glassdoor_reviews_hr.parquet` y `lista_con_sector.xlsx` en las rutas indicadas en el notebook. Selecciona el entorno correspondiente y ejecuta las celdas en orden.

La primera ejecución necesita conexión a Internet para descargar los modelos. El procesamiento puede tardar varios minutos en CPU.

## Limitaciones

Las reseñas son voluntarias, históricas y mezclan países, puestos y áreas, por lo que no representan necesariamente a toda la plantilla.

La clasificación temática es aproximada. En Deutsche Bank, alrededor del **51 % de los cons** queda sin tema asignado o contiene comentarios generales o mixtos. Estos textos se conservan en los denominadores para no inflar los porcentajes de las categorías interpretables.

Antes de tomar decisiones, conviene contrastar las conclusiones con encuestas internas y entrevistas de salida.

## Fuentes

- [Glassdoor Job Reviews](https://www.kaggle.com/datasets/davidgauthier/glassdoor-job-reviews)
- [Glassdoor Job Reviews 2](https://www.kaggle.com/datasets/davidgauthier/glassdoor-job-reviews-2)