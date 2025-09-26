# Lab04: Visualización de datos en Raspberry Pi con Node-RED 

Índice:

1. [Objetivos de aprendizaje](#1-objetivo-de-aprendizaje)
2. [Introducción](#2-introducción)
3. [Requisitos](#3-requisitos)
4. [Procedimiento](#4-procedimiento)
4.1 [Parte 1](#41-parte-1-instalación-y-configuracón-de-node-red)
4.2 [Parte 2](#42-parte-2--crear-un-flujo-en-node-red)
5. [Entregables](#5-entregables)


------------------------------------------------------

## 1. Objetivo de aprendizaje

Desarrollar un flujo en Node-RED que permita seleccionar un color mediante un selector de color, visualizar los valores RGB en un campo de texto y almacenarlos en un archivo de texto. Posteriormente, crear un script en Python que lea este archivo y procese los valores RGB.

## 2. Introducción

```Node-RED``` es una herramienta de programación visual basada en flujos, diseñada para conectar dispositivos, APIs y servicios en línea de manera sencilla.```Node-RED``` permite a los usuarios crear aplicaciones mediante una interfaz gráfica donde se arrastran y conectan nodos que representan funciones o servicios.

```Node-RED``` se ejecuta sobre ```Node.js```, una plataforma de desarrollo basada en ```JavaScript``` que permite ejecutar código ```JavaScript``` en el servidor. ```Node.js``` proporciona un entorno de ejecución eficiente y escalable, ideal para aplicaciones en tiempo real y de alto rendimiento. Al estar construido sobre ```Node.js```, Node-RED hereda sus capacidades y ventajas.

```npm``` (Node Package Manager) es el gestor de paquetes por defecto para ```Node.js```. Permite a los desarrolladores instalar, actualizar y gestionar bibliotecas y módulos que extienden la funcionalidad de sus aplicaciones. npm facilita la integración de miles de paquetes disponibles en su repositorio, lo que permite a los usuarios añadir fácilmente nuevas funcionalidades a sus proyectos.

## 3. Requisitos

### Software
1. Sistema operativo Raspberry Pi OS correctamente instalado y configurado.

2. Acceso ```SSH``` habilitado en la Raspberry Pi.

3. ```Node.js``` y ```npm``` (serán instalados durante el laboratorio).

4. Node-RED (será instalado durante el laboratorio).

5. Python 3 instalado en la Raspberry Pi.


### Conexión de red

Raspberry Pi y computador local conectados a la misma red local para la comunicación mediante SSH y acceso a la interfaz web de Node-RED.

## 4. Procedimiento

### 4.1 Parte 1: Instalación y configuracón de Node-RED:

#### 1. Conexión por SSH a la Raspberry Pi:

Se recomienda realizar la instalación de ```Node-RED``` mediante una conexión SSH establecida desde la terminal de comandos de su computador local, en lugar de utilizar ```Visual Studio Code (VSC)``` como en los laboratorios anteriores. Esto se debe a que ```VSC```, al operar de manera remota a través de SSH, consume más recursos de la Raspberry Pi, lo que puede afectar el rendimiento durante procesos intensivos como la instalación de ```Node-RED```. Además, el uso exclusivo de la terminal minimiza el consumo de memoria y CPU, permitiendo que la Raspberry Pi se enfoque en completar la instalación de manera eficiente.

Para conectarse por SSH a la Raspberry Pi:

1. Abra una terminal de comandos.

2. Ejecute el siguiente comando:

    ```
    ssh usario_raspberry@ip
    ```

    donde:

    * ```usuario_raspberry``` corresponde al nombre de usuario de su Raspberry Pi.

    * ```ip``` corresponde a la dirección IP de su Raspberry Pi en la red local.


    Si el comando es correcto el cliente SSH mostrará un mensaje similar al siguiente:

    ```
    The authenticity of host '192.168.1.100 (192.168.1.100)' can't be established. 
    ECDSA key fingerprint is SHA256:AbCdEfGhIjKlMnOpQrStUvWxYz1234567890abcdefg.
    Are you sure you want to continue connecting (yes/no)?
    ```

    Este mensaje indica que el cliente SSH no puede verificar la identidad del servidor porque es la primera vez que se realiza la conexión.


    Lo que debe hacer es aceptar la conexión escribiendo ```yes``` y presionando ```Enter```. Esto agregará la clave pública del servidor al archivo ```known_hosts``` de su computador local.​

    Si la conexión se realiza con éxito, verá en su terminal que el nombre de usuario y el nombre de la máquina cambian a los correspondientes a la Raspberry Pi. Esto indica que ahora está trabajando directamente en la terminal de la Raspberry Pi.

#### 2. Instalación de Node-RED en Raspberry Pi


El [sitio oficial](https://nodered.org/docs/getting-started/raspberrypi) de Node-RED proprociona un *script* para instalar ```Node.js```, ```npm``` y ```Node-RED``` en una Raspberry Pi. Este *script* también puede usarse para actualizar una instalación existente cuando haya una nueva versión disponible.

Para descargar y ejecutar el *script* ejecute el siguiente comando en una terminal de su Raspberry Pi:

```
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
```

Durante el proceso de instalación, el *script* realizará una serie de verificaciones y hará algunas preguntas. A continuación, se detallan las preguntas más comunes y las respuestas recomendadas:

1. 
    ```
    Are you really sure you want to do this? [y/N]
    ```

    Se debe responder afirmativamente presionando la tecla ```y``` y luego ```Enter```.

2.
    ```
    Would you like to install the Pi-specific nodes? [y/N]
    ```

    Se debe responder afirmativamente presionando la tecla ```y``` y luego ```Enter```.

Posteriormente iniciará la instalación y verá lo siguiente:

![node-red1](/labs/figs/lab04/node_red_install1.png)

**Durante el proceso de instalación, el script realizará una serie de pasos, incluyendo la actualización de Node.js, la instalación de Node-RED y la configuración de nodos específicos para Raspberry Pi. Es importante no interrumpir el proceso y esperar pacientemente hasta que se complete.**

**La instalación puede tardar varios minutos, especialmente en una Raspberry Pi Zero W, debido a su hardware limitado. Es recomendable no cerrar la terminal ni realizar otras acciones durante este tiempo para evitar posibles interrupciones en el proceso.**

Al finalizar, el *script* mostrará el mensaje ```All done.```, como se observa en la imagen de arriba. A continuación, el script imprimirá algunas indicaciones e iniciará automáticamente una configuración esencial de ```Node-RED``` (```Node-RED``` Settings File initialisation). Durante este proceso, se harán varias preguntas; a continuación, se detalla cómo responder a cada una. En la mayoría de los casos, basta con presionar ```Enter``` para seleccionar la opción predeterminada.

![node-red2](/labs/figs/lab04/node_red_install2.png)


La imagen anterior indica que tanto la instalación como la configuración de ```Node-RED``` se han completado exitosamente.

#### 3. Correr localmente Node-RED

Para ejecutar ```Node-RED``` localmente en su Raspberry Pi, se debe usar el siguiente comando:

```
node-red-pi --max-old-space-size=256
```

Este comando inicia ```Node-RED``` en su dispositivo de forma local. Al usar ```node-red-pi```, está ejecutando ```Node-RED``` específicamente optimizado para la Raspberry Pi. La opción ```--max-old-space-size=256``` ajusta la cantidad de memoria que ```Node-RED``` puede usar, limitándola a $256$ MB. Esto es útil para evitar que el proceso consuma demasiada memoria, especialmente si la Raspberry Pi tiene recursos limitados.

Especificamente, al correr ```Node-RED``` localmente, se está iniciando la instancia de ```Node-RED``` directamente en la Raspberry Pi.

Ahora podrá acceder a ```Node-RED``` desde un navegador web de cualquier computador local, a través de la siguiente URL:

```
http://ip:1880
```

donde:

* ```ip``` corresponde a la dirección IP de su Raspberry Pi en la red local.
* ```1880``` es el puerto TCP predeterminado utilizado por ```Node-RED``` para la interfaz web.

Al acceder a esta URL deberá ver la siguiente interfaz:

![node-red3](/labs/figs/lab04/node_red_welcome.png)

Una vez que revise la información en la ventaba de bienvenida, podrá interacturar con la interfaz de Node-RED.


Es importante aclarar que realizar este procedimiento sólo le permite ejecutar el servicio de ```Node-RED``` de forma local, lo que conlleva a que este comando bloquea la terminal de comandos, ya que Node-RED se está ejecutando en primer plano como un servicio. Esto significa que:

1. No se podrá usar esa terminal para otros comandos mientras ```Node-RED``` esté corriendo.

2. Si se cierra esta terminal o se mata este proceso con ```Ctrl + Z``` ya no podrá acceder a la interfaz de ```Node-RED``` a través de la URL en su computador local, como se hizo anteriormente.

3. Para volver a acceder, necesitará reiniciar ```Node-RED``` utilizando el mismo comando o configurarlo como un servicio para que se inicie automáticamente al encender la Raspberry Pi, que es en lo que consiste el siguiente paso.

#### 4. Correr on boot Node-RED:

Para hacer que ```Node-RED``` se ejecute automáticamente al encender tu Raspberry Pi (o cualquier sistema basado en Linux), puede configurarse como un servicio del sistema. Esto se puede lograr utilizando ```systemd```, que es el sistema de administración de servicios en muchas distribuciones de Linux.

Lo anterior se puede lograr ya que en la instalación estándar de Node-RED en una Raspberry Pi, el servicio se crea automáticamente como parte del proceso de instalación. De lo contrario se tendría que crear el servicio manualmente, pero ese no es el caso.

En otras palabras, el *script* de instalación hace lo siguiente:

1. Instala ```Node-RED``` y sus dependencias.

2. Crea un servicio de ```systemd``` para que Node-RED se ejecute automáticamente al arrancar el sistema. Este servicio está configurado para iniciarse como parte de la secuencia de arranque de tu Raspberry Pi.

3. Configura ```Node-RED``` para ejecutarse con la cantidad de memoria adecuada.

Aún así, el servicio no se habilita por defecto aunque se haya creado, por lo que es necesario habilitar el servicio manualmente con:

1. Mate el proceso que está ejecutando ```Node-RED``` localmente, si aún no lo ha hecho, para ello basta con cerrar dicha terminal o oprimir ```Ctrl + Z``` en la terminal que está ejecutando este proceso.

2. Verifique que ya no puede acceder a la interfaz de ```Node-RED``` en la URL anteriomente mencionada.

3. Ejecute el siguiente comando:

    ```
    sudo systemctl enable nodered.service
    ```

    Lo cual hará que se pueda acceder a ```Node-RED``` desde la URL, siempre que la  Raspberry Pi esté encendida, pero sin necesidad de ejecutar el servicio manualmente ocupando una terminal para ello como se hizo en el paso [Correr localmente Node-RED](#3-correr-localmente-node-red).

4. Reinicie la Raspberry Pi:

    ```
    sudo reboot
    ```

Una vez que inicie la Raspberry Pi podrá acceder a la interfaz de ```Node-RED``` a través de la URL previamente mencionada, desde un navegador web de cualquier computador local y podrá acceder a esta interfaz siempre que la Raspberry Pi esté encendida.



### 4.2 Parte 2:  Crear un flujo en Node-RED 

#### Introducción:

La interfaz de ```Node-RED``` es una plataforma visual que permite crear aplicaciones a través de una interfaz de arrastrar y soltar. Está diseñada para facilitar la creación de flujos de trabajo, lo que permite a los usuarios conectar diversos componentes y servicios para realizar tareas automatizadas. A continuación se explica los principales elementos de la interfaz:

![node-red4](/labs/figs/lab04/node_red.png)

1. Panel de flujos (Flow Workspace)

    Es el área principal donde se crean y organizan los flujos. Es un espacio de trabajo en blanco donde se colocan y conectan los nodos para definir el flujo de datos y lógica.

    * Los flujos pueden tener múltiples "hojas" o pestañas, lo que permite organizar diferentes partes de tu proyecto en varias secciones.

    * Los flujos son ejecutables: una vez que se ha creado y conectado el flujo, ```Node-RED``` lo ejecutará para procesar los datos que pasan a través de los nodos.

2. Panel de nodos (Node Palette)

    A la izquierda de la interfaz, se encuentra el panel de nodos o palette, donde se encuentran todos los nodos disponibles para usar en tu flujo. Estos nodos están organizados en categorías según su función (por ejemplo, "redes", "entrada", "salida", "funciones", "sistemas", etc.).

3. Nodos (Nodes):

    Los nodos son los bloques que representan las distintas operaciones que realiza tu flujo. Cada nodo tiene una función específica, y los puedes conectar entre sí para que los datos fluyan de uno a otro. Los nodos se arrastran desde el panel de la izquierda y se colocan en el espacio de trabajo.

    Los nodos pueden ser configurados mediante su interfaz de configuración, que aparece al hacer clic sobre ellos.


4. Panel de propiedades

    Cuando se selecciona un nodo, aparece el panel de propiedades a la derecha de la interfaz. Aquí se configuran las opciones específicas de ese nodo. Cada tipo de nodo tiene propiedades particulares que se pueden configurar según lo que se necesite hacer.

5. Conexiones entre nodos

    Los nodos se conectan entre sí arrastrando un conector desde la salida de un nodo hacia la entrada de otro. Estas conexiones permiten que los datos fluyan de un nodo a otro, pasando de un proceso a otro.

6. Botón ```Deploy```:

    En la parte superior derecha de la interfaz, se encuentra este botpon que publica y ejecuta los cambios que se hayan realizado en el flujo.


7. *Debug Sidebar*: 

    En la parte derecha, se habilita la barra de depuración (*debug*), donde se muestran mensajes y datos de depuración. Los nodos de *debug* permiten monitorear y visualizar el contenido de los mensajes que pasan por el flujo.

8. *Dashboard*:

    El Dashboard de ```Node-RED``` es una característica que permite crear interfaces gráficas de usuario (GUIs) interactivas y visuales directamente desde ```Node-RED```. Estas interfaces pueden ser utilizadas para mostrar datos, controlar dispositivos, y presentar información en tiempo real, todo a través de un navegador web.

#### Crear un flujo para un selector de colores:


1. Instalar el *dashboard* de```Node-RED```:

    1. En la interfaz de ```Node-RED```, vaya a ```Menu > Manage palette > Install```como se muestra en la siguiente imagen: 

        ![node-red5](/labs/figs/lab04/install.png)

    2. Se abrirá la ventana de ```User Settings``` en la opción ```Pallete```. Seleccionar la pestaña ```Install``` como se muestra en la imagen de abajo.

    3. Buscar ```dashboard``` e instalar el paquete como se muesta en la imagen de abajo.

        ![node-red5](/labs/figs/lab04/dashboard.png)


2. Crear el flujo:

    1. Buscar los siguientes nodos en el panel de nodos y arrastarlos a una pestaña de flujo:

        * ```color picker```.

        * ```text input```

        *  ```debug```.

        * ```funtion```.

        * ```wire file```.

    2. Conectar los nodos de la siguiente manera:

        ![node-red6](/labs/figs/lab04/flujo.png)


## 5. Entregables

1. Código fuente: Subir al repositorio el archivo ```.json``` con el flujo implementado en Node-RED.

2. Documentación: En el respectivo ```README.md``` de Github Classroom escribir una documentación técnica describiendo el procedimiento llevado a cabo y los resultados obtenidos.











