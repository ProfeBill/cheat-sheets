# Pastel de Pruebas Unitarias

## Pasos de una prueba
- Establezca las variables de entrada con los valores del caso de prueba
- Establezca el valor esperado de las variables de salida
- Invoque la funcionalidad a probar
- Verifique que las variables de salida tengan los valores esperados

## Bibliotecas a importar

Todas las pruebas unitarias importan la biblioteca unittest 

```
  import unittest
```

## Clase Conjunto de Pruebas

Debe existir por lo menos una clase que contenga las pruebas unitarias, descediente de unittest.TestCase

```
  class CreditCardTest(unittest.TestCase):
```

## Método Caso de Prueba

 Cada prueba unitaria es un metodo la clase Caso de Prueba

```
    def test_normal_1(self):
```

## Verificación del resultado de la prueba

Puede usar cualquiera de los siguientes métodos, dependiendo de la condición que deseaa verificar:

```
  # Prueba que dos variables sean iguales
  assertEqual(a, b)

  # Prueba que no sean iguales
  assertNotEqual(a, b)

  # Prueba que una variable booleana sea verdadera  
  assertTrue(x)

  # Prueba que una variable booleana sea falsa
  assertFalse(x)

  # Prueba que dos variables sean el mismo objeto
  assertIs(a, b)

  # Prueba que dos variables NO sean el mismo objeto
  assertIsNot(a, b)

  # Prueba que una variable sea None
  assertIsNone(x)

  # Prueba que una variable NO sea None
  assertIsNotNone(x)

  # Prueba que una variable pertenezca a un conjunto
  assertIn(a, b)

  # Prueba que una variable NO pertenezca a un conjunto
  assertNotIn(a, b)

  # Prueba que una variable sea instancia de un tipo
  assertIsInstance(a, b)

  # Prueba que una variable NO sea instancia de un tipo
  assertNotIsInstance(a, b)

## Control de Excepciones en los casos de error

La forma mas simple de controlar que un bloque de código si dispare una excepción
es mediante un bloque ```with``` y un llamado a ```assertRaises``` para verificar
que cierto tipo de excepción si se esté disparando.

```
    with self.assertRaises( PaymentLogic.ExcesiveInterestError ):
      PaymentLogic.calcPayment( purchase_amount, interest_rate, num_payments )
```

[Consulta: Pastel de Excepciones](exception.md)


## Ejecución de la prueba

Recuerde invocar en el código principal del módulo al método unittest.main()



``` 

if __name__ == '__main__':
    unittest.main()

```


# Ejemplo completo

```

  # Todas las prueba sunitarias importan la biblioteca unittest
import unittest

  # Las pruebas importan los modulos que hacen el trabajo
import PaymentLogic 


  # Debe existir por lo menos una clase que contenga las pruyebas unitarias
  # descediente de unittest.TestCase
class CreditCardTest(unittest.TestCase):

    # Cada prueba unitaria es un metodo la clase
    def test_normal_1(self):
        # Cada metodo de prueba debe llamar un metodo assert
        # para comprobar si la prueba pasa
        # Datos de Entrada
        purchase_amount = 200000
        interest_rate = 0.031
        num_payments = 36

        # Proceso
        result = PaymentLogic.calcPayment( purchase_amount, interest_rate, num_payments )

        # Datos de salida esperados
        expected = 9297.96

        # Prueba que dos variables sean iguales
        self.assertAlmostEqual( expected, result, 2  )

    # Prueba un caso de error, capturando manualmente la excepcion
    def test_excesive_interest( self ):
        # Entradas
        purchase_amount = 50000
        num_payments = 36
        interest_rate = 0.124

        testOk = False  # Bandera para indicar si la prueba es exitosa
        try:
            # llamar al proceso
            result = PaymentLogic.calcPayment( purchase_amount, interest_rate, num_payments )
            print("No ocurrió ningun excepcion")
            testOk = False
        except PaymentLogic.ExcesiveInterestError :
            # Aqui llega el control cuando se genera una excepcion
            print("SI ocurrio la excepcion")
            testOk = True

        self.assertTrue(  testOk, "No se disparó la excepcion esperada" )            

    # Prueba un caso de error usando assertRaises en una sola línea
    def test_excesive_interest_one_line( self ):
        # Entradas
        purchase_amount = 50000
        num_payments = 36
        interest_rate = 0.124

        # Verifica en una linea si una funcion dispara una excepcion
        self.assertRaises( PaymentLogic.ExcesiveInterestError, PaymentLogic.calcPayment, purchase_amount, interest_rate, num_payments  )

    # Prueba un caso de error, usando assertRaises y un bloque with
    def test_excesive_interest_with( self ):
        # Entradas
        purchase_amount = 50000
        num_payments = 36
        interest_rate = 0.124

        # Verifica si una funcion dispara una excepcion
        # Todas las instrucciones dentro del bloque with se evaluan primero
        # y luego el assertRaises
        with self.assertRaises( PaymentLogic.ExcesiveInterestError ):
          PaymentLogic.calcPayment( purchase_amount, interest_rate, num_payments )

    def test_purchase_zero( self ):
        # Entradas
        purchase_amount = 0
        num_payments = 60
        interest_rate = 0.024

        # Verifica en una linea si una funcion dispara una excepcion por no haber compra
        with self.assertRaises( PaymentLogic.InvalidPurchaseException ):
          PaymentLogic.calcPayment( purchase_amount, interest_rate, num_payments )


  # Este fragmento de codigo permite ejecutar la prueb individualmente
  # Va fijo en todas las pruebas

if __name__ == '__main__':
    unittest.main()

```