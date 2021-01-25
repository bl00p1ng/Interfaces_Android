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

- ### Clase 12. FrameLayout: Alineación por región

  Permite crear layouts que ocupen determinado lugar de la pantalla, en lugar de ocuparla toda como ocurre con los tipos anteriores de Layout. FrameLayout va a crecer tanto como se le indique. En un FrameLayout el ancho y el alto están dictados por el tamaño del elemento más grande que hay en su interior. 

  Una característica de FrameLayout es organiza los elementos uno encima de otro y además permite cargar dentro de él vistas dinámicas.

  **🛈 Nota:** es una buena práctica para mejorar el performance de la App que un FrameLayout sólo tenga una vista hija.

- ### Clase 13.  FrameLayout: Uso práctico

  **dp:** es una unidad de medida que usa Android para calcular el tamaño de llos elementos en pantalla. Fue creada para estandarizar una forma de medida, ya que Android tiene una gran cantidad de pantallas con  densidades de pixeles muy variadas.
  Lo que hace Android para calcular esta medida es dividir cualquier pantalla en una cuadricula (como un cuaderno cuadriculado) donde cada cuadrado es de 8dp x 8dp,por esa razón es bueno intentar diseñar teniendo usando múltiplos de 8 (8dp.16dp, 24 dp) para las medidas de los views, paddings,  márgenes, imágenes,iconos,etc. 

  Por  ejemplo si se va poner altura a un appBar, en lugar de poner 60, lo mejor es poner 64, o si se pone una altura para un imageview en lugar de poner 20lo ideal es poner 16 o 24. Es por esta razón que Android Studio autogenera medidas normalmente en múltiplos de 8 como 8dp, 16dp, 24dp, etc.

- ### Clase 14. Layouts externos: ConstraintLayout

  Es un layout externo similar a RelativeLayout con la excepción de que en ConstraintLayout los elementos reaccionan a las modificaciones que ocurran en la pantalla. Es un Layout muy usado, tanto que es cuando se crea una nueva Activity es el tipo de Layout por default, de hecho ya se encuentra agregado por defecto en las dependencias.

  ConstraintLayout tiene algunas ventajas como:

  - Facilita el hacer animaciones

  - Permite agregar elementos más dinámicos que reaccionen a cambios en el ancho de la pantalla, etc.
  - Es más flexible que otros tipo de layouts pues permite establecer relaciones entre todos los elementos y la propia vista padre.
  - Mejora el uso de la memoria al evitar usar layouts anidados para generar interfaces complejas

  ConstraintLayout usa un namespace llamado ``app`` para estructurar la pantalla.

  Cada uno de los círculos de la imagen representan los puntos sobre los que se puede alinear cada elemento. Dichos puntos son *start*, *end*, *top*, *bottom*.

  ![Puntos sobre los que se puede alinear un constraint layout](https://i.ibb.co/1qkbQkX/constraint-layout.jpg)

  **Ejemplo:**

  ````xml
  app:layout_constraintTop_toTopOf="parent" <!-- Alinea el Top del elemento conel Top del padre -->
  ````

  **🛈 Nota:** todos los elementos de un ConstraintLayout deben tener por lo menos una alineación horizontal y vertical.

  **🛈 Nota:** ``Ctrl + L`` → Organiza los atributos del XML

  Una ventaja de este tipo de layout es que si ocurre un cambio en la pantalla, como por ejemplo que se quite un elemento, el elemento de abajo se va a alinear con respecto a los constraints que tenia el elemento previo, permitiendo así crear interfaces dinámicas.

## 📚 Módulo 6. Estilos y temas

- ### Clase 15. ¿Qué es un estilo?

  Un estilo permite especificar el diseño visual de una aplicación de manera de que los estilos puedan ser reutilizados por diferentes elementos.

  #### Agregar estilos a una aplicación.

  El archivo con los estilos se encuentra en *Android* > *app* > *res* > *values* > *styles.xml*

  Para crear un estilo se usa el tag ``<style>`` y se le asigna un nombre. 

  ````xml
  <?xml version="1.0" encoding="utf-8"?>
  <resources>
      <!-- Base application theme. -->
      <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
          <!-- Customize your theme here. -->
          <item name="colorPrimary">@color/colorPrimary</item>
          <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
          <item name="colorAccent">@color/colorAccent</item>
      </style>
  
      <style name="AppTheme.EditTextStyle" parent="AppTheme">
          <item name="android:textSize">16sp</item>
      </style>
  </resources>
  ````

  

  Lo normal al usar estilos es crear primero tomar las características más comunes y ponerlas en un estilo **padre** y luego crear estilos **hijo** para las características especificas, algo similar a lo que ocurre con la herencia en POO.

  #### Aplicar estilos a una aplicación

  ````xml
  <EditText
  	style="@style/AppTheme.EditTextStyle" />
  ````

- ### Clase 16. ¿Qué es un tema?

  Los **estilos** son útiles para compartir atributos entre widgets. Dichos atributos de comparten de forma individual entre cada Widget.

  Los **temas** por otra parte son estilos aplicados globalmente, es decir, se van a aplicar a ViewGroups, layouts o para toda la App. Cuando se hace una modificación en un tema, dicho cambio se ve involucrado en todos los elementos implicados.

  **📄 AndroidManifest.xml:** es una sección en la que se definen las pantallas que se tienen con respecto al código. Es muy común que dentro del tag ``<application>`` exista un atributo llamado ``android:theme="@style/AppTheme"`` en el que se define el tema global de la aplicación.

  #### Crear un tema

  ````xml
  <!-- CUSTOM THEME -->
  <style name="AppTheme.Red" parent="AppTheme">
      <item name="background">#FFFF0000</item>
  </style>
  ````

  #### Aplicar un tema en una App

  ````xml
  <?xml version="1.0" encoding="utf-8"?>
  <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:theme="@style/AppTheme.Red"></androidx.constraintlayout.widget.ConstraintLayout>
  ````

  Si bien en un tema se establecen estilos globales cada elemento individual puede sobrescribir estos estilos.





