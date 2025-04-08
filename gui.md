# Buenas prácticas para crear una Interfaz de Usuario Gráfica

## Las tres preguntas que el usuario se hace cuando esta mirando su aplicación:

### ¿Dónde estoy?

Indique en todo momento en que parte de la aplicación se encuentra ( y en qué aplicacón se encuentra)

### ¿Qué se espera que haga aqui?

La interfaz de usuario debe expresar claramente  al usuario cuál es el propósito de la opción donde el usuario se encuentra ubicado (qué puede hacer) y cómo hacerlo (qué debe hacer) para que se logre el objetivo.

Esto incluye indicarle que requisitos previos debe cumplir, que información debe ingresar y qué condiciones debe cumplir la información que ingrese.

### ¿Dónde consigo ayuda si me pierdo?

Provea mensajes en la misma aplicación que le indiquen dónde puede leer la documentación o contactar al personal de soporte, sobre todo **en los mensajes de error**

## El Secreto de una Interfaz de Usuario que no produce WTF: EL USUARIO PUEDE COMETER ERRORES

- La aplicación no debe fallar, abortar, volverse inestable cuando el usuario se equivoque, debe permanecer disponible para que el usuario pueda equivocarse de nuevo.
- Permita que el usuario se equivoque, hasta que aprenda como usar la aplicación 
- Cuando el usuario se equivoque, entregue mensajes de error que le ayuden a aprender y salir del problema. Esos mensajes deben responder a tres preguntas:
  - Qué pasó: Ponerle un nombre al error que sucedió. Ese nombre debe describir al problmea para que pueda ser identificado por el usuario cada vez que suceda, o por el personal de soporte. En algunos sistemas avanzados, incluso hay códigos únicos que identifican al error.
  - Por qué pasó: Describa que fue lo que hizo mal el usuario o lo que está mal en el sistema que no permite continuar.
  - Cómo lo soluciono: Indique al usuario las acciones que debe llevar a cabo para solucionar el error y dónde encontrar ayuda si no lo logra  


