# ALWAYS · Olwis Style — contexto del proyecto

Landing estática de una tienda de bolsos en cuero vegano de Medellín.
Un solo `index.html` + carpeta `img/`. Sin build, sin framework, sin
dependencias. Netlify publica `main` automáticamente en
https://always-style.netlify.app

La dueña del proyecto trabaja **desde el celular** y sube archivos por la
interfaz web de GitHub. No usa terminal ni git local. Cualquier instrucción
que se le dé tiene que funcionar tocando botones en el navegador del móvil.

## La venta ocurre en WhatsApp, no aquí

El sitio no tiene carrito. Su trabajo es dar confianza y llevar al
catálogo de WhatsApp Business, donde se cierra la venta por chat.

- Catálogo: https://wa.me/c/573127050472
- Chat: el número es `573127050472`, aparece varias veces en `index.html`
- Instagram: https://www.instagram.com/always_olwis/

Los precios de la página **deben coincidir con el catálogo**. El catálogo
es la fuente de verdad; la página es un reflejo que se actualiza a mano.
El catálogo no se puede leer desde una sesión de Claude (`wa.me` es un
deep link a la app, y además está bloqueado por el proxy de red): la
información hay que pedírsela a ella.

## Dónde se editan los productos

Todo el catálogo vive en el array `catalogo` al inicio del `<script>` de
`index.html`. Es el único lugar que hay que tocar para agregar un bolso,
cambiar un precio o corregir una descripción. `precio` y `antes` van sin
el signo `$`; `antes` es el precio tachado de la promoción.

Productos actuales: Duffle Bag, Black Work, Sweet Extreme, Travel.
Los cuatro se ofrecen en café oscuro, miel y negro.

## La convención de nombres de foto es funcional, no cosmética

Las fotos de producto siguen `bolso-<producto>-<color>.jpg`. Al cargar,
el JS comprueba si cada archivo existe y activa o atenúa el circulito de
color correspondiente. Un color sin foto se muestra tenue y dice
"próximamente".

Esto es deliberado: ella agrega un color subiendo un archivo con el
nombre correcto, sin tocar código. Si se cambia el esquema de nombres,
se rompe esa promesa. Los 404 en consola de las fotos que faltan son
el mecanismo de detección, no un error.

La tabla completa de nombres está en `README.md`, que es el documento
escrito para ella. Mantener las dos cosas sincronizadas.

## Reglas de archivos que ya causaron una caída

- **Nada de espacios, tildes ni mayúsculas en los nombres.** Una subida
  anterior dejó `img/ logo.jpg` (con espacio inicial) y
  `BOLSO BLACK WORK.jpg.jpeg`; esos nombres no sobreviven al encoding de
  URL y el sitio quedó sin imágenes.
- Fotos por debajo de ~150 KB, máximo 270 KB. Buena parte del tráfico
  entra por datos móviles.
- Producto en 4:5 sobre fondo neutro. Lifestyle en 3:4 o 16:10.
- Antes de usar una captura de Instagram hay que recortarle la interfaz
  (flechas laterales y puntos de paginación).

## El carrusel: por qué está hecho así

Usa scroll nativo con `scroll-snap`, y el desplazamiento automático lo
mueve el JS sobre `scrollLeft`. A la primera interacción se detiene para
siempre y cede el control.

La versión anterior animaba `transform` en bucle infinito. Se veía bien,
pero **en móvil los botones de color eran intocables**: se escapaban bajo
el dedo y no hay hover que pause la animación. Lo detectó una prueba de
navegador, no la inspección visual. Si se vuelve a tocar esta sección,
probar el cambio de color con toque real en viewport de móvil.

## Cómo probar antes de subir

```bash
python3 -m http.server 8899        # servir el sitio
# luego, con Playwright (executablePath '/opt/pw-browsers/chromium'):
#   - contar .tarjeta y .colores button.prox
#   - hacer clic y tap en un swatch y verificar que cambia el src
#   - 12 clics en la flecha ">" sin que el carril quede vacío
#   - revisar 404s y errores de consola
#   - comprobar que .dia queda en una sola fila a 1280 / 820 / 390 px
```

Verificar también que no quede ninguna foto huérfana: todo archivo en
`img/` debe aparecer referenciado en `index.html`.

## Estado del repositorio

El trabajo va directo en `main`, que es lo que Netlify publica. La dueña
no quiere ramas de Claude.

Ella sube fotos por la interfaz web mientras se trabaja, así que `main`
avanza sola: conviene `git fetch origin main` antes de empujar y rebasar
encima en vez de forzar.

El repositorio es **público** y ella decidió dejarlo así. El LICENSE
declara todos los derechos reservados y separa la titularidad del código
(Technology Inclusion) de la de las fotos (Olwis Style). La cabecera del
HTML y el pie repiten la autoría; no quitarlos al editar.

## Fotos: ella manda los originales, aquí se procesan

Llegan en HEIC de iPhone (3024x4032) o en JPEG de varios megas. Se
convierten con `pillow-heif` y se dejan en 900px de ancho, calidad 82,
por debajo de 270 KB.

Antes de dar una foto por buena hay que mirarle las placas metálicas: las
generadas con IA han llegado varias veces con "ALWAY" sin la S, y una con
una segunda placa de texto inventado. Es una marca en un sitio comercial,
así que conviene avisarlo aunque la foto la haya pedido ella.

La galería de campaña se mantiene en nueve fotos: en tres columnas, una
décima deja una sola colgando en la cuarta fila, y ella lo nota.

Las fotos de esa galería entran en un marco 3:4 con `object-fit: cover`.
Una foto que ya venga en 3:4 no se recorta y su sujeto se ve más lejos
que el de las vecinas; eso confunde y parece un problema de color cuando
es de encuadre.

## Idioma

Todo el contenido y la comunicación van en español. El tono de los textos
del sitio es paisa, concreto, sin publicidad genérica: "el morral que
aguanta portátil, almuerzo y la reunión de las seis sin verse de oficina".
