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