
# Pastel de Comandos de la Terminal Windows (y Linux)

![Funciona en mi localhost](img/enmilocal.jpg)

## Cómo abrir una ventana de Comandos

- Método 1: Use la tecla Windows|R y digite `cmd`
- Método 2: Ingrese al menú inicio de windows y escriba `cmd` para buscar el ícono de la ventana de comandos
- Método 3: En el explorador de Windows, ubíquese en la carpeta donde desea trabajar y presione la tecla `F4` para entrar a la barra de dirección (o haga click sobre la barra de dirección), a continuación escriba `cmd` y pulse `ENTER`. Esté método tiene la ventaja de abrir la ventana de comandos ubicada directamente en la carpeta dónde se desea trabajar.

**NOTA** : Si prefiere usar el más moderno PowerShell, en lugar de la antigua ventana de comandos, utilice el comando `powershell` en lugar de `cmd`

## Comandos

|  Tarea                               |  CMD             |  PowerShell       | Linux           |
| ------------------------------------ | ---------------- | ----------------- |---------------- |
|  Ver la lista de archivos en la      |  `dir`           |  `dir`            | `ls`            |
|  carpeta actual                      |                  |                   |                 | 
|  Ver el contenido de un archivo      |  `type <file>`   |  `type <file>`    | `cat <file>`    |
|  Limpiar la ventana de comandos      |  `cls`  ----     |  `cls`            | `clear`         |
|  Cambiar de carpeta                  |  `cd <folder>`   |  `cd <folder>`    | `cd <folder>`   |
|  Ver las rutas de busqueda PATH      |  `PATH`          |  `$env:PATH`      | `echo $PATH`    |
|  Encontrar la ruta desde donde corre |  `where python`  |  `(Get-Command python).Path`  |  `whereis python`  |
|  Python                              |  `where py`      |  `(Get-Command py).Path`      |  `whereis py`      |
|  Encontrar la ruta de pip            |  `where pip`     |  `(Get-Command pip).Path`     |  `whereis pip`     |
