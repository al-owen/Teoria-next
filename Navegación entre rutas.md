En el sistema moderno de Next.js (basado en la carpeta `/app`), la navegación entre páginas se hace principalmente con dos herramientas:

1. `<Link/>` (componente para navegación declarativa)
2. `useRouter()` (hook para navegación programática)

## Link
La forma más común y recomendada para navegar entre páginas en Next.js es usando el componente `Link` de `next/link`. Este método hace navegación cliente a cliente (sin tener que recargar la página), con soporte para prefetching automático.

Los beneficios de este método son:
- No se recarga la página
- Next.js hace prefetch automático si el link está visible en pantalla
- Compatible con rutas estáticas, dinámicas, layouts, etc.

**Ejemplo**:

```jsx
// app/page.jsx (homepage)
import Link from 'next/link';

export default function Home() {
  return (
    <div>
      <h1>Bienvenido</h1>
      <Link href="/about">Ir a Acerca de</Link>
    </div>
  );
}
```

## useRouter

Si necesitas navegar en respuesta a una acción (como un botón o función lógica), puedes usar el hook `useRouter` de `next/navigation`:

Los funciones utiles de este método son:
- `router.push('/ruta')` → Navega a una ruta
- `router.replace('/ruta')` → Reemplaza sin dejar historial
- `router.refresh()` → Refresca los datos del server
- `router.back()` → Ir atrás en el historial

**Ejemplo**:

```jsx
'use client'; // obligatorio para usar hooks del cliente

import { useRouter } from 'next/navigation';

export default function BotonRedireccion() {
  const router = useRouter();

  const irAPerfil = () => {
    router.push('/profile');
  };

  return <button onClick={irAPerfil}>Ir al perfil</button>;
}

```