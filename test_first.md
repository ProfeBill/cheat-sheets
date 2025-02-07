# Test First Development

Es una filosofía de desarrollo (no una metodología) que se basa en el principio de primero deben escribirse las pruebas del software, antes de escribir el código.

Este enfoque ayuda a mejorar la calidad, pues se garantiza que siempre se escriban y ejecuten pruebas al software, y no se caiga en la tentación de posponerlas o conformarse con no escribirlas.

La filosofía Test First es una simplificación de la metodología [Test Driven Development](https://en.wikipedia.org/wiki/Test-driven_development), propuesta por Kent Beck a finales del siglo pasado.


[Metodología TDD](https://testdriven.io/test-driven-development/)

[TDD en Python](https://docs.python.org/3/library/unittest.html)


## Principios

-	Los casos de prueba son lo primero que debe escribirse antes de comenzar a programar, al hacerlo, se asegura que se comprenda completamente el problema. Una vez escrito el programa, ya sabemos como verificar que sea correcto
- Solo has entendido el problema, cuando puedes escribir suficientes pruebas
- Todo programa solo tiene una forma correcta de funcionar, pero infinitas formas de fallar
- La calidad no solo está en lo bien que se escriba el código, sino en la cantidad de pruebas que se le hagan
- Un programa "Robusto" es aquel que puede manejar una gran cantidad de situaciones de error y continuar funcionando 


## TDD paso a paso: El semáforo 

[![](https://mermaid.ink/img/pako:eNpVkUFOwzAQRa8y8rpdUGDjBVJF2bEqrJClysST1MKxw9gGVVVPxRG4GJM4SUkW0cz_T3_s8VlUwaCQIiadcGd1Q7pdf22UB_6MJaySDR6e98oPWuV0jDusgdBAbZ2TXCydhhB98YZy6Z7QufBd7FKPyVBr60DCBrYRm0ya4DMjq85hATqOYOBuBg4MHFgdfcJaVykQM_ewH5tF-nr9MKXcwlOsyL5bgsffH2Ob8G9Iz9EcsMjurfGkN7DlCzZ80OzhFWMqaPkPFy7ktKFRGyZcNzOq84BpKb0lVqJFarU1_ETnXlMiHbFFJSSXRtOHEspfmNM5hZeTr4RMlHElKOTmKCSvL3KXO3N931nttH8LYeovf4p3rmM?type=png)](https://mermaid.live/edit#pako:eNpVkUFOwzAQRa8y8rpdUGDjBVJF2bEqrJClysST1MKxw9gGVVVPxRG4GJM4SUkW0cz_T3_s8VlUwaCQIiadcGd1Q7pdf22UB_6MJaySDR6e98oPWuV0jDusgdBAbZ2TXCydhhB98YZy6Z7QufBd7FKPyVBr60DCBrYRm0ya4DMjq85hATqOYOBuBg4MHFgdfcJaVykQM_ewH5tF-nr9MKXcwlOsyL5bgsffH2Ob8G9Iz9EcsMjurfGkN7DlCzZ80OzhFWMqaPkPFy7ktKFRGyZcNzOq84BpKb0lVqJFarU1_ETnXlMiHbFFJSSXRtOHEspfmNM5hZeTr4RMlHElKOTmKCSvL3KXO3N931nttH8LYeovf4p3rmM)

- Comience por escribir una prueba 
- Asegúrese de que la prueba falle
- Escriba el código mínimo para que la prueba pase
- Ejecute la prueba y verifique que pase
- Haga refactoring para asegurarse de que el código cumple las condiciones de Clean Code

## Pasos de una prueba
- Establezca las variables de entrada con los valores del caso de prueba
- Establezca el valor esperado de las variables de salida
- Invoque la funcionalidad a probar
- Verifique que las variables de salida tengan los valores esperados
 

## Test Case

**Definición**

Es un caso documentado de los resultados esperados de la ejecución de un artefacto de software, dado un conjunto específico de entradas que se le provean

**¿Por qué molestarse en construirlos?**

- Garantizan que el usuario haya definido correctamente lo que debe hacer el software 

- Ayudan a que el desarrollador comprenda correctamente los resultados esperados del software
 
- Proporcionan una forma objetiva de verificar si el software cumple con lo que se espera de él
 
- Permiten que se pueda probar el software a futuro cuando sea modificado
 
- Ayudan a escribir la documentación y facilitan la capacitación práctica de los usuarios finales cuando el software sea entregado

### Elementos de un Caso de Prueba

[![](https://mermaid.ink/img/pako:eNo9jDsKwzAQBa8itrLBvoCKVEmXIsRdULNI6w9IWrNeEYLx3SNCkm5meLwdPAcCC2Pkp59R1FzvLl-yCgY0fX8yN2FPGzfNF9r2kweMS0DoIJEkXEL92F02xoHOlMiBrRhoxBLVgctHnWJRHl7Zg1Up1IFwmWawI8atWlkDKp0XnATTv66YH8w_P95cDTvA?type=png)](https://mermaid.live/edit#pako:eNo9jDsKwzAQBa8itrLBvoCKVEmXIsRdULNI6w9IWrNeEYLx3SNCkm5meLwdPAcCC2Pkp59R1FzvLl-yCgY0fX8yN2FPGzfNF9r2kweMS0DoIJEkXEL92F02xoHOlMiBrRhoxBLVgctHnWJRHl7Zg1Up1IFwmWawI8atWlkDKp0XnATTv66YH8w_P95cDTvA)

1. Identidad (Nombre o Número)
2. Datos de Entrada
3. Datos de Salida

### Ejemplos

#### Caso 1

Caso de prueba para el cálculo del valor a pagar por una compra

**Entradas**

- Precio un articulo $ 10000
- Porcentaje de IVA 19%
- Cantidad adquirida #5

**Salidas**

- Valor a pagar $59.500

#### Caso 2

Caso de prueba para al cálculo de la cuota de una compra con tarjeta de crédito

**Entradas**

- Valor de la compra $200.000
- Tasa de interés M.V. $3.1%$
- Número de Cuotas #36

**Salidas**

- Cuota mensual $9.298

La cuota se calcula asi: (P * i) / (1 - (1 + i) ** (-n))

#### Caso 3        

Caso de prueba para el retorno de la inversión de publicidad en YouTube

**Entradas**

- Costo por anuncio   $            3.00 
- Vistas esperadas atraídas por cada anuncio   0.2
- Ingresos por cada vista    $            0.00048 
- Valor total a invertir en anuncios   $  12,500.00 

**Salidas**
- Total anuncios adquiridos  4166.66667 
- Vistas totales esperadas  833.333333
- Total ingresos esperados   $            0.40     

### Clasificación de los Casos de prueba 

#### Normales

Corresponden a las entradas que normalmente el usuario va a ingresar en la mayoría de los casos

No deben arrojar error ni interrumpir la ejecución del código

#### Extraordinarios

Corresponden a casos donde el usuario ingresa valores poco comunes de las variables de entrada, pero posibles.

No deben arrojar error ni interrumpir al ejecución del código

Pueden exigir modificaciones al código para manejar esos casos extraordinarios

#### Error

Corresponden a valores de entrada que impiden la ejecución del código y que deben notificarse al usuario

Interrumpen la ejecución del programa y la funcionalidad debe disparar una Excepción

Las verificaciones de esas condiciones de error siempre se hacen al comienzo de cada funcionalidad


### Características de un buen Caso de Prueba
			
- **Simple** : Que pueda entenderlo un niño de 5 años
- **Completo** : Debe incluir explícitamente todas las variables y evitar cualquier supuesto 
- **Concreto** : Debe incluir solo los datos verdaderamente relevantes
- **Objetivo** : Cualquier persona involucrada en el proyecto debe poder entenderlo igual que otra sin lugar a ambigüedades ni interpretaciones personales
- **Repetible** : Cada vez que se ejecute el caso de prueba, debe arrojar los mismo resultados
- **Automatizable** : Debe ser susceptible de ser ejecutado en forma de un artefacto de software

### Consejos prácticos para escribir buenos TC

- Si no hay caso de prueba, no hay nada que escribir
- Sólo se puede automatizar, lo que se pueda hacer manual
- Si el caso de prueba es diferente, el programa es diferente
- Una vez caso de prueba y programa se construyan y funcionen NUNCA los cambie
- La calidad del software es proporcional a la cantidad de casos de prueba que se escriban para él
