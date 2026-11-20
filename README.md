<div align="center">

# 💣 BlastCore Mods 💣
**The Ultimate & Organized BombSquad Modding Vault for All Versions**

[![Game](https://shields.io)](#)
[![Language](https://shields.io)](#)
[![Versions](https://shields.io)](#)

[About](#-about) • [Structure](#-structure) • [Compatibility](#-compatibility) • [Installation](#-installation) • [FAQ](#-faq) • [Contributing](#-contributing)

</div>

---

## 📖 About

**BlastCore Mods** is a clean, organized archive of **BombSquad** scripts, custom maps, characters, and mini-games. Every mod is strictly sorted by its compatible game version to prevent crashes and script errors.

---

## 📂 Structure

```text
📦 BlastCore-Mods
 ┣ 📂 v1.7.x-Latest/        # Modern Engine (Ballistica API)
 ┃ ┣ 📂 Scripts-Plugins/    # Gameplay mods & custom bombs (.py)
 ┃ ┣ 📂 Custom-Maps/        # New arenas & textures (.py, .bob, .ktx)
 ┃ ┣ 📂 Characters/         # Custom fighters & voices (.py, .cob)
 ┃ ┣ 📂 Mini-Games/         # New game modes (.py)
 ┃ ┗ 📂 Server-Tools/       # Admin commands & lobby tools (.py)
 ┃
 ┣ 📂 v1.6.x/               # Mid-gen releases
 ┣ 📂 v1.5.x/               # Early modern releases
 ┗ 📂 Classic-1.4.x/        # Legacy builds (1.4.148 & older)
```

---

## 📊 Compatibility

Check your game version on the main menu before downloading:

| Folder | Game Versions | Python Engine | Status |
| :--- | :--- | :--- | :--- |
| **`v1.7.x-Latest`** | `1.7.0` ➔ `Latest` | Python 3.10+ | 🟢 Active |
| **`v1.6.x`** | `1.6.0` ➔ `1.6.11` | Python 3.8 | 🟡 Stable |
| **`v1.5.x`** | `1.5.0` ➔ `1.5.29` | Python 3.7 | 🟡 Stable |
| **`Classic-1.4.x`** | `1.4.148` & older | Python 2.7 | 🟠 Legacy |

---

## 🚀 Installation

### 📱 Android
1. Download the mod files matching your game version.
2. Open BombSquad ➔ **Settings** ➔ **Advanced** ➔ **Show Mods Folder**.
3. Move the downloaded files into the `mods` folder.
4. Restart the game. *(For `v1.7+`, enable the mod inside **Settings ➔ Advanced ➔ Plugins**)*.

### 💻 PC (Windows / macOS / Linux)
1. Download the mod files matching your game version.
2. Open BombSquad ➔ **Settings** ➔ **Advanced** ➔ **Show Mods Folder**.
3. Paste the files into the opened directory and restart the game.

---

## 🛠️ FAQ

* **Game crashes on startup?** Remove the last added file from your `mods` folder; it is likely incompatible with your version.
* **Can't access `Android/data` on Android 11+?** Use the in-game **Show Mods Folder** button or **ZArchiver + Shizuku**.
* **Do mods work in multiplayer?** Server scripts and mini-games work for everyone in your lobby; custom skins/maps require all players to have the files.

---

## 🤝 Contributing

1. **Fork** this repository.
2. Upload your mod to the correct `<Version>/<Category>/` folder with a clear name.
3. Open a **Pull Request** with a short description of the mod.

---

## ⚠️ Disclaimer

This is an independent community archive and is not affiliated with **Froemling Games**. All mods belong to their respective creators.

<div align="center">

### ⭐ Star this repository if you find it useful! ⭐

</div>
