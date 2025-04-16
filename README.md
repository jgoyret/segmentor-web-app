# 🧠 VAPAI – Segmentador de Prendas

Web app que permite segmentar prendas de ropa en imágenes. Usando modelos de vision como **GroundingDINO**, **SAM**, la app detecta y recorta ropa a partir de un prompt como `"jean"` o `"sweater"`, devolviendo una imagen con fondo transparente lista para usar.

---

## 🚀 ¿Cómo usar?

1. **Accedé a la app** en [🔗 vercel.app](https://front-vapai-app.vercel.app/)
2. **Escribí un prompt** como `jean`, `camisa`, `face`, etc.
3. **Subí una imagen** con buena luz y fondo neutro (blanco recomendado).
4. **Hacé clic en “Segmentar”**
5. La app procesará la imagen y podrás **descargar la prenda segmentada**.

---

## 🔬 ¿Qué hace esta app?

- Recibe una imagen y un prompt.
- Usa modelos de visión para detectar y recortar esa prenda.
- Devuelve una imagen con fondo transparente.
- Todo esto ocurre en segundos y sin necesidad de entrenar ningún modelo.

---

## 🧰 Tecnologías usadas

| Parte    | Tecnología                  |
| -------- | --------------------------- |
| Frontend | React + Vite + Tailwind CSS |
| Backend  | Node.js + Express           |
| IA       | ComfyUI (local) vía ngrok   |

---

## 🧠 Modelos utilizados

- **GroundingDINO** → interpreta el prompt y encuentra dónde está la prenda. https://github.com/IDEA-Research/GroundingDINO
- **SAM (Segment Anything Model)** → recorta con precisión. https://github.com/facebookresearch/sam2

También se utilizan nodos personalizados como:

- `LoadImageFromBase64` https://github.com/glowcone/comfyui-base64-to-image
- `Send Http Request` https://github.com/cuongloveit/comfy_http_request
- `SegmentAnythingUltra V2` https://github.com/chflame163/ComfyUI_LayerStyle_Advance

---

## 🧩 Nodos utilizados en ComfyUI

Para realizar la segmentación de prendas, el workflow utiliza tres nodos principales en ComfyUI:

### 1. `LoadImageFromBase64`

Este nodo personalizado permite **cargar una imagen desde un string base64**, evitando la necesidad de guardar archivos en disco.
deal para aplicaciones desplegadas en la nube o donde se trabaja con imágenes en memoria.

### 2. `SegmentAnythingUltra V2`

Nodo avanzado de segmentación que combina tres modelos potentes:

- **GroundingDINO**: para localizar la prenda a partir de un texto (`prompt`).
- **SAM (Segment Anything Model)**: para realizar la segmentación.
- **VITMatte**: para mejorar los bordes del recorte.

⚙️ **Parámetros clave utilizados**:

| Parámetro        | Descripción                                           |
| ---------------- | ----------------------------------------------------- |
| `prompt`         | Texto que describe la prenda (ej: `"jean"`).          |
| `threshold`      | Confianza mínima para detectar objetos (ej: `0.3`).   |
| `detail_method`  | Método de refinado de bordes (`VITMatte`).            |
| `process_detail` | Booleano para activar el refinado (`true`).           |
| `device`         | `"cuda"` o `"cpu"` según disponibilidad.              |
| `max_megapixels` | Límite de resolución para evitar errores por memoria. |

### 3. `Send Http Request`

Este nodo envía la imagen segmentada **de vuelta al backend**, una vez finalizado el proceso.

---

## 🧪 Instalación local

### Requisitos

- Node.js
- Python + entorno virtual para ComfyUI
- Cuenta en [ngrok](https://ngrok.com) (o similar) para exponer el backend de IA

### Cloná el repositorio principal

Este repositorio usa submodules para el frontend y el backend. No olvides clonar con --recurse-submodules:

```bash
git clone --recurse-submodules https://github.com/jgoyret/vapai-project
cd vapai-project
```

Instalar frontend

```bash
cd front-vapai-app
npm install
npm run dev
```

Instalar backend

```bash
cd ../back-vapai-app
npm install
```

Agregá un archivo .env

```bash
NGROK_URL=https://tulink.ngrok-free.app
```

ejecuta el backend:

```bash
node index.js
```
