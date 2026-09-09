# typple-landing

Sitio estático de [typpleapp.com](https://typpleapp.com), servido por GitHub Pages
desde la raíz del repo (`CNAME` + `.nojekyll`). No hay build: lo que está en el
repo es lo que se publica.

## Estructura

```
index.html            Landing. Markup + un <script> inline de 6 líneas (borde del nav al scrollear).
css/                  Se cargan en este orden desde index.html:
  fonts.css             @font-face de Plus Jakarta Sans y JetBrains Mono → /fonts
  tokens.css            :root con los design tokens (--accent, --ink-*, --r-*, sombras…)
  base.css              Reset, body, helpers (.container, .eyebrow, .mono)
  nav.css               Barra superior, incluye el estado .scrolled
  hero.css              Hero, badges de tienda, composición del teléfono, animaciones
  sections.css          Trust bar, how it works, features, testimonial, FAQ, CTA, footer
fonts/                *.woff2 por familia y subset (unicode-range decide cuáles se bajan)
og-image.png          Preview de link (1200×630). Fuente y comando en dev/og-image.html
upgrade.html          Checkout de Paddle (abierto desde la app)
mp/result/, mp/return/  Páginas de retorno de Mercado Pago
404.html
.well-known/          assetlinks.json (App Links de Android)
dev/                  No se sirve como parte del sitio; ver abajo
```

## Editar

Copy y estructura, en `index.html`; estilos, en el archivo de `css/` que
corresponda a la sección. Los colores y radios salen todos de `css/tokens.css`:
cambiar `--accent` ahí repinta la marca entera.

Para verlo local hace falta un servidor (las fuentes no cargan por `file://`):

```sh
python3 -m http.server 8080   # → http://localhost:8080
```

## dev/

- `og-image.html` — fuente de `og-image.png`, con el comando para regenerarlo.

## El bundle original

Este sitio salió de un artifact empaquetado: un solo `index.html` de 1,4 MB con
la página entera en base64 y un panel de "Tweaks" en React para ajustar accent,
radios y copy del hero desde el navegador. Se desempaquetó porque cargaba ~4 MB
de JS (React dev + Babel) para renderizar cero elementos visibles, y dejaba el
HTML vacío para los crawlers.

Sigue en el historial, por si alguna vez hace falta volver a abrir ese panel:

```sh
git show 97f0c8e:index.html > index.tweaks.html
```
