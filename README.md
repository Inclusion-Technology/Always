# ALWAYS · Olwis Style

Página web de la tienda. Desarrollada por Technology Inclusion.

**Sitio en vivo:** https://always-style.netlify.app
**Catálogo (precios):** https://wa.me/c/573127050472
**Instagram:** https://www.instagram.com/always_olwis/

---

## Cómo está armado

```
index.html      ← toda la página (textos, productos, estructura)
img/            ← todas las fotos
```

No hay nada más. No necesita servidor, base de datos ni instalación.
Cualquier cambio que se suba a este repositorio se publica solo en Netlify
en menos de un minuto.

### Las secciones, en orden

1. **La semana** — un look por día (Lunes a Viernes)
2. **Los bolsos** — carrusel con los productos del catálogo
3. **Los detalles** — fotos de cerca (herrajes, cierres, porta Pc)
4. **Campaña** — foto grande + galería de lifestyle

---

## Las tareas más comunes

### Cambiar el look de un día de la semana

**No hay que tocar código.** Solo reemplazar la foto:

| Día       | Archivo a reemplazar     |
|-----------|--------------------------|
| Lunes     | `img/look-lunes.jpg`     |
| Martes    | `img/look-martes.jpg`    |
| Miércoles | `img/look-miercoles.jpg` |
| Jueves    | `img/look-jueves.jpg`    |
| Viernes   | `img/look-viernes.jpg`   |

La foto nueva debe llamarse **exactamente igual** que la que reemplaza.
Formato vertical (proporción 4:5), idealmente 900 × 1125 píxeles.

Si además cambia el bolso de ese día, hay que editar el texto (ver abajo).

### Agregar la foto de un bolso en otro color

Cada bolso se ofrece en **café oscuro, miel y negro**. En la página, los tres
circulitos de color aparecen siempre; el que todavía no tiene foto se ve
tenue y al tocarlo dice *"próximamente"*.

Para activarlo solo hay que subir la foto con el nombre exacto:

| Bolso         | Café oscuro                 | Miel                       | Negro                       |
|---------------|-----------------------------|----------------------------|-----------------------------|
| Duffle Bag    | `bolso-duffle-cafe.jpg` ✅   | `bolso-duffle-miel.jpg`    | `bolso-duffle-negro.jpg` ✅  |
| Black Work    | `bolso-blackwork-cafe.jpg` ✅| `bolso-blackwork-miel.jpg` | `bolso-blackwork-negro.jpg` ✅ |
| Sweet Extreme | `bolso-sweet-cafe.jpg` ✅    | `bolso-sweet-miel.jpg`     | `bolso-sweet-negro.jpg`     |
| Travel        | `bolso-travel-cafe.jpg`     | `bolso-travel-miel.jpg`    | `bolso-travel-negro.jpg` ✅  |

✅ = ya está subida. Las demás se pueden subir cuando estén listas.

**No hay que tocar código.** Al subir el archivo con ese nombre, el circulito
se activa solo y empieza a mostrar la foto.

Formato: vertical 4:5, fondo neutro, ~900 px de ancho, menos de 150 KB.

### Cambiar un precio, un nombre o una descripción

Los precios de la página deben coincidir con el catálogo de WhatsApp.
Se editan en `index.html`, en el bloque `catalogo` (al inicio del `<script>`):

```js
{
  nombre:"Black Work",
  det:'Cuero vegano · porta Pc 15" · 5 accesos adicionales',
  precio:"249.900", antes:"319.900",
  fotos:{ ... }
}
```

- `precio` es el que se muestra grande en color camel.
- `antes` es el que sale tachado al lado (el precio sin descuento).
  Si un bolso no está en promoción, poner el mismo valor en ambos o borrar
  la línea `antes`.
- Los valores van **sin** el signo `$` (la página lo agrega sola).

### Agregar un bolso nuevo

En el mismo bloque `catalogo` de `index.html`, copiar un bloque completo
`{ ... }` y cambiarle los datos. Las fotos se suben a `img/` siguiendo la
convención `bolso-<nombre>-<color>.jpg`.

### Cambiar el número de WhatsApp

El número `573127050472` aparece varias veces en `index.html`.
Hay que reemplazarlo en **todas** (buscar y reemplazar todo).

---

## Reglas para no romper nada

- **Los nombres de archivo van en minúsculas, sin tildes, sin espacios.**
  Un espacio en el nombre rompe la dirección web de la foto. Si el archivo
  se llama `BOLSO NEGRO.jpg`, la página no lo va a encontrar.
- Al reemplazar una foto, conservar el mismo nombre exacto.
- Mantener las fotos por debajo de ~150 KB cada una, para que la página
  siga cargando rápido en datos móviles.
- Si algo se daña: en Netlify, sección **Deploys**, se puede volver a
  cualquier versión anterior con un clic ("Publish deploy").

---

## Pendientes

- [ ] Fotos faltantes de color: miel (los cuatro bolsos), negro de Sweet
      Extreme, café de Travel
- [ ] Conectar dominio propio (hoy usa la dirección de Netlify)
- [ ] Definir si se agrega carrito de compra (hoy la venta se cierra por
      WhatsApp)
