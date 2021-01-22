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

- ### Clase 3. Enlazando nuestro layout con el código

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

## 📚 Módulo 3. Creando una UI

- ### Clase 4. La vista de diseño en Android Studio

  #### Referenciar a un Activity en el código de la App

  ````kotlin
  setContentView(R.layout.activity_main)
  ````

  **R** → es una Clase autogenerada que hace referencia a los recursos (📁 res) de la app. Usando esta Clase se puede acceder a los recursos dentro del package res

  **layout** → package layout

  **activity_main** → Nombre del archivo xml que define el Activity

  #### Referenciar a un atributo en el código de la App

  ````kotlin
  R.color.red
  ````

  **🛈 Nota:** Cuando se compila la App, cada archivo de diseño XML se compila en un recurso ``View``. Los recursos de diseño se deben cargar en el código de la App en la implementación de ``Activity.onCreate()``. Para ello se llama a ``setContentView()`` pasando la referencia al recurso de diseño con la sintaxis ``R.layout.nombre_archivo``. **Ejemplo:**

  ````kotlin
override fun onCreate(savedInstanceState: Bundle?) {
      super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)
  }
  ````
  
  
  
  

