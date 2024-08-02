# Documentación del Proyecto: API RESTful CRUD con Spring Boot 3

## Descripción del Proyecto
Este proyecto es una aplicación construida con Spring Boot 3 que implementa una API RESTful para realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre una única tabla en una base de datos. La tabla se mapea al objeto `Product`, y sus atributos son validados usando anotaciones personalizadas. El proyecto incluye un controlador que define las rutas HTTP necesarias para el CRUD y maneja los mensajes de error de validación de campos.

## Estructura del Proyecto

### Configuración y Dependencias:
- `pom.xml`: Archivo de configuración de Maven que gestiona las dependencias del proyecto.
- `.mvn/wrapper`: Directorio que contiene los archivos necesarios para usar Maven Wrapper.

### Código Fuente:
- `src/main/java/com/app/springboot/springboot_crud/`: Directorio principal que contiene el código Java dividido en diferentes paquetes:
  - `controllers`: Contiene el controlador `ProductController`.
  - `entities`: Contiene la entidad `Product`.
  - `repositories`: Contiene el repositorio `ProductRepository`.
  - `services`: Contiene la interfaz `ProductService` y su implementación `ProductServiceImpl`.
  - `validation`: Contiene las clases de validación y las anotaciones personalizadas.

### Recursos:
- `src/main/resources/application.properties`: Archivo de configuración de la aplicación.
- `src/main/resources/messages.properties`: Archivo de propiedades que contiene los mensajes personalizados.

## Funcionamiento de la Aplicación
La aplicación proporciona una API RESTful para gestionar productos, permitiendo realizar operaciones CRUD sobre la entidad `Product`. Los atributos del producto son validados utilizando anotaciones personalizadas para asegurar que los datos cumplen con ciertas restricciones antes de ser procesados.

### Controlador (ProductController)
El controlador define las rutas HTTP necesarias para realizar las operaciones CRUD. Utiliza las anotaciones `@RestController`, `@RequestMapping`, `@GetMapping`, `@PostMapping`, `@PutMapping` y `@DeleteMapping` para mapear las solicitudes HTTP a los métodos correspondientes.

- `@RestController`: Marca una clase como un controlador donde cada método retorna un objeto de dominio en lugar de una vista. Es una combinación de `@Controller` y `@ResponseBody`.
- `@RequestMapping`: Anotación utilizada para mapear solicitudes web a métodos específicos en clases de controladores.
- `@GetMapping`: Maneja solicitudes HTTP GET.
- `@PostMapping`: Maneja solicitudes HTTP POST.
- `@PutMapping`: Maneja solicitudes HTTP PUT.
- `@DeleteMapping`: Maneja solicitudes HTTP DELETE.

### Entidad (Product)
La entidad `Product` representa la tabla en la base de datos. Cada instancia de `Product` corresponde a una fila en la tabla. Los atributos de la entidad son validados usando anotaciones como `@IsRequired` y `@IsExistsDB`.

- `@Entity`: Indica que una clase es una entidad JPA (Java Persistence API) y se mapea a una tabla en la base de datos.
- `@Table`: Especifica el nombre de la tabla en la base de datos asociada con la entidad.
- `@Id`: Define el identificador único de la entidad.
- `@GeneratedValue`: Especifica cómo se genera el valor del identificador, por ejemplo, de manera automática.

### Repositorio (ProductRepository)
El repositorio es una interfaz que extiende `JpaRepository`, proporcionando métodos CRUD estándar para interactuar con la base de datos.

- `JpaRepository`: Interfaz de Spring Data JPA que proporciona métodos CRUD y de paginación/sorting para trabajar con entidades JPA.

### Servicio (ProductService y ProductServiceImpl)
El servicio define la lógica de negocio y se comunica con el repositorio para realizar las operaciones CRUD.

- `@Service`: Indica que una clase es un servicio, un componente de la capa de negocio de la aplicación.

### Validación de Campos
La validación de los atributos de `Product` se realiza utilizando dos anotaciones personalizadas: `@IsRequired` y `@IsExistsDB`. Estas anotaciones se manejan en clases que implementan `ConstraintValidator`.

#### Anotaciones Personalizadas
- `@IsRequired`: Asegura que un campo no sea nulo o vacío.
- `@IsExistsDB`: Verifica que el valor de un campo existe en la base de datos.

#### Implementación de ConstraintValidator
Cada anotación personalizada tiene una clase asociada que implementa `ConstraintValidator` y define la lógica de validación.

- `@Constraint`: Anotación utilizada para marcar una anotación como una restricción de validación. Se utiliza junto con `@Target` y `@Retention`.
- `@Target`: Indica los elementos del programa a los que se puede aplicar una anotación (por ejemplo, campos, métodos).
- `@Retention`: Especifica cuánto tiempo se retiene una anotación (por ejemplo, en tiempo de ejecución).

#### Ejemplo de Anotaciones Personalizadas
- `@IsRequired`: Se utiliza para verificar que un campo no sea nulo o vacío.
  - Clase asociada: `IsRequiredValidation` que implementa `ConstraintValidator<IsRequired, String>` y define la lógica de validación para verificar que el campo no sea nulo o vacío.
- `@IsExistsDB`: Se utiliza para verificar que un valor exista en la base de datos.
  - Clase asociada: `IsExistsValidation` que implementa `ConstraintValidator<IsExistsDB, Long>` y define la lógica de validación para verificar que el valor existe en la base de datos.

### Anotaciones y Librerías Utilizadas
- `@Valid`: Utilizada para indicar que un objeto debe ser validado antes de procesar una solicitud. Se coloca delante del objeto en el controlador.
- `BindingResult`: Interfaz utilizada para detectar y manejar errores de validación. Se coloca como parámetro en los métodos del controlador junto con el objeto validado.
- `@Constraint`: Marca una anotación como una restricción de validación.
- `@Target`: Especifica los elementos del programa a los que se aplica una anotación.
- `@Retention`: Indica cuánto tiempo se retiene una anotación.
- `ConstraintValidator`: Interfaz que debe ser implementada por las clases que definen la lógica de validación de una anotación.

### Mensajes Personalizados
Los mensajes de error personalizados se configuran en `messages.properties`. La anotación `@PropertySource("classpath:messages.properties")` se usa para cargar estos mensajes en la aplicación.

- `@PropertySource`: Anotación utilizada para indicar la ubicación de un archivo de propiedades.

#### Ejemplo de Configuración de Mensajes Personalizados
- `messages.properties`: Archivo de propiedades que contiene los mensajes personalizados de error. Ejemplo:
  ```properties
  error.product.notfound=Product not found
  error.product.required=Product field is required


Este proyecto de Spring Boot 3 demuestra cómo construir una API RESTful para realizar operaciones CRUD con validaciones de atributos utilizando anotaciones personalizadas. La organización clara del código y la separación de responsabilidades aseguran una aplicación mantenible y escalable. Las anotaciones personalizadas y los mensajes de error personalizados proporcionan una robusta validación de datos, mejorando la integridad y la usabilidad de la aplicación.
