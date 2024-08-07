# Proyecto Smart Governance 

Smart Governance se refiere a la aplicación de tecnologías avanzadas y datos inteligentes para mejorar la eficiencia, transparencia y participación ciudadana en la gestión pública y toma de decisiones gubernamentales.

![](https://img.shields.io/github/stars/pandao/editor.md.svg) ![](https://img.shields.io/github/forks/pandao/editor.md.svg) ![](https://img.shields.io/github/tag/pandao/editor.md.svg) ![](https://img.shields.io/github/release/pandao/editor.md.svg) ![](https://img.shields.io/github/issues/pandao/editor.md.svg) ![](https://img.shields.io/bower/v/editor.md.svg)

## Tabla de Contenidos

- [1. Descripción del Dataset](#1-descripción-del-dataset)
  - [Origen de los datos](#origen-de-los-datos)
  - [Número de artículos](#número-de-artículos)

- [2. Pre-procesamiento](#2-pre-procesamiento)
  - [Combinación de BibTeX a CSV](#combinación-de-bibtex-a-csv)
  - [Unificación de Dataset](#unificación-de-dataset)
  - [Limpieza de datos](#limpieza-de-datos)
  - [Transformaciones aplicadas](#transformaciones-aplicadas)

- [3. Visualizaciones](#3-visualizaciones)
  - [Análisis Exploratorio de Datos (EDA)](#análisis-exploratorio-de-datos-eda)
  - [Frecuencia de palabras clave](#frecuencia-de-palabras-clave)

- [4. Modelos no supervisados empleados](#4-modelos-no-supervisados-empleados)
  - [Identificación de conceptos clave](#identificación-de-conceptos-clave)
  - [Agrupación por palabras clave](#agrupación-por-palabras-clave)

## 1. Descripción del Dataset
### Origen de los Datos
### 🔗 Links: <https://www.scopus.com/home.uri>
![](https://upload.wikimedia.org/wikipedia/commons/2/26/Scopus_logo.svg) 

### Número de artículos
- Se seleccionaron 2,851 documentos de Scopus, que incluyen artículos de investigación y conference papers. Los datos, recopilados entre 2020 y 2024, están todos en inglés y se concentran en el tema de smart governance en el contexto de ciudades inteligentes. Estos documentos proporcionan una visión amplia y actualizada sobre los avances tecnológicos y la aplicación de la smart governance.

### 🔗 Links: <https://www.sciencedirect.com/>
![](https://upload.wikimedia.org/wikipedia/commons/3/35/ScienceDirect_logo_2020.svg)

### Número de artículos
- Se descargaron 1,716 artículos de investigación, todos en inglés, que abarcan el período de 2020 a 2024. Estos artículos se enfocan en estudios detallados y análisis profundos sobre la implementación de tecnologías avanzadas en la gestión urbana, específicamente dentro del marco de la smart governance. Los datos de ScienceDirect se descargaron en formato BibTeX.

## 2. Pre-procesamiento
### Combinación de Bibtex a CSV
- Los datos fueron inicialmente descargados en formato BibTeX. Para facilitar su análisis, se realizó una conversión de este formato a CSV utilizando Google Colab.

    ```bash
    !pip install bibtexparser
    ```
    

- Luego ejecutamos el siguiente script

    ```bash
    import bibtexparser
    with open("/content/drive/MyDrive/SCIENCE_DIRECT/ScienceDirect_citations_1721933036744.bib") as bibtex_file:
        bib_database = bibtexparser.load(bibtex_file)
        
	df = pd.DataFrame(bib_database.entries)
	selection = df[['doi', 'number','title','keywords','abstract','year']]
	selection.to_csv('/content/science1.csv', index=False)
    ```
- Así procedemos con cada uno de los archivos BibTeX de ScienceDirect. Después de esto, para unificar todos los archivos en uno solo, ejecutamos el siguiente código:

  ```bash
  # Lista de rutas a los archivos CSV
  csv_files = [
    "/content/science1.csv",
    "/content/science2.csv",
    "/content/science3.csv",
    "/content/science4.csv",
    "/content/science5.csv",
    "/content/science6.csv",
    "/content/science7.csv",
    "/content/science8.csv",
    "/content/science9.csv",
    "/content/science10.csv",
    # Agrega aquí las rutas a los otros archivos CSV]
    # Lista para almacenar los DataFrames 
    dataframes = []
    # Leer cada archivo CSV y agregarlo a la lista de DataFrames
    for file in csv_files:
        df = pd.read_csv(file)
        dataframes.append(df)
    # Combinar todos los DataFrames en uno solo
    combined_df = pd.concat(dataframes, ignore_index=True)
    # Guardar el DataFrame combinado en un nuevo archivo CSV
    combined_df.to_csv('/content/science_combined.csv', index=False)
    ```
### Unificación de Dataset

### Limpieza de datos

### Transformaciones aplicadas

## 3. Visualizaciones
### Análisis Exploratorio
Tiene como objetivo comprender la estructura de los datos, identificar patrones, detectar anomalías y comprobar supuestos. Aquí hay algunos pasos y técnicas comunes involucrados:

### Número de publicaciones en Scopus por año relacionado a Smart governance
![1](https://github.com/user-attachments/assets/85896cda-8491-4d34-a443-a8d395ef52fe)

El gráfico muestra la evolución del número de publicaciones en Scopus relacionadas con "Smart governance" por año, desde 2020 hasta 2024. A continuación, se presenta un análisis detallado:

#### Año 2020:
- **Número de publicaciones:** 490 
- **Observación:** Este es el punto de partida del análisis. Se publicaron 490 documentos en Scopus sobre smart governance.

#### Año 2021:
- **Número de publicaciones:** 586 
**Observación:** Hubo un aumento significativo en las publicaciones, con un incremento de 96 publicaciones respecto al año anterior. Esto puede indicar un creciente interés y desarrollo en el área de smart governance.

#### Año 2022:
- **Número de publicaciones:** 675 
- **Observación:** El número de publicaciones continúa aumentando, alcanzando 675. Esto representa un incremento de 89 publicaciones con respecto al año 2021, lo cual sugiere una tendencia positiva y sostenida en la investigación sobre smart governance.

#### Año 2023:
- **Número de publicaciones:** 704 
- **Observación:** Se alcanza el punto máximo en el número de publicaciones, con 704 documentos. Este año marca el punto culminante del interés en smart governance en el período analizado, con un aumento de 29 publicaciones respecto al año anterior.

#### Año 2024:
- **Número de publicaciones:** 396 
- **Observación:** Hay una disminución drástica en el número de publicaciones, bajando a 396. Esto representa una caída de 308 publicaciones respecto al año 2023. Este descenso abrupto podría deberse a varios factores, como cambios en las prioridades de investigación, saturación del tema, o posibles dificultades en la recopilación de datos recientes.

#### Conclusión:
El gráfico muestra un crecimiento sostenido en el número de publicaciones sobre smart governance en Scopus desde 2020 hasta 2023, seguido de una caída significativa en 2024. Esta tendencia puede reflejar cambios en el interés académico, financiamiento de investigaciones, o nuevos desarrollos en el campo. Es importante investigar más a fondo las posibles causas detrás de esta disminución en 2024 para entender mejor el contexto y las dinámicas de la investigación en smart governance.

### Número de publicaciones en ScienceDirect por año relacionado a Smart governance
![2](https://github.com/user-attachments/assets/6df52177-6487-49a9-bbbe-3dd043cdeedc)
El gráfico muestra la evolución del número de publicaciones en ScienceDirect relacionadas con "Smart governance" por año, desde 2020 hasta 2025. A continuación, se presenta un análisis detallado:

#### Año 2020:
- **Número de publicaciones:** 111 
- **Observación:** Este es el punto de partida del análisis, con un número relativamente bajo de publicaciones.

#### Año 2021:
- **Número de publicaciones:** 168 
- **Cambio:** Aumento de 57 publicaciones (51.4% de incremento) 
- **Observación:** Se observa un crecimiento significativo, lo que podría indicar un aumento del interés en smart governance.

#### Año 2022:
- **Número de publicaciones:** 185
- **Cambio:** Aumento de 17 publicaciones (10.1% de incremento)
- **Observación:** El crecimiento continúa, aunque a un ritmo más moderado que el año anterior.

#### Año 2023:
- **Número de publicaciones:** 237 
- **Cambio:** Aumento de 52 publicaciones (28.1% de incremento)
- **Observación:** Se acelera nuevamente el crecimiento, indicando un interés sostenido y en aumento en el tema.

#### Año 2024:
- **Número de publicaciones:** 298 
- **Cambio:**  Aumento de 61 publicaciones (25.7% de incremento)
- **Observación:** Se alcanza el pico máximo de publicaciones, manteniendo un fuerte crecimiento.

#### Año 2025:
- **Número de publicaciones:** 1 
- **Cambio:** Disminución drástica de 297 publicaciones (99.7% de decremento) 
- **Observación:** Esta caída abrupta es inusual y requiere una explicación. 

#### Conclusión:
El gráfico muestra una tendencia general de crecimiento sostenido desde 2020 hasta 2024, con un aumento total del 168.5% en publicaciones sobre smart governance. Sin embargo, la caída dramática en 2025 rompe abruptamente esta tendencia y requiere una investigación más profunda para entender sus causas.

### Número total de Publicaciones por Fuente
![3](https://github.com/user-attachments/assets/f141cc86-0d94-47e0-8edc-32a08ac2477e)

El gráfico muestra la comparacion de barras entre el número de publicaciones y fuente entre Scopus y ScienceDirect:

#### Scopus:
- **Número total de publicaciones:*** 2851 
- **Observación:** Scopus es claramente la fuente dominante en este conjunto de datos.

#### ScienceDirect:
- **Número total de publicaciones:** 1000 
- **Observación:** ScienceDirect tiene un número significativo de publicaciones, pero considerablemente menor que Scopus.

#### Comparación:
- Scopus tiene 1851 publicaciones más que ScienceDirect.
- Las publicaciones en Scopus son 2.851 veces más numerosas que en ScienceDirect.
- Scopus representa aproximadamente el 74% del total de publicaciones entre estas dos fuentes, mientras que ScienceDirect representa el 26% restante.

#### Conclusión
Este gráfico proporciona una visión clara de la distribución de publicaciones entre estas dos importantes fuentes académicas, destacando la posición dominante de Scopus en este conjunto de datos específico.

### Nube de palabras
![4](https://github.com/user-attachments/assets/2b1c3562-64bb-4f20-b414-296a1e7569b3)

En estos gráficos muestra las palabras claves dentre Scopus y ScienceDirect


### Análisis Univariado
Este tipo de análisis se enfoca en resumir y visualizar los datos para entender mejor su distribución, centralidad, dispersión y otros aspectos importantes. A continuación, se presentan los aspectos clave y las técnicas comunes empleadas en el análisis univariado:

### Districión de documentos por año 
![5](https://github.com/user-attachments/assets/45f3faa2-2bbe-4477-b9a3-2e39a2a35036)

Este gráfico detalla los numeros de documentos que se han recolectado por cada año del 2020 hasta el 2024

#### Año 2020:
- **Número de documentos:** Aproximadamente 600 
- **Observación:** Punto de partida del análisis, con un número considerable de documentos.

#### Año 2021:
- **Número de documentos:** Alrededor de 750 
- **Cambio:** Aumento significativo respecto a 2020 <br><br>
- **Observación:** Indica un crecimiento notable en el interés o la producción de documentos sobre el tema.

#### Año 2022:
- **Número de documentos:** Cerca de 850 
- **Cambio:** Continúa el aumento, aunque a un ritmo menor que el año anterior 
- **Observación:** Sugiere un interés sostenido y creciente en el tema.

#### Año 2023:
- **Número de documentos:** Aproximadamente 950 
- **Cambio:** El pico más alto en el gráfico 
- **Observación:** Representa el año con mayor producción de documentos, indicando posiblemente el punto máximo de interés o actividad en el campo.

#### Año 2024:
- **Número de documentos:** Alrededor de 700 
- **Cambio:** Disminución significativa respecto a 2023 
- **Observación:** Indica una reducción en la producción de documentos, posiblemente debido a cambios en las tendencias de investigación o factores externos.

#### Tendencia general:
- Se observa un aumento constante desde 2020 hasta 2023.
- El año 2023 marca el pico de producción de documentos.
- Hay una disminución notable en 2024 y una caída dramática en 2025.

#### Conclusión:
El gráfico muestra una tendencia de crecimiento seguida por una disminución. El aumento hasta 2023 sugiere un interés creciente en el tema, mientras que la disminución posterior podría indicar una saturación del campo, cambios en las prioridades de investigación, o factores externos que afectan la producción de documentos. La caída en 2025 requiere una explicación adicional o verificación de datos.

### Distribución de Citaciones
![6](https://github.com/user-attachments/assets/25cf618c-3b9e-494a-ae2e-ed3acd94cd8b)

Este gráfico muestra la distribución de citaciones en una base de datos bibliográfica. 

#### Forma general:
- La distribución sigue una curva exponencial decreciente, típica de las distribuciones de citaciones en la literatura académica.

#### Pico inicial:
- Hay un pico muy alto cerca del origen (0 citaciones), que representa la mayor frecuencia.
- Esto indica que una gran cantidad de documentos reciben pocas o ninguna citación.

#### Decrecimiento rápido:
- La frecuencia disminuye drásticamente a medida que aumenta el número de citaciones.
- La caída es especialmente pronunciada entre 0 y 50 citaciones.

#### Cola larga:
- Después de aproximadamente 50 citaciones, la curva se aplana, formando una "cola larga".
- Esto sugiere que muy pocos documentos reciben un alto número de citaciones.

#### Conclusión
Este gráfico muestra una distribución de citaciones muy sesgada, donde la mayoría de los documentos reciben pocas citaciones, mientras que unos pocos alcanzan un alto impacto en términos de citas. Esta es una característica común en la literatura académica y científica.

### Análisis Bivariado
Ayuda a entender cómo dos variables interactúan entre sí, si existe una correlación o dependencia, y cómo una variable puede influir en la otra. 
### Relación entre Año de Publicaciones y Citaciones
![7](https://github.com/user-attachments/assets/a6153b2a-65e6-43cd-a47b-554183e683d8)

Este gráfico muestra la relación entre el año de publicación y el número de citaciones mediante diagramas de caja (box plots) entre los años 2020 a 2024.

#### 2020:
- Mayor rango intercuartílico, indicando mayor variabilidad en las citas. 
- La mediana (línea en la caja) es la más alta, alrededor de 5 citas.
- Presenta varios valores atípicos (outliers) por encima de 25 citas.

#### 2021:
- Rango intercuartílico ligeramente menor que 2020.
- La mediana es algo más baja que en 2020.
- También muestra valores atípicos por encima de 20 citas.

#### 2022:
- Continúa la tendencia de disminución en el rango intercuartílico y la mediana.
- Menos valores atípicos, pero algunos alcanzan cerca de 25 citas.

#### 2023:
- Rango intercuartílico significativamente menor.
- La mediana está cerca de 1 o 2 citas.
- Muestra varios valores atípicos, algunos llegando a 20 citas.

#### 2024:
- Representado solo por puntos, sugiriendo muy pocas citas en general.
- La mayoría de las publicaciones probablemente tienen 0 o 1 cita.
- Un valor atípico alcanza alrededor de 22 citas.

#### Conclusión 
Este gráfico ilustra claramente cómo el número de citas tiende a aumentar con el tiempo desde la publicación, con una notable variabilidad y algunos trabajos de alto impacto que se destacan como valores atípicos.

### Top 15 Términos Frecuentes
![image](https://github.com/user-attachments/assets/6aede9df-f4b5-43af-b3df-026d8459984e)

Este gráfico muestra los 15 términos más frecuentes en un conjunto de datos, probablemente relacionados con smart governance y ciudades inteligentes. 

#### Término:
- "Smart" es el término más utilizado, con una frecuencia cercana a 9000, esto sugiere que el concepto de "inteligencia" es central en los documentos analizados.
- "Governance" es el segundo término más frecuente, con alrededor de 4800 menciones, esto indica un fuerte enfoque en aspectos de gestión y administración.
- "Data" es el tercer término más común, seguido de cerca por "technology" y "digital" más abajo en la lista, esto refleja la importancia de los datos y la tecnología en el contexto de smart governance.
- "City" y "cities" aparecen en cuarta y quinta posición respectivamente.
- "Urban" también está presente, lo que refuerza el enfoque en entornos urbanos.
- "Research", "study", y "development" están presentes, indicando un fuerte componente de investigación en el campo.
- "Management" y "energy" aparecen en la lista, sugiriendo la importancia de la gestión de recursos y la energía en el contexto de ciudades inteligentes.
- "Paper" podría referirse a documentos de investigación.
- "Technologies" en plural complementa la presencia de "technology" singular.
#### Conclusión
En conclusión, este gráfico proporciona una visión general de los temas clave en el campo de smart governance y ciudades inteligentes, destacando la importancia de la tecnología, los datos, la gestión urbana y la investigación en este ámbito.

### Intertopic distance map
![image](https://github.com/user-attachments/assets/6a6fa4ef-784c-4b48-82f4-77329403a0bc)

El Tópico 1 representa el enfoque más significativo dentro de la base de datos analizada, abarcando el 38.4% de los tokens, los términos clave como "smart", "city", "governance", "urban", y "data" sugieren un fuerte énfasis en la aplicación de tecnologías inteligentes y el uso de datos para mejorar la gobernanza urbana. Hay un claro enfoque en la investigación y el desarrollo en este campo, con una atención particular a la sostenibilidad y la energía.

![image](https://github.com/user-attachments/assets/32608ff1-5984-4e9e-a11f-ccab46044253)

El Tópico 2 parece enfocarse más en los aspectos tecnológicos y de datos de las ciudades inteligentes que representa el 31.4% de los tokens, con un énfasis particular en blockchain y energía, mientras que el enfoque en gobernanza ha disminuido en comparación con el Tópico 1 anterior, los términos clave como "blockchain", "digital", y "technology" tienen mayor prominencia, en cambio "Energy" y "development" parecen tener más peso en este tópico.

![image](https://github.com/user-attachments/assets/a91a81dc-346c-4a1e-a1ce-43340562a49c)

El Tópico 3 parece enfocarse más en los aspectos de gobernanza y gestión de las ciudades inteligentes, con un equilibrio entre los elementos tecnológicos y los aspectos sociales y urbanos que representa el 30.1% de los tokens, los término claves como "Smart" sigue siendo el término más frecuente, "Governance" ha vuelto a subir a la segunda posición, similar, en cambio "Research", "cities", y "city" completan los cinco términos más relevantes, "Management" aparece como un término importante, ocupando la sexta posición, "Study" y "urban" también tienen una relevancia notable en este tópico.

## 4. Modelos no supervisados empleados

### Identificación de conceptos clave
### Top 40 palabras más frecuentes
![image](https://github.com/user-attachments/assets/6684580e-26d4-4a90-9898-075eee77cf17)

### Distribución de Documentos en Tópicos - LDA
![image](https://github.com/user-attachments/assets/5b66e379-d27a-4e9a-9873-ea9290406d7f)

### Distribución de Documentos en Tópicos - NMF
![image](https://github.com/user-attachments/assets/0c292af9-8278-41ae-a5c5-8a778106a0fb)


### Agrupación por palabras clave
### Nube de Palabras - LDA
![image](https://github.com/user-attachments/assets/30921fc2-d9d9-4422-aa71-9e8b14adac7a)

### Nube de palabras - NMF 
![image](https://github.com/user-attachments/assets/32bee730-6db1-40d5-b3ce-bcb61af35042)





