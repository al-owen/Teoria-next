Para instalar Next.js, puedes seguir estos pasos usando `npm` o `yarn`, que son los gestores de paquetes más comunes para proyectos de JavaScript:

1. **Pre-requisitos:** Asegúrate de tener Node.js instalado en tu sistema. Esto incluye `npm`, que viene con Node.js. Puedes descargarlo desde el sitio oficial de [Node.js](https://nodejs.org/).
    
2. **Crear un Nuevo Proyecto de Next.js:** Puedes crear un nuevo proyecto utilizando `create-next-app`, que configura todo automáticamente para un inicio rápido. Abre tu terminal y ejecuta el siguiente comando:

``` bash
npx create-next-app nombre-de-tu-proyecto
```

  Reemplaza `nombre-de-tu-proyecto` con el nombre que desees para tu directorio del proyecto (si no especificas el nombre del proyecto, te lo pedirá después). Este comando descargará todas las dependencias necesarias y creará una estructura de proyecto con archivos de ejemplo.

Al momento de crear el proyecto te hará varias preguntas, normalmente son las siguientes, aunque dependiendo de la versión podrían ser otras.

``` bash
Need to install the following packages:
create-next-app@14.2.1
Ok to proceed? (y) y
√ What is your project named?..test  # si no se ha expresado antes
√ Would you like to use TypeScript?..No / Yes #Si queremos usar typescript
√ Would you like to use ESLint?...No / Yes #yes
√ Would you like to use Tailwind CSS?...No / Yes #si queremos usar tailwind
√ Would you like to use `src/` directory?... No / Yes #yes
√ Would you like to use App Router? (recommended)... No / Yes #yes
√ Would you like to customize the default import alias (@/*)? ... No / Yes #No
```

    
3. **Iniciar el Servidor de Desarrollo:** Una vez instalado el proyecto, navega hacia el directorio del proyecto en tu terminal:
    
``` bash
cd nombre-de-tu-proyecto
```

Y luego inicia el servidor de desarrollo con:

``` bash
npm run dev
```

o si estás usando `yarn`, puedes usar:

``` bash
yarn dev
```

   Este comando inicia el servidor de desarrollo y generalmente podrás ver tu nueva aplicación de Next.js ejecutándose en `http://localhost:3000` en tu navegador.
