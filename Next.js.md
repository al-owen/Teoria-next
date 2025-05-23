Next.js es un framework de desarrollo web basado en React que permite la creación de aplicaciones web modernas con renderizado del lado del servidor (SSR) y generación de sitios estáticos (SSG). Los fundamentos de cómo funciona Next.js son los siguientes:

### 1. Renderizado del Lado del Servidor (SSR)

Next.js mejora el rendimiento y la indexabilidad de las aplicaciones al permitir que las páginas se rendericen en el servidor antes de ser enviadas al navegador. Esto significa que el servidor genera el HTML completo de cada página en respuesta a las solicitudes de los usuarios, lo cual es especialmente beneficioso para el SEO y el tiempo de carga inicial. Los datos necesarios para renderizar las páginas, como las consultas a una base de datos o llamadas a APIs externas, se manejan durante este proceso.

### 2. Generación Estática de Sitios (SSG)

Next.js también soporta la generación estática de sitios, lo que permite pre-renderizar páginas durante el tiempo de compilación. Esto se traduce en archivos HTML estáticos que pueden servirse rápidamente desde un CDN. Esta técnica es ideal para sitios que no cambian con frecuencia y necesitan tiempos de carga ultrarrápidos.

### 3. Enrutamiento Basado en el Sistema de Archivos

#### Forma antigua 
El enrutamiento en Next.js se maneja mediante el sistema de archivos en el directorio `pages`. Cada archivo JS, JSX, TS o TSX en el directorio `pages` se convierte automáticamente en una ruta accesible. Por ejemplo, `pages/about.js` se traduce en `www.tusitio.com/about`. Este enrutamiento incluye soporte para parámetros dinámicos, rutas API y carga perezosa de componentes. 

#### Forma moderna (recomendada)
También existe una nueva forma de enrutar las páginas que es mediante un sistema llamado "App Routes", este nuevo sistema de enrutamiento funciona con la carpeta  `/app` introduce una arquitectura mucho más modular. Aquí, las rutas se definen mediante carpetas y archivos `page.js`, pero además se pueden incluir archivos especiales como `layout.js` (para definir layouts persistentes por sección), `loading.js` (para mostrar una interfaz de carga mientras se obtiene contenido), `error.js` (para manejar errores por ruta), y más. Este nuevo enfoque también incorpora el uso de Server Components, lo cual permiten renderizar componentes directamente en el propio servidor de forma eficiente, reduciendo el tamaño del JavaScript enviado al cliente y mejorando su rendimiento.

### 4. Optimizaciones Automáticas

Next.js viene con una serie de optimizaciones automáticas, como la división automática de código para cargar solo el JavaScript necesario para renderizar la página actual, soporte para imágenes optimizadas, y mucho más. Estas optimizaciones ayudan a mejorar la velocidad de la página y la experiencia del usuario sin esfuerzo manual adicional.

### 5. API Routes

Next.js permite crear funciones API directamente dentro del fichero `routes.js`. Cada archivo en este directorio se trata como un endpoint de API separado. Estas API routes son ideales para manejar lógica del lado del servidor, operaciones de base de datos, o como parte de una arquitectura de microservicios.