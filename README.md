🧠 VAPAI — Segmentador de Prendas
VAPAI es una web app que permite segmentar prendas de ropa en imágenes usando modelos avanzados de visión por computadora a través de ComfyUI. Pensado para facilitar procesos creativos o técnicos, este sistema detecta prendas específicas (como "jean", "sweater", "camisa") y las recorta con fondo transparente para su posterior uso.

<!-- podés agregar una imagen acá si tenés una -->

🌐 ¿Cómo funciona?
El usuario sube una imagen y escribe el nombre de la prenda que desea segmentar (prompt).

El frontend envía la imagen al backend, donde es procesada y convertida a base64.

El backend construye un flujo de trabajo dinámico y lo envía a ComfyUI expuesto vía ngrok.

ComfyUI ejecuta el nodo de segmentación (SegmentAnythingUltra V2) y devuelve una imagen con la prenda recortada.

El backend recibe la imagen y la mantiene en memoria.

El frontend hace "polling" hasta que la imagen esté lista, la muestra al usuario y permite descargarla.

🧰 Tecnologías usadas
🖼️ Modelos utilizados
SegmentAnythingUltra V2 (SAM + Grounding DINO + VITMatte)

LoadImageFromBase64 (nodo personalizado)

Send Http request (nodo para enviar imágenes al backend)

🖥️ Stack
Frontend: React + Vite + Tailwind CSS

Backend: Node.js + Express + Sharp

ComfyUI: Corriendo localmente, expuesto mediante ngrok

Deploy:

Frontend en Vercel

Backend en Render

ComfyUI en local + ngrok

🧪 ¿Cómo probarlo?
Accedé a la web app 🟣 Link a VAPAI (Vercel)

Escribí un prompt simple (ej: jean, sweater, camisa, face, etc).

Subí una imagen con fondo blanco y buena luz.

Hacé clic en Segmentar

Esperá unos segundos y descargá la prenda segmentada.

🚀 Para desarrolladores
Estructura del repo
bash
Copy
Edit
vapai-project/
├── front/ # Frontend con React + Vite
│ └── App.jsx
│ └── ...
├── back/ # Backend con Express
│ └── index.js
│ └── workflow_segment.json
├── README.md
Variables de entorno necesarias
En /back/.env
env
Copy
Edit
NGROK_URL=https://xxxxxxx.ngrok-free.app
PORT=3001
🧠 Sobre la segmentación
Este sistema se basa en una combinación de modelos de segmentación de última generación que permiten identificar objetos dentro de una imagen sin necesidad de entrenamiento adicional. Gracias al uso de GroundingDINO, el sistema puede interpretar prompts textuales como "jean" o "sweater", mientras que SAM recorta la región identificada con alta precisión. La mejora final se realiza con VITMatte para lograr bordes suaves y precisos.

📦 Roadmap
Subida de imágenes

Segmentación en memoria (sin guardar en disco)

Descarga de imagen segmentada

Soporte para múltiples imágenes (batch .zip)

Feedback visual más avanzado (barra de progreso)

WebSocket feedback desde ComfyUI

Deploy completo de ComfyUI en la nube

🧵 Créditos
Este proyecto fue realizado como parte de una prueba técnica para VAPAI Studio.
Hecho con ❤️ por @juangoyret
