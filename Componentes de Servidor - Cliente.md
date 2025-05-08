En el desarrollo web moderno, particularmente en frameworks como Next.js, es común diferenciar entre componentes de servidor y componentes de cliente, cada uno con roles específicos en la construcción y optimización de aplicaciones.

[Rendering: Composition Patterns | Next.js](https://nextjs.org/docs/app/building-your-application/rendering/composition-patterns)

| Que necesitas hacer?                                                         | Server Component | Client Component |
| ---------------------------------------------------------------------------- | ---------------- | ---------------- |
| Fetch data                                                                   | ✔️               | X                |
| Access backend resources (directly)                                          | ✔️               | X                |
| Keep sensitive information on the server (access tokens, API keys, etc)      | ✔️               | X                |
| Keep large dependencies on the server / Reduce client-side JavaScript        | ✔️               | X                |
| Add interactivity and event listeners (onClick(), onChange(), etc)           | X                | ✔️               |
| Use State and Lifecycle Effects (useState(), useReducer(), useEffect(), etc) | X                | ✔️               |
| Use browser-only APIs                                                        | X                | ✔️               |
| Use custom hooks that depend on state, effects, or browser-only APIs         | X                | ✔️               |
| Use React Class components                                                   | X                | ✔️               |

### Componentes de Servidor

Los **componentes de servidor** son ejecutados durante el proceso de renderizado en el servidor, antes de que la página sea enviada al navegador del usuario. Este enfoque es parte de lo que se conoce como renderizado del lado del servidor (SSR, por sus siglas en inglés). Los componentes de servidor pueden realizar tareas como la obtención de datos desde una base de datos o una API externa, manipulación de sesiones, y configuraciones iniciales antes de que la página sea visible al usuario. En Next.js, estos componentes se utilizan para asegurar que el contenido crítico sea cargado de manera eficiente y esté disponible de inmediato al cargar la página.

Una ventaja significativa de usar componentes de servidor es mejorar la velocidad percibida de carga de la página y la optimización para motores de búsqueda (SEO), ya que el contenido ya está presente en el HTML cuando llega al navegador.

### Componentes de Cliente

Los **componentes de cliente**, en cambio, se ejecutan en el navegador del usuario después de que la página ha sido cargada. Estos componentes son típicos en el renderizado del lado del cliente (CSR, por sus siglas en inglés). Son responsables de manejar interacciones del usuario, efectos dinámicos, eventos, y actualizaciones de estado que dependen de la interacción en el cliente. En el contexto de Next.js, aunque el renderizado inicial se haga en el servidor, los componentes de cliente toman el relevo para cualquier actualización dinámica y manejo de estado con React en el navegador.

Una ventaja de los componentes de cliente es su capacidad para crear experiencias de usuario altamente interactivas y dinámicas. Pueden responder en tiempo real a las acciones del usuario sin necesidad de volver a consultar al servidor, lo que es ideal para aplicaciones web dinámicas y ricas en características.

Para especificar el ámbito en el que una tarea se debe ejecutar (servidor o cliente) tenemos que tener en cuenta 2 cosas: por defecto los componentes son de servidor y si queremos cambiar a que el componente sea de tipo cliente tenemos que usar `"use client"` al inicio del fichero. Por lo general si queremos usar hooks se deben hacer en un componente de cliente, dado que es un valor que habitualmente variará dependiendo de las acciones que tome el usuario.

Ejemplo de componente cliente:

``` JSX
"use client"; //al utilizar un hook debemos hacer el componente cliente 
import Link from "next/link";
import { usePathname } from "next/navigation";

export default function LinkNav({ href, children }) {
	const path = usePathname();
	return (
		<Link
		href={href}
		className={`block transition-colors hover:text-red-500 duration-300" px-4 py-3 text-grey-200 bg-slate-900 rounded ${path.startsWith(href) ? 'text-orange-400' : 'text-white'}`}>
			{children}
		</Link>
	);
}
```