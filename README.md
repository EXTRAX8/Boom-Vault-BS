<div align="center">

# 💣 Boom-Vault-BS 💣
**The Ultimate & Organized BombSquad Modding Vault for All Versions**

[![Game](https://shields.io)](#)
[![Language](https://shields.io)](#)
[![Versions](https://shields.io)](#)

[About](#-about) • [Structure](#-structure) • [Compatibility](#-compatibility) • [Installation](#-installation) • [FAQ](#-faq) • [Contributing](#-contributing)

</div>

---

## 📖 About

**Boom-Vault-BS** is a clean, organized archive of **BombSquad** scripts, custom maps, characters, and mini-games. Every mod is strictly sorted by its compatible game version and API to prevent crashes and script errors.

---

## 📂 Structure

```text
📦 Boom-Vault-BS
 ┣ 📂 v1.8.x-Latest/        # Latest Engine (Ballistica API 9)
 ┃ ┣ 📂 Scripts-Plugins/    # Gameplay mods & custom bombs (.py)
 ┃ ┣ 📂 Custom-Maps/        # New arenas & textures (.py, .bob, .ktx)
 ┃ ┣ 📂 Characters/         # Custom fighters & voices (.py, .cob)
 ┃ ┣ 📂 Mini-Games/         # New game modes (.py)
 ┃ ┗ 📂 Server-Tools/       # Admin commands & lobby tools (.py)
 ┃
 ┣ 📂 v1.7.x/               # Modern Engine (Ballistica API 8)
 ┣ 📂 v1.6.x/               # Mid-gen releases (API 7)
 ┣ 📂 v1.5.x/               # Early modern releases
 ┗ 📂 Classic-1.4.x/        # Legacy builds (1.4.148 & older)
```

---

## 📊 Compatibility

Check your game version on the main menu before downloading:

| Folder | Game Versions | Engine / API | Status |
| :--- | :--- | :--- | :--- |
| **`v1.8.x-Latest`** | `1.8.0` ➔ `Latest` | Python 3.11+ (API 9) | 🟢 Active |
| **`v1.7.x`** | `1.7.0` ➔ `1.7.62` | Python 3.10+ (API 8) | 🟢 Supported |
| **`v1.6.x`** | `1.6.0` ➔ `1.6.11` | Python 3.8 (API 7) | 🟡 Stable |
| **`v1.5.x`** | `1.5.0` ➔ `1.5.29` | Python 3.7 | 🟡 Stable |
| **`Classic-1.4.x`** | `1.4.148` & older | Python 2.7 | 🟠 Legacy |

---

## 🚀 Installation

### 📱 Android (Mobile / TV)
1. Download the mod files matching your game version.
2. Open BombSquad ➔ **Settings** ➔ **Advanced** ➔ **Show Mods Folder**.
3. Move the downloaded files into the `mods` folder.
4. Restart the game. *(For `v1.7+` & `v1.8+`, enable the mod inside **Settings ➔ Advanced ➔ Plugins**)*.

### 💻 PC (Windows / macOS / Linux)
1. Download the mod files matching your game version.
2. Open BombSquad ➔ **Settings** ➔ **Advanced** ➔ **Show Mods Folder**.
3. Paste the files into the opened directory and restart the game.

---

## 🛠️ FAQ

* **Game crashes on startup?** Remove the last added file from your `mods` folder; it is likely incompatible with your version or API.
* **Can't access `Android/data` on Android 11+?** Use the in-game **Show Mods Folder** button or a file manager that supports data access.
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

### ⭐ Star Boom-Vault-BS if you find it useful! ⭐

</div>
