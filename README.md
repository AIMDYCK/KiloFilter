<div align="center">

# 📦 KiloFilter

### Organize, analyze and rescue your files — **by type, without the mess.**

A modern, dark-themed Windows utility that scans messy folders, classifies files
by category and extension, detects duplicates with cryptographic hashing, and
copies a clean, organized result — all from a single window.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Release](https://img.shields.io/badge/release-v2.1.0-blue.svg)](../../releases)
[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4.svg)](https://dotnet.microsoft.com/download/dotnet/8.0)
[![Platform](https://img.shields.io/badge/platform-Windows-0078D6.svg)](#-requirements)
[![Made with WinForms](https://img.shields.io/badge/UI-WinForms-68217A.svg)](#-architecture)
[![Languages](https://img.shields.io/badge/languages-6-brightgreen.svg)](#-localization)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

</div>

---

## 📖 What is KiloFilter?

Sorting a folder full of mixed files by hand — images here, documents there,
videos somewhere else — is slow, repetitive and error-prone. Duplicates hide in
plain sight, quietly eating up disk space.

**KiloFilter does all of that for you.**

Point it at a source folder and it scans recursively, groups every file by type
and by your own custom categories, and copies an organized, easy-to-browse
structure to the destination. It can also hunt down duplicates with BLAKE3
cryptographic hashing and remove them using an intelligent strategy — while
keeping the original files safe at all times.

> **Non-destructive by design.** KiloFilter copies files into an organized
> structure; your originals stay exactly where they are. Nothing is deleted
> unless you explicitly ask for it.

---

## 📸 Screenshot

### Main window — analyze, classify and rescue at a glance

<p align="center">
  <img src="Assets/screenshot.png" alt="KiloFilter — main window" width="900">
</p>

---

## ✨ Key Features

<table>
<tr>
<td width="50%" valign="top">

### 📂 Smart file organization
- **Auto classification** — scans folders recursively and sorts by type.
- **Two-level structure** — organized by *Category → Extension*
  (`Images/JPG/`, `Documents/PDF/`).
- **Custom categories** — create your own groups and manage their extensions.
- **Safe copy** — organized files are copied out; originals remain untouched.

### 🔍 Duplicate detection
- **Three-stage detection** — size grouping → partial hash (64 KB) → full hash.
- **BLAKE3 hashing** — fast, reliable cryptographic fingerprinting.
- **Detailed reports** — file counts, paths and total wasted space.
- **Instant reopening** — reload previous analyses without rescanning.

</td>
<td width="50%" valign="top">

### ❌ Smart duplicate deletion
- **Three strategies** — Keep Newest, Keep Oldest or Keep Smallest.
- **Real-time preview** — see exactly what will be deleted before confirming.
- **Advanced filtering** — search by filename and filter by size range.
- **Space calculation** — shows how much disk space will be freed.

### 🎨 Built for humans
- **Multilingual UI** — 6 languages, switchable at runtime.
- **Drag & drop** — drop folders straight into the source/destination fields.
- **Cancellable operations** — interrupt long scans and exports anytime.
- **Dark theme** — a clean, custom Windows Forms interface.

</td>
</tr>
</table>

---

## 🧩 Duplicate Deletion Strategies

Choose the strategy that matches your intent — the preview updates instantly.

| Strategy | What it keeps | Best for |
|---|---|---|
| **🆕 Keep Newest** | The most recently modified file | Keeping the latest version |
| **📜 Keep Oldest** | The original / oldest file | Archival, preserving originals |
| **🗜️ Keep Smallest** | The smallest file in the group | Maximizing freed disk space |

---

## 📋 Requirements

| Component | Why you need it | Link |
|---|---|---|
| **Windows 7 / 10 / 11** (x64) | The app is a Windows Forms desktop application | — |
| **.NET 8 Desktop Runtime** | To run the lightweight (framework-dependent) build | [Download](https://dotnet.microsoft.com/download/dotnet/8.0) |

> 💡 The **standalone** build bundles the runtime — no separate installation is
> required. Just download and run.

---

## 📥 Installation

### Option A — Portable *(recommended)*

Download `KiloFilter.exe` from the [Releases](../../releases) page and
double-click it. The standalone build is self-contained: no installation and no
external dependencies.

### Option B — Build from source

```sh
git clone https://github.com/AIMDYCK/KiloFilter.git
cd KiloFilter
dotnet publish -c Release -r win-x64 --self-contained false -o publish
```

The executable will be at `publish\KiloFilter.exe`.

---

## 🚀 How to Use

### Basic file organization
1. **Source Folder** — select the folder with your files (or drag & drop it).
2. **Analyze Disk** — scan and auto-classify files by type.
3. **Review** — check categories and file statistics.
4. **Configure** — adjust categories, blacklist and minimum file sizes *(optional)*.
5. **Destination Folder** — choose where organized files will be copied.
6. **Rescue** — copy selected files into the organized category/extension tree.

### Smart duplicate deletion *(v2.1.0+)*
1. **Analyze Duplicates** — scan for identical files using cryptographic hashing.
2. **Apply Filters** *(optional)* — search by filename and set a min/max size range.
3. **Select a strategy** — Keep Newest, Keep Oldest or Keep Smallest.
4. **Review the preview** — see files marked for deletion and the total space freed.
5. **❌ Smart Delete** — execute the deletion, then confirm in the dialog.

> ⏹️ Use the **Cancel** button at any time to interrupt analysis, duplicate
> scanning or a file rescue.

---

## 🧠 How It Works

### File organization
1. Scans the source folder recursively.
2. Groups files by extension and custom categories.
3. Filters by blacklist and minimum file size settings.
4. Organizes output hierarchically: **Category → Extension**.
5. Displays results in an interactive list with statistics.

### Duplicate detection
1. **Stage 1** — groups files by identical file size.
2. **Stage 2** — hashes the first 64 KB of each file (fast comparison).
3. **Stage 3** — computes the full BLAKE3 hash for exact matches.
4. **Report** — shows duplicate groups with the total wasted space.
5. **Optional deletion** — safely remove duplicates while keeping originals.

---

## 🏗️ Architecture

KiloFilter is a **.NET 8 Windows Forms** application built around a small,
focused core that separates analysis, caching and UI concerns.

```
Program.cs ──► MainForm
                 │
     ┌───────────┼───────────────┬───────────────┐
     │           │               │               │
  Core/        Forms/          Models/         Assets/
 (logic)      (WinForms UI)    (data models)   (icons, media)
```

### Project structure

```
KiloFilter/
├── Program.cs            # Application entry point
├── Core/                 # Localization, caching and duplicate logic
│   ├── CacheManager.cs
│   ├── Localization.cs
│   └── SmartDuplicateDeleter.cs
├── Forms/                # Windows Forms GUI
├── Models/               # Plain data models
├── Assets/               # Graphic resources (screenshot, icons)
├── KiloFilter.csproj
├── KiloFilter.sln
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

---

## 🌍 Localization

| Code | Language |
|---|---|
| `en` | English *(default)* |
| `es` | Spanish |
| `fr` | French |
| `de` | German |
| `it` | Italian |
| `ja` | Japanese |

Translations are managed by [`Core/Localization.cs`](Core/Localization.cs:1) and
can be switched live from the UI — **no restart required**.

---

## ⚡ Performance: Smart Cache System

Analyzing the same folders repeatedly is fast thanks to the built-in cache:

1. **First analysis** — scans the folder completely and saves results to cache.
2. **Subsequent analysis** — detects changes using cryptographic content hashing.
3. **No changes?** — instantly reloads the previous results (typically < 1 second).
4. **Changes detected?** — offers a fresh scan or loading the cached results anyway.

**Cache management**
- Stored as human-readable JSON in `%AppData%\Roaming\KiloFilter\Cache`.
- Entries older than **30 days** are removed automatically on startup.
- Browse, reload or delete individual entries from the **📋 History** window.

---

## 🛠️ Tech Stack

- **Language**: C# 12
- **Framework**: .NET 8 (Windows Forms)
- **Hashing**: BLAKE3 (cryptographic file fingerprinting)
- **Concurrency**: `Parallel.ForEach` for multithreaded scanning
- **UI**: Windows Forms with a custom dark theme
- **Localization**: 6 languages (English, Spanish, French, German, Italian, Japanese)

---

## ⚠️ Disclaimer

> Use at your own risk. The author is not responsible for any data loss. Always
> verify destination paths and keep backups of important files.

---

## 🤝 Contributing

Contributions are what make open source amazing! Whether it's a bug report, a
translation, a documentation fix or a new feature — you are welcome.

Please read **[CONTRIBUTING.md](CONTRIBUTING.md)** for the repository structure
and the pull request process.

- 🐛 Found a bug? [Open an issue](../../issues)
- ✨ Have an idea? [Open a feature request](../../issues)

---

## 📄 License

Released under the [MIT License](LICENSE). See the [`LICENSE`](LICENSE:1) file
for details.

---

## 🛠️ Credits & Development

**KiloFilter** was designed and developed by **AIMDYCK**.

This project was built with the help of the following tools and technologies:

- **Visual Studio** — the primary IDE for .NET 8 / Windows Forms development, debugging and publishing.
- **Supermaven** — AI-powered code completion that accelerated day-to-day coding.
- **Roo Code** — the AI coding agent used to plan, refactor and implement the application.
- **DeepSeek API** — the large language model powering the AI-assisted development workflow.

A heartfelt thank you to the open source community behind **BLAKE3** and the
**.NET** platform, without whom this project would not exist.

<div align="center">

**Made with ❤️ for anyone drowning in unsorted files**

⭐ If you like this project, don't forget to star the repository! ⭐

</div>
