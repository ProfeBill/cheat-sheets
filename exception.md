# Excepciones en Python

## Componentes de un buen mensaje de error

Un buen mensaje de error debe responder tres preguntas al usuario: 

* ¿Que sucedió? : De un nombre al error que permita identificarlo cuando se comunique con el perosnal técnico.

* ¿Por qué sucedió? Explique la causa del error e incluya los datos de entrada que tienen problemas y causaron el error

* ¿Cómo lo corrijo? Indique las acciones correctas esperadas del usuario: valores válidos de variables, prerrequisitos que debe cumplir, acciones que debe evitar

## Creación de clases de Excepción

### Clase simple sin mensaje ni parámetros

```
class ExcepcionPorInteresesExcesivos( Exception ): 
    pass
```

### Clase de Excepción con mensaje personalizado

```
class ExcepcionDeNumeroDePagosNoValido( Exception ): 
    """ 
    Excepcion personalizada para indicar que el nmero de cuotas es menor o igual a cero

    """
    def __init__( self ):
        super().__init__( f"Number of payments must be greater than zero" )

```

### Clase de Excepción con mensaje personalizado y parámetros

```

class ExcepcionPorInteresesExcesivos( Exception ): 
    """ 
    Custom exception for interest rates above maximun

    Exepcion personalizada para indicar que una tasa de interes supera
    el tope máximo

    """
    def __init__( self, interest ):
        """
        To raise this exception, pass the intrest rate used as parameter to constructor

        Para usar esta excepción, debe llamar al constructor indicando la tasa usada
        """
        super().__init__( f"Invalid interest rate {interest} maximun allowed is {MAX_INTEREST}" )

```


## Lanzamiento de las excepciones


## Control de las excepciones