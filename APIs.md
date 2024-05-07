En Next.js 14, el enrutamiento para APIs ha evolucionado con la introducción de los **Route Handlers** en el directorio `app`. Estos manejadores permiten una forma más flexible y organizada de gestionar las rutas API dentro de tu aplicación Next.js.

### Estructura del Directorio

Los Route Handlers se colocan dentro del directorio `app/api`. Cada archivo dentro de este directorio se denomina `route.ts` (o `route.js` si usas JavaScript). La URL de acceso a cada manejador está determinada por la estructura del directorio que contiene el archivo `route.ts`. Por ejemplo, un manejador de rutas en `app/api/users/route.ts` manejará las solicitudes a `/api/users`​.

### Sintaxis de Route Handlers

Dentro de cada archivo `route.ts`, defines funciones específicas para cada tipo de solicitud HTTP, como GET, POST, PUT, etc. Esto es un cambio respecto a la estructura anterior del directorio `pages`, donde un solo archivo API manejaba todos los tipos de solicitudes. Esta nueva estructura permite manejar de manera más efectiva y clara las diferentes solicitudes HTTP sin necesidad de utilizar declaraciones condicionales complicadas dentro de una única función.

### Ejemplo de Uso

Por ejemplo, en un archivo `route.ts`, podrías tener algo así:

```js
import { NextRequest } from "next/server";
export async function GET(request) {
	const data = { message: "Hello from the API" };
	return NextResponse.json(data); 
}  
export async function POST(request) {   // Código para manejar una solicitud POST 
}
```

Cada función (GET, POST, etc.) maneja una solicitud HTTP específica. Esta estructura hace que sea sencillo escribir lógicas de servidor limpias y mantenibles​

### Ventajas

Los Route Handlers mejoran la organización del código y facilitan la implementación de lógicas API complejas dentro de las aplicaciones Next.js. Además, esta estructura apoya todas las mejoras de rendimiento y características modernas de Next.js, como la renderización en el servidor y la generación de sitios estáticos.