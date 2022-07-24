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

wget https://bootstrap.pypa.io/get-pip.py

sudo apt-get install python3-distutils

sudo apt-get install python3-apt

sudo python3 get-pip.py

sudo pip3 install pyserial

mkdir -p ~/Arduino/hardware/espressif

cd ~/Arduino/hardware/espressif

git clone https://github.com/espressif/arduino-esp32.git esp32

cd esp32

git submodule update --init --recursive

cd tools

python3 get.py

El siguiente comando transforma la manera en la que Arduino hace uso de Python y Python3, por lo que debes asegurarte de haber ejecutado correctamente los comandos anteriores. Se admiten warnings pero no errores.

sudo ln -s /usr/bin/python3 /usr/bin/python

Ahora has configurado el sistema de forma adecuada para que el IDE de Arduino pueda programar el ESP32CAM.

:)

![arduino_checar](https://user-images.githubusercontent.com/72757419/179071093-fb390a00-b44f-4c45-8317-0db00c1e5885.JPG)

Conexión de la SP32_CAM
Se realiza la siguiente conexión entre la SP32CAM y el FTDI

![imagen](https://user-images.githubusercontent.com/72757419/180626414-8fa6cdd5-09bd-48da-84c8-23fb65f2b9bf.png)

Las conexiones deben tener el siguiente orden

ESP32CAM 	FTDI
5V 	      Vcc
GND 	     GND
UOT 	     RX
UOR 	     TX
IO0-GND Para entrar en el modo programador y conectar el FTDI al equipo de cómputo

Las conexiones se verán así
![imagen](https://user-images.githubusercontent.com/72757419/180626497-e5d6b25f-febf-43e2-9903-23082974f337.png)
![imagen](https://user-images.githubusercontent.com/72757419/180626501-9a6209a1-6948-4a35-83c7-efc09938d74e.png)

Nota: Después de conectra el cable del FTDi a la computadora hay que activar los puerrtos USB en la máquina virtual.
- Activar el monitor serial en el arduino IDe para observar que está listo para programar la SP32 CAM
- Cargar el programa de CAmeraWebServer en la tarjeta SP32CAM seleccionando la tarjeta adecuada
- Esperara hasta que aparezca Hard resetting via RTS pins
- Quitar el jumper o el cable  conecto IO0-GND para salir del modo programador
- Resetear el SP32CAM
- Si todo salió bien aparecerá el mensaje en el monitor serial dandonos la IP para comenzar el streaming 
![imagen](https://user-images.githubusercontent.com/72757419/180626634-212ac296-444c-41e5-b659-211871fb7d3c.png)
El resultado es este
![imagen](https://user-images.githubusercontent.com/72757419/180626937-1c44865b-9fb3-4b19-bb4d-e3b810d54670.png)




