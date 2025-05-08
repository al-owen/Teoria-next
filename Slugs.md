En las últimas versiones de Next.js (13+ con App Router), el manejo de slugs y rutas dinámicas sigue una lógica parecida a la del sistema anterior (`pages/`), pero con mejoras importantes gracias al poder del nuevo sistema basado en la carpeta `/app`.

## Estructura básica de una ruta dinámica

```sh
/app
|_/blog
  |_/[slug]
    |_ page.jsx
```
Esta estructura define una ruta como `/blog/titulo-de-post`, donde `slug` es un parámetro dinámico que puedes capturar dentro de tu componente.

## ¿Cómo acceder al valor del slug?

En el **App Router**, los parámetros de ruta se acceden desde el hook especial:
``` jsx
import { useParams } from 'next/navigation';

export default function BlogPostPage() {
  const params = useParams();
  const slug = params.slug;

  return <h1>Estás viendo el post: {slug}</h1>;
}
```