## Lab 1: Directorio telefónico con clases, listas y diccionarios

## 1. Objetivo general:

Desarrollar un sistema de directorio telefónico utilizando programación orientada a objetos (POO) en Python. Se utilizarán clases para modelar contactos, listas para almacenarlos y diccionarios para optimizar las búsquedas. El programa debe permitir agregar, buscar, eliminar y mostrar contactos, además de incluir validaciones de datos y persistencia en archivos ```JSON``` o ```CSV```.

## 2. Objetivos de aprendizaje:

* Comprender la estructura y el uso de clases en Python para modelar entidades.

* Aplicar listas y diccionarios para organizar y optimizar la búsqueda de información.

* Implementar verificaciones para asegurar la calidad de los datos ingresados.

* Guardar y recuperar información utilizando formatos ```JSON``` o ```CSV```.

* Crear un menú interactivo para gestionar las funcionalidades del directorio.

## 3. Requerimientos

1. Clase ```Contacto```:

    * ```Atributos```: 

        * ```id```: Identificador único del contacto.
        * ```nombre```: Nombre completo del contacto.
        * ```telefono```: Número de teléfono de 10 dígitos.
        * ```fecha_nacimiento```: Fecha de nacimiento del contacto (debe ser válido).
        * ```correo```: Correo electrónico (debe ser válido).
        * ```area```: Área dentro de una empresa o institución a la que pertenece el contacto.

    * ```Métodos```: 
        * ```__str__()```:  Devuelve una representación formateada del contacto. 

2. Clase ```Directorio```:

    * ```Atributos```:

        * ```contactos```: Lista para almacenar objetos ```Contacto```.

        * ```indice_telefonos```: Diccionario para indexar contactos por su número de teléfono.

        * ```indice_ids```: Diccionario para indexar contactos por su ID único.

        * ```indice_areas```: Diccionario para indexar contactos por área.

        * ```areas```: Área dentro de la empresa a la que pertenece el contacto (seleccionada de una lista predefinida).

    * ```Métodos```:

        * ```agregar_contacto()```:  Agrega un contacto validando los datos y guardándolo automáticamente.

        * ```agregar_area()```: Permite agregar una nueva área predefinida.

        * ```seleccionar_area()```: Permite al usuario elegir un área de una lista numerada

        * ```buscar_por_telefono()```: Busca un contacto por número de teléfono.

        * ```buscar_por_id()```: Busca un contacto por su ID único.

        * ```buscar_por_area()```: Busca contactos por área dentro de la empresa.

        * ```eliminar_contacto_id()```: Elimina un contacto usando su ID único.

        * ```eliminar_contacto_tel()```: Elimina un contacto por número de teléfono.

        * ```mostrar_contactos()```: Muestra todos los contactos ordenados alfabéticamente.

        * ```cargar_datos```: Carga los contactos desde un archivo ```JSON``` o ```csv```.

3. Validaciones:

    * ```validar_telefono()```: Verifica que el número contenga exactamente 10 dígitos.

    * ```validar_correo()```: Confirma que el correo tenga un formato correcto.

    * ```validar_fecha_nacimiento()```: Asegura que la fecha ingresada cumpla con el formato YYYY-MM-DD.

4. Persistencia de datos: Guardar y cargar los contactos en un archivo ```JSON``` o ```csv```.


## 4. Actividades

  1. Diseño de clases: Definir las clases ```Contacto``` y ```Directorio``` con sus atributos y métodos.

  2. Implementación de métodos: Implementar los métodos de la clases para gestionar los contactos.

  3. Validaciones: Implementar las funciones de validación y úsalas en el método agregar_contacto.

  4. Persistencia de datos: Implementar los métodos ```guardar_datos``` y ```cargar_datos```.

  5. Interfaz de Usuario: Crear un menú interactivo para que el usuario pueda usar el directorio.

  6. Pruebas: Probar todas las funcionalidades del programa y corregir los errores.

## Entregables

  1. Código fuente: Subir al repositorio el archivo ```Python``` con el código completo del programa.

  2. Documentación: En el respectivo ```README.md``` de **Github Classroom** escribir una documentación técnica describiendo las funcionalidades implementadas y los desafíos encontrados.

  
