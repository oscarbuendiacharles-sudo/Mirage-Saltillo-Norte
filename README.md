# Mirage Saltillo Norte

Sitio de una sola página para el distribuidor autorizado Mirage en Saltillo,
Coahuila. Vende dos cosas: minisplits y cámaras de seguridad.

**En vivo:** https://mirage-saltillo-norte.vercel.app

HTML, CSS y JavaScript sin dependencias. No hay build ni framework. Se sirve
como sitio estático en cualquier lado.

## Cómo verlo en local

```bash
python3 -m http.server 8765 --directory mirage-saltillo-norte
```

Luego abre http://localhost:8765

Tiene que servirse por HTTP. Si abres el `index.html` con doble clic vas a ver
la versión de imagen fija, porque el navegador bloquea `fetch` en archivos
locales. Esa versión es un estado real del sitio, no un error.

## Qué contiene

| Archivo | Qué es |
|---|---|
| `index.html` | Todo el sitio: estructura, estilos y comportamiento en un archivo |
| `assets/hero-scrub.mp4` | El video del héroe, 7.3 MB, recodificado con keyframe cada 8 cuadros para que el scrub no tartamudee |
| `assets/hero-poster.jpg` | Primer cuadro. Se pinta antes de que llegue el video |
| `assets/hero-ending.jpg` | Cuadro final. Es el héroe de celular y la imagen de la sección de contacto |
| `assets/clima.jpg`, `seguridad.jpg` | Las dos imágenes de sección |
| `assets/logo-mirage.png` | Logo oficial con el wordmark en blanco, para fondo oscuro |
| `robots.txt`, `sitemap.xml` | Para los buscadores |

## Decisiones de construcción

- **El video se maneja con el scroll.** Se descarga completo como Blob y se
  reproduce desde memoria, porque hay servidores sin soporte de descarga
  parcial y ahí el scrub se rompe. Las búsquedas de tiempo están encoladas: si
  hay una en curso, la siguiente espera. Sin eso, Chrome tartamudea.
- **En celular no se descarga el video.** Cinco condiciones deciden entre
  scrub e imagen fija (ancho, orientación, tipo de puntero, altura y
  movimiento reducido), y son idénticas en CSS y en JavaScript. El teléfono
  ni siquiera pide el archivo de 7 MB.
- **La página funciona sin el video.** Si no carga, queda completa sobre la
  imagen fija y el anillo de carga desaparece en vez de quedarse girando.
- **Movimiento reducido se respeta en los dos sentidos**, incluso si se activa
  con la página ya abierta.
- **El formulario no tiene servidor.** Arma un mensaje y abre WhatsApp con él
  ya escrito. El sitio lo dice tal cual, para no prometer un buzón que no
  existe.
- **Las imágenes son generadas** y se cambian por fotografías de trabajos
  reales cuando estén. El pie de página lo aclara.

## Qué falta

| Pendiente | Detalle |
|---|---|
| Verificación de Search Console | Falta pegar la etiqueta HTML que da Google en el `<head>` |
| Fotos reales | Sustituir las tres imágenes generadas por trabajos del negocio |
| Dominio propio | Al cambiarlo hay que actualizar `canonical`, `og:url`, `og:image`, `robots.txt` y `sitemap.xml` |

Los originales pesados (video crudo, imágenes a tamaño completo, logo oficial)
viven fuera de este repositorio a propósito. Aquí va solo lo que se publica.
