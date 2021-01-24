# Curso Básico de Diseño de Interfaces con Android Studio

## 📚 Módulo 1. Introducción

- ### Clase 1. UI en Android: ¿Por qué? ¿Cómo?

  - #### XML

    Es un lenguaje de marcado en el que se representan mediante **tags**, **atributos** y contenido.

    ````xml
    <TAG atributo="valor">
    	Contenido
    </TAG>
    
    <TAG-2 atributo="valor" />
    ````

  - #### Namespace

    Es un una forma de darle contexto o categoría a un tag. Permite definir donde un elemento tiene un valor definido.

    ````xml
    <NAMESPACE:TAG atr="val">
    	Contenido
    </NAMESPACE:TAG>
    ````

    Un ejemplo para entender esto un poco mejor es el siguiente:

    ````xml
    <Profesor:Luis trabajo:horario="9-11" trabajo:id="luisprof@un.com" personal:id="@luis"></Profesor:Luis>
    ````

    Si definiera sólo un tag ``<luis>`` no se sabría con certeza de quién se esta hablando, pero al definir un namespace se da más contexto pues se da a entender que ``<Luis>`` es un profesor. Además los namespaces no sólo se pueden usar en tags sino también en atributos, por ejemplo en vez de poner un atributo que sólo ponga ``horario="9-11"`` se puede dar más contexto estableciendo con un namespace que ese horario es el de su trabajo.

    Para saber de donde proviene un namespace se usa el atributo ``xmlns:platzi="http:platzi.com/">`` en el que se especifica la URL de laque un namespace tiene su procedencia.

## 📚 Módulo 2. Revisando los archivos para una UI

- ### Clase ?. Estructura de Archivos

  **Package Name:** el identificador único que tendrá la App en Play Store. Lo recomendable es tener dominio de un sitio web del que uno sea dueño seguido del nombre de la App, por ejemplo ``com.misitioweb.nombreapp``

  #### Estructura de Archivos de una App Android

  En la pestaña de *Android* se tiene entre otras cosas:

  - 📁 **res** → Almacena los recursos de la App(imágenes. colores, textos, dimensiones)
    - 📁 **drawable** → Representa gráficos (Todo aquello que pueda ser dibujado en una pantalla)
    - 📁 **layout** → Representa todas las estructuras de pantallas que se creen.
    - 📁 **mipmap** → Guarda los iconos de la App en sus diferentes tamaños.
    - 📁 **values** → Aquí se administran los recursos de la App (Colores, cadenas, dimensiones o arreglos)
      - 📄 colors.xml → Permite administrar los colores de la App
      - 📄 strings.xml → Guarda los Strings de las App. Es una buena práctica guardar los textos que se repiten o que requieren una traducción en este archivo
      - 📄 dimens.xml → Almacena dimensiones compartidas (ancho de una pantalla, alto de una imagen, tamaños de fuente de un texto, etc)
    - 📁 **font** → Guarda las funtes de la App
    - 📁 **animations** → Al,acena XML para las animaciones
    - 📁 **xml** → Contiene preferencias de usuario y datos más complejos.
    - 📁 **raw**  → Contiene archivos como vídeos o audios.

- ### Clase 3. Enlazando nuestro layout con el código

  **Referenciar a un Activity en el código de la App**

    ```kotlin
    setContentView(R.layout.activity_main)                                
    ```
  
    **R** → es una Clase autogenerada que hace referencia a los recursos (📁 res) de la app. Usando esta Clase se puede acceder a los recursos dentro del package res

    **layout** → package layout

    **activity_main** → Nombre del archivo xml que define el Activity

    #### Referenciar a un atributo en el código de la App

    ````xml
    R.color.red
    ````

    **🛈 Nota:** Cuando se compila la App, cada archivo de diseño XML se compila en un recurso ``View``. Los recursos de diseño se deben cargar en el código de la App en la implementación de ``Activity.onCreate()``. Para ello se llama a ``setContentView()`` pasando la referencia al recurso de diseño con la sintaxis ``R.layout.nombre_archivo``. **Ejemplo:**

    ````kotlin
      override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
      setContentView(R.layout.activity_main)
    }
    ````

## 📚 Módulo 3. Creando una UI

- ### Clase 4. La vista de diseño en Android Studio

  **Palette:** elementos que se pueden agregar al Layout y que ya están incluidos en Android

  **Blueprint:** muestra los elementos en su forma "abstracta" como pequeñas cajas conectadas entre si

  **Component Tree:** muestra la anidación de cada uno de los elementos con respecto a las vistas que tenga por dentro.
  
  

## 📚 Módulo 4. Widgets y Vistas

- ### Clase 6. ViewGroup y View: Diferencias básicas

  - #### View

      Es un elemento individual que se va a mostrar por pantalla. Por lo generar estos tags se cierran en la misma línea en la que se definen. 

      ````xml
      <TextView />
      <ImageView />
      <EditText />
      ````

  - #### ViewGroup
  
      Agrupa vistas relacionadas entre si. Cuando se tiene elementos dentro de este los cambios que se hagan a un ViewGroup afectarán también a los elementos que lo contienen.
  
      ````xml
      <LinealLayout android:gravity="start"> <!-- ViewGroup -->
      	<TextView />
          <ImageView />
          <EditText />
      </LinealLayout>
      ````
  
      En el ejemplo anterior el atributo ``gravity`` aplicado al ViewGroup ``<LinealLayout>`` afectará también a los Views que están en su interior.
  
      **🛈 Nota:** pueden haber tantos ViewGroups anidados como sea necesario, no hay una limitación al respecto. **Ejemplo:**
  
      ````xml
      <?xml version="1.0" encoding="utf-8"?>
      <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
          android:orientation="vertical" android:layout_width="match_parent"    
          android:layout_height="match_parent"
          android:gravity="end|bottom"> 
          <!-- gravity afectará a los elementos del ViewGroup. "end|bottom" → Permite poner varios valores -->
          
          <TextView
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="Hola Mundo!" />
      
          <EditText
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:autofillHints="Hi" />
          
      </LinearLayout>
      ````

- ### Clase 7.  Atributos importantes: alto, ancho y id

  ````xml
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  ````

  Estos atributos son obligatorios, permiten definir como un elemento se va distribuir con respecto a su contenido. Pueden recibir por valores:

  - ``wrap_content`` → Hace que el elemento crezca tanto como el contenido que tenga.
  - ``match_parent`` → Hace que un elemento ocupe toda la pantalla.

  **🛈 Nota:** para agregar colores se usa la sintaxis ``@color/red``. Esto trae el color que se le especifique de entre los que están definidos en los recursos de la App. **Ejemplo;**

  ````xml
  android:background="@color/purple_200"
  ````

- ### Clase 8.  Otros atributos y el namespace tools

  Hay un atributo muy importante dentro de las vistas es el *id*:

  ````xml
  android:id="@+id/nombreID"
  ````

  **🛈 Nota:** como id se pueden poner las iniciales del elemento en cuestión, un contexto sobre sobre el layout y que representa dicho elemento. **Por ejemplo:** para un ``<TextView>`` en el Activity main que representa un título el id sería:

  ````xml
  android:id="@+id/tvMainTitle"
  ````

  Para referirse a este elemento en el código de la app se usaría la siguiente sintaxis:

  ````kotlin
  R.id.tvMainTitle
  ````

  **🛈 Nota:** se pueden referenciar imágenes en el xml de un Activity usando ``@mipmap/nombreImg`` o ``@drawable/nombreImg``

  #### Namespace tools

  Permite ver cambios en la Interfaz en tiempo de diseño sin generar una versión final de la App con dichos cambios. **Ejemplo:**

  ````xml
  tools:text="Hello World!"
  ````

  Esto es mu útil para ver cómo quedará la estructura final de la App pero sin usar los valores finales.

## 📚 Módulo 5. Layouts base

- ### Clase  9. LinearLayout: Organizacion lineal

  Es el layout más común para alinear los elementos en pantalla. A este layout hay que agregarle el atributo ``orientation="vertical"`` ó ``orientation="horizontal"`` 

  #### Orientation vertical

  ![Orientation vertical](https://i.ibb.co/xmk7LfP/orientation-vertical.jpg)

  Los elementos se posicionan uno debajo del otro ocupando el espacio que les corresponde en pantalla.

  #### Orientation horizontal

  ![Orientation horizontal](https://i.ibb.co/92Kcc3n/orientation-horizontal.jpg)

  Los elementos se posicionan uno al lado del otro de izquierda a derecha, con la excepción de los países en los que se lee de derecha a izquierda pues en esos países se invierte el orden en el que se muestran los elementos.

  También es posible tener ``LinearLayout`` con diferentes orientaciones anidados:

  ![LinearLayout Anidados](https://i.ibb.co/zQx8mPQ/linear-Layout-anidados.jpg)

  #### Agregar imágenes a un Layout
  
  ````xml
  <ImageView
          android:layout_width="140dp"
          android:layout_height="wrap_content"
          android:src="@drawable/logo" />
  ````
  
  **dp:** *density points* es una medida que se basa en la densidad de pixeles de la pantalla. Esta medida le permite a Android decidir como se va a mostrar un elemento o estirar las imágenes en base a la densidad de pixeles.
  
  **🛈 Nota:** Android tiene algunos colores predefinidos para evitar tener que definir todo desde cero. Estos se acceden con la sintaxis ``@android:color/nombreColor``. **Ejemplo:**
  
  ````xml
  android:background="@android:color/white"
  ````
  
  
  
  ``android:layout_gravity="start"`` → La gravedad afecta sólo al elemento que tiene este atributo y no a todo el ViewGroup como ocurre con ``gravity``.
  
  **🛈 Nota:** aparte de las imágenes Android también permite definir vectores en archivos XML. Para ello hay que hacer click en *file* > *New* > *Vector Asset*. 
  
  Android incluye algunos vectores ya definidos, estos se pueden ver en *Clip art*.
  
  Para agregar uno de estos iconos a un elemento, por ejemplo un ``<EditText>`` se usa la siguiente sintaxis:
  
  ````xml
  android:drawableStart="@drawable/vector_person"
  ````
  
  
  
  ``android:layout_weight="1`` → Establece la prioridad de un elemento cuando se construya el layout.
  
- ### Clase 10. RelativeLayout: organizando con referencias

  RelativeLayout permite crear interfaces con diseños más complejos con elementos situados en diferentes posiciones, en lugar de sólo tener un elemento después de otro como ocurre con ``<LinearLayout>``.

  Este tipo de layout hace posible crear interfaces como esta:

  ![RelativeLayout](https://i.ibb.co/Gn329sh/relative-layout.jpg)

  RelativeLayout se basa en referencias, cada elemento indica en donde se va a ubicar con respecto a su elemento padre.

  #### Atributos de RelativeLayout

  - ``layout_alignParentStart="true"``

    ![alignParentStart](https://i.ibb.co/r5y7WJd/align-Parent-Start.jpg)

  - ``layout_alignParentTop="true"``

    ![alignParentTop](https://i.ibb.co/ydw9XXF/align-Parent-Top.jpg)

  - ``layout_alignParentEnd="true"``
  
    ![alignParentEnd](https://i.ibb.co/kBYgCkV/align-Parent-End.jpg)
  
  - ``layout_below="@id/B"`` → Alinea un elementos con respecto a otro, este último se especifica mediante un id.
  
    ![layout_below](https://i.ibb.co/McnJP27/layout-below.jpg)
  
  - ``layout_alignParentBottom="true"`` → Alinea el elemento en la parte inferior del elemento padre. ``layout_alignParentStart="true"`` → Como el elemento no tiene un tamaño fijo, este atributo hace que el elemento se estire hasta el borde de la pantalla
  
    ![alignParentBottom](https://i.ibb.co/N6NM7Vm/align-Parent-Bottom.jpg)
  

- ### Clase 11. RelativeLayout: Uso práctico

  Una ventaja de RelativeLayout es que en este se pueden crear interfaces usando menos ViewGroups, lo cuál hace el árbol jerárquico menos pesado.

  ``android:layout_centerInParent="true"`` → Centra un elemento de forma horizontal y vertical.

  **🛈 Nota:** es una buena práctica en layouts que se quiere abarcar todo el espacio de pantalla, indicar un width de 0dp y usar ``alignParentStart`` y ``alignParentEnd`` para que el elemento ocupe todo el espacio disponible sin importar el espacio de la pantalla.

  





