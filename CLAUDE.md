# Plantilla «Club de pádel y deporte» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **enérgico**
(pista de competición: azul eléctrico + lima + grafito sobre claro, letra condensada en cursiva enorme, líneas de pista
de pádel de fondo, bandas que entran en diagonal, fotos con corte en diagonal, marcador de partido). Todo en castellano
de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…).
  - `primario` = azul eléctrico: portada, torneos, panel del formulario, botones sobre claro, sellos de iconos y pie.
  - `acento` = lima: reservas, cifras (marcador), tarifa destacada, raya de la portada, etiquetas, botones sobre azul y grafito.
  - `fondo` + `texto` = claro + grafito. La banda grafito sale de `texto`: si el cliente pone fondo oscuro y texto claro, se invierte y todo se recoloca.
  - Derivados en `src/styles/global.css`: `--grafito`, `--sobre-grafito`, `--claro-2`, `--sobre-acento`, `--sobre-primario`, `--resalte`, `--resalte-texto`, `--btn-fondo` y `--btn-texto` (lo que cambia en cada banda).
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-titulos`: Bahnschrift, DIN Condensed, Roboto Condensed, Arial Narrow… con `font-stretch: 75%` y cursiva; texto en system-ui). Bandas `.banda-clara|clara2|grafito|azul|lima`, `.corte` / `.corte-inv` (entrada en diagonal), `.lineas-pista` (líneas de pista de fondo), `.foto-pista` (hueco de foto con respaldo), `.chip` (etiquetas), botones `.btn` (pastilla con flecha) y `.btn-sec`, cabecera `.cabecera--pista`, pie `.pie--azul`. Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: las fotos van en `public/fotos/` (lista y descripción en `fotos.json`); si una foto todavía no existe, `Imagen.astro` enseña su respaldo `public/placeholders/<mismo nombre>.svg`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Fotos de personas: `/placeholders/persona.svg` (no se generan caras).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = sello azul inclinado con la inicial + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie`. El pie enseña el eslogan con `boton_cabecera`, el próximo torneo (el primero de `torneos`) y `contacto.horario`.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`.
- `hero` → `hero.astro`: pantalla completa, foto a sangre con panel azul en diagonal, `titulo` enorme (la última palabra en lima; mejor 3-5 palabras), `texto`, `cta`, `cta_secundario`, `items: [{titulo, icono}]` en la franja lima de abajo y marcador con el próximo torneo (sale solo de `torneos`).
- `pistas` → `pistas.astro`: `pistas: [{nombre, texto, tipo, precio, imagen}]` en fotos altas de borde a borde (hasta 4 por fila). `tipo`: «Cubierta» (azul) o «Exterior» (lima). `cta` opcional.
- `reservas` → `reservas.astro`: `texto`, `enlace_reservas` (web o aplicación de reservas: botón «Reservar online», se abre aparte; vacío = sin botón), `cta` (p. ej. WhatsApp), `nota` e `items: [{titulo, texto}]` (pasos numerados).
- `clases` → `clases.astro`: `imagen` a sangre en diagonal y `clases: [{nombre, texto, nivel, precio, duracion}]` en filas. `cta` opcional.
- `torneos` → `torneos.astro`: `torneos: [{fecha, titulo, categoria, precio, estado}]`. `fecha` libre («14 nov 2026»): el número va en grande. `estado`: «Inscripción abierta» (lima), «Completo» (tachado), «Próximamente»… Pon los torneos en orden y quita los pasados: el primero es el «próximo».
- `tarifas` → `tarifas.astro`: `tarifas: [{nombre, precio, periodo, incluye, destacado}]`; `incluye` con «;»; `destacado: true` en lima.
- `instalaciones` → `instalaciones.astro`: `items: [{titulo, texto, icono}]` y `galeria: [ruta…]` en mosaico de borde a borde (la primera grande; con 5 fotos queda cerrado).
- `cifras` → `cifras.astro`: `items: [{titulo: número, texto}]` en marcador. Sin cifras no se pinta. No inventes cifras.
- `opiniones` → `opiniones.astro`: `testimonios: [{texto, autor, nota}]`; la primera enorme. No inventes opiniones.
- `preguntas` → `preguntas.astro` (acordeón `details/summary`; sin preguntas no se pinta).
- `contacto` → `contacto.astro`: teléfono enorme, datos de `contacto` y formulario en panel azul («Me interesa» con reservar pista, las clases, torneos y las tarifas). `boton_formulario` opcional.
- `texto` → `texto.astro`: apartado genérico (párrafos, `imagen` 50/50 a sangre, `items`, `cta`). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, torneos, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas (las fechas y las horas, siempre).
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Precios siempre como texto entre comillas. Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: torneos`, `tipo: clases`…) y su propio id. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y una banda (`Seccion` con `banda=` y, si quieres, `corte=`). `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base y salen solos de `site.yaml`. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida y respaldo), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral (`.contenedor`), bandas y fotos de borde a borde, sin scroll horizontal en móvil. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Iconos: `src/components/ui/Icono.astro` (de deporte: `pala, pelota, pista, tienda, aparcamiento, trofeo, cronometro, ducha, taza`; y `estrella, reloj, mapa, usuarios, nino`…).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.
