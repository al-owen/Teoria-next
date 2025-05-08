En Next.js, hay varios nombres de ficheros reservados que tienen un significado especial y se utilizan para configurar y controlar diferentes aspectos de una aplicación.

1. **`page.tsx` (o `page.js`)**: Este archivo define el componente React que se renderiza para una ruta determinada. Cada carpeta dentro del directorio `app` que contenga un archivo `page.tsx` representa una ruta accesible en la aplicación.
2. **`layout.tsx` (o `layout.js`)**: Utilizado para definir layouts que pueden envolver una o varias páginas. Estos layouts se aplican a todas las páginas dentro de su carpeta y subcarpetas, a menos que se especifique un layout diferente en las subcarpetas.
3. **`error.tsx` (o `error.js`)**: Este archivo permite personalizar la página de error que se muestra cuando ocurre un error no capturado durante el renderizado de la aplicación, como un error 404 o 500.
4. **`loading.tsx` (o `loading.js`)**: Proporciona una manera de definir un componente de carga que se mostrará mientras se cargan las páginas o datos asincrónicos dentro de la aplicación.
5. **`not-found.tsx` (o `not-found.js`)**: Se utiliza para personalizar la página que se muestra cuando la URL no coincide con ninguna ruta definida en la aplicación.
6. `route.tsx`(o `route.js`): Se utiliza para crear rutas API, por ejemplo, una página que no devuelva un codigo jsx, sino que devuelva datos en formato JSON.
Para obtener más información, nos debemos dirigir a la documentación oficial [API Reference: File Conventions | Next.js](https://nextjs.org/docs/app/api-reference/file-conventions)

