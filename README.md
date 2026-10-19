# Auto‑3D Cartoon Generator (Free, Cloud‑Only)

## What this repository does
- **You provide a Hindi script** (plain‑text or JSON).  
- A **Google Colab notebook** runs **Blender (3‑D)** on a free GPU, builds a simple scene, sync‑lip‑syncs the script with a synthetic Hindi voice (Coqui TTS) and renders a **15‑20 min** video.
- The rendered MP4 is saved to **your Google Drive** (no local install needed).
- A tiny **HTML dashboard** (hosted on GitHub Pages) polls a status file on Drive so you can see progress without leaving the browser.
- All tools used are **free**: Blender (open‑source), Colab (free tier), Coqui TTS (free models), Google Drive, GitHub Pages.

## Folder layout (under `C:\Users\sskum\.gemini\scratch\auto‑3d‑cartoon`)
```
auto‑3d‑cartoon/
│   README.md               # This file
│   script.json             # Put your Hindi story here (see format below)
│   colab_notebook.ipynb    # Run in Google Colab – renders the video
│   dashboard.html          # Simple monitor page (host on GitHub Pages)
│   .gitignore              # Ignore Drive credentials
└───assets/                # (optional) custom 3‑D models, textures
```

## Step‑by‑step usage (no local install)
1. **Clone / copy the folder** to your machine (just download the ZIP from the GitHub repo we will create for you).  
2. **Edit `script.json`** – add your Hindi dialogue.  
3. **Open the notebook**: Click the link we generate below → *Open in Colab* → run all cells.  
   - The notebook will ask you to **mount your Google Drive** (free).  
   - It will download a minimal Blender build, generate a basic scene (a simple stage, cartoon‑style characters), synthesize the voice, and start rendering.  
4. **Monitor**: Open `dashboard.html` (hosted on GitHub Pages, URL provided after we push). It shows a progress bar and a link to the final MP4 when done.  
5. **Download** the MP4 from your Drive folder and upload to YouTube.

## Script format (`script.json`)
```json
{
  "title": "Your Video Title",
  "scenes": [
    {
      "character": "hero",
      "line": "नमस्ते दोस्तों! आज हम एक नई कहानी सुनाने वाले हैं…",
      "duration": 5
    },
    {
      "character": "sidekick",
      "line": "वाह! कितनी रोचक लग रही है कहानी!",
      "duration": 4
    }
    // add more scenes – total duration should be ~ 900‑1200 seconds (15‑20 min)
  ]
}
```
*You can keep adding objects; the notebook will concatenate the lines and generate a single audio track.*

## Creating the GitHub repo (one‑click script)
We provide a tiny PowerShell script (`create_repo.ps1`) that:
- Initializes a local git repo.
- Commits all files.
- Uses the **GitHub CLI** (`gh`) to create a new repository under your account (you need a personal access token – we’ll guide you).  
- Pushes the repo and enables **GitHub Pages** (source: `main` branch, `/`).

> **You do not need to install anything locally** – just copy the script, run it, and follow the prompts.

## How the rendering works (inside Colab)
1. `!apt-get install -y blender` – installs the latest Blender (≈ 200 MB, free).  
2. Load the JSON script and generate a **phoneme‑timed** audio file using **Coqui TTS** (Hindi model).  
3. Create a **basic cartoon rig** (cubes, simple materials) – the notebook uses Blender’s Python API to sync mouth shapes to the audio.  
4. Render frames at 24 fps, encode with **ffmpeg** to `output.mp4`.  
5. Move the MP4 to `MyDrive/auto‑3d‑cartoon/output/`.

## FAQ
- **Do I need a powerful PC?** No. All heavy lifting happens in Colab.  
- **Will I be charged?** Only if you exceed Colab’s free quota (unlikely for a single 20‑min video).  
- **Can I use my own 3‑D models?** Yes – place them in the `assets/` folder and the notebook will import them automatically.  
- **What about music?** The notebook downloads a royalty‑free Indian‑style loop from **Free Music Archive** and mixes it at low volume.

---

**Next step:** Add your Hindi script to `script.json` (replace the placeholder content). Then run the Colab notebook using the link we’ll give you shortly.

---

*All files are stored under `C:\Users\sskum\.gemini\scratch\auto‑3d‑cartoon`. If you need the repo URL or the Colab link, let me know.*
