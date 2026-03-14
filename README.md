# 🧪 Laboratorio: Documentación de Pruebas de API REST

 Esta actividad debe documentarse íntegramente en este archivo `README.md`. Por cada punto, el estudiante debe ejecutar la petición indicada y completar los espacios en blanco con la **Respuesta del Servidor** y el **Código de Estado** real obtenido en su entorno local.

---

## 🚀 Guía de Pruebas y Documentación

### 1. Crear un nuevo estudiante

 1. Crear un nuevo estudiante
 - *Método*: POST
- *URL*: http://localhost:8080/api/students
- *Body (JSON)*:
    json
    {
      "firstName": "Deimer",
      "lastName": "Lara",
      "email": "Deimer@example.com",
      "birthDate": "1991-01-15",
      "phone": "3014445566"
    }
- **respuesta del servidor**:  
    json
     {
        "firstName": "Deimer",
        "lastName": "Lara",
        "email": "Deimer@example.com",
        "birthDate": "1991-01-15",
        "id": 1,
        "phone": "3014445566"
    }
- *codigo de estado (status code)*: 201 Created

### 2. Obtener la lista completa
- *Método*: GET
- *URL*: http://localhost:8080/api/students
- *Respuesta*:
    json
    
    {
        "firstName": "Deimer",
        "lastName": "Lara",
        "email": "Deimer@example.com",
        "birthDate": "1991-01-15",
        "id": 1,
        "phone": "3014445566"
    },
    {
        "firstName": "Pedro",
        "lastName": "Ruiz",
        "email": "pedro@example.com",
        "birthDate": "2000-01-15",
        "id": 2,
        "phone": "1234567890"
    },
    {
        "firstName": "juan",
        "lastName": "casa",
        "email": "mato@example.com",
        "birthDate": "2000-01-15",
        "id": 3,
        "phone": "1234567890"
    },
    {
        "firstName": "antonio",
        "lastName": "cañas",
        "email": "antonio@example.com",
        "birthDate": "2000-01-15",
        "id": 4,
        "phone": "1234567893"
    }

- **codigo de estado (status code)**:200 OK

### 3. buscar estudiante por ID (existente)
- **Método**: `GET`
- **URL**: `http://localhost:8080/api/students/2`
- **respuesta del servido**:
    json
    {
     "firstName": "Pedro",
        "lastName": "Ruiz",
        "email": "pedro@example.com",
        "birthDate": "2000-01-15",
        "id": 2,
        "phone": "1234567890"
    }
- *codigo de estado (status code)*:200 OK

### 4. Obtener un estudiante por Email
- *Método*: GET
- *URL*: http://localhost:8080/api/students/email/antonio@example.com
- *respuesta del servidor*:
    json
    {
    "firstName": "antonio",
        "lastName": "cañas",
        "email": "antonio@example.com",
        "birthDate": "2000-01-15",
        "id": 4,
        "phone": "1234567893"
    }
- **codigo de estado (status code)**:200 OK

### 5. Actualizar un estudiante
- **Método**: `PUT`
- **URL**: `http://localhost:8080/api/students/1`
- **Body (JSON)**:
    json
    { 
        "firstName": "Deimer",
        "lastName": "Lara",
        "email": "Deimer.yav@example.com",
        "birthDate": "1991-01-15",
        "phone": "3014445566"
    }
    
- **respuesta del servidor**:
    json
    {
     "firstName": "Deimer",
        "lastName": "Lara",
        "email": "Deimer.yav@example.com",
        "birthDate": "1991-01-15",
        "id": 1,
        "phone": "3014445566
    }
- *codigo de estado (status code)*:200 OK

### 6. Ecenario de error buscar ID inexistente
- *Método*: GET
- *URL*: http://localhost:8080/api/students/5
- *respuesta del servidor*:
Not Found
- *codigo de estado (status code)*:404 Not Found

### 7. Eliminar un estudiante
- *Método*: DELETE
- *URL*: http://localhost:8080/api/students/4
- *respuesta del servidor*:
No Content
- *codigo de estado (status code)*: 204 No Content


## cuestionario de analisis


### 1.¿Cuál es la diferencia entre los códigos de estado 200 y 201? ¿En qué endpoints se obtuvieron cada uno?

- *respuesta*:
200 : significa que la peticion fue exitosa
201 : significa que la peticion fue exitosa y ademas se creo un nuevo recurso
endpoints de 200 OK: GET, PUT, DELETE.
endpoints de 201 CREATED: POST.

### 2.En el escenario de error (punto 6), ¿qué información devuelve la API y por qué es importante para un desarrollador frontend recibir un código 404 en lugar de un código 500?

- *respuesta*:

Este devuelve fecha y hora del error, estatus del error,nombre del error.
Es mejor por que es mas especifico y permite al frontend manejar correctamente el error mejorando la esperiecia para el usuario ademas sigue las buenas practicas rest.

### 3.¿Qué sucede en la base de datos PostgreSQL cuando se ejecuta con éxito la petición DELETE? (Explique brevemente en términos de persistencia).

- *respuesta*:

Cuando la peticion DELETE se ejecuta con exito el servidor asu vez elimina el registro correspondiente . en terminos de persistencia :
- el registro deja de existir en la tabla
- ya no puede ser consutado mediente un GET
- la informacion se elimina de manera definitiva
- el combio queda almacenado 

### 4.Si intentara crear un estudiante con el mismo email que ya existe en la base de datos, ¿qué cree que sucedería y qué código de error sería el más adecuado para devolver?

- *respuesta*:

Si el campo tiene una restriccion UNIQUE postgreSQL rechazaria la insercion  generara una excepcion por violacion de integridad.El codigo de estatus que devolveria seria un 409 conflict que indicaria un conflicto entre los datos actuales

### 5.¿Por qué utilizamos el método PUT para actualizar y no el método POST? ¿Cuál es la convención técnica detrás de esta decisión?

- *respuesta*:

Se utiliza el metodo PUT para actualizar por que segun la convencion REST el endpoint PUT es modificar y el endpoint POST es para crear nuevos recursos sin ser idempotente, por el contrario PUT si lo es. Lo que significa que multiples solicitudes iguales producen elmismo resultado. Asi la api sera mas clara organizada y alineada