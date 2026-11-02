# Plantilla NoExpertise · Club de pádel y deporte

Web enérgica para clubes de pádel y tenis: pistas, reservas, escuela, torneos y tarifas de socio.

- Sectores: pádel, club deportivo, tenis, alquiler de pistas, escuela deportiva. Estilo: enérgico. Plan mínimo: gratis.
- Secciones: hero, pistas, reservas, clases, torneos, tarifas, instalaciones, cifras, opiniones, preguntas, contacto (+ `texto` para apartados nuevos).
- Campos propios: `pistas[]` (nombre, texto, tipo, precio, imagen), `reservas.enlace_reservas` (enlace externo opcional), `clases[]` (nombre, texto, nivel, precio, duracion), `torneos[]` (fecha, titulo, categoria, precio, estado), `tarifas[]` (nombre, precio, periodo, incluye con «;», destacado) y `contacto.boton_formulario`.
- A ancho completo: portada a pantalla completa con foto a sangre, panel azul en diagonal con líneas de pista, marcador del próximo torneo y franja lima; pistas en fotos altas de borde a borde; reservas sobre lima; escuela con foto a sangre cortada en diagonal; cuadro de torneos sobre azul; tarifas en columnas sobre grafito; mosaico de instalaciones sin márgenes; cifras en marcador; contacto partido con panel azul hasta el borde.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`SportsActivityLocation`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) hechas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.clases.clases` con `detalle` tiene su página en `/clases/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
