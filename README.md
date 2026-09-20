# ALWAYS · Olwis Style

Página web de la tienda. Desarrollada por Technology Inclusion.

**Sitio en vivo:** https://always-style.netlify.app

---

## Cómo está armado

```
index.html      ← toda la página (textos, precios, estructura)
img/            ← todas las fotos
```

No hay nada más. No necesita servidor, base de datos ni instalación.
Cualquier cambio que se suba a este repositorio se publica solo en Netlify
en menos de un minuto.

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

### Cambiar un precio

En `index.html`, buscar el precio viejo (ej. `$189.900`) y reemplazarlo.
Ojo: cada precio aparece en **dos lugares** — en la tarjeta del producto
(sección "Los bolsos") y en el bloque `looks` del final del archivo.
Hay que cambiarlo en ambos.

### Cambiar el texto de un día

Al final de `index.html` está el bloque `looks`, con una entrada por día:

```js
lunes:{
  img:"img/look-lunes.jpg",
  alt:"Look de lunes: morral negro con camiseta café y pantalón camel",
  titular:"Marrón y negro,<br>para arrancar la semana",
  bajada:"El duffel de chapas de acero que carga tu semana completa...",
  nombre:"Duffel Bag · Negro",
  detalle:"Cuero vegano · solapa con chapas de acero",
  precio:"$219.900"
},
```

Se edita el texto entre comillas. Reglas:

- No borrar las comillas ni las comas.
- `<br>` fuerza un salto de línea en el titular.
- `alt` es la descripción para personas con lectores de pantalla y para Google.
  Vale la pena mantenerla al día.

### Cambiar el número de WhatsApp

El número `573127050472` aparece varias veces en `index.html`.
Hay que reemplazarlo en **todas** (buscar y reemplazar todo).

---

## Reglas para no romper nada

- Los nombres de archivo van en minúsculas, sin tildes ni espacios.
- Al reemplazar una foto, conservar el mismo nombre exacto.
- Mantener las fotos por debajo de ~150 KB cada una, para que la página
  siga cargando rápido en datos móviles.
- Si algo se daña: en Netlify, sección **Deploys**, se puede volver a
  cualquier versión anterior con un clic ("Publish deploy").

---

## Pendientes

- [ ] Conectar dominio propio (hoy usa la dirección de Netlify)
- [ ] Definir si se agrega carrito de compra (hoy la venta se cierra por WhatsApp)
