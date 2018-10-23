# Machine Learning con Watson Studio

> Presentación [Introducción a Machine Learning](https://ibm.box.com/v/ml-ppt)

## Componentes Incluidos
* [Watson Studio](https://console.bluemix.net/catalog/services/watson-studio): Watson Studio es una herramienta end-to-end que permite desarrollar modelos de machine learning y deep learning combinando los principales proyectos Open Source y herramientas propias de IBM en la nube.
* [Apache Spark](https://console.bluemix.net/catalog/services/apache-spark): Apache Spark es un framework de computación en clúster optimizado para el procesamiento de datos a gran escala y extremadamente rápido.
* [Jupyter Notebook](http://jupyter.org/): Es una aplicación web Open Source que le permite crear y compartir documentos que contienen código en vivo, ecuaciones, visualizaciones y texto narrativo.

# Prerequisitos

* Cuenta activa de [IBM Cloud](https://console.bluemix.net)

# Paso a Paso

### 1. Clonar el repo

Descarga o clona el repositorio `watson-studio` localmente. 
En una terminal, puedes ejecutar:

```
$ git clone https://github.com/libardolara/watson-studio
```

### 2. Crear los servicios en IBM Cloud

* Crea el servicio [Object Storage](https://console.bluemix.net/catalog/services/cloud-object-storage)
* Crea el servicio [Watson Studio](https://console.bluemix.net/catalog/services/watson-studio)
* Crea el servicio [Apache Spark](https://console.bluemix.net/catalog/services/apache-spark)
* Crea el servicio [Machine Learning](https://console.bluemix.net/catalog/services/machine-learning)

### 3. Crear un Proyecto en Watson Studio

Abre tu servicio de Watson Studio ya sea en [dashboard de IBM Cloud](https://console.bluemix.net/dashboard/apps/) o en el site de [Watson Studio](https://www.ibm.com/cloud/watson-studio) haciendo click en _Sign in_

* En la pagina principal de Watson Studio haz click en _New Project_ y crea un proyecto con todos los recursos (Complete)
* Dale un nombre a tu proyecto
* Asegurate que en Storage este escogido el servicio de **Object Storage** que creaste en el numeral anterior. Si no esta seleccionado debes hacer click en _Add > Existing_ y selecciona de la lista desplegable el servicio.
* Haz click en _Create_

> Vamos a agregar al proyecto servicios adicionales como _Apache Spark_ y _Watson Machine Learning_

* Haz click en la pestaña _Settings_
* Navega hacia abajo hasta la sección _Associated Services_ 
* Haz click en _Add Service_ y selecciona _Spark_
* En la pestaña _Existing_ selecciona tu servicio de **Apache Spark**
* La herramienta te redirige automaticament a la sección de _Associated Services_, haz click en _Add Service_ y selecciona _Watson_
* En la lista de servicios de _Watson_ haz click _Add_ para el servicio de _Machine Learning_
* En la pestaña _Existing_ selecciona tu servicio de **Machine Learning**
* La herramienta te redirige al proyecto en la sección _Associated Services_

### 4. Trabajar con un Data Set

* En la pestaña de _Assests_ en la sección _Load_ arrastra el archivo [Churn.csv](Churn.csv)
* Al cargar un archivo se crea automaticamnte un _Data Asset_. Haz click en el _Data Asset_.
* Analiza los datos, si necesitas entender el contexto de las columnas encuentra la metadata en [Churn.txt](Churn.txt)
* Haz click en _Refine_

> En este punto vamos a usar el servicio **Data Refinery** para crear un flujo de modificación de los datos.

* Haz click en el menú de los 3 puntos para la Columna _RowNumber_ y selecciona la opción _Remove_
* Repite el punto anterior para las columnas _CustomerID_ y _Surname_
* En el campo Operation pega el siguiente codigo para cambiar los campos que deberian ser enteros

```
mutate_at(vars('CreditScore','Age','Tenure','NumOfProducts','HasCrCard','IsActiveMember','Exited'),funs(as.integer))
```

> **Data Refinery** permite usar codigo R para modificar las columnas del data set.

* En el campo Operation pega el siguiente codigo para cambiar los campos que deberian ser decimales

```
mutate_at(vars('Balance','EstimatedSalary'),funs(as.numeric))
```

* Ahora ve a la pestaña _Profile_ y observa la distribución de cada columna.
* Ahora ve a la pestaña _Visualization_ y crea un **Histograma** con variable x _CreditScore_ particionado por _Gender_
* Descarga la grafica haciendo click en el icono de descargar.
* Activa el flujo de datos haciendo click en el boton de play (Un triangulo).
* Haz click en el boton _Save and Run_
* En el dialogo emergente haz click en _View_ y espera a que el flujo termine.
* Vuelve a tu proyecto haciendo click en el nombre del proyecto en el menú de navegación

### 5. Trabajar con Watson Machine Learning
