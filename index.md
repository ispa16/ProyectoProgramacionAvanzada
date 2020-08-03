# Resultados
## Grupos poblacionales del Ecuador.
En el año 2008 el Ecuador fue reconocido como un estado intercultural y pluricultural (Díaz & Atúnez, 2016), asi lo estableció la constitución de Montecristi desde el primer articulo: "El Ecuador es un Estado constitucional de derechos y justicia, social, democrático, soberano, independiente, unitario, intercultural, plurinacional y laico. Se organiza en forma de república y se gobierna de manera descentralizada. La soberanía radica en el pueblo, cuya voluntad es el fundamento de la autoridad, y se ejerce a través de los órganos del poder público y de las formas de participación directa previstas en la Constitución". (art.1, Constitución de la República del Ecuador)

La interculturalidad que expresa la constitución vigente establece que, las definiciones sociales como idiomas nativos, costumbres, jurisdicción, entre otros, de los indígenas deben ser respetados por todos los pueblos de nacionalidad ecuatoriana como los blancos y meztizos, mantiendo asi como una correcta convivencia bajo el respeto mutuo sin discriminación y bajo el cumplimiento de sus derechos.  
> Art.6, Constitución de la República del Ecuador), Todas las ecuatorianas y los ecuatorianos son ciudadanos y gozarán de los derechos establecidos en la Constitución. La nacionalidad ecuatoriana es el vínculo jurídico político de las personas con el Estado, sin perjuicio de su pertenencia a alguna de las nacionalidades indígenas que coexisten en el Ecuador.

Y a su vez en el aritculo 11, de la Constitución de la República del Ecuador se establece que:

> Art.11, Todas las personas son iguales y gozarán de los mismos derechos, deberes y oportunidades. Nadie podrá ser discriminado por razones de etnia, lugar de nacimiento, edad, sexo, identidad de género, identidad cultural, estado civil, idioma, religión, ideología, filiación política, pasado judicial, condición socio-económica, condición migratoria, orientación sexual, estado de salud, portar VIH, discapacidad, diferencia física; ni por cualquier otra distinción, personal o colectiva, temporal o permanente, que tenga por objeto o resultado menoscabar o anular el reconocimiento, goce o ejercicio de los derechos. La ley sancionará toda forma de discriminación. El Estado adoptará medidas de acción afirmativa que promuevan la igualdad real en favor de los titulares de derechos que se encuentren en situación de desigualdad.

Habiendo establecido esto, los análisis de esta presentación se centran en la implementación de sentencias informáticas para demostrar cual ha sido la situación de cada persona caracterizada por su etnia, específicamente a la población de orígen del Ecuador, los indígenas. 
## Cantidad de Personas clasificadas por su etnia

	z.show(data.groupBy("etnia").count().sort(desc("count")))
<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

## ¿Cuál es el porcentaje de indígenas (personas de población nativa u originaria del país) con respecto al porcentaje total de personas a las que se les tomó la encuesta?

	val indg = data.where($"etnia" === "1 - Indígena")
	print(f"${(indg.count * 100)/data.count.toDouble}%.2f%% de Indígenas encuestados")
<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

Ahora sabemos que las personas indigenas son unos de los grupos a los que mas se les a relizado la encuesta, es necesario determinar cual es el el estado laboral de los índigenas, con el fin de ir obteniendo una aproximacion de como se ha sucitado las condiciones laborales a lo largo de estos años.
## ¿Cuál es la clasificación de indígenas con respecto a sus condición laboral (condicion_actividad)?

> print(f"${(indg.where($"condicion_actividad" === "1 - Empleo Adecuado/Pleno").count * 100)/indg.count.toDouble}%.2f%% Empleo Adecuado\n${(indg.where($"condicion_actividad" === "2 - Subempleo por insuficiencia de tiempo de trabajo").count * 100)/indg.count.toDouble}%.2f%% Subempleo por insuficiencia de trabajo\n${(indg.where($"condicion_actividad" === "4 - Otro empleo no pleno").count * 100)/indg.count.toDouble}%.2f%% Otro empleo no pleno\n${(indg.where($"condicion_actividad" === "5 - Empleo no remunerado").count * 100)/indg.count.toDouble}%.2f%% Empleo no remunerado\n${(indg.where($"condicion_actividad" === "6 - Empleo no clasificado").count * 100)/indg.count.toDouble}%.2f%% Empleo no clasificado\n${(indg.where($"condicion_actividad" === "7 - Desempleo abierto").count * 100)/indg.count.toDouble}%.2f%% Desempleo Abierto\n${(indg.where($"condicion_actividad" === "8 - Desempleo oculto").count * 100)/indg.count.toDouble}%.2f%% Desempleo Oculto")

## ¿Cuál es la cantidad de indígenas que están con desempleo?
Se puede establecer mediante información del INEC que en la encuesta EMENDU, el desempleo se divide en dos partes, una denominada desempleo abierto y otra denominada desempleo oculto, en este analisis de datos, no se toma en cuenta a las personas con desempleo oculto para establecer dicho analisis, esto debido a que las personas caracterizadas por este, son aquellas que no han obtenido trabajo, pero por diversas razones que son competentes a cada individuo mas no a una socailizacion economica:

> **Desempleo oculto:** Personas sin empleo, que no estuvieron empleados la semana pasada, que no buscaron trabajo y no hicieron gestiones concretas para conseguir empleo o para establecer algún negocio en las cuatro semanas por alguna de las siguientes razones: tiene un trabajo esporádico u ocasional; tiene un trabajo para empezar inmediatamente; espera respuesta por una gestión en una empresa o negocio propio; espera respuesta de un empleador o de otras gestiones efectuadas para conseguir empleo; espera cosecha o temporada de trabajo o piensa que no le darán trabajo o se cansó de buscar.

<a href="https://github.com/ispa16/ProyectoProgramacionAvanzada/wiki/Informaci%C3%B3n-General"> Para más información acerca de las definiciones de la encuesta EMENDU, visite este link</a>

De esta manera podemos establecer que la información mas concreta para este análisis son aquellos indigenas que hallan sido catalogados con "desempleo abierto", ya que esta hace referencia a personas que han estado en la búsqueda de empleo durante una semana antes de realizarle dicha encuesta y no han logrado encontrarlo, la pregunta estaría mejor formulada de la siguiente manera:
### _¿Cuál es la cantidad de indígenas que se encuentran con desempleo abierto (búsqueda activamente de empleo durante el mes anterior a la encuesta sin éxito)?_

	indg.where($"condicion_actividad" === "7 - Desempleo abierto").count

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

Las personas con desempleo abierto son 915, esto daria a interpretar que las personas indigenas no sufren en su mayor parte de desempleo. Puede que la educacion haya sido un valor influyente en este resultado, podemos establecer la informacion que denota de Rodriguez (2018) en su artículo construir la interculturalidad. Políticas educativas, diversidad cultural y desigualdad en Ecuador: 
	La unidad educativa Tránsito Amaguaña, situada al interior del Mercado Mayorista, en el sur de Quito, acoge alumnos de nacionalidad indígena kichwa. La situación de pobreza en las comunidades, donde las distintas reformas agrarias no han llevado a un reparto equitativo de la tierra ni han logrado detener el proceso de empobrecimiento de la población indígena en el campo...Procedentes en su mayoría de comunidades situadas en la región andina, los niños que asisten a esta escuela forman parte del proyecto migratorio de sus progenitores, quienes trabajan en el Mercado como cargadores y vendedores de alimentos.

Para analizar si existe alguna influencia que denote a la educación como parte fundamental de encontrar una empleo más factiblemente. Nos podemos preguntar:
## ¿Cuál es el nivel de educación que tienen los indígenas desempleados abiertamente?

	val indgEduc =  indg.where($"condicion_actividad" === "7 - Desempleo abierto") 
	z.show(indgEduc.groupBy("nivel_de_instruccion").count().as("cantidad").sort(desc("count")))
	
<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>
Se puede denotar que no es una relacion proporcional, las estadísticas nos presentan que la educación aparentemente si ha incidido, esto debido a que se puede ver que las personas con mayor nivel de instruccion son las que representan la menor cantidad de desempleados indígenas.
## ¿Puede una persona indígena con desempleo abierto, tener un ingreso laboral diferente de 0? ¿No es esto contradictorio? Compruebelo.

	z.show(indgEduc.where($"ingreso_laboral" > 0))
	indgEduc.where($"ingreso_laboral" > 0).count

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

### ¿Cómo es posible que una persona con un "desempleo abierto" tenga un ingreso laboral que no sea 0?
Se puede considerar varios posibles errores:

* **Primero:** La sentencia este mal escrita o con un error, lo cual es posible, pero se descarta al usar otra herramienta para comprobar su veracidad (SQL) en el cual demuestra usando filtros que existen encuestados indigenas, con desempleo oculto que tienen un ingreso laboral mayor a 0.

/////////////////////////////////////////

* **Segundo:** El archivo de origen vino con defectos, otra opcion posible, pero tambien descartada cuando leemos los significados de cada columna.

_Posible Respuesta:_ La pagina web oficial de la EMENDU,  ofrece información acerca de que es el desempleo oculto y que considera el mismo. Siendo asi el significado de esta variable "Personas sin empleo, que no estuvieron empleados en la semana pasada y que buscaron trabajo e hicieron gestiones concretas para conseguir empleo o para establecer algún negocio en las cuatro semanas anteriores a la entrevista."

_Se puede considerar como verdadera esta sentencia ya que, podemos deducir que el ingreso laboral que decretaron estas personas en la encuesta pertenece al ingreso laboral que recibian una semana antes de la encuesta, cuando aun estaban empleados._

Ahora que determinamos a la educacion como un factor 
## ¿Cuál es el valor máximo y mínimo que gana un indígena que tiene el nivel mas alto de estudios (Post-grado)?

val indgEducPost = (indg.where($"nivel_de_instruccion" === "10 - Post-grado"))
z.show(indgEducPost.select("ingreso_laboral").summary("max", "min"))

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

## ¿Existe una diferencia de salario que un indigena(post-grado) recibe de ingreso laboral promedio, con respecto al valor de ingreso laboral promedio de un ecuatoriano meztizo(post-grado)?

z.show(indgEducPost.select("ingreso_laboral").summary())

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

Boxsplots rta

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


## ¿Es posible que con el tiempo los niveles de empleo adecuado y desempleo en los indígenas hayan aumentado con respecto a los demas grupos poblacionales? ¿Es posible demostrar como ha variado su condicion laboral con el paso de los años?


## ¿Qué hay con respecto a las personas que no son indígenas? ¿Se puede observar una similaridad en cuanto a la estadistica?


### Respuesta
Los datos demuestran que aparentemenete no ha habido algun tipo de relegamiento hacia los indigenas, ya que todos los grupos poblacionales han demostrado que han tendido a la baja con respecto al empleo adecuado en el ecuador, además de que la tasa de desempleo (oculto y abierto) a tendido a la baja en todos los grupos.

## De las personas indígenas ¿Es posible que hayan sido las mujeres las mas que menor valor de ingreso han obtenido? ¿Existe alguna diferencia significativa entre el porcentaje de ingresos laborales que generaron las mujeres en  con respecto a los hombres?

	z.show(indg.groupBy("anio").pivot("genero").agg( round((sum("ingreso_laboral")*100)/13925210) ).orderBy("anio"))
	
<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>




## Variables a comparar

En el Ecuador historicamente los indigenas han sido el grupo mas vulnerable desde la conquista de los espanoles,desde entonces este grupo etnico ha sido discriminado por los demas grupos, relegandolos a una posicion desfavorable con respecto a otros grupos etnicos, al otro lado de la balanza tenemos a los mestizos quienes en la actualidad son el grupo etnico comun en el pais y muchos lo consideran como el privilegiado ya que en su mayoria se encuentra ubicados en areas centricas de las provincias mientras que los indigenas se encuentran relegados a las areas rurales 

Actualmente existe la creencia de que estas diferencias ya quedaron en el pasado, los ultimos gobiernos han impulsado distintas campanas con este proposito como es la del buen vivir (sumak kawsay), tambien se han hecho muchas campanas de alfabetizacion orientados para estos sectores, sumado a esto tenemos tambien tenemos las distintas campanas de informacion del gobierno nacional que dan a entender que esta problematica social ya quedo en el pasado, por lo que buscaremos datos en ambos grupos sociales para despues compararlos y llegar a una conclusion 


Una de las formas en las que se muestra la discrimanacion en el dia a dia es a la hora en la que las empresas presinden de sus empleados por lo que un indice de deseempleo mayor en los indigenas seria una indicio de racismo


## Porcentaje de desempleo indigena en el area urbana y rural

Para estas consultas nos centraremos en las siguientes columnas:

* area: La columna describe el area donde se encuentra viviendo la persona (rural o urbana)
* condicion_activada: La columna describe como estasu condicion laboral actualmente es decir si se encuentra empleado o no
Generalmente se tiene la creencia que los indigenas viven en su mayoria en el area rural, mientras que los mestizos en el area urbana, por lo que el deseempleo deberia proporcional a esto 

indigenas

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

mestizos

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

En las ultimas decadas los indigenas han empezado a migrar a las ciudades en busca de mejores oportunidades, sim embargo no todos han encontrado estas oportunidades ya que en la grafica vemos que existe un mayor deseempleo para los indigenas en el area urbana 
en contraste en los mestizos tambien existe un mayor indice de desempleo en el area urbana ya que la mayoria no suele migrar por lo que se quedan buscando oportunidades en su ciudad natal


## Media de ingresos de indigenas segun el grupo de ocupacion

Se cree que los indigenas no suelen ser tratados con equidad al momento de ser pagados con diferencia a otros grupos que suelen ser denominados privilegiados por lo que intentaremos averiguar si esto es verdad

Para estas consultas usaremos las siguientes columnas:

* grupo_ocupacion: Es la rama o sextor de trabajo en la que se opera
* ingreso_laboral: es la cantidad de dinero que resive mensualmente por su trabajo


indigenas

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

mestizos

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

podemos observar la media de ingresos por cada grupo de ocupacion, en general vemos que en los mismos campos los indigenas ganan menos que los mestizos esto puede ser debido a que los mestizos pueden ocupar cagos mas altos en los mismos campos, mientras que a los indigenas los relegan a cargos bajos y no suelen conseguir ascensos, esto es otro indicio de discriminacion

## Media de ingresos de indigenas segun la zona urbana o rural

Ahora ya sabemos que los mestizos ganan mas que los indigenas, los indigenas se encuentran ubicados en su mayoria en el area rural por lo que los indigenas recien graduados o que emigraron por sus estudios buscan estar cerca de su familia por lo que podrian buscar empleo cerca de estas zonas, historicamente la zona urbana tiene empleos mejor pagados que la rural, por lo que queremos ver si esto podria explicar los datos anteriores


indigenas

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

mestizos

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

En esta consulta podemos confirmar que los indigenas ganan menos que los mestizos en el area urbana y rural, por lo que seguimos viendo que la brecha salarial sigue existiendo independientemente del area urbana o rural 

## Media de ingresos de indigenas segun el nivel de instruccion

Ya confirmamos que los indigenas ganan menos independientemente del sector en el que viven, ahora podemos suponer que esto es debido a que ganan menos al no tener el mismo nivel de educacion, por lo que debemos verificar si esta hipotesis es valida Para estas consultas nos centraremos en las siguientes columnas:

* nivel_de_instruccion: La columna describe el grado de estudios que tienen las personas encuestadas
* ingreso_laboral: es la cantidad de dinero que resive mensualmente por su trabajo


indigenas

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

mestizos

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

finalmente podemos comprobar que pese a tener el mismo grado de estudio en promedio los mestizos ganan mas dinero que los indigenas en todas las categorias de nivel de estudio 

#### conclusion

En estas consultas comprobamos que existe una brecha salarial entre indigenas y mestizos que es considerable y en la que no incide ni el area en el que estan ubicados ni su nivel de estudio, ademas sabemos que los indigenas que se desempenan en los mismos grupos de ocupacion ganan menos que los mestizos, con esto podemos confirmar que existe descriminacion contra los indigenas al momento de remunerados o al momento de ser ascendidos



Una de las formas en las que se muestra la discrimanacion en el dia a dia es a la hora en la que las empresas presinden de sus empleados por lo que un indice de deseempleo mayor en los indigenas seria una indicio de racismo

## Numero de desempleo indigena segun el nivel de instruccion

Ahora nos enfocaremos en la categoria de deseempleo abierto es decir que no incluye otras formas de empleo inadecuado como trabajos transitorios
 Para estas consultas nos centraremos en las siguientes columnas:

* nivel_de_instruccion: La columna describe el grado de estudios que tienen las personas encuestadas
* condicion_activada: La columna describe como esta su condicion laboral actualmente es decir si se encuentra empleado o no

Ahora averiguaremos como es porcentualmente el desempleo en ambos grupos etnicos para averiguar si existe una diferencia considerable entre el porcentaje de deseemplo entre estos grupos Para la grafica usaremos un grafico de barras que son los mas utiles para comparar categorias y su frecuencia , que es lo que buscamos en esta consulta

indigenas

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

mestizos

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

Podemos apreciar que el porcentaje de deseempleo sigue una tendencia similar en ambos grupos,  vemos que en la categoria de educacion superior universitaria el deseempleo es mucho mayor en los mestizos por lo que concluimos que los mestizos tienden a ir mas a la universidad a diferencia de los indigenas por lo mismo que el indice es mayor para los mestizos ya que no existen oportunidades para todos los graduados,  otra difrencia notable es en la primaria el indice es considerabemente mayor en los indigenas ya que a diferencia de los mestizos, los indigenas suelen abandonar su eduacion en este nivel debido al poco interes que tienen los padres en la educacion de sus hijos o a la falta de recursos para esta

## Porcentaje de desempleo segun el estado civil

El estado civil influye en alguna manera en el indice de deseempleo?, existe alguna diferencia con los mestizos ? Para estas consultas nos centraremos en las siguientes columnas:

* estado civil: La columna describe si la persona se encuentra soltera o tiene alguna relacion que establece ciertos derechos y deberes
* condicion_activada: La columna describe como estasu condicion laboral actualmente es decir si se encuentra empleado o no

Generalmente se tiene la creencia de que los indigenas son mas apegados a su familia por lo que  buscan la forma de mantenerla, esto deberia de influir en el indice de deseempleo ?

indigenas

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

mestizos

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

Los resultados son muy similares por lo que concluimos que en los dos grupos etnicos existe el sentido de responsabilidad en la gentee casada para insistir en la busqueda de un trabajo, mientras que la gente soltera no siente esta responsabilidad y no insiste en la busqueda de un trabajo, un dato a resaltar es que en ambos casos las personas viudas, son las que tienen un menor indice de deseempleo

## Evolucion de deseempleo indigena segun el genero

como ha evolucionado el deseempleo en la poblacion indigena en este tiempo en el cual ha existido una crisis creciente? Para estas consultas nos centraremos en las siguientes columnas:

* year: La columna describe el año en el que la persona que realizo la encuesa
* genero: La columna describe el sexo de la persona que realizo la encuesa
* condicion_activad: La columna describe como esta su condicion laboral actualmente es decir si se encuentra empleado o no
Otro factor de discriminacion es el genero, historicamente las mujeres tambien han sido relegadas, pero esta tendencia sigue en la actualidad ?

indigenas

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

mestizos

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

En las graficas podemos observar que el  año con mayor indice deseempleo es el 2017  año en el que la economia del Ecuador crecio un 3%, por lo que vemos en el 2018 una notoria mejoria en el indice de deseempleo
Obsevamos que en el sector indigena, las mujeres tienen el indice de deseemplo mas bajo en todos los años a diferencia de las mujeres mestizas que tienen el indice de deseempleo mas alto en todos los años, esto se explica ya que durante los ultimos 5 años su presencia a nivel de dirigencia y representatividad en distintos movimientos sociales se incremento, lo que nos da a entender que las mujeres indigenas buscan roles mas importantes, mientras que las mujeres mestizas han actuado de forma mas discreta 

#### Conclusion
El indice de deseempleo entre ambos grupos sociales es muy similar, por lo que concluimos que no existe discriminacion hacia los indigenas en el momento en que se realizan los despidos, destacando notoriamente a las mujeres indigenas cuyos indices de deseempleo son los mas bajos  y que mientras el deseempleo aumento en el año 2017, en las mujeres indigenas la tendencia siguio hacia un menor indice de desempleo 

## Evolucion del nivel de instruccion indigena en los años

Por ultimo queremos saber como ha evolucionado el nivel de instruccion en el pueblo indigena a traves de este tiempo y si existe alguna relacion con los mestizos, siguiendo la creencia de que los indigenas tienden a preparase cada vez mas? 
Para estas consultas nos centraremos en las siguientes columnas:

* year: La columna describe el año en el que la persona que realizo la encuesa
* nivel_de_instruccion: La columna describe el grado de estudios que tienen las personas encuestadas


indigenas

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

mestizos

<iframe src="https://801c17614aae.ngrok.io/#/notebook/2FCCUUVSD/paragraph/paragraph_1593403281153_-2087515944?asIframe" style="width: 500px; height: 400px; border: 0px"></iframe>

vemos que el numero de personas con educacion en los diferentes niveles tiende a variar mucho en los indigenas mientras que en los mestizos el numero  no varia esta diferencia la apreciamos sobre todo en la primaria donde el numero de personas con este grado de educacion ha disminuido contrastandolo con la consulta hecha anteriormente que nos da el alto indice de deseempleo en los indigenas con educacion primaria, por lo que concluimos que los adultos indigenas han tomado conciencia sobre esto e instan a sus hijos a acabar sus estudios por lo que el numero ha disminuido 

## conclusion 
Los indigenas han mejorado su condicion social a lo largo de los ultimos años, las campanas de alfabetizacion en comunidades rurales, la inversion en escuelas en areas rurales y el continuo crecimiento de la emigracion a las zonas urbanas  han logrado que la brecha entre indigenas y mestizos se acorte sobre todo a la hora en la que las empresas se desacen de sus trabajadores donde los datos demuestran que no existe preferencia hacia un grupo en particular, sim embargo aun existe una brecha salarial que debe ser superada y que es una muestra de que la discriminacion aun existe hacia estos grupos en el ambito laboral

## A considerar

* Todas las funciones utilizadas para la realizacion del presente EDA se encuentran detalladas en la siguiente direccion: https://github.com/ispa16/ProyectoProgramacionAvanzada/wiki/Funciones-a-utilizar
* Algunas graficas pueden dar el error "No data to show", considere abrir la pestana "settings" y colocar la key y los values segun corresponda





_____________________________________________________________________________________________________________________________________________________
# Bibliografía
Díaz Ocampo, E., & Antúnez Sánchez, A. (2016). _El conflicto de competencia en la justicia indígena del Ecuador._ Temas Socio-Jurídicos, 35(70), 95-117. https://doi.org/10.29375/01208578.2503

Constitución de la República del Ecuador, 20 de Octubre de 2008. https://educacion.gob.ec/wp-content/uploads/downloads/2012/08/Constitucion.pdf

Rodríguez, Maria (2018). _Construir la interculturalidad. Políticas educativas, diversidad cultural y desigualdad en Ecuador._ Recuperado de: http://scielo.senescyt.gob.ec/scielo.php?script=sci_arttext&pid=S1390-12492018000100217

El telegrafo, 29 de Junio de 2019. Las mujeres indígenas ganan espacio y liderazgo. https://www.eltelegrafo.com.ec/noticias/politica/3/mujeres-indigenas-espacio-liderazgo-ecuador

El telegrafo, 03 de septiembre de 2019 . Ecuador invierte $ 10.250 millones en educación básica y bachillerato. www.eltelegrafo.com.ec. https://www.eltelegrafo.com.ec/noticias/sociedad/6/inversion-educacion-basica-bachillerato-ecuador

Banco Central del Ecuador, 29 de Marzo 2018.  Ecuador creció 3.0% en 2017 y confirma el dinamismo de su economía . https://www.bce.fin.ec/index.php/boletines-de-prensa-archivo/item/1080-ecuador-crecio-30-en-2017-y-confirma-el-dinamismo-de-su-economia#:~:text=La%20econom%C3%ADa%20ecuatoriana%20(PIB)%20en,en%20t%C3%A9rminos%20reales%20de%203.0%25.&text=El%20Gasto%20de%20Consumo%20Final%20del%20Gobierno%20General%2C%20en%20el,PIB%20en%200.56%20puntos%20porcentuales




