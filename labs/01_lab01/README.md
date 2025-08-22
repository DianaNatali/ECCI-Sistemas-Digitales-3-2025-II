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

### 3.1 Clase ```Contacto```: 

Representar la entidad fundamental del sistema.

* **Atributos**: 

    | Nombre | Tipo | Descripción |
    |----------|----------|----------|
    | ```id``` | ```int```|Identificador único del contacto.   |
    |```nombre```   | ```str```  | Nombre completo (mínimo 2 palabras)   |
    | ```telefono```    | ```str```   | Exactamente 10 dígitos numéricos|
    | ```fecha_nacimiento```    | ```str```   | Formato ISO 8601: ```YYYY-MM-DD```|
    | ```correo```    | ```str```   | Formato email válido (RFC 5322)|
    | ```area```    | ```str```   | Área organizacional válida|


* **Métodos**: 
    * ```__init__()```: Constructor con validaciones básicas.
    * ```__str__()```:  Devuelve una representación formateada del contacto:

        Representación formal: ```ID: 1 | Juan Pérez | 📞 5512345678 | Ventas```

    * ```to_dict()```: Serialización a diccionario para persistencia

### 3.2 Clase ```Directorio```:

Gestionar la colección de contactos y operaciones.

* **Atributos**:

    * ```contactos```: Lista para almacenar objetos ```Contacto```.

    * ```indice_telefonos```: Diccionario para indexar contactos por su número de teléfono.

    * ```indice_ids```: Diccionario para indexar contactos por su ID único.

    * ```indice_areas```: Diccionario para indexar contactos por área.

    * ```areas```: Área dentro de la empresa a la que pertenece el contacto (seleccionada de una lista predefinida).

* **Métodos principales**:

    * ```agregar_contacto()```:  Agrega un contacto validando los datos y guardándolo automáticamente.

    * ```buscar_por_telefono()```: Busca un contacto por número de teléfono.

    * ```buscar_por_id()```: Busca un contacto por su ID único.

    * ```buscar_por_area()```: Busca contactos por área dentro de la empresa.

    * ```eliminar_contacto()```: Elimina por ID o teléfono, manteniendo consistencia de índices

    * ```mostrar_contactos()```: Muestra todos los contactos ordenados alfabéticamente.

* **Métodos de gestión de área**:

    * ```agregar_area()```: Permite agregar una nueva área predefinida.

    * ```seleccionar_area()```: Permite al usuario elegir un área de una lista numerada

* **Persistencia**:

    * ```guardar_datos```:  Guarda los datos en archivo ```JSON``` o ```csv```.

    → **Estrategia de persistencia**:
    
    - Formato JSON (Recomendado):

    ```
    [
      {
        "id": 1,
        "nombre": "Juan Pérez",
        "telefono": "5512345678",
        "fecha_nacimiento": "1990-05-15",
        "correo": "juan@empresa.com",
        "area": "Ventas"
      }
    ]
    ```

    - Formato CSV:

    ```
    id,nombre,telefono,fecha_nacimiento,correo,area
    1,Juan Pérez,5512345678,1990-05-15,juan@empresa.com,Ventas
    ```

### 3.3 Clase ```InterfazUsuario```

Manejar la interacción con el usuario final

* **Atributos**

    * ```directorio```: Instancia de la clase Directorio

* **Métodos Principales**

    * **Métodos de Navegación**

        * ```mostrar_menu_principal()```: Muestra las opciones principales

        * ```ejecutar()```: Bucle principal que controla la ejecución

    * **Métodos de Entrada**

        * ```leer_opcion()```: Lee y valida una opción del menú

        * ```leer_dato()```: Lee un dato simple del usuario


### 3.3 Validaciones:

* ```validar_nombre()```:     

    * Mínimo 2 palabras (nombre y apellido)

    * Longitud mínima: 5 caracteres

    * Solo caracteres alfabéticos y espacios

* ```validar_telefono()```: 

    * Longitud exacta: 10 caracteres
    
    * Solo dígitos numéricos (0-9)

* ```validar_correo()```: Confirma que el correo tenga un formato correcto: ```usuario@dominio.extension```.

* ```validar_fecha_nacimiento()```: 

    *  Formato ISO 8601: ```YYYY-MM-DD```

    * Rango válido: 1925-01-01 a fecha actual

    * Días válidos según mes y año



## Entregables

1. Código fuente completo (archivo ```.py```).

2. Documentación técnica en ```README.md con```:

    * Diagrama de clases

    * Explicación detallada de cada clase y método

    * Instrucciones de uso

3. Archivos de persistencia de ejemplo (JSON/CSV)

4. Casos de prueba implementados
  
