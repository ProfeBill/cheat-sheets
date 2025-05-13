# Flask


## Preliminares

Para la documentación completa de Flask, diríjase a https://flask.palletsprojects.com/en/3.0.x/quickstart/

El primer paso es instalar el framework Flask mediante el siguiente comando:

  pip install flask

Su aplicación debe contener un módulo principal que se llame app.py (puede tener otro nombre, pero requerirá hacer cambios en la forma en que ejcuta la aplicación)

## Escribiendo el servidor

Para convertir el módulo en un módulo web, importe el módulo Flask

```
from flask import Flask    
```

Necesitaremos una variable que represente a nuestra aplicación y nos dé acceso a la funcionalidad de Flask 

```
app = Flask(__name__)     
```

El mecanismo para convertir una función normal en un servicio web son los decoradores @app......

```
@app.route('/')      
def hello():
    return 'Hola Mundo Web!'
```

Y por último, si se va a ejecutar el módulo individualmente y no como parte de una aplicación web, se agrega 
al final del módulo la inicialización de la aplicación Flask

```
if __name__=='__main__':
   app.run()
```

## Ejecución

Puede ejecutar la aplicación directamente, pero tendría que reiniciar cada vez que haga cambios.

Si ejecuta flask directamente en modod debug, el detectará cada vez que haga cambios en el código
y recargará automáticamente.

Para ejecutar Flask en moddo Debug:

python3 -m flask run --debug