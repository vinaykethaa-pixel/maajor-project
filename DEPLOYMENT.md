# 🚀 Render Deployment Guide

Follow these steps to deploy your Medical AI Liver Segmentation platform to Render.

## 1. Prepare your GitHub Repository
Ensure all your latest changes are pushed to GitHub. (I have already done this for you with the latest mobile fixes).

## 2. Create a Web Service on Render
1. Log in to [dashboard.render.com](https://dashboard.render.com).
2. Click **New +** and select **Web Service**.
3. Connect your GitHub repository (`vinaykethaa-pixel/maajor-project`).

## 3. Configure the Web Service
Set the following settings in the Render dashboard:
- **Name**: `liver-segmentation-ai` (or any name you prefer)
- **Environment**: `Python 3`
- **Region**: (Choose the one closest to you)
- **Branch**: `main`
- **Build Command**: 
  ```bash
  pip install -r requirements.txt && python manage.py collectstatic --noinput && python manage.py migrate
  ```
- **Start Command**: 
  ```bash
  gunicorn Liver_Image_Segmentation_Using_DeepLearning.wsgi --timeout 120
  ```

## 4. Set Environment Variables
Go to the **Environment** tab on Render and add these variables:
- `PYTHON_VERSION`: `3.10.0`
- `DEBUG`: `False` (Set to `True` only if you need to debug errors initially)
- `SECRET_KEY`: (Generate a long random string or use the one from your settings.py)

## 5. Deployment
- Click **Create Web Service**.
- Render will start building your project. You can monitor the logs in the dashboard.
- Once finished, Render will provide a URL (e.g., `https://liver-segmentation-ai.onrender.com`).

---

> [!IMPORTANT]
> **Database Note**: By default, this project uses SQLite (`db.sqlite3`). On Render, SQLite databases are reset every time the service restarts. For a permanent database, you should create a **Render PostgreSQL** instance and update your `DATABASES` setting.

> [!TIP]
> **Static Files**: The project is already configured with `WhiteNoise`, so Render will automatically serve your CSS, images, and JavaScript files correctly.

---
**Status**: Mobile-responsive fixes are applied. Deployment files (`Procfile`, `render.yaml`) are ready.
