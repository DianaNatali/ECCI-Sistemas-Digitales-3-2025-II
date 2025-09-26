# Lab03: Visualización de datos en Raspberry Pi con VNC Viewer

## Objetivo de aprendizaje

Desarrollar un programa en Python que simule la lectura de un sensor y grafique los datos en tiempo real desde la Raspberry Pi Zero W, usando interfaz gráfica a través de VNC Viewer.

## Requisitos

* Raspberry Pi con Raspberry Pi OS instalado.

* Conexión a red local (Wi-Fi o Ethernet).

* Un computador con Windows, macOS o Linux.

* Python 3 y matplotlib instalados en la Raspberry Pi:

    ```
    sudo apt update
    sudo apt install python3-matplotlib
    ```

## Procedimiento

### Parte 1: Habilitar acceso gráfico con VNC

Los siguientes pasos se ejecutar conectando una pantalla HDMI, un mouse y un teclado a la raspberry:

1. Habilitar VNC en la Raspberry Pi

    En la terminal:

    ```
    sudo raspi-config
    ```

    * Ir a Interface Options → VNC → Enable.

    * Salir del menú y reiniciar la raspberry:

        ```
        sudo reboot
        ```

2. Obtener la IP a la que está conectada la Raspberry Pi

    Cuando encianda la raspeberry ejecutar en una terminal:

    ```
    ifconfig
    ```

3. Instalar y usar VNC Viewer en el computador

    * Descarga desde:

        https://www.realvnc.com/en/connect/download/viewer/

    * Abrir VNC Viewer.

    * Escribir la IP de la Raspberry Pi y presionar Enter.

    * Ingresar:

        * **Usuario:** Por lo general es  ```pi```

        * **Contraseña**

    Se abrirá el escritorio de la Raspberry Pi.

### Parte 2: Código Python para graficar en tiempo real

1. Instalar la biblioteca ```Matplotlib``` de Python en su raspberry:

    ```
    sudo apt update
    sudo apt install python3-matplotlib -y
    ```

2. Aceptar la tarea en Github Classroom y ejecutar el código que encontrará en el respectivo repositorio.

3. Apropiarse del código del ítem anterior y agreguar funcionalidades o cambiar parámetros según lo requiera.

#### Explicación

| Sección                | Descripción                                                             |
|------------------------|-------------------------------------------------------------------------|
| `vcgencmd measure_temp` | Comando del sistema para leer la temperatura del CPU.                   |
| `subprocess.check_output` | Ejecuta comandos del sistema desde Python.                              |
| `matplotlib.pyplot`    | Biblioteca para graficar datos.                                         |
| `plt.ion()`            | Activa modo interactivo para actualizar la gráfica sin bloquear el código. |
| `time.sleep()`         | Controla el intervalo de lectura (cada 0.5 s).                          |



## Entregables

1. Código fuente: Subir al repositorio el archivo Python con el código completo del programa.

2. Documentación: En el respectivo ```README.md``` de Github Classroom escribir una documentación técnica describiendo las funcionalidades implementadas y los desafíos encontrados.
