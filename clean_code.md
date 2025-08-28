# Reglas de Código Limpio para Python

Inspirado en https://testdriven.io/blog/clean-code-python/ 

## Nombres
Uno de los aspectos más importantes de escribir código limpio son las convenciones de nomenclatura. Siempre debes usar nombres significativos y que revelen la intención. Siempre es mejor usar nombres largos y descriptivos que nombres cortos con comentarios.

```python
# Esto esta mal
# representa el número de usuarios activos
ua = 55

# Esto esta bien
cantidad_de_usuarios_activos = 55
```
## Variables
### 1. Usa sustantivos para los nombres de las variables.
### 2. Usa nombres descriptivos/reveladores de intenciones.
Otros desarrolladores deberían ser capaces de averiguar lo que almacena una variable con solo leer su nombre.
```Python
# Esto está mal
c = 5
d = 12

# Esto está bien
contador_de_ciudades = 5
tiempo_transcurrido_en_días = 12
```
### 3. Usa nombres pronunciables
Siempre debes usar nombres pronunciables; De lo contrario, tendrá dificultades para explicar sus algoritmos en voz alta.
```python
from datetime import datetime

# Esto está mal
genyyyymmddhhmmss = datetime.strptime('04/27/95 07:14:22', '%m/%d/%y %H:%M:%S')

# Esto está bien
fecha_y_hora_generados = datetime.strptime('04/27/95 07:14:22', '%m/%d/%y %H:%M:%S')
```
### 4. Evita el uso de abreviaturas ambiguas
No trates de inventar tus propias abreviaturas. Es mejor que una variable tenga un nombre más largo que un nombre confuso.
```python
# Esto está mal
pn = 'Bob'
fc = 1621535852

# Esto está bien
primer_nombre = 'Bob'
fecha_creacion = 1621535852
```
### 5. Usa siempre el mismo vocabulario
Usa siempre el mismo vocabulario
```python
# Esto está mal
primer_nombre_cliente = 'Bob'
apellido_comprador = 'Smith'

# Esto está bien
primer_nombre_cliente = 'Bob'
apellido_cliente = 'Smith'
```
### 6. No uses "números mágicos" / magic numbers
Los números mágicos son números extraños que aparecen en un código, que no tienen un significado claro. Veamos un ejemplo:
```python
import random

# Esto está mal
def roll():
    return random.randint(0, 36)  # ¿qué se supone que representa el 36?

# Esto está bien
CONTADOR_ESTUDIANTES = 36

def roll():
    return random.randint(0, ID_ESTUDIANTES)
```
En lugar de usar números mágicos, podemos extraerlos en una variable significativa.

### 7. Usar nombres de dominio de solución
Si usas muchos tipos de datos diferentes en tu algoritmo o clase y no puedes distinguirlos a partir del propio nombre de la variable, no tengas miedo de agregar el sufijo del tipo de datos al nombre de la variable. Por ejemplo:
```python
# Esto está bien
lista_de_puntuaciones = [12, 33, 14, 24]
diccionario_de_palabras = {
    'm': 'manzana',
    'b': 'Banano',
    'c': 'cereza',
}
```
Y aquí hay un mal ejemplo (porque no puedes averiguar el tipo de datos a partir del nombre de la variable):
```python
# Esto está mal
nombres = ["Nick", "Mike", "John"]
```
### 8. No agregues contexto redundante
No agregue datos innecesarios a los nombres de las variables, especialmente si está trabajando con clases.
```python
# Esto está mal
class Persona:
    def __init__(self, primer_nombre_persona, apellido_persona, edad_persona):
        self.primer_nombre_persona = primer_nombre_persona
        self.apellido_persona = apellido_persona
        self.edad_persona = edad_persona


# Esto está bien
class Persona:
    def __init__(self, primer_nombre, apellido, edad):
        self.primer_nombre = primer_nombre
        self.apellido = apellido
        self.edad = edad
```
Ya estamos dentro de la clase Persona, por lo que no es necesario agregar un prefijo a cada variable de clase "_persona"

### 9. Evite números en nombres de variables

Si una variable tiene un número en el nombre, posiblemente signifique que es mejor utilizar un array 

```
# Esto está mal

pos1 = 34
pos2 = 5
pos3 = 89

# Esto está bien

posiciones = [ 34, 5, 89 ]

```


### 10. Estándares

Escriba los nombres de variables en Minúsculas y Utilice guión bajo _ (underscore) para separar las palabras.


```
# Esto está mal
PrimerNombre = 'Bob'
fechaCreacion = 1621535852

# Esto está bien
primer_nombre = 'Bob'
fecha_creacion = 1621535852
```


## Funciones
### 1. Usar verbos para los nombres de las funciones
### 2. No utilices palabras diferentes para el mismo concepto
Escoge una palabra para cada concepto y apégate a ella. El uso de diferentes palabras para el mismo concepto causará confusión.
```python
# Esto está mal
def obtener_nombre(): pass
def buscar_edad(): pass

# Esto está bien
def obtener_nombre(): pass
def obtener_edad(): pass
```
### 3. Escribe funciones cortas y sencillas
### 4. Las funciones solo deben realizar una sola tarea
Si su función contiene la palabra clave 'y', probablemente pueda dividirla en dos funciones. Veamos un ejemplo:
```python
# Esto está mal
def buscar_y_mostrar_personal():
    datos = # ...

    for persona in datos:
        print(persona)


# Esto está bien
def buscar_personal():
    return # ...

def mostrar_personal(datos):
    for persona in datos:
        print(persona)
```
Las funciones deben hacer una cosa y, como lector, hacen lo que esperas que hagan.

**Nota:  Una buena regla general es que cualquier función dada no debería tardar más de unos minutos en comprenderse. Regresa y revisa parte del código antiguo que escribiste hace unos meses. Probablemente debería refactorizar cualquier función que tarde más de cinco minutos en entender. Al fin y al cabo, este es tu código. Piensa en cuánto tiempo tardará otro desarrollador en entenderlo.**

### 5. Mantén tus argumentos al mínimo

Los argumentos de la función deben reducirse al mínimo. Idealmente, sus funciones solo deberían tener uno o dos argumentos. Si necesita proporcionar más argumentos a la función, puede crear un objeto de configuración que pase a la función o dividirlo en varias funciones.

Ejemplo:

```python
# Esto está mal
def renderizar_articulo_del_blog(titulo, autor, fecha_de_creacion, fecha_de_actualizacion, contenido):
    # ...

renderizar_articulo_del_blog("Clean code", "Nik Tomazic", 1622148362, 1622148362, "...")


# Esto está bien
class ArticuloDelBlog:
    def __init__(self, titulo, autor, fecha_de_creacion, fecha_de_actualizacion, contenido):
        self.titulo = titulo
        self.autor = autor
        self.fecha_de_creacion = fecha_de_creacion
        self.fecha_de_actualizacion = fecha_de_actualizacion
        self.contenido = contenido

articulo_del_blog1 = ArticuloDelBlog("Clean code", "Nik Tomazic", 1622148362, 1622148362, "...")

def renderizar_articulo_del_blog(articulo_del_blog):
    # ...

renderizar_articulo_del_blog(articulo_del_blog1)
```
### 6. No uses banderas en las funciones
Las banderas son variables (generalmente booleanas) que se pasan a las funciones, que la función utiliza para determinar su comportamiento. Se consideran un mal diseño porque las funciones solo deben realizar una tarea. La forma más fácil de evitar las banderas es dividir la función en funciones más pequeñas.
```python
texto = "Esta es una entrada de blog genial."


# Esto está mal
def transformar(texto, mayuscula):
    if mayusculas:
        return text.upper()
    else:
        return text.lower()

texto_mayuscula = transformar(texto, True)
texto_minuscula = transformar(texto, False)


# Esto está bien
def mayuscula(texto):
    return text.upper()

def minuscula(texto):
    return text.lower()

texto_mayuscula = mayuscula(texto)
texto_minuscula = minuscula(texto)
```
### 7. Evita los efectos secundarios
Una función produce un efecto secundario si hace cualquier cosa que no sea tomar un valor y devolver otro valor o valores. Por ejemplo, un efecto secundario podría ser escribir en un archivo o modificar una variable global.

### 8. Estándares

- Utiliza siempre minúsculas para los nombres de las funciones y usa underscores _ para separar palabras
- Utiliza parámetros nombrados para invocar funciones y evitar Magic Literals
- Al declarar las funciones, utiliza siempre pistas de tipo

```python

# Esto está mal
def transformar(texto, mayuscula):
    if mayusculas:
        return text.upper()
    else:
        return text.lower()

texto_mayuscula = transformar(texto, True)
texto_minuscula = transformar(texto, False)


# Esto está bien
def mayuscula(texto : str):
    return text.upper()

def minuscula(texto : str):
    return text.lower()

texto_mayuscula = mayuscula(texto = "Convierteme a Mayuscula" )
texto_minuscula = minuscula(texto = "QUIERO SER MINUSCULA" )
```



## Comentarios
No importa cuánto intentemos escribir código limpio, todavía habrá partes de su programa que necesiten una explicación adicional. Los comentarios nos permiten decirle rápidamente a otros desarrolladores (y a nosotros mismos del futuro) por qué lo escribimos de la manera en que lo hicimos. Ten en cuenta que agregar demasiados comentarios puede hacer que tu código sea más desordenado de lo que sería sin ellos.

### 1. No comentes un código malo, reescríbelo
Comentar el código incorrecto, es decir, solo te ayuda a corto plazo. Tarde o temprano, uno de tus colegas tendrá que trabajar con tu código y terminará reescribiéndolo después de pasar varias horas tratando de averiguar qué hace.

### 2. El código legible no necesita comentarios
Si tu código es lo suficientemente legible, no necesitas comentarios. Agregar comentarios inútiles solo hará que su código sea menos legible. He aquí un mal ejemplo:
```python
# Esto comprueba si el usuario con el ID dado no existe.
if not User.objects.filter(id=user_id).exists():
    return Response({
        'detalle': 'El usuario con este ID no existe.',
    })
```
Como regla general, si necesita agregar comentarios, deben explicar "por qué" hizo algo en lugar de "qué" está sucediendo.

### 3. No agregues comentarios de ruido
No agregues comentarios que no agreguen nada de valor al código. Esto es malo:
```python
numeros = [1, 2, 3, 4, 5]

#  Esta variable almacena la media de una lista de números.
media = sum(numeros) / len(numeros)
print(media)
```
### 4. Usa los tipos correctos de comentarios
La mayoría de los lenguajes de programación tienen diferentes tipos de comentarios. Aprenda sus diferencias y utilícelas en consecuencia. También debe aprender la sintaxis de la documentación de comentarios. Un buen ejemplo:
```python
def model_to_dict(instance, fields=None, exclude=None):
    """
    Devuelve un dict que contiene los datos en ``instance`` adecuado para pasar como
    argumento de la palabra clave ``initial`` de un formulario.
    ``fields`` es una lista opcional de nombres de campos. Si se proporciona, devuelve sólo los campos
    con nombre.
    ``exclude`` es una lista opcional de nombres de campos. Si se proporciona, excluye el campo
    del dict devuelto, incluso si están listados en el argumento ``fields``.
    argumento.
    """
    opts = instance._meta
    data = {}
    for f in chain(opts.concrete_fields, opts.private_fields, opts.many_to_many):
        if not getattr(f, 'editable', False):
            continue
        if fields is not None and f.name not in fields:
            continue
        if exclude and f.name in exclude:
            continue
        data[f.name] = f.value_from_object(instance)
    return data
```
### 5. No dejes código comentado
Lo peor que puedes hacer es dejar el código comentado en tus programas. Todo el código de depuración o los mensajes de depuración deben eliminarse antes de enviarlos a un sistema de control de versiones, de lo contrario, sus colegas tendrán miedo de eliminarlo y su código comentado permanecerá allí para siempre.

### 6. Usos correctos de los comentarios

#### Cómo una explicación de la intención. 
#### Cómo una aclaración del código. 
#### Cómo una advertencia de las consecuencias.

## Clases
Para mantener su código lo más organizado posible, debe dividirlo en varios archivos que luego se dividen en diferentes directorios. Si vas a escribir código en un lenguaje orientado a la programación orientada a la programación orientada a objetos pequeños, también debes seguir los principios básicos de programación orientada a objetos, como la encapsulación, la abstracción, la herencia y el polimorfismo.

### Alta Cohesión

Una clase debe tener una sola responsbilidad. Dicho de otras forma, no debe existir más de una razón para cambiar una clase. 

### Bajo Acoplamiento

Una clase debe depender del mínimo posible de otras clases. Sobre todo, evite la herencia siempre que sea posible.

### Estándar de nombres

El nombre de la clase debe responder a la pregunta ¿para qué #$%#%&%@ sirve?

Debe ser un sustantivo (con adjetivos que lo acompañen, si es necesario)

Debe usar el estándar CamelCase, según las guias de pythonic code

## Excepciones

### No mezcles el manejo de errores con el código. 

El código que controla una condición de error y dispara una excepción, debe estar encapsulado en su propia función.

### Usa excepciones en lugar de devolver códigos de error. 

Para eso son las excepciones, y por eso las amamos

### No devuelvas nulo, tampoco pases nulo. 

Es un indico de que se debe disparar una excepción o retornar un objeto siguiendo el patrón Null Object

### Lanza excepciones con contexto.

Dentro de cada excepción, debe incluirse la suficiente información para responder estas tres preguntas:

1. Qué sucedió
2. Por qué ocurrió
3. Dónde ocurrió
4. Cómo se soluciona