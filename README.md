# API
[APRENDIBLE](https://www.youtube.com/watch?v=AqsM4ZKW8v0&list=PLpKWS6gp0jd-FRvVvaMzbYPu3gAJZfQQ4&index=4&ab_channel=Aprendible)

## Application Programming Interface
Interfaz de Programación de Aplicaciones


Peticiones <-----> Respuestas

## Arquitectura REST
REpresentational State Transfer
Transferencia de Estado Representacional

La arquitectura se basa en 6 restricciones

1. Client-Server: Cliente - servidor
   Separación de responsabilidades, la API debe estar separada del cliente
2. Stateless: Sin estado
   Cada petición contiene toda la información necesaria para que el servidor la procese
   El estado de sesión del usuario se mantiene totalmente en el cliente.
   Se utilizan access token para la autenticación
3. Cacheable: En caché
   Las respuestas se la API se pueden almacenar en caché de forma implícita, explícita y/o negociable.
4. Uniform Interfaz: Interfaz uniforme
   La petición deberá identifica los recursos que está buscando a través de una URL.
   En las respuestas se proveen hipervínculos que permiten navegar por la API.
5. Layered System: Sistema de capas
   Orientados a la escalabilidad, el cliente no sabe si la petición la resuelve el servidor, un sistema de cachés o un balanceador de cargas.
6. Code-on-demand: Código en demanda
   El servidor puede extender o personalizar temporalmente la funcionalidad del cliente mediante transferencia de lógica.

API RESTful funciona mediante el protocolo HTTP

### Recurso
Información, datos, cualquier cosa que se pueda nombrar y acceder a través de una URL específica.
- Documento, imágen, colección de recursos.

## Peticiones HTTP
- Método: Verbo HTTP
  - GET - Obtener recursos
  - POST - Crear un recurso
  - PUT - Reemplazar un recurso
  - PATCH - Actualizar un recurso
  - DELETE - Eliminar un recurso
- URI: Uniform Resource Identifier
  Permite interactuar con el recurso
- Payload: Cuerpo
  Representación de un recurso para su actualización
- Header
- Cookie
- Query

## Respuestas HTTP
Códigos de estado:

- Información: 1xx
- Exitosos: 2xx
  - 200 OK
  - 201 Created
  - 204 No Content
- Redirección: 3xx
  - 301 Moved Permanently
  - 302 | 303 Found at this other URL
  - 307 Temporary redirect
  - 308 Permanent redirect
- Error del cliente: 4xx
  - 400 Bad request
  - 401 Unauthorized
  - 403 Forbidden
  - 404 Not found
  - 405 Method not allowed
- Error del servidor: 5xx
  - 500 Internal Server Error
  - 502 Bad Gateway
  - 503 Service Unavaliable

## JSON:API Specification
Es una especificación de cómo un cliente debe solicitar que se busquen o modifiquen los recursos y cómo un servidor debe responder a esas solicitudes.

- ### Convención
  - Al tener reglas preestablecidas, tanto en el backend como en el frontend pueden ser desarrollados en paralelo.
  - Se minimiza el tiempo de desarrollo, al no tener que crear una propia convención.
  - Es replicable y reutilizable.

- ### Herramientas
  - Existen herramientas que ayudan a la adhesión de esta especificación.
  - [JsonApi.org/implementations](https://jsonapi.org/implementations/)

- ### Buenas prácticas

## Estructura de un documento
Documento ss el cuerpo de una petición o respuesta, objeto de JSON con la siguiente estructura:

````
{
  "data" : [],
  "errors" : [],
  "meta" : {},
  "included" : [],
  "links" : {},
  "jsonapi" : {}
}
````

Unicamente puede existir data o errors en una respuesta. El resto puede combinarse según las necesidades.

- ### Data
  Contiene la información principal del documento, puede ser un objeto o una colección de objetos, puede ser nulo o una colección vacía.
  - Resource object
    - Cada objeto se conoce como *Resource Object* (Objeto de recurso) que contenga un tipo y un identificador, ambos obligatorios y son cadena de caracteres.
      - `type` El tipo de objeto
      - `id` Identificador
    - El objeto en su mas mínima expresión se le conoce como *Resource Identifier Object*.
    - Otros elementos
      - `attributes` Contiene todos los atributos del recurso.
      - `relationships` Contiene las relaciones con otros recursos.
      - `links` Contiene un link a si mismo.
      - `meta` Cualquier información adicional.

- ### Errors
  Debe ser una colección que contiene todos los objetos de error.

- ### Meta
  Cualquier información adicional que queramos enviar.

- ### Jsonapi
  Objeto que contiene la versión de la API, si no se envía, se asume que es la versión 1.0.

- ### Links
  Links de paginación para navegar, es común combinarlos con el objeto meta.

- ### Included
  Si se desean incluir los datos y atributos de una relación de objetos, es opcional e incluye todos los objetos de recursos relacionados con los datos primarios. Se le llama también documento compuesto.

## Query parameters

- ### Include
  Indica a la API que relación debe incluir en la respuesta.
- ### Sort
  Ordenar registros, con prioridad de izquierda a derecha. Con el símbolo - se ordena descendentemente.
- ### Sparse Fieldsets
  Qué atributos queremos de uno o varios recursos.
- ### Filter
  Filtrar los resultados, hacer búsquedas generales sobre los atributes.
- ### Page
  Paginación de resultados
  - page[size]: Cantidad de recursos por página.
  - page[number]: Número de página.

## Content Negotiation
Tanto las peticiones del cliente como las respuestas del servidor deben tener el header

````
"Content-Type": "application/vnd.api+json"
````