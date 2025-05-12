# 🖼️ Ollama Vision Analyzer

  

A one‑file Gradio web app for rapid visual scene understanding with **llama3.2‑vision** served through **[Ollama](https://ollama.ai/)**. Select or upload a picture, hit **Analyze**, and receive a rich, structured JSON description including detected objects, scene, colors, text and more.

---

## ✨ Features

* **Local & Upload Sources** – choose from `~/images` or drag‑and‑drop a file.
* **Live Preview** – instant thumbnail before analysis.
* **Custom Prompts** – override the default analysis request with your own instructions.
* **Schema‑Constrained Output** – responses are validated JSON that fits the `ImageDescription` schema.
* **Model Health Check** – one‑click readiness probe for the Ollama vision model.
* **Self‑contained** – single Python script, no external front‑end build.
* **Shareable** – `demo.launch(share=True)` makes a public link via Gradio.

---

## 🚀 Quick start

```bash
# 1. Clone the repo (or copy the single script)
git clone https://github.com/bigdog3000/Ollama_Vision.git
cd Ollama_Vision

# 2. Create a virtual env (recommended)
conda create -n ollamaimage python=3.11 -y
conda activate ollamaimage

# 3. Install deps
pip install -r requirements.txt
#   or directly:
# pip install gradio pillow pydantic ollama

# 4. Run Ollama with the llama3.2‑vision model
ollama serve &               # starts the Ollama backend
ollama pull llama3.2-vision  # first‑time model download

# 5. Launch the Gradio app
gadio_vision_ollama.py  # listens on http://localhost:8040
```

> **Note**: By default the app scans `~/images` for selectable pictures. Symlink or copy whatever you like into that folder, or edit `list_image_files()` to point elsewhere.

---

## 🧩 JSON Schema

```text
ImageDescription
 ├─ summary:          str
 ├─ objects[]
 │   ├─ name:         str
 │   ├─ confidence:   float  (0–1)
 │   └─ attributes:   str
 ├─ scene:            str
 ├─ colors[]:         str
 ├─ time_of_day:      "Morning" | "Afternoon" | "Evening" | "Night"
 ├─ setting:          "Indoor" | "Outdoor" | "Unknown"
 └─ text_content:     str | null
```

All model responses are expected to match this shape, making them easy to post‑process or feed into downstream pipelines.

---

## 🖥️ Screenshots


![image](https://github.com/user-attachments/assets/271af9bb-bafe-43fc-9d63-b7e599b54625)


---

## 🔧 Configuration

| Variable      | Default    | Description                                     |
| ------------- | ---------- | ----------------------------------------------- |
| `IMAGES_DIR`  | `~/images` | Folder scanned for the dropdown list            |
| `SERVER_PORT` | `8040`     | Change `demo.launch()` call to override port    |
| `SHARE`       | `True`     | Set `share=False` to disable public Gradio link |

You can also point **Ollama** at a remote server via the `OLLAMA_HOST` environment variable.

---

## 🛠️ Extending

* **Alternative models**: swap `llama3.2-vision` in both `check_model_ready()` and `analyze_image()`.
* **Post‑processing**: parse `output_box` JSON into domain‑specific dashboards or databases.
* **Batch mode**: wrap `analyze_image()` in a loop to process many files headlessly.

---

## 🙏 Acknowledgements

* [Gradio](https://github.com/gradio-app/gradio) – dead‑simple ML front‑ends.
* [Ollama](https://github.com/jmorganca/ollama) – local model runner with vision support.
* Llama 3 contributors for the underlying vision model.

---

## 📜 License

Released under the [MIT License](LICENSE).

> Made with ❤️ and llamas.
