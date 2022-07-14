# ESP32-CAM
 Configuración para usar la tarjeta ESP32_CAM

 Para poder programar el módulo ESP32CAM es necesario cumplir una serie de requisitos muy específicos. Estos requisitos se enlistan a continuación:

    Modulo ESP32CAM .
    o    Tipo AI-Thinker.
    o    Procesador ESP32-S a 240MHz y 4MB ROM.
    Cámara modelo OV2640.
    Programador FTDI o convertidor TTL-USB equivalente.
    Protoboard.
    Cables Jumper.
    Ubuntu 20.04.
    IDE Arduino 1.8.1 o superior para Linux.
    Git para Linux.
    Conexión a Internet.

     Ubuntu 20.04 corriendo en VirtualBox

     Configuración de IDE de Arduino
     
     Para programar el ESP32CAM se utilizará la IDE de Arduino en su versión 1.8.1 o superior

En caso de que no tengas instalada la IDE de Arduino, puedes consultar la siguiente guía de instalación https://docs.arduino.cc/software/ide-v1/tutorials/Linux

Es muy importante que leas la guía completa, pues es necesario ejecutar algunos comandos para permitir que la IDE de Arduino pueda acceder a los puertos serie y comunicarse con el ESP32CAM para poder programarlo y monitorearlo.

Las instrucciones han sido obtenidas directamente del repositorio de Espressif para Arduino.

espressif/arduino-esp32: Arduino core for the ESP32 (github.com)

Agrega el enlace de tarjetas extra en las preferencias. Para ello haz clic en el menú File y luego en Preferences. En el cuadro de diálogo que aparece, pega la siguiente URL en la sección Additional Boards Manager.

https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json 

A continuación, dirígete al Board Manager haciendo clic en Tools, Board y Board’s Manager. En el cuadro de búsqueda del Board Manager escribe lo siguiente:

esp32

Aparecerá solo una opción, haz clic en el botón instalar. Esto agregará una parte de los archivos necesarios para habilitar el IDE de Arduino para programar el ESP32CAM.

Una vez realizada la configuración del Board’s Manager en el IDE de Arduino, es necesario instalar los drivers del ESP32 para que sea posible programarlo. A continuación se muestran los comandos necesarios, los cuales tienen como propósito configurar el entorno para ejecutar el archivo get.py, el cual realiza las configuraciones necesarias para que la IDE de Arduino sea capaz de programar el ESP32.

Nota: Los siguientes comandos parten del hecho de que tienes GIT instalado previamente.

sudo usermod -a -G dialout $USER

Copy

wget https://bootstrap.pypa.io/get-pip.py

Copy

sudo apt-get install python3-distutils

Copy

sudo apt-get install python3-apt

Copy

sudo python3 get-pip.py

Copy

sudo pip3 install pyserial

Copy

mkdir -p ~/Arduino/hardware/espressif

Copy

cd ~/Arduino/hardware/espressif

Copy

git clone https://github.com/espressif/arduino-esp32.git esp32

Copy

cd esp32

Copy

git submodule update --init --recursive

Copy

cd tools

Copy

python3 get.py

El siguiente comando transforma la manera en la que Arduino hace uso de Python y Python3, por lo que debes asegurarte de haber ejecutado correctamente los comandos anteriores. Se admiten warnings pero no errores.

sudo ln -s /usr/bin/python3 /usr/bin/python

Ahora has configurado el sistema de forma adecuada para que el IDE de Arduino pueda programar el ESP32CAM.

:)





