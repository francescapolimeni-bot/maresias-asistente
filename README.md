# Asistente Maresias Deco

Asistente de asesoramiento en decoración para [maresiasdeco.com.ar](https://www.maresiasdeco.com.ar), construido como una aplicación web estática que se puede incrustar en cualquier sitio.

---

## Archivos

| Archivo | Descripción |
|---|---|
| `maresias-asistente.html` | La interfaz completa del asistente |
| `catalogo.json` | El catálogo de productos, categorías e info de la tienda |

Estos dos archivos tienen que estar **en la misma carpeta** para que funcionen juntos.

---

## Cómo actualizar el catálogo

El asistente lee `catalogo.json` cada vez que carga. Cuando cambiás algo en la tienda, editás ese archivo y el bot se actualiza automáticamente.

### En GitHub (sin saber Git)

1. Entrás al repositorio en github.com
2. Hacés click en `catalogo.json`
3. Hacés click en el ícono de lápiz (editar)
4. Hacés los cambios
5. Commit changes → el asistente se actualiza en ~1 minuto

---

## Estructura del catálogo

### Sección `tienda`

```json
"tienda": {
  "url": "https://www.maresiasdeco.com.ar",
  "instagram": "https://www.instagram.com/maresias.deco",
  "whatsapp": "+541136927855",
  "logo": "URL de la imagen del logo",
  "promo": "Texto de la promo que aparece en el footer"
}
```

### Sección `categorias`

Cada categoría tiene esta estructura:

```json
"living": {
  "label": "Living",
  "url": "https://www.maresiasdeco.com.ar/muebles",
  "items": [ ... ]
}
```

### Estructura de un producto con precio fijo

```json
{
  "id": 1,
  "nombre": "Lámpara Rocinha",
  "cat": "Iluminación",
  "precio": 245200,
  "transfer": 196160,
  "cuotas": "6 cuotas s/i $40.867",
  "imagen": "https://URL-de-la-imagen.jpg",
  "url": "https://www.maresiasdeco.com.ar/producto"
}
```

> `transfer` es el precio con 20% de descuento. Se calcula como `precio * 0.8`.

### Estructura de un producto con rango de precios

```json
{
  "id": 5,
  "nombre": "Sillones y camastros",
  "cat": "Sillones",
  "precio": null,
  "rangeMin": 320000,
  "rangeMax": 1200000,
  "imagen": "https://URL-de-la-imagen.jpg",
  "url": "https://www.maresiasdeco.com.ar/categoria"
}
```

### Estructura de un producto a pedido y a medida

```json
{
  "id": 8,
  "nombre": "Mesa ratona petiribi",
  "cat": "Ratonas",
  "precio": null,
  "apedido": true,
  "imagen": "https://URL-de-la-imagen.jpg",
  "url": "https://www.maresiasdeco.com.ar/producto"
}
```

---

## Agregar un producto nuevo

1. Abrís `catalogo.json`
2. Buscás la categoría donde va el producto
3. Agregás un objeto nuevo al array `items` con un `id` que no esté en uso
4. Guardás y hacés commit

## Eliminar una categoría entera

Borrás el bloque de esa categoría dentro de `"categorias"`. El asistente solo muestra las categorías que existen en el JSON.

## Agregar una categoría nueva

Agregás un bloque nuevo dentro de `"categorias"` con la misma estructura que las existentes, y agregás la key al selector de ambientes dentro del HTML (línea que contiene `buildAmbientSelector`).

---

## Cómo incrustarlo en Empretienda

Empretienda permite agregar HTML en el footer del sitio. Pegás este código donde quieras que aparezca:

```html
<iframe
  src="https://TU-USUARIO.github.io/maresias-asistente/maresias-asistente.html"
  width="100%"
  height="680px"
  frameborder="0"
  style="border:none; border-radius:14px; max-width:480px; display:block; margin:0 auto;">
</iframe>
```

Reemplazá `TU-USUARIO` con tu usuario de GitHub y `maresias-asistente` con el nombre del repositorio.

---

## Tecnologías

- HTML, CSS y JavaScript vanilla — sin dependencias ni frameworks
- Llama a la API de Claude (Anthropic) para respuestas libres
- Lee el catálogo desde `catalogo.json` en cada carga
- Compatible con cualquier hosting de archivos estáticos (GitHub Pages, Netlify, etc.)
