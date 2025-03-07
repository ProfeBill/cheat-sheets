# Separación de Responsabilidades y el modelo MVC


## Principio

*Todo problema complejo se puede solucionar si se divide en una serie de problemas mas sencillos*

## Responsabilidades de cada componente

### Model

* Conceptos del Dominio del Problema
* Funcionalidad
* Control de Errores
* Casos de Uso

### View

* Entrada y Salida al usuario
* Validaciones de Datos ingresados
* Depende de la tecnologia de UI utilizada

### Controller
    
* Comunicación con la base de datos
* Data Access Objects
* Object Relational Mapping
* CRUD: Create, Read,Update, Delete
            
## Reglas de Acoplamiento

* Modelo no puede usar ni Vista ni Controlador
* Controlador puede usar a Modelo, pero no a Vista
* Vista puede usar a Modelo y a Controlador
* Solo Controlador se puede comunicar con la Base de Datos

## Estructura sugerida de carpetas

```python
myproject/
├── src/
|    ├── model/
|    │   ├── __init__.py
|    │   ├── logic.py
|    │   ├── more_logic.py
|    │   └── other_logic.py
|    ├── view/
|    │   ├── console
|    |   |   └─ main.py
|    │   ├── gui
|    |   |   └─ kivy.py
|    │   └── web
|    |       └─ app.py
|    └── controller/
|    │   ├── __init__.py
|        ├── urls.py
|        └── blueprints.py
├── tests
├── .gitignore
├── config.py
└── README.MD
```

## Ajustes para importar módulos correctamente en Python

### Convertir carpetas en módulos

Para convertir un carpeta en un módulo que pueda ser importado, 
cree un archivo llamado `__init__.py` en la carpeta (no necesita contener nada).

### Importación de modulos desde la carpeta src

Para importar los módulo dentro de la carpeta src, agregue esta carpeta a la ruta de búsqueda
de Python incluyedo las siguientes líneas antes de importar en cada módulo

```

import sys 
sys.path.append("src")

# Luego puede importar normalmente
from model import logic
```

### Agregar rutas de busqueda a Python en Visual Studio Code

Edite el archivo settings.json y agregue estas entradas:

```
    "python.autoComplete.extraPaths": [
       "src"
    ],
    "python.analysis.extraPaths": [
        "src"
    ],
```
