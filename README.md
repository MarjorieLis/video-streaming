# Proyecto de Streaming de Video en la Web

Este proyecto implementa una solución completa de **streaming de video optimizado para interfaces web**, incluyendo videos progresivos (MP4 y WebM), subtítulos en WebVTT y una variante HLS con segmentos `.ts`.

El objetivo es demostrar una integración real en HTML utilizando buenas prácticas de rendimiento, compatibilidad y accesibilidad.

---

## 🎬 Recursos de Video Generados

### ✔ MP4 (H.264/AAC) – Alta compatibilidad  
Codificado con:

ffmpeg -i video.mp4 -c:v libx264 -preset slow -crf 22 -movflags +faststart -c:a aac -b:a 128k video_1024x576.mp4


### ✔ WebM (VP9/Opus) – Mejor compresión
Codificado con:

ffmpeg -i video.mp4 -c:v libvpx-vp9 -crf 32 -b:v 0 -row-mt 1 -c:a libopus -b:a 96k video_1024x576.webm


### ✔ HLS – Streaming adaptativo con segmentos
Generado con:

ffmpeg -i video.mp4 -c:v libx264 -b:v 1800k -c:a aac -b:a 128k
-hls_time 4 -hls_playlist_type vod playlist.m3u8


Esto produce:
- `playlist.m3u8`
- `playlist0.ts` → `playlist6.ts`

---

## 🌐 Integración en HTML

El archivo `index.html` incluye:

- MP4 + WebM como fuentes progresivas
- Reproducción HLS usando compatibilidad nativa (Safari) o **HLS.js**
- Subtítulos WebVTT (`subs.vtt`)
- Controles accesibles y `preload="metadata"`

---

# 🚀 Cómo ejecutar el proyecto correctamente

⚠ **IMPORTANTE:**  
HLS no funciona abriendo el HTML con doble clic (`file://`).  
Debes usar un **servidor local** para que los segmentos `.ts` carguen correctamente.

---

## OPCIÓN 1 — Usar Live Server (recomendado)

1. Abre la carpeta del proyecto en **VS Code**  
2. Instala la extensión **Live Server**  
3. Clic derecho en `index.html` → **Open with Live Server**

Se abrirá en:

http://127.0.0.1:5500


✔ Funciona MP4  
✔ Funciona WebM  
✔ Funciona HLS  
✔ Funciona WebVTT  

---

## OPCIÓN 2 — Usar Python (sin instalar nada adicional)

En la terminal dentro de la carpeta del proyecto:

python -m http.server 8000


Luego abre:

http://localhost:8000

