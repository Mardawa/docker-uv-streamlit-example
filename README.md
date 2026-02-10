# 🚀 Minimal Streamlit Setup with Docker & uv

This project is a minimal template for running a Streamlit application using:

- **Docker** for reproducible environments  
- **uv** as the ultra‑fast Python package/dependency manager  
- **Docker Compose Watch** for hot‑reloading during development  

It provides a clean and modern workflow with almost zero local setup.

---

## 📦 Project Structure

```
.
├── Dockerfile
├── docker-compose.yml
├── pyproject.toml
├── uv.lock
└── src/
    └── app.py
```

---

## ▶️ Run the App (with Hot Reload)

Requires **Docker Compose 2.22.0 and later** to support `compose watch`.

Start the development server:

```bash
docker compose watch
```

This will:

- build the container  
- sync changes from your local `./src` into the container  
- automatically reload Streamlit when files change  

Open the app at:

👉 <http://localhost:8501>

---

## ▶️ Run Without Hot Reload (Production‑like)

```bash
docker compose up --build
```

---

## 🧪 Example Streamlit App (`src/app.py`)

```python
import streamlit as st

st.title("Hello from Streamlit + Docker + uv!")
st.write("This is a minimal reproducible setup.")
```

---

## ⚙️ Key docker-compose Settings

The project uses Docker Compose’s `develop.watch` feature:

```yaml
develop:
  watch:
    - action: sync
      path: ./src
      target: /app/src
    - action: rebuild
      path: ./uv.lock
```

- **sync:** updates app code live  
- **rebuild:** triggers when dependencies change  

---

## 🧰 Using uv Locally (Optional)

Install dependencies:

```bash
uv sync
```

Run Streamlit locally without Docker:

```bash
uv run streamlit run src/app.py
```

---

## 🧹 Cleanup

Stop containers:

```bash
docker compose down
```

Remove unused Docker resources:

```bash
docker system prune -a
```

---
