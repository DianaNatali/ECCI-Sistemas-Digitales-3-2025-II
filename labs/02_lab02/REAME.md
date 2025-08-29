## Lab02: Introducción a Raspberry Pi Zero W y 2 W

## 1. Introducción

Esta guía está diseñada para ayudar a configurar y utilizar una **Raspberry Pi Zero W** y **2 W** desde cero. Aprenderán a instalar el sistema operativo, configurar la red y acceder de forma remota.

## 2. Objetivos de aprendizaje

* Entender los componentes básicos y requisitos de hardware de la Raspberry Pi Zero W y 2 W.

* Instalar y configurar el sistema operativo Raspberry Pi OS.

* Acceder y administrar la Raspberry Pi de forma remota mediante SSH.

* Configurar la red y realizar ajustes iniciales en el sistema.

* Instalar software esencial para proyectos futuros.


## 3. Materiales

* Raspberry Pi Zero W o Raspberry Pi Zero 2 W.

* Tarjeta microSD (mínimo 8GB, recomendado 16GB o más).

* Adaptador de corriente (5V, 2A recomendado).

* Cable micro-USB OTG y teclado/mouse (opcional).

* Adaptador HDMI a mini-HDMI y pantalla (opcional).

* Computador con lector de tarjetas microSD.

* Conexión a internet.


## 4. Intoducción a raspberry

Revisar la siguiente documentación: [raspberry](/labs/02_lab02/raspberry_intro.md).

## 5. Instalación del Sistema Operativo

1. Descargar Raspberry Pi Imager desde: https://www.raspberrypi.com/software/

2. Insertar la tarjeta microSD en su computador.

3. Abrir Raspberry Pi Imager y seleccionar:

    1. Sistema operativo: Raspberry Pi OS (Lite o Full)

    2. Dispositivo de almacenamiento: La tarjeta microSD detectada

    ![imager](/labs/figs/lab02/imager.png)

4. (Opcional) Configura Wi-Fi y SSH en "Ajustes avanzados".

5. Hacer clic en ```Next``` y esperar a que finalice el proceso.

## 6. Configuración Inicial

### 6.1 Primer arranque

1. Insertar la microSD en la Raspberry Pi.

2. Conectar la raspberry a la energía y a una pantalla (si está disponible).

3. Si configuró Wi-Fi en Raspberry Pi Imager, la Raspberry se conectará automáticamente.


## 6.2 Acceso por SSH (Sin pantalla)

1. Encontrar la dirección IP:

    Abra una terminal en Windows (PowerShell o Símbolo del sistema) y ejecute:

    ```
    arp -a
    ```

2. Para conectar la Raspberry Pi mediante SSH en Visual Studio Code, siga estos pasos:

    1. Instalar la extensión SSH en VS Code

        1. Abra Visual Studio Code en su computador.
        2. Vaya a la pestaña **Extensiones** ```(Ctrl + Shift + X)```.
        3. Busqye **Remote - SSH** e instalarlo.

    2. Configurar la conexión SSH

        1. Abra la paleta de comandos en VS Code ```(Ctrl + Shift + P)```.
        2. Escriba ```Remote-SSH: Connect to Host...``` y seleccionelo.
        3. En la ventana emergente, seleccione ```Add New SSH Host....```
        4. Escriba el siguiente comando (reemplace ```<direccion_ip>``` con la IP de la Raspberry Pi):

            ```
            ssh pi@<direccion_ip>
            ```

        5. Presione ```Enter``` y seleccione un archivo de configuración (```.ssh/config``` en su usuario de Windows).

## 6.3 Configuración básica

Ejecute en la terminal de la Raspberry:

```
sudo raspi-config
```

Opciones recomendadas:

* ```Change User Password```: Cambiar la contraseña predeterminada.

* ```Network Options > Wi-Fi```: Configurar la red.

* ```Localisation Options```: Ajustar el idioma y zona horaria.

* ```Interface Options > SSH```: Activar SSH si no está activado.

* ```Advanced Options > Expand Filesystem```: Maximizar el espacio en la microSD.

Actualizar el sistema: Ejecute en la terminal lo siguiente:

```
sudo apt update && sudo apt upgrade -y  
```

## Entregables

Los estudiantes deberán mostrar en clase la configuración y acceso remoto de la Raspberry Pi.