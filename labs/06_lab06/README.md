# Lab06: Servidor MQTT en Raspberry Pi con IP pública (ngrok) y cliente ESP32 con sensor LM75

## Objetivos

* Configurar ngrok en la **Raspberry Pi** para exponer el broker **MQTT** y el dashboard de **Node-RED** públicamente.

* Programar el **ESP32** en MicroPython para leer datos de temperatura y humedad desde el sensor HDC1080.

* Publicar las lecturas vía **MQTT** hacia el broker remoto.

* Visualizar los datos en el dashboard de **Node-RED** accesible por Internet.

## Introducción

En este laboratorio se aprenderá a publicar datos de sensores IoT desde un **ESP32** u otro microcontrolador, porgramado con Micropython, hacia un broker **MQTT** remoto ubicado en una **Raspberry Pi**, y acceder al dashboard de **Node-RED** desde cualquier lugar a través de una IP pública generada con **ngrok**.

La arquitectura general del sistema es la siguiente:


<p align="center"> <img src="/labs/figs/lab06/arch.png" alt="Arquitectura MQTT con ngrok y ESP32" width=600> </p>

## Procedimiento:

### 1. Parte 1: Generar una IP pública con ngrok en la Raspberry Pi

1. Paso 1 – Crear cuenta y obtener token:

    1. Ir a https://ngrok.com
    2. Registrarse gratis y copiar el AuthToken (en el panel principal).

2. Paso 2 – Instalar ngrok

    ```
    sudo apt update
    sudo apt install unzip -y
    wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-arm.zip
    unzip ngrok-stable-linux-arm.zip
    sudo mv ngrok /usr/local/bin/
    ```

3. Paso 3 – Configurar el token

    ```
    ngrok config add-authtoken EL_AUTHTOKEN_AQUI
    ```

4. Paso 4 – Exponer los servicios

    1. Para Node-RED (puerto ```1880```):

        ```
        ngrok http 1880
        ```

        Se debe ver algo tipo:

        ```
        Forwarding https://f2a1-2800-xxxx.ngrok.io -> http://localhost:1880
        ```

        Usar esa URL HTTPS pública para acceder al dashboard desde cualquier lugar.

    2. Para Mosquitto (puerto ```1883```):

        ```
        ngrok tcp 1883
        ```

        Se debe ver algo tipo:

        ```
        tcp://0.tcp.ngrok.io:15234 -> localhost:1883
        ```

        Esa dirección y puerto serán los que configurará el ESP32 para conectarse al broker remoto.


        **Consejo:** puedes mantener ambas terminales abiertas:
una ejecutando ngrok http ```1880``` (Node-RED) y otra ngrok tcp ```1883``` (MQTT).


## 2. Parte 2: Sensor LM75 en el microcontrolador comunicando con el broker MQTT remoto

En esta parte se configurará el microcontrolador como cliente MQTT, encargado de leer la temperatura medida por el sensor LM75 y publicarla periódicamente hacia el broker Mosquitto que se ejecuta en la Raspberry Pi.

1. Conexión del sensor LM75

| Pin LM75 | ESP32   |
| -------- | ------- |
| VCC      | 3.3 V   |
| GND      | GND     |
| SDA      | GPIO 21 |
| SCL      | GPIO 22 |



<p align="center"> <img src="/labs/figs/lab06/sensor-esp32.png" alt="Arquitectura MQTT con ngrok y ESP32" width=400> </p>

2. Programar el microcontrolador

    Crear el  código en el microcontrolador con nombre usando Thonny u otra herramienta. Este programa realiza las siguientes acciones:

    * Se conecta a la red Wi-Fi.

     Establece comunicación I²C con el LM75.

    * Lee la temperatura cada 5 s.

    * Publica los valores en un topic MQTT (```in/micro/sensor/temperatura```).

3. Verificación del envío de datos

    * Abrir **Node-RED** (http://IP_raspberry:1880).

    * Crear un nodo ```mqtt in``` configurado con:

        * Servidor: localhost

        * Puerto: 1883

        * topic: ```in/micro/sensor/temperatura```

    * Conectar ese nodo a un nodo ```thermometer``` para visualizar la temperatur. Si no lo tienen instalarlo desde el ```Pallete``` como se explicón en el [lab04](/labs/04_lab04/README.md).

    * Abrir el dashboard desde la URL pública HTTPS que generó ngrok. 