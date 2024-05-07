El enrutamiento con el directorio `app` en Next.js representa una evolución significativa en cómo se manejan las rutas en aplicaciones construidas con esta plataforma. Este sistema, introducido en la versión 13, proporciona una forma más flexible y organizada de definir rutas y componentes relacionados.
## Estructura de Carpetas

En el directorio `app`, cada carpeta representa una ruta potencial en tu aplicación. Los nombres de las carpetas se traducen directamente en rutas en la URL. Por ejemplo, una carpeta llamada `about` se accederá mediante `/about`.

## Archivos Page

Dentro de cada carpeta de ruta, puedes colocar un archivo llamado `page.tsx` (o `page.js` si estás utilizando JavaScript). Este archivo define el componente de React que se renderiza cuando se accede a esa ruta específica. Por ejemplo, para la ruta `/about`, Next.js buscará un archivo `about/page.tsx` dentro del directorio `app`.

## Archivos Layout

Además de los archivos de página, puedes definir archivos de layout, que ayudan a establecer componentes comunes de UI que envuelven una o más páginas. Por ejemplo, puedes tener un archivo `layout.tsx` en la raíz del directorio `app` que aplica un diseño común a todas las páginas, o puedes tener diseños específicos dentro de subdirectorios para aplicar diferentes estilos o estructuras a grupos de páginas.

## Rutas Anidadas

El enrutamiento anidado se maneja fácilmente al crear subcarpetas dentro de las carpetas de rutas. Cada subcarpeta puede tener su propio archivo `page.js`, permitiendo la creación de rutas más detalladas y estructuradas, como `/about/team` para un archivo ubicado en `app/about/team/page.tsx`.

## Rutas Dinámicas

Puedes crear rutas dinámicas utilizando corchetes en los nombres de las carpetas, por ejemplo, `[id]`. Esto indica que la parte de la ruta es variable, como en `/posts/[id]`, donde diferentes valores de `id` renderizarán diferentes páginas basadas en datos correspondientes.

## Rutas y Grupos Paralelos

Las rutas paralelas y los grupos de rutas ofrecen maneras avanzadas de agrupar y manejar múltiples componentes y páginas bajo una sola estructura de layout. Por ejemplo, puedes tener un grupo de rutas que comparte un layout común sin que el nombre del grupo aparezca en la URL, utilizando paréntesis en el nombre de la carpeta, como `(group)`. Las rutas paralelas se utilizan para renderizar múltiples rutas simultáneamente y se denotan con un `@` al principio del nombre de la carpeta.