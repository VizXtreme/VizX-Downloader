# 🎵 VizX-Downloader

### A YouTube Media Downloader

[![Release](https://img.shields.io/badge/Release-v1.0-blue?style=for-the-badge)](https://github.com/)
[![Platform](https://img.shields.io/badge/Platform-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/)
[![Aria2](https://img.shields.io/badge/aria2c-Optimized-A62627?style=for-the-badge)](https://aria2.github.io/)

**VizX-Downloader** is a standalone Windows application that lets you search and download music and videos from YouTube. It features a responsive dark-mode web dashboard, downloads multiple files in parallel, embeds original album art/metadata automatically, and saves your download queue so you can resume downloads even after restarting the app.

Because it is compiled into a single executable (`VizX-Downloader.exe`), **you do not need Python or pip installed** to run it.

---

## ⚡ Key Features

*   **Interactive Search**: Type a song name in the search bar, preview the thumbnail/duration, and start the download with a single click.
*   **Bulk Queueing**: Paste a list of track names or YouTube links (one per line) in the bulk tab to fetch and download them all in a batch.
*   **Audio & Video Quality Options**:
    *   **Audio**: Extracts high-quality `.m4a` files.
    *   **Video**: Choose between `1080p`, `720p`, and `480p` MP4 files.
*   **Auto-Artwork & Metadata**: Automatically retrieves track details and embeds original thumbnails directly into the downloaded files as cover art.
*   **Active Controls**: Start, pause, resume, or cancel downloads on the fly. View live progress bars, speed metrics, and estimated time remaining (ETA).
*   **Session Persistence**: Saves your queue to a local database. If you close the app, your downloads will reload in a "Paused" state so you can resume them exactly where you left off.
*   **Temp Cleanup**: Cleans up leftover `.part` and `.ytdl` files on startup and shutdown to keep your disk clean.
*   **Speed Booster**: If `aria2c` is installed on your computer, the app automatically leverages it to download using up to 16 parallel connections for maximum speeds.

---

## 🛠️ Prerequisites

While you don't need Python, you do need one external tool on your system for the app to work:

1.  **FFmpeg (Required)**: Needed to extract audio and merge high-quality video/audio streams together.
    *   **How to install**: Open PowerShell and run:
        ```powershell
        winget install Gyan.FFmpeg
        ```
        *(Or download the installer manually from [ffmpeg.org](https://ffmpeg.org) and make sure to add it to your system Environment `PATH`).*
2.  **Aria2 (Optional, for 10x speed boost)**: 
    *   **How to install**: Open PowerShell and run:
        ```powershell
        winget install aria2
        ```

---

## 🚀 How to Run the App

1.  Download the latest release from the Releases page.
2.  Double-click **`VizX-Downloader.exe`**.
3.  A terminal window will open to start the local backend server, and your default web browser will automatically open to `http://127.0.0.1:5000`.
4.  **To shut down the app**: Simply click the red **Quit** (power icon) button in the top-right header of the web page. This safely pauses your queue, sweeps temporary files, and closes the terminal window automatically.

---

## 📁 App Layout

Once run, the executable creates and manages the following files in its folder:

```text
├── VizX-Downloader.exe    # The standalone app (double-click to run!)
└── VizX-Downloads/        # [Auto-generated] Where your downloads are saved
    ├── .downloads_state.json  # Hidden database tracking your paused/completed downloads
    └── ...                 # Your downloaded music and videos!
```

---

## 🔍 Troubleshooting

#### ❌ **Downloads fail at 100% (or audio conversion errors)**
*   **The Cause**: FFmpeg is either not installed or the system can't find it.
*   **The Fix**: Make sure you installed FFmpeg via the command above. Restart your computer (or close and re-open the command prompt/terminal) so Windows registers the new system variable.

#### ❌ **Downloads are slow**
*   **The Fix**: Install `aria2` via `winget` or by downloading it manually. Once installed, `VizX-Downloader.exe` will automatically detect it and download files using 10 concurrent streams.

#### ❌ **"Unable to extract video data" errors**
*   **The Cause**: YouTube frequently changes its site layout, causing the built-in scraping engine to temporarily break.
*   **The Fix**: Ensure you are using the latest version of `VizX-Downloader.exe`. Re-downloading the updated release build will include the latest scraper updates.
