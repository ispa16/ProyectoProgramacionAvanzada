# Resultados
## Grupos poblacionales del Ecuador.
En el año 2008 el Ecuador fue reconocido como un estado intercultural y pluricultural (Díaz & Atúnez, 2016), asi lo estableció la constitución de Montecristi desde el primer articulo: "El Ecuador es un Estado constitucional de derechos y justicia, social, democrático, soberano, independiente, unitario, intercultural, plurinacional y laico. Se organiza en forma de república y se gobierna de manera descentralizada. La soberanía radica en el pueblo, cuya voluntad es el fundamento de la autoridad, y se ejerce a través de los órganos del poder público y de las formas de participación directa previstas en la Constitución". (art.1, Constitución de la República del Ecuador)

La interculturalidad que expresa la constitución vigente establece que, las definiciones sociales como idiomas nativos, costumbres, jurisdicción, entre otros, de los indígenas deben ser respetados por todos los pueblos de nacionalidad ecuatoriana como los blancos y meztizos, mantiendo asi como una correcta convivencia bajo el respeto mutuo sin discriminación y bajo el cumplimiento de sus derechos.  
> Art.6, Constitución de la República del Ecuador), Todas las ecuatorianas y los ecuatorianos son ciudadanos y gozarán de los derechos establecidos en la Constitución. La nacionalidad ecuatoriana es el vínculo jurídico político de las personas con el Estado, sin perjuicio de su pertenencia a alguna de las nacionalidades indígenas que coexisten en el Ecuador.

Y a su vez en el art.11, Constitución de la República del Ecuador:

Todas las personas son iguales y gozarán de los mismos derechos, deberes y oportunidades. Nadie podrá ser discriminado por razones de etnia, lugar de nacimiento, edad, sexo, identidad de género, identidad cultural, estado civil, idioma, religión, ideología, filiación política, pasado judicial, condición socio-económica, condición migratoria, orientación sexual, estado de salud, portar VIH, discapacidad, diferencia física; ni por cualquier otra distinción, personal o colectiva, temporal o permanente, que tenga por objeto o resultado menoscabar o anular el reconocimiento, goce o ejercicio de los derechos. La ley sancionará toda forma de discriminación. El Estado adoptará medidas de acción afirmativa que promuevan la igualdad real en favor de los titulares de derechos que se encuentren en situación de desigualdad.
## Inicialización de las Variables

val myDataSchema = StructType(
	Array(
		StructField("id_persona", DecimalType(26, 0), true), 
		StructField("anio", IntegerType, true), 
		StructField("mes", IntegerType, true), 
		StructField("provincia", IntegerType, true), 
		StructField("canton", IntegerType, true), 
		StructField("area", StringType, true), 
		StructField("genero", StringType, true), 
		StructField("edad", IntegerType, true), 
		StructField("estado_civil", StringType, true), 
		StructField("nivel_de_instruccion", StringType, true), 
		StructField("etnia", StringType, true), 
		StructField("ingreso_laboral", IntegerType, true), 
		StructField("condicion_actividad", StringType, true), 
		StructField("sectorizacion", StringType, true), 
		StructField("grupo_ocupacion", StringType, true), 
		StructField("rama_actividad", StringType, true), 
		StructField("factor_expansion", DoubleType, true)
	));

// Uso del esquema
val data = spark.read
.schema(esquemaEstructurado)
.option("header", "true")
.option("delimiter", "\t")
.csv("Datos_ENEMDU_PEA_v2.csv")

Habiendo establecido esto, los análisis de esta presentación se centran en la implementación de sentencias informáticas para demostrar cual ha sido la situación de cada persona caracterizada por su etnia, específicamente a la población de orígen del Ecuador, los indígenas. 
# Cantidad de Personas clasificadas por su etnia
_________________________________________________________________________________________________________

z.show(data.groupBy("etnia").count().sort(desc("count")))
_________________________________________________________________________________________________________
%md
## ¿Cuál es el porcentaje de indígenas (personas de población nativa u originaria del país) con respecto al porcentaje total de personas a las que se les tomó la encuesta?
_________________________________________________________________________________________________________

val indg = data.where($"etnia" === "1 - Indígena")
print(f"${(indg.count * 100)/data.count.toDouble}%.2f%% de Indígenas encuestados")
_________________________________________________________________________________________________________
%md
Primeramente, es necesario determinar cual es el el estado laboral de los índigenas, con el fin de ir obteniendo una aproximacion de como se ha sucitado 
## ¿Cuál es la clasificación de indígenas con respecto a sus condición laboral (condicion_actividad)?
_________________________________________________________________________________________________________
print(f"${(indg.where($"condicion_actividad" === "1 - Empleo Adecuado/Pleno").count * 100)/indg.count.toDouble}%.2f%% Empleo Adecuado\n${(indg.where($"condicion_actividad" === "2 - Subempleo por insuficiencia de tiempo de trabajo").count * 100)/indg.count.toDouble}%.2f%% Subempleo por insuficiencia de trabajo\n${(indg.where($"condicion_actividad" === "4 - Otro empleo no pleno").count * 100)/indg.count.toDouble}%.2f%% Otro empleo no pleno\n${(indg.where($"condicion_actividad" === "5 - Empleo no remunerado").count * 100)/indg.count.toDouble}%.2f%% Empleo no remunerado\n${(indg.where($"condicion_actividad" === "6 - Empleo no clasificado").count * 100)/indg.count.toDouble}%.2f%% Empleo no clasificado\n${(indg.where($"condicion_actividad" === "7 - Desempleo abierto").count * 100)/indg.count.toDouble}%.2f%% Desempleo Abierto\n${(indg.where($"condicion_actividad" === "8 - Desempleo oculto").count * 100)/indg.count.toDouble}%.2f%% Desempleo Oculto")
_________________________________________________________________________________________________________
%md
## ¿Cuál es la cantidad de indígenas que están con desempleo?
Se puede establecer mediante información del INEC que en la encuesta EMENDU, el desempleo se divide en dos partes, una denominada desempleo abierto y otra denominada desempleo oculto, en este analisis de datos, no se toma en cuenta a las personas con desempleo oculto para establecer dicho analisis, esto debido a que las personas caracterizadas por este, son aquellas que no han obtenido trabajo, pero por diversas razones que son competentes a cada individuo mas no a una socailizacion economica:

	Desempleo oculto: Personas sin empleo, que no estuvieron empleados la semana pasada, que no buscaron trabajo y no hicieron gestiones concretas para conseguir empleo o para establecer algún negocio en las cuatro semanas por alguna de las siguientes razones: tiene un trabajo esporádico u ocasional; tiene un trabajo para empezar inmediatamente; espera respuesta por una gestión en una empresa o negocio propio; espera respuesta de un empleador o de otras gestiones efectuadas para conseguir empleo; espera cosecha o temporada de trabajo o piensa que no le darán trabajo o se cansó de buscar.

<a href="https://github.com/ispa16/ProyectoProgramacionAvanzada/wiki/Informaci%C3%B3n-General"> Para más información acerca de las definiciones de la encuesta EMENDU, visite este link</a>

De esta manera podemos establecer que la información mas concreta para este análisis es la "desempleo abierto" ya que esta hace referencia a personas que han buscado empleo durante una semana antes de realizarle dicha encuesta y no han logrado encontrarlo, la pregunta quedaría asi:
### _¿Cuál es la cantidad de indígenas que estan con desempleo abierto (búsqueda activamente de empleo durante el mes anterior a la encuesta sin éxito)?_
_________________________________________________________________________________________________________
indg.where($"condicion_actividad" === "7 - Desempleo abierto").count
_________________________________________________________________________________________________________
%md
Las personas con desempleo abierto son 915, esto daria a interpretar que las personas indigenas no sufren en su mayor parte de desempleo. Puede que la educacion haya sido un valor influyente en este resultado, podemos establecer la informacion que denota de Rodriguez (2018) en su artículo construir la interculturalidad. Políticas educativas, diversidad cultural y desigualdad en Ecuador: 
	La unidad educativa Tránsito Amaguaña, situada al interior del Mercado Mayorista, en el sur de Quito, acoge alumnos de nacionalidad indígena kichwa. La situación de pobreza en las comunidades, donde las distintas reformas agrarias no han llevado a un reparto equitativo de la tierra ni han logrado detener el proceso de empobrecimiento de la población indígena en el campo...Procedentes en su mayoría de comunidades situadas en la región andina, los niños que asisten a esta escuela forman parte del proyecto migratorio de sus progenitores, quienes trabajan en el Mercado como cargadores y vendedores de alimentos.

Para analizar si existe alguna influencia que denote a la educación como parte fundamental de encontrar una empleo más factiblemente. Nos podemos preguntar:
## ¿Cuál es el nivel de educación que tienen los indígenas desempleados abiertamente?
_________________________________________________________________________________________________________
val indgEduc =  indg.where($"condicion_actividad" === "7 - Desempleo abierto") 
z.show(indgEduc.groupBy("nivel_de_instruccion").count().as("cantidad").sort(desc("count")))
_________________________________________________________________________________________________________
%md
Se puede denotar que no es una relacion proporcional, las estadísticas nos presentan que la educacion aparentemente si ha incidido, esto debido a que 
## ¿Puede una persona indígena con desempleo abierto, tener un ingreso laboral diferente de 0? ¿No es esto contradictorio? Compruebelo.
_________________________________________________________________________________________________________
indgEduc.where($"ingreso_laboral" > 0)
indgEduc.where($"ingreso_laboral" > 0).count
_________________________________________________________________________________________________________
%md
	### ¿Cómo es posible que una persona con un "desempleo abierto" tenga un ingreso laboral que no sea 0?
	....
_________________________________________________________________________________________________________
%md
Ahora que determinamos a la educacion como un factor 
## ¿Cuál es el valor máximo y mínimo que gana un indígena que tiene el nivel mas alto de estudios (Post-grado)?
_________________________________________________________________________________________________________
val indgEducPost = (indg.where($"nivel_de_instruccion" === "10 - Post-grado"))
z.show(indgEducPost.select("ingreso_laboral").summary("max", "min"))
_________________________________________________________________________________________________________
%md
## ¿Existe una diferencia de salario que un indigena(post-grado) recibe de ingreso laboral promedio, con respecto al valor de ingreso laboral promedio de un ecuatoriano meztizo(post-grado)?
_________________________________________________________________________________________________________
z.show(indgEducPost.select("ingreso_laboral").summary())
_________________________________________________________________________________________________________
%md
	### ¿Existen valores nulos?
_________________________________________________________________________________________________________
	z.show(indgEducPost.select("ingreso_laboral").groupBy("ingreso_laboral").count().sort(desc("count")))
_________________________________________________________________________________________________________
%md
	### Limpieza de Nulos
_________________________________________________________________________________________________________
	val postIndg = indgEducPost.select("ingreso_laboral").where($"ingreso_laboral".isNotNull)
_________________________________________________________________________________________________________
%md
	### Búsqueda de acotas
_________________________________________________________________________________________________________
	val cantValoresEnDifRangos =  scala.collection.mutable.ListBuffer[Long]()
		val minValue = 0.0
		val maxValue = 5264
		val bins = 5.0
		val range = (maxValue - minValue)/bins
		var minCounter = minValue
		var maxCounter = range
		while (minCounter < maxValue){
		  val valoresEnUnRango = postIndg.where($"ingreso_laboral".between(minCounter,maxCounter))
		  cantValoresEnDifRangos.+=(valoresEnUnRango.count())
		  minCounter = maxCounter
		  maxCounter = maxCounter + range
		}
_________________________________________________________________________________________________________
%md
	### Resultados de rangos
_________________________________________________________________________________________________________
	println("Valores en diferentes rangos: ")
	cantValoresEnDifRangos.foreach(println)
_________________________________________________________________________________________________________
%md
	### Promedio
_________________________________________________________________________________________________________
	val prom = postIndg.select(mean("ingreso_laboral")).first()(0).asInstanceOf[Double]
_________________________________________________________________________________________________________
%md
	### Desviación Estándar
_________________________________________________________________________________________________________
	val desviacion = postIndg.select(stddev("ingreso_laboral")).first()(0).asInstanceOf[Double]
		desviacion: Double = 950.1400043069507
_________________________________________________________________________________________________________

Limites inf y supe......

_________________________________________________________________________________________________________
%md
	### Indígenas
_________________________________________________________________________________________________________

%md
	### Meztizos
_________________________________________________________________________________________________________
Boxsplots rta
_________________________________________________________________________________________________________
%md
	### Respuesta:
	Considerando los resultados de los 2 algoritmos, se puede deducir que en efecto, existe una diferencia entre lo que gana un indigena (post-grado) en promedio,
		con lo que gana un meztizo de similares caracteristicas, pero realmente no es una diferencia significativa, es un valor encontrado en un rango entre 130 -170.
		Vease:
		
		**Algoritmo 1 (salario promedio):**

		indigena =  1387.386075949367		meztizo = 1553.2442199775533
		
			diferencia = | 1387.39 - 1553.24 | = |- 165.85 |
			diferencia = 165.85

		**Algoritmo 2 (salario promedio):**

	 	indigena =  1291.5526315789473		meztizo = 1425.7911637173327

			diferencia = | 1291.55 - 1425.8 | = |- 134.25 |
			diferencia = 134.25
_________________________________________________________________________________________________________
%md
## ¿Es posible que con el tiempo los niveles de empleo adecuado y desempleo en los indígenas hayan aumentado con respecto a los demas grupos poblacionales? ¿Es posible demostrar como ha variado su condicion laboral con el paso de los años?
_________________________________________________________________________________________________________

%md
## ¿Qué hay con respecto a las personas que no son indígenas? ¿Se puede observar una similaridad en cuanto a la estadistica?
_________________________________________________________________________________________________________
%md
	### Respuesta
	Los datos demuestran que aparentemenete no ha habido algun tipo de relegamiento hacia los indigenas, ya que todos los grupos poblacionales han demostrado que han tendido a la baja con respecto al empleo adecuado en el ecuador, además de que la tasa de desempleo (oculto y abierto) a tendido a la baja en todos los grupos.
_________________________________________________________________________________________________________
## De las personas indígenas ¿Es posible que hayan sido las mujeres las mas que menor valor de ingreso han obtenido? ¿Existe alguna diferencia significativa entre el porcentaje de ingresos laborales que generaron las mujeres en  con respecto a los hombres?

z.show(indg.groupBy("anio").pivot("genero").agg( round((sum("ingreso_laboral")*100)/13925210) ).orderBy("anio"))
_________________________________________________________________________________________________________



_________________________________________________________________________________________________________
Al final de todo............
%md
# Bibliografía
Díaz Ocampo, E., & Antúnez Sánchez, A. (2016). _El conflicto de competencia en la justicia indígena del Ecuador._ Temas Socio-Jurídicos, 35(70), 95-117. https://doi.org/10.29375/01208578.2503

Constitución de la República del Ecuador, 20 de Octubre de 2008. https://educacion.gob.ec/wp-content/uploads/downloads/2012/08/Constitucion.pdf

Rodríguez, Maria (2018). _Construir la interculturalidad. Políticas educativas, diversidad cultural y desigualdad en Ecuador._ Recuperado de: http://scielo.senescyt.gob.ec/scielo.php?script=sci_arttext&pid=S1390-12492018000100217
