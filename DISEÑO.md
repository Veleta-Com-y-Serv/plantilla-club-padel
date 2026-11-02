# Club de pádel y deporte: brief de diseño

Plantilla `club-padel` creada el 02/11/2026 a partir de `musica-espectaculos` (orden 570, tercera tanda «ancho completo»)
con `php artisan plantillas:nueva`. De la base solo queda la estructura técnica (index, seo, site.ts, Imagen, formulario
`mailto`, Base.astro); todo lo visual es nuevo. Este fichero se queda en el repo para quien la rediseñe después.

## Brief

- **Para quién**: clubes de pádel y tenis, alquiler de pistas, clubes deportivos y escuelas deportivas (`padel`,
  `club-deportivo`, `tenis`, `pistas`, `escuela-deportiva`). Su cliente entra a ver pistas y precios, reservar,
  apuntarse a clases o a un torneo.
- **Acción principal**: reservar pista (enlace a la web o aplicación de reservas, `enlace_reservas`, o WhatsApp); después,
  clase de prueba, inscripción en torneos y hacerse socio.
- **Tono y estilo** (`energico`): deportivo, rápido, luminoso. Sí: cartelería de torneos de pádel y marcadores de pista.
  No: el gimnasio oscuro con rayas de advertencia (`gimnasio-deporte`) ni el cartel nocturno de gira (`musica-espectaculos`).
- **Concepto**: «pista de competición». Las líneas blancas de una pista de pádel vista desde arriba (20 × 10 m) son la
  trama de fondo; las bandas entran en diagonal como el corte de una bandeja; las cifras y el próximo torneo van en un
  marcador de partido; la raya lima cruza la portada como la trayectoria de la bola.
- **Paleta de ejemplo**: primario `#1f4bff` (azul eléctrico), acento `#c6f432` (lima), fondo `#f3f5f9` (claro), texto
  `#16191f` (grafito). Bandas: clara, clara2 (claro teñido de azul), grafito (= texto), azul (= primario) y lima
  (= acento). Letra sobre azul y lima calculada con `oklch` (`--sobre-primario`, `--sobre-acento`).
- **Tipografía**: titulares en condensada del sistema (Bahnschrift, DIN Condensed, Roboto Condensed, Arial Narrow) con
  `font-stretch: 75%`, cursiva y mayúsculas, 2,9-7 rem; antetítulos en la misma letra espaciada con raya inclinada;
  texto en system-ui.
- **Formas**: diagonales con `clip-path` (bandas `.corte` y `.corte-inv`, fotos de clases y de texto, panel de la
  portada, franja del pie, esquina de la tarifa destacada), sellos de iconos inclinados con sombra lima, botones en
  pastilla con flecha en círculo, etiquetas redondas.
- **Ritmo de bandas**: portada azul con foto → pistas grafito (fotos de borde a borde con rayas lima) → reservas lima
  → clases claro (foto a sangre) → torneos azul con líneas → tarifas grafito → instalaciones claro (mosaico) → cifras
  lima (marcador) → opiniones grafito → preguntas claro2 → contacto grafito + panel azul → pie azul con franja lima.

## Apartados

1. `hero`: foto de pista a sangre, panel azul en diagonal (en móvil, velo azul de abajo arriba), título enorme con la
   última palabra en lima, dos botones, marcador del próximo torneo (escritorio) y franja lima con `items` e iconos.
2. `pistas`: `pistas` (nombre, texto, tipo «Cubierta|Exterior», precio, imagen) en fotos altas, hasta 4 por fila.
3. `reservas`: `enlace_reservas` + `cta` + `nota` y pasos (`items`) numerados en grande.
4. `clases`: `imagen` + `clases` (nombre, texto, nivel, precio, duracion) en filas con etiqueta de nivel.
5. `torneos`: `torneos` (fecha, titulo, categoria, precio, estado) en cuadro de filas con fecha en bloque lima.
6. `tarifas`: `tarifas` (nombre, precio, periodo, incluye, destacado) en columnas separadas por rayas.
7. `instalaciones`: `items` con icono y `galeria` en mosaico.
8. `cifras`: `items` (titulo = número, texto) en marcador.
9. `opiniones`: `testimonios`.
10. `preguntas`: `preguntas` en acordeón.
11. `contacto`: teléfono enorme y formulario en panel azul hasta el borde.

## Fotos

`fotos.json` (11): portada 16:9 (pista cubierta con cristal y césped azul), 4 pistas 3:4 (central panorámica, nave
de pistas cubiertas, exterior al atardecer, detalle con pala y bolas), clases 4:3 (monitora de espaldas, sin caras) y
5 de instalaciones 3:2 (cenital de pistas, vestuario, tienda de palas, terraza, bola sobre el césped). Sin texto
legible, sin logotipos ni personas reconocibles.

## Qué no hacer

- Fondo oscuro general con rayas de advertencia o botones en paralelogramo (es `gimnasio-deporte`).
- Duotono de las fotos, cinta corrida o pegatina redonda (es `musica-espectaculos`).
- Tarjetas blancas en caja centrada estrecha.

## Páginas propias (fichas)
Con la misma piel que la portada: cabecera y pie de la plantilla, migas (Inicio › Sección › Elemento), hero con la foto del
elemento (sin foto, su icono), `detalle` en párrafos, tabla de datos, caja de contacto, galería (`imagenes`) y otros elementos
de la misma lista.

Fichas de clases (`/clases/<slug>/`): cabecera en banda azul con líneas de pista y corte diagonal abajo, título condensado en
cursiva con la última palabra en lima, foto de la clase cortada en diagonal (sin foto, sello lima con icono), marcador
grafito con los datos y caja lima con la clase de prueba, galería en banda grafito con raya lima y «Otras clases» en
banda clara2 con corte y tarjetas de borde superior azul.
