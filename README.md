# Jump2Digital Hackathon

## Introducción

Se han utilizado los dataset de alquileres y el de ruido, al considerarse que este podía ofrecer mayor relación con la información de los alquileres.

Las variables seleccionadas del dataset de alquileres fueron: trimestre, código de distrito, código de barrio y precio. Antes de la eliminación del resto de variables, se empleo las 2 categorías te tipo de alquiler para crear las variables precio/m2 y superficie (quedando precio como columna para el precio total de la vivienda).

El dataset de ruido se transformó completamente, ya que se analizó que conceptos y rangos de ruido ofrecían más útilidad. Analizando únicamente el dataset de ruido se vio que el concepto TOTAL para las diferentes franjas horarias era el que aportaba más información, por lo que se crearon un dataset con 'Codi_Districte', 'Codi_Barri' y las 36 columnas para cada combinación de 'Concepte' y 'Rang_soroll' seleccionadas (donde se almacenarán los valores de 'Valor' para dicha combinación). Posteriormente, tras analizar la correlación con las columnas de precio de alquileres y las propias columnas de ruido usando  el dataset combinado, se redujo las variables a sólo: 'TOTAL_DEN_65-70 dB', 'TOTAL_DEN_70-75 dB', 'TOTAL_N_60-65 dB' y 'TOTAL_N_65-70 dB'.

El dataset resultante tenía, por tanto, las siguientes columnas: Trimestre, Codi_Districte, Codi_Barri, Preu, Preu/m2, Superficie, TOTAL_DEN_65-70 dB, TOTAL_DEN_70-75 dB, TOTAL_N_60-65 dB y TOTAL_N_65-70 dB.

## Depuración de los datos

Se eliminaron 5 distritos que contenían missing values en los datos de precio y se logró imputar el preción de un registro faltante para un barrio mediante KNNImputer. Por otra parte, se evaluó los outliers y se consideró mantener los outliers al no deberse a errores en la introducción de los datos y poder conllevar una elevada pérdida de información. Finalmente, durante el proceso de clusterización de los barrios, se excluyeron las columnas de trimestre y código y se aplicó una estandarización de los valores del resto de columnas, antes de proceder al cálculo de PCA y la posterior clusterización.

## Resultados obtenidos

En el EDA detallado en el notebook se ha dió una descripción de la evolución a lo largo de los trimestres del precio total, por metro cuadrado y superficie para los distintos distritos y barrios. En dicho EDA se señalaba los distritos y barrios con viviendas más caras, baratas, grandes y pequeñas, junto a un analisis de la evolución de los precios en cada trimestre (siendo esta generalmente alzista). En el EDA del dataset de ruido se observó cuales eran los distritos más bulliciosos y tranquilos, así como que como era de esperar la franja nocturna era la más silenciosa.

Durante el proceso de clusterización se detectaron 3 clusters, no muy diferenciables del resto tal como mostraba su bajo coeficiente de Silhouette. Tras analizar los SHAP values de cada cluster se vio que el primer cluster, Cluster 0, se enfoca en aquellas viviendas con un precio promedio y con registros altos de ruido elevado. Por su parte, el segundo cluster, Cluster 1, se enfoca en aquellas viviendas baratas y escasos registros de ruido elevado. Finalmente, el tercer cluster, Cluster 2, se enfoca en viviendas muy caras y de grandes superficies.

## Conclusiones

La información quizás más interesante ha sido la extraida del dataset base, el de alquileres. Proporcionandonos información de los diferentes precios y superficies de las viviendas por distrito y barrio. Por el contrario, el impacto del ruido en el dataset de alquiler fue más bajo del esperado, así como la clusterización realizada se basa unos datos poco separables, lo que le resta cierta solidez. Finalmente, la columna Trimestre quedo al final en desuso, ya que la información a lo largo del tiempo era demasiado escasa para crear un modelo predictivo para determinar el valor de las viviendas a futuro por zona.
