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
apellido_cliente = 'Smith'

# Esto está bien
primer_nombre_cliente = 'Bob'
apellido_cliente = 'Smith'
```
## Comentarios

## Funciones

## Clases

## Pruebas
