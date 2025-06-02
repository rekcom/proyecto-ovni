# proyecto-ovni
🛸 Proyecto de Análisis de Avistamientos OVNI - Evaluación Big Data
Autor: Camilo Silva
Curso: Big Data
Evaluación parcial: 40%
Modalidad: Batch
Presentación: Sitio web GitHub Pages
🔍 1. Ingesta
El archivo de datos avistamientos.csv fue subido manualmente al servicio Cloud Storage de Google Cloud Platform.

Se creó un bucket llamado: nombre-alumno

Se cargó el archivo de manera directa en el bucket

🧹 2. Transformación y limpieza
Se utilizó Cloud Dataprep (Trifacta) para limpiar y preparar el dataset:

Se corrigió el nombre de la columna state/province, ya que no era compatible con BigQuery (state_province)

Se eliminaron filas con nulos en campos clave (como shape, state, date)

Se estandarizó texto en minúsculas y se filtraron datos inválidos

✅ Finalmente, los datos limpios se cargaron en una tabla de BigQuery:

Dataset: ovni

Tabla: avistamientos

🗃️ 3. Carga en BigQuery
Desde Dataprep se cargó el archivo limpio directamente en BigQuery.

Se verificó que la tabla tuviera datos válidos con la siguiente consulta:

sql
Copiar
Editar
SELECT * FROM `proyecto.ovni.avistamientos` LIMIT 10;

📊 4. Consultas SQL y Visualización
Las siguientes consultas fueron realizadas en BigQuery, y visualizadas en Looker Studio con gráficos vinculados:

🥧 Gráfico de Torta: 5 formas de objeto más vistas
sql
Copiar
Editar
SELECT shape, COUNT(*) AS cantidad
FROM `proyecto.ovni.avistamientos`
GROUP BY shape
ORDER BY cantidad DESC
LIMIT 5;

📅 Gráfico de Barras: Avistamientos por año
sql
Copiar
Editar
SELECT EXTRACT(YEAR FROM date) AS anio, COUNT(*) AS cantidad
FROM `proyecto.ovni.avistamientos`
GROUP BY anio
ORDER BY cantidad DESC;

🗺️ Mapa: Avistamientos por estado (EE.UU.)
sql
Copiar
Editar
SELECT state, COUNT(*) AS cantidad
FROM `proyecto.ovni.avistamientos`
WHERE country = 'us'
GROUP BY state
ORDER BY cantidad DESC;

🧾 Evidencia
El proceso fue documentado con capturas de pantalla de:

Subida del archivo a Cloud Storage

Proceso de limpieza en Dataprep

Tabla cargada en BigQuery

Consultas en SQL

Visualización en Looker Studio

Todos los recursos están disponibles en esta página y repositorio.
🌐 Sitio Web
Puedes revisar el sitio en:
👉 https://rekcom.github.io/proyecto-ovni/

✅ Conclusión
A lo largo de este trabajo se logró implementar exitosamente un flujo completo de procesamiento de datos en modalidad batch, utilizando herramientas del ecosistema de Google Cloud Platform. Desde la ingesta inicial del archivo CSV en Cloud Storage, pasando por la transformación y limpieza de datos con Cloud Dataprep, hasta su carga en BigQuery para análisis posteriores, se demostró el manejo práctico de una arquitectura moderna de procesamiento de datos.

Gracias a las consultas realizadas en SQL y la visualización mediante Looker Studio, fue posible generar insights claros a partir de los datos de avistamientos de OVNIs. Este proceso no solo permitió identificar patrones relevantes —como los estados con mayor número de reportes o las formas más comunes de los objetos observados— sino también evidenció la importancia de mantener un pipeline de datos limpio, bien estructurado y automatizable.

Finalmente, la presentación del trabajo en un sitio web estático con GitHub Pages permitió entregar los resultados de forma accesible, clara y visualmente ordenada, reforzando habilidades clave tanto en ciencia de datos como en comunicación efectiva de resultados.

