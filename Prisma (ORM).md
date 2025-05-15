Prisma ORM es una herramienta moderna de mapeo objeto-relacional (ORM) diseñada para trabajar con diversas bases de datos en aplicaciones de Node.js, incluyendo aplicaciones construidas con Next.js. Prisma facilita el manejo de operaciones de base de datos mediante un modelo de datos y una API de consulta de alto nivel que se integra de manera eficiente en el ecosistema de JavaScript y TypeScript.

## Configuración Inicial

1. **Instalación:** Primero, necesitas instalar Prisma CLI y Prisma Client en tu proyecto Next.js:
``` bash
npm install prisma --save-dev
npm install @prisma/client
```
   
2. **Inicialización:** Inicializa Prisma en el proyecto:
``` bash
npx prisma init
```

Esto crea un nuevo directorio `prisma` con un archivo `schema.prisma`, donde defines tu modelo de datos y otro `.env` donde defines los datos de conexión.

3. **Fichero .env:**  En el fichero `.env` debemos especificar la información para poder conectar la aplicación a la base de datos. Tendremos que especificar el driver que usaremos, el usuario, contraseña, etc. La sintaxis es la siguiente:
   `DATABASE_URL="<driver>://<user>:<password>@<hostname>/<db>?schema=public"`. Por ejemplo:
``` env
	DATABASE_URL="mysql://root:@localhost:3306/recetarium?schema=public"
```

4. **Modelo de Datos:** En el archivo `schema.prisma`, defines los modelos que corresponden a las tablas en tu base de datos. Por ejemplo:
``` prisma
model User {
	id    Int    @id @default(autoincrement()) //id
	name  String @db.VarChar(100) //Crea strings de tipo varchar(100)
	email String @unique //declara un valor unico
	age   Int   //declara un numero
	createdAt DateTime @default(now()) //declara la columna de creacion
	updatedAt DateTime @updatedAt //declara la columna de actualizacion
}
```
para poder consultar todos los tipos de datos y sus parámetros, podéis consultar la pagina web de la documentación [Models | Prisma Documentation](https://www.prisma.io/docs/orm/prisma-schema/data-model/models) y [Prisma Schema API | Prisma Documentation](https://www.prisma.io/docs/orm/reference/prisma-schema-reference)  

  5. **Migraciones:** Genera y ejecuta migraciones para crear o actualizar la estructura de tu base de datos según el modelo definido:

``` bash
npx prisma migrate dev --name init
```

## Integración con Next.js

Prisma puede ser utilizado tanto en el servidor de API de Next.js como en App routes para realizar operaciones de base de datos:

1. **Fichero de conexión:** Para poder conectarnos a prisma, tenemos que crear un objeto de tipo `PrismaClient` para ello, lo habitual es crear un fichero dentro del directorio `/src` llamado `/src/lib` el fichero normalmente tiene como nombre `prisma.js` o `prisma.ts`. En el, tenemos crearemos la conexión de manera global, para poder llamarlo desde cualquier sitio, en caso contrario, tendríamos que crear una instancia de Prisma en cada componente. Nos debería queda de la siguiente manera: 
   **Importante:** tenéis que tener en cuenta que la ruta del cliente tiene que ser la que esta en la carpeta `generated` **no** la que esta en `node_modules` 
``` js
import { PrismaClient } from "@/generated/prisma/client";

let prisma;
if (process.env.NODE_ENV === "production") {
    prisma = new PrismaClient();
} else {
    if (!global.prisma) {
        global.prisma = new PrismaClient();
    }
    prisma = global.prisma;
}
export default prisma;
```
 - Ahora, lo primero que tenemos que hacer es ejecutar el siguiente comando para que prisma lea el esquema de datos, crea o actualize el cliente prisma, genere el código e instancie el cliente prisma:
```bash
npx prisma generate
```
- Una vez creada la carpeta `generated/prisma` podemos ejecutar el servidor
```
npm run dev
```
- para evitar tener que hacer este proceso cada vez que modifiquemos los esquemas o configuración de prisma, podemos automatizarlo añadiendo en `package.json` lo siguiente: 
```
{
  "scripts": {
    "postinstall": "prisma generate",
    "dev": "next dev"
    ....
  }
}
```

2. **En API Routes:** Puedes utilizar Prisma para interactuar con la base de datos directamente desde las rutas API de Next.js. Por ejemplo, en `pages/api/users.js` podrías tener:
``` javascript
import { PrismaClient } from '@prisma/client';
const prisma = new PrismaClient();

export default async function handler(req, res) {
	const users = await prisma.user.findMany();
	res.json(users); 
}
```

3. **En App Router:** También puedes usar Prisma con componentes o rutas App para recuperar datos antes de renderizar una página:

``` javascript
import prisma from "@/lib/prisma";

export default async function Page() {
  const users = await prisma.user.findMany();
  return (
    <main>
      <h1>Usuarios</h1>
      <ul>
        {users.map(u => (
          <li key={u.id}>{u.name} – {u.email}</li>
        ))}
      </ul>
    </main>
  );
}
```    

Para poder acceder a la base de datos, prisma ofrece una alternativa simplificada que es el "studio", para acceder a el, podemos entrar utilizando el comando:
```bash 
npx prisma studio
```

### Beneficios de Usar Prisma con Next.js

- **Seguridad Tipo:** Prisma ofrece un sistema de tipado fuerte que ayuda a evitar errores comunes en tiempo de ejecución y mejora la calidad del código.
- **Facilidad de Uso:** Prisma reduce la complejidad del código necesario para interactuar con la base de datos, gracias a su API intuitiva y potente.
- **Rendimiento:** Optimizado para trabajar eficientemente en entornos de servidor y durante el renderizado del lado del servidor en Next.js.
