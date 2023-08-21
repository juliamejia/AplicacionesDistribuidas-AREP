# AplicacionesDistribuidas-AREP
construir una aplicación para consultar la información de películas de cine.  
Julia Marcela Mejia Perez  
## EJECUCION 
1. Clonar el repositorio usando este codigo desde el cmd, en la carpeta que gustes  
    `git clone https://github.com/juliamejia/AplicacionesDistribuidas-AREP.git`

2. Dentro de la carpeta llamada networking abrimos el cmd y ejecutamos el siguiente comando  
   `mvn clean package exec:java -D "exec.mainClass"="org.example.HttpServer"`
   lo cual nos mostrará que el proyecto se ejecutó correctamente  
   <img width="567" alt="image" src="https://github.com/juliamejia/AplicacionesDistribuidas-AREP/assets/98657146/a2d6e0cd-2cc7-4998-8636-f09336c65408">  

3. Desde cualquier browser, digitamos la direccion http://localhost:35000 como se muestra en la imagen
   <img width="417" alt="image" src="https://github.com/juliamejia/AplicacionesDistribuidas-AREP/assets/98657146/737bb3ee-d13a-4783-a8bb-cb20a011dc1d">

4. Digitamos la pelicula que estamos buscando y nos muestra toda la información acerca de esa pelicula
   <img width="914" alt="image" src="https://github.com/juliamejia/AplicacionesDistribuidas-AREP/assets/98657146/73ebe8e3-71e7-4ecd-a338-3e831c785045">

5. Para visualizar el javadoc ejecutamos el siguiente comando  
    `mvn javadoc:javadoc"` y vamos a la carpeta networking->target->site->apidocs donde encontraremos todos los documentos creados como se muestra en la imagen   
    <img width="618" alt="image" src="https://github.com/juliamejia/AplicacionesDistribuidas-AREP/assets/98657146/2da5584d-b117-4b05-9b47-fa0986ebf50b">

## TEST  
Para correr los test ejecutamos el comando `mvn test` dentro de la carpeta networking  
    <img width="429" alt="image" src="https://github.com/juliamejia/AplicacionesDistribuidas-AREP/assets/98657146/179f5ebc-034f-4f6a-a399-436f1b00230d">  


# Descripcion  
## Extensible 
Es extensible en la clase HttpConnection ya que:  
   * encapsula la lógica para realizar solicitudes HTTP a la API de OMDB. Esto significa que puede reutilizar fácilmente esta clase en diferentes partes de su   aplicación siempre que necesite obtener datos de la API de OMDB.  
   * El uso de constantes para la URL base y la clave API permite una fácil configuración de estos valores. Si necesita cambiar el punto final o la clave de la API, solo necesita actualizar estas constantes.  
   * Separación de preocupaciones: la clase se enfoca en la comunicación HTTP y el manejo de respuestas API. Esta separación le permite cambiar o mejorar la lógica de comunicación HTTP sin afectar el resto de su aplicación.

Tambien es extensible en la clase Caché ya que: 
* Establece un mecanismo de almacenamiento en caché simple utilizando un ConcurrentHashMap, que permite el almacenamiento eficiente y seguro de subprocesos de pares clave-valor. La estructura del código hace que sea relativamente sencillo agregar más funciones o realizar mejoras en el futuro.

## Patrones  
* Tiene Enfoque Modelo-Vista-Controlador (MVC):  
Si bien no está completamente implementado, el código exhibe una separación rudimentaria de preocupaciones similar al patrón MVC. La configuración del servidor y el manejo de solicitudes se pueden considerar como el controlador y la generación de respuestas como parte de la vista.  
* Patrón de método de plantilla (en getHello y getIndexResponse):  
Se puede considerar que los métodos getHello y getIndexResponse aplican un patrón de método de plantilla. Definen la estructura de generación de respuestas, pero permiten que las subclases proporcionen partes específicas (contenido HTML/JSON) (o en este caso, llamadas a métodos como crearTabla).
* Patrón de estrategia (potencial):  
El código podría evolucionar potencialmente para aplicar el patrón de estrategia si abstrae la generación de respuesta en clases separadas y usa una interfaz o clase base para definir la estructura común (como el patrón de método de plantilla). Esto permitiría intercambiar fácilmente diferentes estrategias de respuesta (HTML, JSON, etc.).
** Patrón de proxy o adaptador (potencial):
Dependiendo de cómo interactuaría con la API de OMDB, es posible que necesite usar un patrón de Proxy o Adaptador para encapsular las interacciones de la API de una manera más estructurada y abstracta.  

## Modular  
1. Diseño Modular en HttpConnection  
Se puede modularizar aún más separando las preocupaciones y brindando más flexibilidad:  
* Moviendo la lógica de comunicación de la API a su propia clase, permitiría una mejor encapsulación y pruebas más sencillas. La clase podría encapsular métodos como getResponse, buildRequestUrl y parseApiResponse.  
* Pasar las dependencias necesarias (URL, clave API) a través del constructor o los parámetros del método, lo que hace que la clase sea más flexible y fácil de probar.  
* Implementae el manejo de errores adecuado dentro de esta clase y genere excepciones que el código de llamada pueda detectar y manejar adecuadamente.  

2. Diseño Modular en HttpServer:  
Se puede modularizar para lograr una mejor separación de preocupaciones:  
* Extrayendo la lógica de configuración del servidor en una clase separada que maneje la inicialización y configuración del servidor. Esto podría incluir métodos para iniciar, detener y configurar el servidor.  
* Implementar un enrutador o una clase de controlador de solicitudes responsable de enrutar las solicitudes entrantes a los controladores apropiados según el URI u otros criterios. De esta manera, puede extender fácilmente el servidor para manejar diferentes tipos de solicitudes.  









