# Proyecto Microservicios

## Descripción del proyecto
Este proyecto corresponde al desarrollo de una arquitectura basada en microservicios utilizando Spring Boot. 
La aplicación permite gestionar productos e inventario mediante servicios independientes conectados a bases de datos relacionales y comunicación REST entre microservicios.

## Integrantes
- Martín Troncoso
- Jürgen Bormuth

## Microservicios desarrollados

### Productos
Microservicio encargado de administrar la información de productos disponibles en el sistema.

Funciones:
- Crear productos
- Listar productos
- Buscar productos por ID
- Actualizar productos
- Eliminar productos

### Inventario
Microservicio encargado de gestionar el stock y disponibilidad de productos.

Funciones:
- Registrar inventario
- Consultar stock
- Actualizar cantidades
- Eliminar registros de inventario
- Comunicación con microservicio Productos

## Tecnologías utilizadas
- Java
- Spring Boot
- Maven
- MySQL
- JPA / Hibernate
- Postman
- GitHub

## Endpoints implementados

### Productos http://localhost:8081/productos
- GET /productos
- GET /productos/{id}
- POST /productos
- PUT /productos/{id}
- DELETE /productos/{id}

Tabla guía:
{
    "nombre": "",
    "descripcion": " ",
    "precio": (precio normal).0,
    "stock": 15,
    "categoria": "",
    "proveedor": ""
} 
(editar con los datos que desee)

### Inventario http://localhost:8082/inventario
- GET /inventario
- GET /inventario/{id}
- POST /inventario
- PUT /inventario/{id}
- DELETE /inventario/{id}

Tabla guía:
{
    "id": (idproducto),
    "productoId": (),
    "stockActual": (),
    "stockMinimo": (),
    "ubicacion": ""
} 
(editar con los datos que desee)

## Comunicación entre microservicios
El microservicio Inventario consume información remota del microservicio Productos mediante endpoints REST.

## Prevención
- Al momento de utilizar el DELETE se debe recordar que obligatoriamente puede borrar tablas desde el microservicio Inventario y no Productos. La razón es que, nuestro programa funciona de manera que al borrar desde Inventario, automáticamente se eliminará de el microservicio Productos sin esfuerzo. Sin embargo, si se elimina desde Productos antes que Inventarios, se deberá eliminar también de forma manual la tabla del microservicio Inventario.(Esta exigencia es simplemente para acelerar el proceso.)

- Se debe usar en la base de datos un "ALTER TABLE productos AUTO_INCREMENT = (id eliminada);" y un ALTER TABLE inventario AUTO_INCREMENT = (misma id);
Al momento de eliminar una tabla, su ID seguirá en aumento. Por ejemplo: Si usted elimina la tabla ID:6  y no utiliza el comando AUTO_INCREMENT, al momento de crear una tabla se usará la ID:7, no la ID:6 ya que los datos seguiran en aumento. Es por eso que es un paso totalmente necesario para una creación prolija.

(Sí, los microservicios pueden crear y eliminar tablas normalmente sin necesidad de usar el comando, esto se implementó solamente para obtener una respuesta más "ordenada" a la hora de trabajar.)