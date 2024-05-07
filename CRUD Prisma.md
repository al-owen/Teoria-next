Para poder hacer un crud básico usando prisma aquí tienes un ejemplo base de como debería hacerse:
En los siguientes ejemplos se asume que se esta usando el fichero de conexión global siguiente:
``` js
import { PrismaClient } from '@prisma/client';
const globalForPrisma = global;
const prisma = globalForPrisma.prisma || new PrismaClient();
if(process.env.NODE_ENV !== "production") globalForPrisma.prisma = prisma
export default prisma;
```
también se asume que se esta utilizando los ficheros `route.js` o `route.ts` dentro del directorio [[APIs]]. Para poder pasar valores dinámicos se usa `{params}` y para ello debemos crear el fichero `route.js` dentro de un directorio que tenga `[]`, por ejemplo `[id]`.

## Ejemplos:

### Mostrar todos

Este código recupera todos los registros de la tabla meal en la base de datos utilizando Prisma ORM y devuelve esos datos en formato JSON.

```js
import { NextResponse } from "next/server";
import prisma from "@/lib/prisma";

export async function GET() {
  try{
    // Intenta obtener todos los registros de comidas
    const meals = await prisma.meal.findMany();
    // Si tiene éxito, devuelve los registros con un estado HTTP 201
    return NextResponse.json({data:meals}, {status: 201});
  }catch(error){
    // En caso de error, devuelve un error HTTP 500
    return new NextResponse(error.message, {status: 500});
  }
}
```
### Crear

Este fragmento maneja la creación de un nuevo registro en la tabla meal. Utiliza los datos proporcionados en la solicitud POST para crear un nuevo registro.

``` js
import { NextResponse } from "next/server";
import prisma from "@/lib/prisma";

export async function POST(request) {
  try {
    // Extrae los datos del cuerpo de la solicitud
    const data = await request.json();
    // Crea un nuevo registro en la base de datos con esos datos
    const meal = await prisma.meal.create({ 
      data:data 
    });
    // Devuelve los datos del nuevo registro con un estado HTTP 201
    return new NextResponse(JSON.stringify(meal), {
      headers: {"Content-Type": "application/json"},
      status: 201
    });
  } catch (error) {
    // En caso de error, devuelve un error HTTP 500
    return new NextResponse(error.message, { status: 500});
  }
}
```

### Mostrar uno

Este código busca un registro específico por ID en la tabla meal. Si el registro no existe, devuelve un error 404.

``` js
import { NextResponse } from "next/server";
import prisma from "@/lib/prisma";

export async function GET(request, { params }) {
  const id = parseInt(params.id);
  try {
    // Intenta encontrar una comida específica por ID
    const meal = await prisma.meal.findFirst({
      where: {id: id},
    })
    if (!meal) {
      // Si no se encuentra la comida, devuelve un error 404
      return new NextResponse("Meal not found", { status: 404 });
    }
    // Si se encuentra la comida, devuelve los datos
    return new NextResponse(JSON.stringify(meal), { status: 200 });
  } catch (error) {
    // En caso de error, devuelve un error HTTP 500
    return new NextResponse(error.message, { status: 500});
  }
}
```

### Actualizar

Este fragmento actualiza un registro existente en la tabla meal basado en el ID proporcionado. Si el registro no existe, devuelve un error 404.

``` js
import { NextResponse } from "next/server";
import prisma from "@/lib/prisma";

export async function POST(request, { params }) {
  try {
    const id = parseInt(params.id);
    const data = await request.json();

    const result = await prisma.meal.update({
      where: {id: id},
      data: data
    })
    if (!result) {
      // Si no se encuentra la comida, devuelve un error 404
      return new NextResponse("Meal not found", { status: 404 });
    }
    // Si la actualización es exitosa, devuelve los datos actualizados
    return NextResponse.json({ message: result}, { status: 200 });
    
  } catch (error) {
    // En caso de error, devuelve un error HTTP 500
    return new NextResponse(error.message, { status: 500});
  }
}
```

### Eliminar

Este código elimina un registro de la tabla meal basado en el ID proporcionado. Si la operación es exitosa, devuelve un mensaje confirmando la eliminación.

``` js
import { NextResponse } from "next/server";
import prisma from "@/lib/prisma";

export async function DELETE(request, { params }) {
  try {
    const id = parseInt(params.id);
    const result = await prisma.meal.delete({
      where: {id: id},
    })
    // Devuelve un mensaje de éxito tras la eliminación
    return NextResponse.json({ message: result}, { status: 200 });
  } catch (error) {
    // En caso de error, devuelve un error HTTP 500
       return new NextResponse(error.message, { status: 500});
  }
}
```