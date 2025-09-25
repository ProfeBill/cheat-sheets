# Kivy

## Compilación del EXE para Windows

### Prerrequisitos

* Instalar pyinstaller

```
pip install -U pyinstaller
```

* Asegurese de que el archivo principal que ejecuta su aplicación se encuentre en la carpeta raiz del repositorio (junto al README).

Una forma elegante de hacerlo, es crear un archivo que simplemente importe al archivo principal del GUI dentro de la carpeta src/view/model

```
import sys
sys.path.append( "src" )

from view.gui.payment_gui import PaymentApp

PaymentApp().run()
```

### Compilación

Compile su programa como un solo exe de Windows con este comando:

```
pyinstaller -F --paths=src [MI PROGRAMA PRINCIPAL EN LA CARPETA RAIZ].py
```

Asegúrese de utilizar la opción -F o --onefile para generar un solo archivo ejecutable y 
la opción `--paths=src` para que el compilador busque dentro de la carpeta `src`

El ejecutable quedará ubicado dentro de la carpeta dist de su repositorio

Asegúrese de agregar las carpetas `dist` y `build` al `.gitignore` para evitar que el repositorio se llene de basura.


## Compilación del APK para Android

### Prerrequisitos

* Si el equipo es Windows, Asegurese de instalar Ubuntu 22.04 en WSL (debe reiniciar al final):
```
wsl --install Ubuntu-22.04 
```

* Instalar pip3

Actualice primero el apt. Desde una consola de WSL ejecute:

```
sudo apt update
sudo apt -y upgrade
sudo apt install -y python3-pip
```
* Instalar buildozer

Asegúrese de leer primero los instructivos https://kivy.org/doc/stable/guide/packaging-android.html#buildozer y https://buildozer.readthedocs.io/en/latest/installation.html

Comandos:

```
# Instalar buildozer
pip3 install --user --upgrade buildozer
# Instalar Java OpenJDK y demás dependencias requeridas
sudo apt install -y git zip unzip openjdk-17-jdk python3-pip autoconf libtool pkg-config zlib1g-dev libncurses5-dev libncursesw5-dev libtinfo5 cmake libffi-dev libssl-dev
pip3 install --user --upgrade Cython==0.29.33 virtualenv  # the --user should be removed if you do this in a venv

# Ejecute esta línea y también edite su archivo ~/.bashrc y agregue esta línea al final
export PATH=$PATH:~/.local/bin/
```

* Clonar el repositorio en una carpeta dentro de WSL

Si usa WSL en Windows, clone el repositorio dentro de la partición Linux, no en la partición Windows

```
git clone https://github.com/ProfeBill/tictactoe.git
cd tictactoe
```
* Inicializar el proyecto

```
buildozer init
# Edite el archivo de propiedades del proyecto y establezca al meno las propiedades title y package.name
nano buildozer.spec
# Recuerde que se guarda con Ctrl-S y se sale con Ctrl-X
```
  
* Compilar

**IMPORTANTE** Asegúrese de que el archivo principal de la aplicación se llame ```main.py```

```
buildozer -v android debug
# Una vez compilado, el APK queda almacenado en la carpeta bin, para ver el archivo resultante :
ls bin
# Puede copiarlo a la partición Windows
cp bin/profetriki-0.1-arm64-v8a_armeabi-v7a-debug.apk /mnt/c/carpeta_destino_en_winodws
```


### Recomendaciones Generales

- Lea la documentación oficial, use IA solo si tiene problemas y necesita sugerencias
- No compile en virtualenv
