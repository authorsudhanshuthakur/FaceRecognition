# FelisEye Cloud Deployment Guide

FelisEye is a complete, full-stack web application with a **FastAPI Python backend** (providing offline AI facial recognition, liveness detection, and encrypted biometric storage) and a **responsive Neumorphic Single Page Web App** (Vanilla HTML5/CSS3/ES6).

Because the biometric recognition engine requires native C++ machine learning libraries (`dlib`, `face_recognition`, `OpenCV`), you have two simple ways to deploy:

1. **Option 1 (Recommended & Turnkey): Full-Stack Container Cloud** — Render, Railway, Fly.io, Hugging Face Spaces, or Koyeb (Runs the complete web UI + AI backend together under a single URL with zero configuration).
2. **Option 2: Decoupled Deployment** — Deploy the static web UI on Netlify or Vercel, and proxy API calls to your free backend instance on Render or Railway.

---

## Option 1: 1-Click Full-Stack Deployment (Recommended)

### A. Deploy to Render (100% Free)
1. Push your FelisEye repository to **GitHub** or **GitLab**.
2. Go to [Render Dashboard](https://dashboard.render.com/) and click **New +** ➔ **Web Service**.
3. Select your repository.
4. Render will automatically detect `render.yaml` and `Dockerfile`.
5. Configuration:
   - **Environment**: `Docker`
   - **Plan**: `Free`
   - **Health Check Path**: `/`
6. Click **Deploy Web Service**.
7. Once finished, Render gives you a public HTTPS URL (e.g. `https://feliseye.onrender.com`). Open this URL on your browser or phone to use the app!

---

### B. Deploy to Railway
1. Go to [Railway](https://railway.app/) and click **New Project** ➔ **Deploy from GitHub repo**.
2. Select your FelisEye repository.
3. Railway automatically detects `railway.json` and `Dockerfile`.
4. Under project **Settings** ➔ **Networking**, click **Generate Domain**.
5. Your app is live!

---

### C. Deploy to Hugging Face Spaces (Free Docker Hosting)
1. Create a new Space on [Hugging Face Spaces](https://huggingface.co/spaces).
2. Select **Space SDK**: **Docker** (Blank).
3. Push or upload your FelisEye repository.
4. Hugging Face builds and runs the container automatically using the pre-configured parameters in `Dockerfile`.

---

## Option 2: Deploying to Netlify or Vercel

If you want your static UI hosted on Netlify or Vercel's global CDN:

### A. Deploying to Netlify
1. Log in to [Netlify](https://app.netlify.com/) and click **Add new site** ➔ **Import an existing project**.
2. Connect your GitHub repository.
3. Netlify automatically reads `netlify.toml`:
   - **Publish directory**: `static`
4. Open [netlify.toml](file:///c:/Users/sudha/Desktop/FelisEye_/netlify.toml) in your code editor and replace `https://feliseye-api.onrender.com` with your actual live backend URL from Render/Railway.
5. Click **Deploy site**.

---

### B. Deploying to Vercel
1. Log in to [Vercel](https://vercel.com/) and click **Add New...** ➔ **Project**.
2. Import your GitHub repository.
3. Open [vercel.json](file:///c:/Users/sudha/Desktop/FelisEye_/vercel.json) in your code editor and update `https://feliseye-api.onrender.com` with your live backend URL from Render/Railway.
4. Click **Deploy**.

---

## Option 3: Running via Docker Locally or on a VPS
To run FelisEye anywhere with Docker:

```bash
# Build the Docker image
docker build -t feliseye .

# Run the container
docker run -d -p 10000:10000 --name feliseye feliseye
```
Access the application at `http://localhost:10000`.
