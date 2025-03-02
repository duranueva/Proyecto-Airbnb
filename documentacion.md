# Documentación: Analisis y Dashboard de Airbnb en Ciudad de México

<!-- ![](/img/img_1.png) -->

<p align="center">
  <img src="/img/img_1.png" alt="Description" width="1000">
</p>

Jean Durán Villanueva. Febrero 2024.


# Resumen
El siguiente documento detalla el analisis de datos y dashboard de Airbnb en Ciudad de México. Muestra el procesamiento, limpieza, analisis y despliegue de los datos más relevantes de las propiedades Airbnb en Ciudad de México. Para ello se utilizaron herramientas como Python (Notebooks), SQL, Excel y Power BI. El proposito es explorar la distribución de los datos, que pueden ayudar a observar los patrones más significativos en las  locaciones, precios, tipos de propiedad. Util por ejemplo, para un sector inmobiliario interesado en ingresar a este mercado.

# Introducción

**Contexto y Motivación:** Al ser el sector turistico e inmobiliario tan grande en Ciudad de México, decidí generar un analisis sobre los datos de Airbnb, la cual es la opción más popular en este sector. Por ello, un analisis de estos datos puede ser una gran oportunidad para demostrar mis capacidades en esta area de la computación y la industria.

**Objetivos del Proyecto:** Con este proyecto, pretendo identificar las tendencias que se encuentran en los datos, como las demarcaciones con el mayor numero de propiedades y su distribución geografica así como estos se relacionan con los precios.


# Descripción de los Datos

**Nota:** Los precios se encuentran siempre en la moneda MXN, aunque no se mencione explicitamente.

**Fuente de los Datos:**  Obtuve la información del sitio [Inside Airbnb](https://insideairbnb.com ). Existen diferentes formatos e información para una misma región, pero me decidí por una en especifico, el archivo `listing.csv` que muestra un listado de la información y metricas de las propiedades de Airbnb en la ciudad. Dado el formato, decidí utilizar Notebooks de Google Colab para procesar los datos con Python, dado la practicidad y la cómoda visualización de este proceso con la herramienta de Google. La información corresponde a Diciembre 2024.

**Formato, Volumen:** Para el Dataset, utilicé la librería Pandas para convertir los datos en un DataFrame y poder manipularlos de manera sencilla y eficiente. Se tratan de poco más de 26 mil registros. Entre los datos más relvantes, se encuentran:
- Precio por noche
- Ubicacion exacta (latitud, longitud)
- Nombre del Host
- Tipo de habitacion (Habitacion privada, habitacion compartida, Departamento completo)

![](/img/img_2_1.jpg)


**Extracción de Datos:** Una manera sencilla de poder extraer los datos es tomar el archivo directamente de internet, utilizando la librería `requests`. Pero al no tener garantías de obtener el mismo archivo utilizado para este analisis en el futuro (y poder reproducir los mismos resultados mencionados aquí), decidí descargarlo y cargarlo en el repositorio. El link se encuentra en la ultima sección de este documento.

 




# Metodología y Herramientas Utilizadas

**Entorno de Trabajo:** Utilicé un Notebook de Google Colab con Python, lo que facilita la reproducibilidad del análisis. En el, las librerias pandas y sqlite3. Hice uso de SQL para hacer consultas sobre los datos. Convertí los datos a un formato Excel para poder utilizar los datos en Power BI y desplegarlos en un dashboard interactivo. 
## **Procesamiento de Datos:**
**Limpieza y Preprocesamiento:**  Borré columnas sin valores como `license` y `neighbourhood_group ` que no aportaban al analisis. 

Creé una base de datos para almacenarlos y hacer consultas sobre estos. 
![](/img/img_3.jpg)

Convertí los valores NaN en NULL para ser procesados por la base de datos que creé. Además de procesar las cadenas con apostrofes ` ' ` simples, ya que la sintaxis de SQL detecta una comilla simple como el inicio o fin de una cadena, remplazandolo por una doble comilla simple `''`. Utilicé la librería `sqlite3` porque permite generar una base de datos por la practicidad de utilizar una  herramienta dentro de Colab. 
![](/img/img_4.jpg)
![](/img/img_5.jpg)


## **Análisis Exploratorio:** 
- Investigue el numero de registros existentes: 26 mil.
![](/img/img_6_1.jpg)
- Encontré además que la forma en que dividen los vecindarios o `neighbourhood` se refiere a las 16 alcaldías que conforman Ciudad de México. Además de conocer cuales el numero de propiedades registradas en cada una de estas. Encontré los distintos tipos de estancias que se manejan.
![](/img/img_7.jpg)
- Identifiqué el tipo de estancias que maneja Airbnb, al menos en la ciudad, además de la cantidad de cada una de estas.
![](/img/img_8.jpg)
- Investigué el número de host que existen (12 mil), el cual es menor al numero de instancias (26 mil), lo cual nos sugiere que existe un gran número de host manejando más de una misma estancia. 
![](/img/img_9.jpg)
- Lo anterior me llevó a buscar los hosts con mayores estancias. Los números me impactaron, pues es imporbable que una misma persona o un equipo pequeño pueda manejar más de 200 estancias como lo es "Bluegorund". Indagando un poco más descubro que existen empresas dedicadas a la renta de inmuebles por medio de estas aplicaciones. Es decir, todo una industria dedicada a trabajar bajo el esquema de Airbnb. Y aunque el modus operandi es distinto entre una compañía y otra, hay algunas que manejan desde la compra de un inmueble hasta la contstrucción y manejo de edificios operando completamente bajo este esquema de estancias cortas. 
![](/img/img_10.jpg)
- Ya con el dashboard, descubrí que en promedio predominan (en un 99%) como tipo de estancia los inmuebles completos (departamento o casa), seguido de habitacion privada. 
![](/img/img_11.png)
- Descubrí que el precio promedio por noche en la ciudad es de \$1900 y que los precios varían desorbitadamente desde el mínimo de \$116 por noche, hasta los \$870 mil. Esto debido a que en Airbnb es posible rentar cualquier tipo de inmueble: Desde una habitación compartida hasta un castillo (que existen este tipo en la ciudad).
![](/img/img_12.png)
- Analicé que existe una muy probable correlación entré el porcentaje de inmuebles respecto al 100% de estos y su precio por noche promedio. Tal es así que Cuahtémoc con el 46% de los inmuebles tiene un precio por noche promedio de \$2,300 y Tláhuac con el 0.2%, tiene un precio por noche promedio de \$387.
![](/img/img_13.png)
![](/img/img_14.png)


#  Visualización y Dashboard:
![](/img/img_26.png)

- **Obtención de datos:** Por medio de pandas, convertí el DataFrame previamente limpiado a un archivo Excel (.xlsx), pues hace mucho más sencillo la carga de datos a PowerBI desde una tabla de este tipo de archivos.

- **Slicer de Demarcaciones:** Me parecía que los datos más relevantes a resaltar son las zonas o Alcaldías, pues es muy evidente el cambio de precios y número de estancias entre una y otra, además de ser una manera sencilla de organizar la información.
![](/img/img_15.png)

- **Rango de precios:** Además, el rango de precios es muy importante para filtrar zonas de oportunidad, por lo que fue otro elemento clave en el dashboard.
![](/img/img_16.png)

- **Mapa de locaciones:** Por medio de los valores latitud y longitud fue posible encontrar las puntos exactos donde se ubican las propiedades.
![](/img/img_17.png)

- **Mapa de Alcaldías:** Me parecía esencial poder identificar tambíen la demarcación completa, reconociendo sus limites, teniendo así una visualización aumentada de las zonas especificas de cada alcaldía que contaban con estancias Airbnb. Para ello, me guié del valor `neighbourhood` y la creación de una nueva columna tomando ese valor y enriqueciendolo con "Alcaldía `neighbourhood`, Ciudad de México, México" (para que el gráfico del Mapa pudiera identificarlas de manera correcta). Sin embargo, tuve problemas para que se puedieran idenfiticar todas las demarcaciones, aunque lo considero un detalle menor pero a la vez importante notarlo. ![](/img/img_18.png)

Así lucen juntos.

![](/img/img_19.png)

- **Tarjetas:** Esta se actualizan dependiendo las Alcaldías, tipo de estancia o el rango de precio que se seleccionen. Pueden seleccionarse una o más de estas al mismo tiempo para filtrar la información (por medio de click + Shift).
	- Propiedades: Muestra el número de estancias según los filtros aplicados. Si no se seleccionada, se muestra el total%.
	- Porcentaje seleccionado: Muestra el porcentaje de estancias según los filtros aplicados. Si no se seleccionan elementos, se muestra el 100%.
	- Precio promedio: Muestra el precio promedio de las estancias según los filtros aplicados. Si no se seleccionan elementos, se muestra el promedio de todas las estancias.
![](/img/img_20.png)

Digamos que queremos saber el precio promedio de las habitaciones privadas en la Alcaldía Cuauhtemoc, pues seleccionamos ambas (tanto la Alcaldía Cuauhtemoc como las habitaciones privadas de las graficas pie chart) y obtenemos que el precio promedio es \$1,200
![](/img/img_21.png)

- **Grafico distribucion de precios:** Cómo todos los dashboards, este se actualiza dependiendo los filtros aplicados. En el **eje x** se encuentran los `precios`, y en el **eje y** se encuentra COUNT(Price), que refleja `la frecuencia de los precios`, es decir, que tanto se repite un mismo precio.
![](/img/img_22.png)

- **Grafico Pie Chart:**
    De igual forma, se actualiza dependiendo los filtros aplicados.
	- **Alcaldías**: Muestra el porcentaje y número de estancias que tiene cada una de las alcaldías.
    ![](/img/img_23.png)
	- **Tipo de estancia**: Muestra el porcentaje y numero de estancias. 
    ![](/img/img24.png)

# Resultados y Análisis

## Hallazgos Clave:

- El 99% de las estancias se concentran en Departamento/Casa (66%) y habitación privada (33%).
![](/img/img_8.jpg)
![](/img/img_27.png)

- Existen empresas dedicadas a rentar por medio de Airbnb, la empresa con mayor número de estancias es Blueground, con 238.
![](/img/img_10.jpg)

- 3 Alcaldías concentran casi el 75% de las estancias de la ciudad:
	- Cuautémoc con 46.1%
	- Miguel hidalgo con 17.1%
	- Benito Juarez con 11.6%
    ![](/img/img_25.png)
    
- El precio por noche promedio es de \$1,900. ![](/img/img_29.png)

	- Encontramos una posible correlación entre el numero de estancias respecto a su precio por noche. Mientras se concentren más estancias en una Alacaldía, los precios incrementan. Dabamos como ejemplo Cuauhtémoc y Tlahuac. Con precios promedio de \$2,300 y \$387 respectivamente. ![](/img/img_13.png) ![](/img/img_14.png)

	- Los precios van desde los \$116 hasta los \$800 mil, pues Airbnb permite rentar desde habitaciones compartidas hasta salones de fiesta o estancias poco comunes como castillos o mansiones. Por ello el gap tan impresionante en precios. ![](/img/img_30.png)


# Conclusiones y Recomendaciones

Sin duda Airbnb fue un cambio de paradigma en la industria del turismo, volviendose insignia. No por nada existen un número tan grande en Ciudad de México. Este analisis puede ser de gran valor para un sector inmobiliario interesado en obtener datos sobre esta industria y lo redituable que se puede volver. Como posibles mejoras o un proyecto complementario a este, considero que el analisis de cómo han incrementado los precios de vivienda y renta en zonas especificas de la ciudad a partir de Airbnb es un desafío interesante.

# Desafíos y Lecciones Aprendidas

Tuve varios desafíos que me retrasaron. En especifico con los detalles, que se sabe, es donde se suele tener dolores de cabeza. Podría comentar el hecho de que las comillas simples ' en SQL deben pasarse como doble comilla simple '' para que las cadenas se puedan obtener correctamente (y que al procesar los datos, sí se guardan con una comilla simple). Otro desafío fue el de conectar un servidor SQL a Power BI, pues implicaba un esfuerzo demasiado grande para lo innecesario que se vuelve si simplemente se convierte el DataFrame a un archivo Excel y se le pasa a Power BI.

Aunque no se traté del proyecto más complejo, creo que pude encontrar insights interesantes y analizar la información de una manera enriquecedora. Este analisis puede servir para demostrar mis capacidades e incluso para personas interesadas en conocer esta información que puede ser de un alto valor para un sector interesado en ingresar a esta industria. 


# Referencias y Anexos
- [Repositorio de Github](https://github.com/duranueva/Proyecto-Airbnb)
- [Dashboard Power BI (Archivo)](https://github.com/duranueva/Proyecto-Airbnb/blob/main/tools/proyecto.pbix)
- [Notebook de Python](https://colab.research.google.com/drive/1dyiZyBeV2cTuW8U4jARMFNF27jTNMdYb?usp=sharing)
- [Dataset](https://github.com/duranueva/Proyecto-Airbnb/blob/main/tools/listings.csv). 
- [Sitio de Datos Airbnb, donde se tomó el Dataset](https://insideairbnb.com/get-the-data/)
- [Inmuebles creados para el modelo de renta Airbnb](https://www.eluniversal.com.mx/metropoli/edifican-inmuebles-para-rentarlos-en-la-plataforma-airbnb-turismo/?utm_source=chatgpt.com)




