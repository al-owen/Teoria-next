1. Next, por defecto, renderiza los componentes en el servidor.
2. Si hago un console log no se muestra en el cliente porque usa componentes de servidor.
3. Los enlaces se hacen mediante directorios en el caso de rutas dinámicas usamos `[]`, por ejemplo `[slug]`.
4. Usar `<Link>`, envés de `<a>` para que la página no tenga que recargar.
5. Page, icon.png y Layout son palabras reservadas. 
	1. Tal como index.html, `page.js` o `page.tsx`, sirve para indicar el fichero principal dentro de cada ruta.
	2. Layout es el fichero donde se pone los elementos en común, ya sea en general (en toda la página) o solo aplique a una ruta en concreto. Es necesario que exista como mínimo un fichero de layout en root.
	3. `metadata` es otra palabra reservada que sirve para declarar objetos de metadatos, lo que en html sería `<head>`
	4. `icon.png` es otro nombre reservado que, por defecto se usara como el favicon de la página. 
6. **Nota importante:** algunas extensiones pueden generar un error `Warning: Extra attributes from the server: class`, en principio, desactivando `I still don't care about cookies` me soluciono el problema, pero puede que haya otras extensiones (especialmente relacionadas con las cookies) que generen el mismo error.

## Parte 2 

1. Cuando usamos componentes de cliente tenemos que especificarlo
2. Podemos escapar de una string de la siguiente manera:
``` jsx
export default function test(){
	const color = "red"
	return(
		<div className={`font-bold text-center 
		h-screen ${color === 'red'? 'text-red-500': 'text-blue-500'}`}>
	        <h1>Hola mundo!</h1>
	    </div>
	)
}
```
3. Las apis se generan en directorios dentro del directorio `api` y se declaran rellenando un fichero llamado `route.js` o `route.ts` dentro del fichero se declaran los métodos POST, GET, PUT, DELETE, UPDATE, etc.
4. Para hacer la petición a la base de datos, se pueden usar ORMs como prisma, consultas vainilla o con librerías como `Axios`.
5. 