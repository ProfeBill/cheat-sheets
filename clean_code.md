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
generar_fecha_y_hora = datetime.strptime('04/27/95 07:14:22', '%m/%d/%y %H:%M:%S')
```
### 4. Evita el uso de abreviaturas ambiguas
No trates de inventar tus propias abreviaturas. Es mejor que una variable tenga un nombre más largo que un nombre confuso.
```python
# Esto está mal
pn = 'Bob'
fc = 1621535852

# Estp está bien
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
ID_ESTUDIANTES = 36

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
text = "This is a cool blog post."


# This is bad
def transform(text, uppercase):
    if uppercase:
        return text.upper()
    else:
        return text.lower()

uppercase_text = transform(text, True)
lowercase_text = transform(text, False)


# This is good
def uppercase(text):
    return text.upper()

def lowercase(text):
    return text.lower()

uppercase_text = uppercase(text)
lowercase_text = lowercase(text)
```
## Comentarios

## Clases

## Pruebas
