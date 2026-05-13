## Quick run instructions

Follow these exact commands in PowerShell on Windows (from the repo root) to run the Streamlit demo locally.

Requirements:
- Python 3.9–3.11
- Git
- (Optional) Docker

1) Clone the repo (if needed) and enter the folder

```powershell
git clone https://github.com/AlbertY123/butt_or_bread.git
cd butt_or_bread
```

2) Create and activate a virtual environment (skip if `.venv` already exists)

```powershell
python -m venv .venv
# PowerShell activation:
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
& .\.venv\Scripts\Activate.ps1
# (Or CMD): .\.venv\Scripts\activate.bat
```

3) Install dependencies

```powershell
& .\.venv\Scripts\python.exe -m pip install --upgrade pip
& .\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

4) Run the Streamlit app

```powershell
& .\.venv\Scripts\python.exe -m streamlit run streamlit_app.py
```

- On first run Streamlit shows a telemetry onboarding prompt — press Enter to skip.
- The app serves on http://localhost:8501 by default.

5) If the model download fails or you prefer to pre-download the weights

```powershell
Invoke-WebRequest -Uri "https://github.com/Kawaeee/butt_or_bread/releases/download/v1.3/buttbread_resnet152_3.h5" -OutFile .\buttbread_resnet152_3.h5
```

Place `buttbread_resnet152_3.h5` in the repo root so the app loads it locally.

6) Optional — run training (requires your prepared `datasets/` folder)

```powershell
& .\.venv\Scripts\python.exe train.py --dataset-path datasets/ --model-path buttbread_resnet152_3.h5 --epochs 3
```

7) Optional — Docker

```powershell
docker build -t butt-bread-image .
docker run --rm --name=butt-bread-container -p 8501:8501 butt-bread-image
# or with docker-compose
docker-compose build
docker-compose up
```

Troubleshooting tips
- If you see `streamlit : The term 'streamlit' is not recognized`, use the explicit `python -m streamlit` command above or activate the venv.
- If you see JSON decode or encoding errors, pull the latest repo (the app opens `streamlit_app.json` as UTF-8).
- If you see disk/psutil errors on Windows, pull the latest repo (the health check now uses `shutil.disk_usage`).

If you want, I can also add a short `README` section about training details, dataset layout, or how to run the predictor notebook.
