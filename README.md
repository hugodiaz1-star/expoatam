# Stand Expo ATAM 2026 — VMS Energy

Landing interactiva y material web del stand de **VMS Energy** en la **XLVI Convención y Expo ATAM 2026** (Asociación de Técnicos Azucareros de México), WTC Veracruz.

El corazón del proyecto es una **página HTML de un solo archivo** con la foto del stand y puntos pulsantes: al tocar cada punto se abre la ficha del equipo (qué hace, marca, ficha técnica). Incluye además una vista de rayos-X/esquema eléctrico, secciones de portafolio, un caso de éxito real y un formulario de captura de leads. Todas las páginas son **autocontenidas**: las imágenes y logos van embebidos en base64, así que cada archivo funciona por sí solo sin depender de carpetas externas.

## Contenido del repositorio

| Archivo | Qué es |
|---|---|
| `index.html` | Página índice que enlaza a todas las piezas (útil como raíz de GitHub Pages). |
| `stand-ATAM-2026.html` | **Entregable principal.** Landing interactiva del stand con puntos, rayos-X y secciones comerciales. |
| `Ficha Informativa AZUCARERO - VMS Energy.html` | Ficha informativa de una página orientada al sector azucarero. |
| `Caso de Exito Ingenio Tamazula - Standalone.html` | Caso de éxito: variador regenerativo 300 HP, Ingenio Tamazula. |
| `webar-stand/` | Experiencia de Realidad Aumentada sin app (visor 3D + modelo `.glb`). Ver su `LEEME-despliegue.md`. |
| `apps-script-formulario.gs` | Backend del formulario de leads (Google Apps Script). |

> El material de trabajo (fichas de fabricantes, catálogos PDF, cartas de invitación, fotos y renders en `assets/`) y las herramientas internas de edición (`editor-*.html`) **no forman parte de este repositorio**: se excluyen vía `.gitignore` por contener material con derechos de terceros / datos de cliente o por ser utilidades de trabajo.

## Publicar con GitHub Pages

Las páginas son estáticas, así que se hospedan gratis con GitHub Pages:

1. Sube el repositorio a GitHub (ver instrucciones abajo).
2. En GitHub: **Settings → Pages**.
3. En **Source**, elige la rama `main` y la carpeta `/ (root)`. Guarda.
4. En un par de minutos la web queda en `https://<usuario>.github.io/<repositorio>/`.

`index.html` se abre por defecto y enlaza al resto. Para ir directo al stand: `https://<usuario>.github.io/<repositorio>/stand-ATAM-2026.html`.

> El WebAR exige HTTPS (GitHub Pages lo cumple). No funciona abriendo el archivo directamente desde el disco.

## Configurar el formulario de leads

El formulario del stand envía cada contacto a `contacto@vmsenergy.com` mediante un Google Apps Script. Para activarlo:

1. Abre `apps-script-formulario.gs` y sigue las instrucciones del encabezado (se publica como *Web App* en https://script.google.com).
2. Copia la URL que termina en `/exec`.
3. En `stand-ATAM-2026.html`, pega esa URL en la constante `FORM_ENDPOINT`.

Mientras no se configure, el formulario funciona como prototipo (muestra "¡Gracias!" sin enviar).

## Editar el HTML principal

`stand-ATAM-2026.html` es grande (~3 MB) porque incorpora imágenes en base64. Al editarlo conviene hacerlo **por script** (Python/bash), no con editores que reescriban todo el archivo, y verificar después que el JavaScript sigue válido (`node --check`) y que los cierres `</script></body></html>` están presentes. El modelo de datos vive dentro del `<script>`: `POINTS` (los puntos del stand) y `BRANDS` (la grilla de marcas). Los logos se guardan una sola vez en el objeto `L={...}` y se referencian por interpolación.

## Marcas y derechos

Este repositorio contiene material de marca de **VMS Energy** y logotipos/nombres de fabricantes (Siemens, Schneider Electric, Keyence, Triol, Advantech, Sigenergy, Woodward, entre otros) que son marcas registradas de sus respectivos propietarios, incluidos con fines de representación comercial del stand. Ver `LICENSE`.

## Contacto

VMS Energy · contacto@vmsenergy.com · vmsenergy.com
Guadalajara +52 33 3813 0739 · Cd. del Carmen +52 938 381 4824
