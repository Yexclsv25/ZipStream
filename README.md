# ZipStream 📦⚡

**Download what's inside a ZIP — not the ZIP.**

ZipStream is a native Android downloader built with Kotlin and C++ that streams and extracts files directly from remote `.zip` archives using HTTP byte-range requests. Instead of downloading a massive 30GB–60GB archive and needing **double the free space** just to unpack it, ZipStream reads the remote central directory and writes extracted files straight to your storage on the fly.

---

### ✨ Key Features
* **Zero Double-Storage Overhead:** Never hold both the compressed `.zip` file and the unpacked files on your phone at the same time.
* **Native C++ Core & ZIP64 Support:** Custom C++ engine (`zip_format.cpp`, `entry_writer.cpp`) parses standard and ZIP64 central directories (tested with 70,000+ entries) and verifies CRC32 checksums and file sizes on the fly.
* **Parallel Byte-Range Streaming:** Configurable 1–8 concurrent HTTP range connections for fast downloads.
* **Smart Resume & Skip:** Automatically skips already-completed files and resumes partially written uncompressed (`STORE`) entries after a connection drop.
* **Selective File Filtering:** Filter downloads by filename or extension (e.g., `.rpf`) so you only pull the exact files you need.
* **Custom HTTP Headers:** Add custom cookies or authorization tokens for restricted download links.
* **Background Foreground Service:** Keeps streaming reliably in the background with a live progress notification and one-tap **Cancel** button.
* **Dark-First Material 3 UI:** Clean dashboard showing live download speed, ETA, file count, overall progress, and individual per-file progress bars.

---

### 📱 How It Works
1. **Paste a direct download link** (must be hosted on a server that supports HTTP `Accept-Ranges: bytes`).
2. **Grant "All Files Access"** on first launch so ZipStream can write directly to your public storage.
3. **Tap Start** — ZipStream fetches the remote ZIP directory, preserves the exact folder hierarchy, and extracts everything straight into `Download/ZipStream/<zip name>/`.

---

### ⚠️ Current Limitations
* **Server Requirements:** The host server must support HTTP byte-range requests (`206 Partial Content`).
* **Encryption & Compression:** Password-protected ZIPs and non-standard compression methods are currently skipped/marked as failed entries.
* **Resume Behavior:** Uncompressed (`STORE`) files resume from the exact byte offset; compressed (`DEFLATE`) entries restart from zero if interrupted.

---

### 🛠️ Tech Stack & Architecture
* **Language:** Kotlin + C++17 (connected via JNI)
* **Build System:** Gradle, Android NDK, CMake, ViewBinding
* **UI:** Material Design 3 (Dark-first theme)
* **Package Name:** `com.zipstream.app`

---

### 🚧 Project Status
ZipStream is currently in active development. The native C++ core has passed stress testing on large ZIP64 archives, and final Android build verification is underway.

👉 **Click `Watch` -> `Custom` -> `Releases` at the top right of this repository to get notified as soon as the first beta APK is uploaded!**

---

### 🗺️ Planned Roadmap
- [x] Native C++ ZIP & ZIP64 central directory parser
- [x] Parallel HTTP byte-range downloader (1–8 threads)
- [x] File extension filtering & custom HTTP headers
- [ ] Built-in link resolvers (Buzzheavier, MediaFire, Pixeldrain)
- [ ] Sequential `.rar` & split `.part1.rar` streaming support
- [ ] `.7z` & `.iso` header mapping
