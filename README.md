Análisis de Rendimiento Físico: Datos de Kaggle

Por Franco

Después de trabajar con métricas de redes sociales, decidí aplicar Data Analytics a mi área de especialización: el ejercicio y la salud. Utilicé un dataset de Kaggle con información de más de 13,000 personas para analizar cómo la edad y el género influyen en las capacidades físicas.

¿Qué busqué analizar?

Como estudiante de educacion fisica, mi objetivo fue verificar mediante datos la degradación de la fuerza explosiva y la resistencia muscular a lo largo de los años, utilizando métricas reales como el salto en largo, abdominales y fuerza de agarre.

Herramientas y Procesamiento

Google BigQuery (SQL): Para la limpieza, filtrado y agregación de datos.

Cloud Storage: Para el alojamiento de archivos CSV de gran volumen.

Kaggle: Fuente del dataset "Body Performance".

Consultas SQL Clave

En este proyecto apliqué lógica de segmentación (Bucketing) para agrupar las edades en rangos y poder extraer promedios significativos de rendimiento:

SQL
SELECT 
  CASE 
    WHEN age BETWEEN 20 AND 29 THEN '20-29'
    WHEN age BETWEEN 30 AND 39 THEN '30-39'
    WHEN age BETWEEN 40 AND 49 THEN '40-49'
    ELSE '50+' 
  END AS rango_etario,
  gender as genero,
  ROUND(AVG(gripForce), 2) as fuerza_agarre_media,
  ROUND(AVG(`sit-ups counts`), 2) as abdominales_media,
  ROUND(AVG(`broad jump_cm`), 2) as salto_explosivo_media
FROM `proyecto-franco-475201.kaggle_salud.rendimiento_fisico`
GROUP BY 1, 2
ORDER BY 1, 2

Conclusión del Análisis

Los datos muestran una caída más pronunciada en el salto explosivo que en la fuerza de agarre a medida que aumenta la edad. Esto tiene una explicación fisiológica clara (pérdida de fibras rápidas), y poder visualizarlo con SQL me permite fundamentar la teoría con evidencia estadística sólida.
