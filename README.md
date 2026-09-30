# SER Inversiones: sitio web

Página de presentación de **SER Sociedad de Inversiones**. Es una sola página que describe los tres rubros de la sociedad y muestra los datos de contacto.

- Dominio previsto: **serinversiones.cl**
- Contacto que aparece en la página: jpmarin@serinversiones.cl · +56 9 6309 3207

## Qué trae este ZIP

```
ser-web/
├── public/              ← todo lo que se publica
│   ├── index.html       ← la página completa (HTML + CSS en un solo archivo)
│   ├── favicon.svg      ← ícono de la pestaña del navegador
│   ├── og-image.jpg     ← imagen que aparece al compartir el link (1200×630)
│   └── robots.txt
├── recursos/
│   └── SER-presentacion.jpg   ← la misma presentación como imagen (no se publica)
├── vercel.json          ← configuración de Vercel
├── CLAUDE.md            ← contexto para Claude Code
└── README.md
```

Es un **sitio estático**: no usa frameworks, no necesita `npm install` ni un paso de build. Vercel publica tal cual la carpeta `public/`.

## Publicar en Vercel

### Opción A: con GitHub (recomendada)
1. Crear un repositorio nuevo (por ejemplo `ser-web`) y subir el contenido de esta carpeta.
2. En vercel.com: **Add New → Project**, importar el repositorio.
3. En *Framework Preset* elegir **Other**. No hace falta configurar un comando de build: el `vercel.json` ya indica que el directorio de salida es `public`.
4. **Deploy**. Cada cambio que se suba al repositorio se publica solo.

### Opción B: con la línea de comandos
```bash
npm i -g vercel
cd ser-web
vercel          # primera vez: crea y vincula el proyecto
vercel --prod   # publica en producción
```

## Conectar el dominio serinversiones.cl

1. En Vercel: **Project → Settings → Domains → Add**, agregar `serinversiones.cl` y también `www.serinversiones.cl` (redirigido al dominio principal).
2. Vercel indica qué registros DNS crear. Hay dos caminos:
   - **Cambiar los servidores DNS en NIC Chile** a los de Vercel (`ns1.vercel-dns.com`, `ns2.vercel-dns.com`). Es lo más simple, **pero ojo**: si el email @serinversiones.cl ya funciona (Google Workspace, Microsoft 365, etc.), hay que volver a crear en Vercel los registros **MX, SPF (TXT) y DKIM** del correo. Si no, el email deja de funcionar.
   - **Mantener el DNS actual** y solo agregar los registros que pide Vercel (normalmente un registro `A` para el dominio raíz y un `CNAME` para `www`). Así no se toca el correo.
3. El certificado HTTPS lo emite Vercel de forma automática.

## Editar contenidos

Todo el texto está en `public/index.html`:

| Qué cambiar | Dónde buscar |
|---|---|
| Frase principal | `<h1>` dentro de `.lede` |
| Descripción de cada rubro | los tres `<article class="rubro">` |
| Email y celular | `<footer class="foot">`: se cambia el texto **y** el `href` (`mailto:` / `tel:`) |
| Colores | variables en `:root` al comienzo del `<style>` (tema claro) y en el bloque `@media (prefers-color-scheme: dark)` (tema oscuro) |

Si cambia el dominio, actualizar también `canonical`, `og:url` y `og:image` en el `<head>`.

## Detalles del diseño

- **Tipografías** (Google Fonts): Archivo (títulos y logotipo SER, se usa el eje de ancho `wdth` 125), IBM Plex Sans (texto) e IBM Plex Mono (etiquetas).
- **Colores (tema claro)**: fondo `#EDEFEA`, texto `#17231F`, verde pino `#2E5A4C`, trigo `#A87A24`.
- **Modo oscuro** automático según la configuración del dispositivo.
- **Responsive**: sobre 820 px los rubros van en 3 columnas; en celular se apilan.
- El año del copyright se actualiza solo con JavaScript.

## Mejoras opcionales

- Botón de WhatsApp: `https://wa.me/56963093207`
- Vercel Web Analytics: se activa en *Project → Analytics* y luego se agrega su script al `index.html`
- Si el sitio va a crecer (más páginas, formulario de contacto), conviene migrarlo a Next.js. El HTML y el CSS actuales se pueden reutilizar tal cual.
