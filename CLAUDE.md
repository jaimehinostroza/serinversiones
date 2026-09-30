# CLAUDE.md: SER Inversiones (sitio web)

## Proyecto
Landing de una sola página para **SER Sociedad de Inversiones** (Chile). Idioma: español de Chile (`lang="es-CL"`). Dominio de producción: `serinversiones.cl`. Hosting: Vercel.

## Stack
- Sitio **estático**: `public/index.html` contiene todo el HTML y CSS. No hay framework, dependencias ni paso de build.
- `vercel.json` define `outputDirectory: "public"` y `cleanUrls`.
- Deploy: push a la rama principal (integración Git de Vercel) o `vercel --prod`.

## Contenido aprobado por el cliente (no cambiar sin pedirlo)
- Frase principal: "Invertimos en activos reales: tierra, propiedades y rentas."
- Bajada: "SER es una sociedad de inversiones con presencia en tres rubros complementarios."
- Rubros:
  1. **Compra y venta de propiedades en remates**: solo remates *judiciales* (el cliente pidió quitar "extrajudiciales").
  2. **Arriendo de inmuebles**: incluye un strip center temático.
  3. **Explotación agrícola**: siempre **un predio, en singular**.
- Contacto: jpmarin@serinversiones.cl · +56 9 6309 3207 (`tel:+56963093207`).
- El cliente pidió quitar la frase sobre "construir patrimonio con visión de largo plazo". No volver a agregarla.

## Sistema de diseño
- Tokens CSS en `:root` (claro) y en `@media (prefers-color-scheme: dark)` (oscuro). Usar siempre las variables; no escribir colores directo en los componentes.
  - Claro: `--ground #EDEFEA`, `--ink #17231F`, `--muted #55635D`, `--line #C9D0C9`, `--pine #2E5A4C`, `--wheat #A87A24`
  - Oscuro: `--ground #111916`, `--ink #E6ECE7`, `--muted #9AA8A1`, `--line #2C3A34`, `--pine #7FB9A3`, `--wheat #D9AE5C`
- Tipografías: Archivo (display; logotipo SER con `font-stretch: 125%`, peso 800), IBM Plex Sans (cuerpo), IBM Plex Mono (etiquetas en mayúsculas con tracking).
- Detalle de marca: las líneas horizontales bajo "SER" representan surcos de cultivo (`.mark::after`).
- Íconos SVG inline de trazo (`stroke="currentColor"`, color `--pine`).
- Breakpoint único: 820 px (3 columnas → 1 columna).
- Mantener: foco visible en links, `prefers-reduced-motion`, margen lateral mínimo de 16 px.

## Al hacer cambios
- Si cambia el texto, regenerar `public/og-image.jpg` (1200×630) para que la vista previa al compartir coincida.
- Si cambia el dominio, actualizar `canonical`, `og:url` y `og:image`.
- Probar en 390 px de ancho y en modo oscuro.
