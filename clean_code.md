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

### 9. Estándares

Escriba los nombres de variables en Minúsculas y Utilice guión bajo _ (underscore) para separar las palabras.


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

## Clases
Para mantener su código lo más organizado posible, debe dividirlo en varios archivos que luego se dividen en diferentes directorios. Si vas a escribir código en un lenguaje orientado a la programación orientada a la programación orientada a objetos pequeños, también debes seguir los principios básicos de programación orientada a objetos, como la encapsulación, la abstracción, la herencia y el polimorfismo.

Dividir el código en varias clases hará que el código sea más fácil de entender y mantener. No hay una regla fija sobre la longitud que debe tener un archivo o una clase, pero haga todo lo posible para mantenerlos pequeños (preferiblemente menos de 200 líneas).

La estructura de proyecto predeterminada de Django es un buen ejemplo de cómo debería estructurarse su código:

```python
awesomeproject/
├── main/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── blog/
│   ├── migrations/
│   │   └── __init__.py
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
└── templates
```
Django es un marco MTV (Modelo - Plantilla - Vista), que es similar a un marco MVC que discutimos anteriormente. Este patrón divide la lógica del programa en tres partes interconectadas. Puede ver que cada aplicación está en un directorio separado y cada archivo sirve para una cosa específica. Si su proyecto está dividido en varias aplicaciones, debe asegurarse de que las aplicaciones no dependan demasiado unas de otras.
## Pruebas
Las pruebas automatizadas siempre han sido un tema candente en el desarrollo de software, pero en la era de la integración continua y los microservicios, se habla aún más de ellas. Hay muchas herramientas que pueden ayudarte a escribir, ejecutar y evaluar tus pruebas en tus proyectos de Python. Echemos un vistazo a algunos de ellos.

### Pytest
Mientras que la biblioteca estándar de Python viene con un marco de pruebas unitarias llamado ùnittest, pytest es el marco de pruebas de referencia para probar el código de Python.

pytest hace que sea fácil (¡y divertido!) escribir, organizar y ejecutar pruebas. Cuando se compara con unittest, de la biblioteca estándar de Python, pytest:
1. Requiere menos código repetitivo, por lo que los conjuntos de pruebas serán más legibles.
2. Admite la instrucción simple, que es mucho más legible y fácil de recordar en comparación con los métodos -- como , , y -- en unittest.assert assertSomething assertEquals assertTrue assertContains
3. Se actualiza con más frecuencia ya que no forma parte de la biblioteca estándar de Python.
4. Simplifica la configuración y el desmontaje del estado de prueba con su sistema de accesorios.
5. Utiliza un enfoque funcional.

Además, con pytest, puedes tener un estilo coherente en todos tus proyectos de Python. Digamos que tienes dos aplicaciones web en tu pila, una construida con Django y la otra construida con Flask. Sin pytest, lo más probable es que aproveches el marco de pruebas de Django junto con una extensión de Flask como Flask-Testing. Por lo tanto, los conjuntos de pruebas tendrían diferentes estilos. Con pytest, por otro lado, ambos conjuntos de pruebas tendrían un estilo consistente, lo que facilitaría saltar de uno a otro.
Pytest también tiene un gran ecosistema de plugins mantenido por la comunidad.

Algunos ejemplos:
1. pytest-django - proporciona un conjunto de herramientas hechas específicamente para probar aplicaciones de Django
2. pytest-xdist - se utiliza para ejecutar pruebas en paralelo
3. pytest-cov: agrega compatibilidad con cobertura de código
4. pytest-instafail: muestra los fallos y errores inmediatamente en lugar de esperar hasta el final de una ejecución.

### Mocking
Las pruebas automatizadas deben ser rápidas, aisladas/independientes y deterministas/repetibles. Por lo tanto, si necesita probar el código que realiza una solicitud HTTP externa a una API de terceros, realmente debe simular la solicitud. ¿Por qué? Si no lo haces, entonces esa prueba específica será:
1. Lento ya que está haciendo una solicitud HTTP a través de la red
2. Dependiendo del servicio de terceros y de la velocidad de la propia red
3. No determinista, ya que la prueba podría arrojar un resultado diferente en función de la respuesta de la API

La simulación es la práctica de reemplazar objetos reales con objetos simulados, que imitan su comportamiento, en tiempo de ejecución. Por lo tanto, en lugar de enviar una solicitud HTTP real a través de la red, simplemente devolvemos una respuesta esperada cuando se llama al método simulado.
Por ejemplo:
```python
import requests


def get_my_ip():
    response = requests.get(
        'http://ipinfo.io/json'
    )
    return response.json()['ip']


def test_get_my_ip(monkeypatch):
    my_ip = '123.123.123.123'

    class MockResponse:

        def __init__(self, json_body):
            self.json_body = json_body

        def json(self):
            return self.json_body

    monkeypatch.setattr(
        requests,
        'get',
        lambda *args, **kwargs: MockResponse({'ip': my_ip})
    )

    assert get_my_ip() == my_ip
```
**¿Qué está pasando aquí?**

Usamos el accesorio monkeypatch de pytest para reemplazar todas las llamadas al método desde el módulo con la devolución de llamada que siempre devuelve una instancia de .get requests lambda MockedResponse
**Usamos un objeto porque devuelve un objeto Response.requests**
Podemos simplificar las pruebas con el método create_autospec del módulo. Este método crea un objeto ficticio con las mismas propiedades y métodos que el objeto pasado como parámetro:unittest.mock
```python
from unittest import mock

import requests
from requests import Response


def get_my_ip():
    response = requests.get(
        'http://ipinfo.io/json'
    )
    return response.json()['ip']


def test_get_my_ip(monkeypatch):
    my_ip = '123.123.123.123'
    response = mock.create_autospec(Response)
    response.json.return_value = {'ip': my_ip}

    monkeypatch.setattr(
        requests,
        'get',
        lambda *args, **kwargs: response
    )

    assert get_my_ip() == my_ip
```
Aunque pytest recomienda el enfoque monkeypatch para simular, la extensión pytest-mock y la biblioteca unittest.mock vanilla de la biblioteca estándar también son buenos enfoques.
### Code Coverage
Otro aspecto importante de las pruebas es la cobertura del código. Es una métrica que indica la relación entre el número de líneas ejecutadas durante las ejecuciones de prueba y el número total de todas las líneas de la base de código. Para ello podemos utilizar el plugin pytest-cov, que Coverage.py integra con pytest.

Una vez instalado, para ejecutar pruebas con informes de cobertura, agregue la opción de la siguiente manera:--cov
```python
$ python -m pytest --cov=.
```
Producirá una salida como la siguiente:
```
================================== test session starts ==================================
platform linux -- Python 3.7.9, pytest-5.4.3, py-1.9.0, pluggy-0.13.1
rootdir: /home/johndoe/sample-project
plugins: cov-2.10.1
collected 6 items

tests/test_sample_project.py ....                                             [ 66%]
tests/test_sample_project_mock.py .                                           [ 83%]
tests/test_sample_project_mock_1.py .                                         [100%]

----------- coverage: platform linux, python 3.7.9-final-0 -----------
Name                                  Stmts   Miss  Cover
---------------------------------------------------------
sample_project/__init__.py                1      1     0%
tests/__init__.py                         0      0   100%
tests/test_sample_project.py              5      0   100%
tests/test_sample_project_mock.py        13      0   100%
tests/test_sample_project_mock_1.py      12      0   100%
---------------------------------------------------------
TOTAL                                    31      1    97%


==================================  6 passed in 0.13s ==================================
```

Por cada archivo en la ruta del proyecto, obtienes:

1. Stmts - número de líneas de código
2. Error: número de líneas que no fueron ejecutadas por las pruebas
3. Cover: porcentaje de cobertura del archivo
En la parte inferior, hay una línea con los totales de todo el proyecto.
Tenga en cuenta que, aunque se recomienda lograr un alto porcentaje de cobertura, eso no significa que las pruebas sean buenas, ya que prueban cada una de las rutas de acceso felices y excepcionales del código. Por ejemplo, las pruebas con aserciones como pueden lograr un alto porcentaje de cobertura, pero el código aún no se ha probado prácticamente porque no se cubren las rutas de acceso de excepción.assert sum(3, 2) == 5

### Mutation Testing
Las pruebas de mutación ayudan a garantizar que las pruebas cubran realmente el comportamiento completo del código. Dicho de otra manera, analiza la efectividad o robustez de su conjunto de pruebas. Durante las pruebas de mutación, una herramienta itera a través de cada línea de su código fuente, realizando pequeños cambios (llamados mutaciones) que deberían romper su código. Después de cada mutación, la herramienta ejecuta las pruebas unitarias y comprueba si las pruebas fallan o no. Si las pruebas siguen siendo superadas, el código no ha sobrevivido a la prueba de mutación.

Por ejemplo, supongamos que tiene el siguiente código:
```python
if x > y:
    z = 50
else:
    z = 100
```
La herramienta de mutación puede cambiar el operador así:> >=
```python
if x >= y:
    z = 50
else:
    z = 100
```
mutmut es una biblioteca de pruebas de mutaciones para Python. Veámoslo en acción.

Supongamos que tienes la siguiente clase:Loan
```python
# loan.py

from dataclasses import dataclass
from enum import Enum


class LoanStatus(str, Enum):
    PENDING = "PENDING"
    ACCEPTED = "ACCEPTED"
    REJECTED = "REJECTED"


@dataclass
class Loan:
    amount: float
    status: LoanStatus = LoanStatus.PENDING

    def reject(self):
        self.status = LoanStatus.REJECTED

    def rejected(self):
        return self.status == LoanStatus.REJECTED
```
Ahora, supongamos que desea rechazar automáticamente las solicitudes de préstamo que superan las 250.000:
```python
# reject_loan.py

def reject_loan(loan):
    if loan.amount > 250_000:
        loan.reject()

    return loan
```
A continuación, escribió la siguiente prueba:
```python
# test_reject_loan.py

from loan import Loan
from reject_loan import reject_loan


def test_reject_loan():
    loan = Loan(amount=100_000)

    assert not reject_loan(loan).rejected()
```
Cuando realices pruebas de mutación con mutmut, verás que tienes dos mutantes supervivientes:
```
$ mutmut run --paths-to-mutate reject_loan.py --tests-dir=.

- Mutation testing starting -

These are the steps:
1. A full test suite run will be made to make sure we
   can run the tests successfully and we know how long
   it takes (to detect infinite loops for example)
2. Mutants will be generated and checked

Results are stored in .mutmut-cache.
Print found mutants with `mutmut results`.

Legend for output:
🎉 Killed mutants.   The goal is for everything to end up in this bucket.
⏰ Timeout.          Test suite took 10 times as long as the baseline so were killed.
🤔 Suspicious.       Tests took a long time, but not long enough to be fatal.
🙁 Survived.         This means your tests needs to be expanded.
🔇 Skipped.          Skipped.

1. Running tests without mutations
⠏ Running...Done

2. Checking mutants
⠸ 2/2  🎉 0  ⏰ 0  🤔 0  🙁 2  🔇 0
```
Puedes ver los mutantes supervivientes por ID:
```
$ mutmut show 1

--- reject_loan.py
+++ reject_loan.py
@@ -1,7 +1,7 @@
 # reject_loan.py

 def reject_loan(loan):
-    if loan.amount > 250_000:
+    if loan.amount >= 250_000:
         loan.reject()

     return loan
```
```
$ mutmut show 2

--- reject_loan.py
+++ reject_loan.py
@@ -1,7 +1,7 @@
 # reject_loan.py

 def reject_loan(loan):
-    if loan.amount > 250_000:
+    if loan.amount > 250001:
         loan.reject()

     return loan
```
Mejore su prueba:
```python
from loan import Loan
from reject_loan import reject_loan


def test_reject_loan():
    loan = Loan(amount=100_000)
    assert not reject_loan(loan).rejected()

    loan = Loan(amount=250_001)
    assert reject_loan(loan).rejected()

    loan = Loan(amount=250_000)
    assert not reject_loan(loan).rejected()
```
Si vuelves a realizar pruebas de mutación, verás que no ha sobrevivido ninguna mutación:

```

$ mutmut run --paths-to-mutate reject_loan.py --tests-dir=.

- Mutation testing starting -

These are the steps:
1. A full test suite run will be made to make sure we
   can run the tests successfully and we know how long
   it takes (to detect infinite loops for example)
2. Mutants will be generated and checked

Results are stored in .mutmut-cache.
Print found mutants with `mutmut results`.

Legend for output:
🎉 Killed mutants.   The goal is for everything to end up in this bucket.
⏰ Timeout.          Test suite took 10 times as long as the baseline so were killed.
🤔 Suspicious.       Tests took a long time, but not long enough to be fatal.
🙁 Survived.         This means your tests needs to be expanded.
🔇 Skipped.          Skipped.

1. Running tests without mutations
⠏ Running...Done

2. Checking mutants
⠙ 2/2  🎉 2  ⏰ 0  🤔 0  🙁 0  🔇 0
```
Ahora su prueba es mucho más robusta. Cualquier cambio involuntario dentro de reject_loan.py producirá una prueba fallida.

**NOTA: Las herramientas de prueba de mutaciones para Python no son tan maduras como algunas de las otras que existen. Por ejemplo, mutant es una herramienta de prueba de mutación madura para Ruby.**


Al igual que con cualquier otro enfoque, las pruebas de mutación tienen una compensación. Si bien mejora la capacidad de su conjunto de pruebas para detectar errores, tiene el costo de la velocidad, ya que tiene que ejecutar todo su conjunto de pruebas cientos de veces. También te obliga a probarlo todo. Esto puede ayudar a descubrir rutas de acceso de excepciones, pero tendrá muchos más casos de prueba que mantener.

### Hypothesis
Hypothesis es una biblioteca para realizar pruebas basadas en propiedades en Python. En lugar de tener que escribir diferentes casos de prueba para cada argumento que desee probar, las pruebas basadas en propiedades generan una amplia gama de datos de prueba aleatorios que dependen de las ejecuciones de pruebas anteriores. Esto ayuda a aumentar la solidez de su conjunto de pruebas al tiempo que disminuye la redundancia de las pruebas. En resumen, su código de prueba será más limpio, más seco y, en general, más eficiente, sin dejar de cubrir una amplia gama de datos de prueba.

Por ejemplo, supongamos que tiene que escribir pruebas para la siguiente función:
```python
def increment(num: int) -> int:
    return num + 1
```
Podrías escribir la siguiente prueba:
```python
import pytest


@pytest.mark.parametrize(
    'number, result',
    [
        (-2, -1),
        (0, 1),
        (3, 4),
        (101234, 101235),
    ]
)
def test_increment(number, result):
    assert increment(number) == result
```
No hay nada de malo en este enfoque. Su código está probado y la cobertura del código es alta (100% para ser exactos). Dicho esto, ¿qué tan bien se prueba el código en función de la gama de entradas posibles? Hay bastantes números enteros que se podrían probar, pero solo cuatro de ellos se utilizan en la prueba. En algunas situaciones, esto es suficiente. En otras situaciones, cuatro casos no son suficientes, es decir, código de aprendizaje automático no determinista. ¿Qué pasa con los números realmente pequeños o grandes? O digamos que su función toma una lista de números enteros en lugar de un solo número entero: ¿qué pasa si la lista está vacía o contiene un elemento, cientos de elementos o miles de elementos? En algunas situaciones, simplemente no podemos proporcionar (y mucho menos siquiera pensar) en todos los casos posibles. Ahí es donde entran en juego las pruebas de base de propiedades.

**NOTA: Los algoritmos de aprendizaje automático son un gran caso de uso para las pruebas basadas en propiedades, ya que es difícil producir (y mantener) ejemplos de pruebas para conjuntos complejos de datos.**

Los marcos de trabajo como Hypothesis proporcionan recetas (Hypthesis las llama estrategias) para generar datos de prueba aleatorios. Hypothesis también almacena los resultados de las ejecuciones de pruebas anteriores y los utiliza para crear nuevos casos.

**NOTA: Las estrategias son algoritmos que generan datos pseudoaleatorios basados en la forma de los datos de entrada. Es pseudoaleatorio porque los datos generados se basan en datos de pruebas anteriores.**

La misma prueba que utiliza pruebas basadas en propiedades a través de hipótesis tiene el siguiente aspecto:
```python
from hypothesis import given
import hypothesis.strategies as st


@given(st.integers())
def test_add_one(num):
    assert increment(num) == num - 1
```
st.integers() es una estrategia de hipótesis que genera números enteros aleatorios para realizar pruebas mientras que el decorador se utiliza para parametrizar la función de prueba. Por lo tanto, cuando se llama a la función de prueba, los enteros generados, de la estrategia, se pasarán a la prueba. @given
```
$ python -m pytest test_hypothesis.py --hypothesis-show-statistics

================================== test session starts ===================================
platform darwin -- Python 3.8.5, pytest-6.1.1, py-1.9.0, pluggy-0.13.1
rootdir: /home/johndoe/sample-project
plugins: hypothesis-5.37.3
collected 1 item

test_hypothesis.py .                                                               [100%]
================================= Hypothesis Statistics ==================================

test_hypothesis.py::test_add_one:

  - during generate phase (0.06 seconds):
    - Typical runtimes: < 1ms, ~ 50% in data generation
    - 100 passing examples, 0 failing examples, 0 invalid examples

  - Stopped because settings.max_examples=100


=================================== 1 passed in 0.08s ====================================
```
### Type Checking
Las pruebas son código y deben tratarse como tales. Al igual que su código de negocio, debe mantenerlos y refactorizarlos. Es posible que incluso tenga que lidiar con errores de vez en cuando. Debido a esto, es una buena práctica mantener sus pruebas cortas, simples y directas al grano. También debe tener cuidado de no probar demasiado su código.

Los comprobadores de tipos en tiempo de ejecución (o dinámicos), como Typeguard y pydantic, pueden ayudar a minimizar el número de pruebas. Echemos un vistazo a un ejemplo de esto con pydantic.

Por ejemplo, supongamos que tenemos un que tiene un solo atributo, una dirección de correo electrónico: User
```python
class User:

    def __init__(self, email: str):
        self.email = email


user = User(email='john@doe.com')
```
Queremos estar seguros de que el correo electrónico proporcionado es realmente una dirección de correo electrónico válida. Entonces, para validarlo, tendremos que agregar algún código auxiliar en algún lugar. Junto con escribir una prueba, también tendremos que dedicar tiempo a escribir la expresión regular para esto. Pydantic puede ayudar con esto. Podemos usarlo para definir nuestro modelo: User
```

from pydantic import BaseModel, EmailStr


class User(BaseModel):
    email: EmailStr


user = User(email='john@doe.com')
```
Ahora, el argumento email será validado por pydantic antes de que se cree cada nueva instancia. Cuando no es un correo electrónico válido, es decir, se generará un ValidationError. Esto elimina la necesidad de escribir nuestro propio validador. Tampoco necesitamos probarlo, ya que los mantenedores de pydantic se encargan de eso por nosotros.UserUser(email='something')

Podemos reducir el número de pruebas para cualquier dato proporcionado por el usuario. Y, en su lugar, solo tenemos que probar que a se maneja correctamente.ValidationError

Veamos un ejemplo rápido en una aplicación Flask:
```python
import uuid

from flask import Flask, jsonify
from pydantic import ValidationError, BaseModel, EmailStr, Field


app = Flask(__name__)


@app.errorhandler(ValidationError)
def handle_validation_exception(error):
    response = jsonify(error.errors())
    response.status_code = 400
    return response


class Blog(BaseModel):
    id: str = Field(default_factory=lambda: str(uuid.uuid4()))
    author: EmailStr
    title: str
    content: str
```
Prueba:
```pyython
import json


def test_create_blog_bad_request(client):
    """
    GIVEN request data with invalid values or missing attributes
    WHEN endpoint /create-blog/ is called
    THEN it should return status 400 and JSON body
    """
    response = client.post(
        '/create-blog/',
        data=json.dumps(
            {
            'author': 'John Doe',
            'title': None,
            'content': 'Some extra awesome content'
        }
        ),
        content_type='application/json',
    )

    assert response.status_code == 400
    assert response.json is not None
```
### Conclusión
Las pruebas a menudo pueden parecer una tarea desalentadora. Siempre hay ocasiones en las que puede serlo, pero esperamos que este artículo te haya proporcionado algunas herramientas que puedes utilizar para facilitar las pruebas. Concentre sus esfuerzos de prueba en disminuir las pruebas escamosas. Las pruebas también deben ser rápidas, aisladas/independientes y deterministas/repetibles. Al final, tener confianza en su conjunto de pruebas le ayudará a implementar en producción con más frecuencia y, lo que es más importante, le ayudará a dormir por la noche.
