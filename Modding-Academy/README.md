<div align="center">

# 🎓 BombSquad All-in-One Modding Encyclopedia 🎓
### Complete Guide to Coding Every Type of Mod Across ALL Game Versions!
**Authored by EXTRAX8 — Boom-Vault-BS**

[![Engine](https://shields.io)](#)
[![APIs](https://shields.io)](#)
[![Language](https://shields.io)](#)

</div>

---

## 📌 Table of Contents
1. [API Versions & Code Order (All Updates)](#-1-api-versions--code-order-all-updates)
2. [Core Engine Libraries (`babase`, `bascenev1`, `bauiv1`)](#-2-core-engine-libraries)
3. [How to Code ALL 7 Types of Mods](#-3-how-to-code-all-7-types-of-mods)
   * [Type 1: Gameplay & Power-Up Mods](#type-1-gameplay--power-up-mods-spaz)
   * [Type 2: Custom Bombs & Explosions](#type-2-custom-bombs--explosions)
   * [Type 3: Server Mods & Admin Chat Commands](#type-3-server-mods--admin-chat-commands)
   * [Type 4: Smart AI Bots & Spawners](#type-4-smart-ai-bots--spawners)
   * [Type 5: Custom Mini-Games (Game Activities)](#type-5-custom-mini-games-game-activities)
   * [Type 6: Custom Maps & Arenas](#type-6-custom-maps--arenas)
   * [Type 7: Custom Characters & UI Menus](#type-7-custom-characters--ui-menus)
4. [Legacy Translation Table (`v1.4` ➔ `v1.8+`)](#-4-legacy-translation-table-v14--v18)

---

## 🕰️ 1. API Versions & Code Order (All Updates)

Every `.py` mod in BombSquad **must** start with the exact API header for its target version, followed by imports, the export tag, and your class:

| Game Version | Required First Line | Python | Core Modules |
| :--- | :--- | :--- | :--- |
| **v1.8.x (Latest)** | `# ba_meta require api 9` | Python 3.11+ | `babase`, `bascenev1`, `bauiv1` |
| **v1.7.20 – v1.7.62** | `# ba_meta require api 8` | Python 3.10+ | `babase`, `bascenev1`, `bauiv1` |
| **v1.5.x – v1.7.19** | `# ba_meta require api 6` *(or `7`)* | Python 3.7–3.10 | `ba`, `_ba`, `bastd` |
| **v1.4.148 & Older** | *(No meta tag)* | Python 2.7 | `bs`, `bsInternal`, `bsUtils` |

### Strict Code Order (API 8 & 9):
```python
# 1. API Tag (Must be Line 1)
# ba_meta require api 9

# 2. Imports
from __future__ import annotations
import babase
import bascenev1 as bs
import bauiv1 as bui

# 3. Export Declaration (No blank line between this and the class!)
# ba_meta export babase.Plugin
class MyMod(babase.Plugin):
    def on_app_running(self) -> None:
        bui.screenmessage('Mod Loaded!', color=(0, 1, 0))
```

---

## 📚 2. Core Engine Libraries

* **`babase`**: App lifecycle (`babase.Plugin`), global timers (`babase.apptimer`), and logging.
* **`bascenev1` (`bs`)**: Match physics, timers (`bs.timer`), chat (`bs.chatmessage`), and 3D nodes (`bs.newnode`).
* **`bascenev1lib`**: Built-in actors (`Spaz`, `Bomb`, `PowerupBox`, `Flag`).
* **`bauiv1` (`bui`)**: Menus, windows (`bui.Window`), buttons (`bui.buttonwidget`), and screen messages (`bui.screenmessage`).

---

## 🛠️ 3. How to Code ALL 7 Types of Mods

Here is how to build **every type of mod** in BombSquad (shown in modern **API 9**, adaptable to older versions using Section 4):

---

### Type 1: Gameplay & Power-Up Mods (`Spaz`)
Modifies player abilities (speed, health, infinite gloves, shields, or gravity) by hooking into `Spaz.__init__`.

```python
# ba_meta require api 9
from __future__ import annotations
import babase
from bascenev1lib.actor.spaz import Spaz

# ba_meta export babase.Plugin
class SuperPlayerPlugin(babase.Plugin):
    def on_app_running(self) -> None:
        old_init = Spaz.__init__
        def new_init(self, *args, **kwargs):
            old_init(self, *args, **kwargs)
            self.equip_boxing_gloves()  # Infinite gloves
            self.equip_shields()        # Energy shield
            self.hitpoints_max = 2000   # Double health
            self.hitpoints = 2000
        Spaz.__init__ = new_init
```

---

### Type 2: Custom Bombs & Explosions
Modifies `Bomb.__init__` or triggers custom blast radii, ice freezes, or shockwaves upon explosion.

```python
# ba_meta require api 9
from __future__ import annotations
import babase
import bascenev1 as bs
from bascenev1lib.actor.bomb import Bomb

# ba_meta export babase.Plugin
class MegaBombPlugin(babase.Plugin):
    def on_app_running(self) -> None:
        old_init = Bomb.__init__
        def new_init(self, *args, **kwargs):
            old_init(self, *args, **kwargs)
            # Increase blast radius and make bomb glow red
            self.blast_radius *= 2.0
            if self.node:
                self.node.color = (1.0, 0.1, 0.1)
        Bomb.__init__ = new_init
```

---

### Type 3: Server Mods & Admin Chat Commands
Used for dedicated servers: intercepts chat messages to run commands (`/kick`, `/heal`, `/announce`) and manage players.

```python
# ba_meta require api 9
from __future__ import annotations
import babase
import bascenev1 as bs

# ba_meta export babase.Plugin
class ServerCommandsPlugin(babase.Plugin):
    def on_app_running(self) -> None:
        old_chat = bs.chatmessage
        def custom_chat(msg: str, *args, **kwargs):
            old_chat(msg, *args, **kwargs)
            if msg.strip().lower() == '/healall':
                activity = bs.get_foreground_host_activity()
                if activity:
                    with activity.context:
                        for player in activity.players:
                            if player.actor and player.actor.is_alive():
                                player.actor.hitpoints = player.actor.hitpoints_max
                        bs.broadcastmessage('All players healed by Server!', color=(0, 1, 0))
        bs.chatmessage = custom_chat
```

---

### Type 4: Smart AI Bots & Spawners
Spawns AI fighters (`SpazBotSet` and `BomberBot`, `BrawlerBot`, `TriggerBot`) into the match.

```python
# ba_meta require api 9
from __future__ import annotations
import babase
import bascenev1 as bs
from bascenev1lib.actor.spazbot import SpazBotSet, BrawlerBot

# ba_meta export babase.Plugin
class BotSpawnerPlugin(babase.Plugin):
    def spawn_bot(self) -> None:
        activity = bs.get_foreground_host_activity()
        if activity:
            with activity.context:
                bot_set = SpazBotSet()
                bot_set.spawn_bot(BrawlerBot, pos=(0, 5, 0), spawn_time=1.0)
```

---

### Type 5: Custom Mini-Games (Game Activities)
Creates a brand-new selectable game mode in your playlist using `# ba_meta export bascenev1.GameActivity`.

```python
# ba_meta require api 9
from __future__ import annotations
import bascenev1 as bs
from bascenev1lib.game.deathmatch import DeathMatchGame

# ba_meta export bascenev1.GameActivity
class TurboDeathMatch(DeathMatchGame):
    name = 'Turbo Deathmatch'
    description = 'Fast-paced combat with low gravity!'

    def on_begin(self) -> None:
        super().on_begin()
        # Custom match rule announcement
        bs.broadcastmessage('TURBO MODE STARTED!', color=(1, 0.5, 0))
```

---

### Type 6: Custom Maps & Arenas
Maps require 3D mesh files (`.bob`), textures (`.ktx`), and a Python map definition exported with `# ba_meta export bascenev1.Map`.

```python
# ba_meta require api 9
from __future__ import annotations
import bascenev1 as bs
from bascenev1lib.maps import HockeyStadium

# ba_meta export bascenev1.Map
class CustomNeonArena(HockeyStadium):
    name = 'Neon Stadium'

    def __init__(self) -> None:
        super().__init__()
        # Tint the arena lighting to neon blue
        gnode = bs.getactivity().globalsnode
        gnode.tint = (0.4, 0.6, 1.3)
```

---

### Type 7: Custom Characters & UI Menus
* **Custom Characters:** Registered using `Appearance('CharacterName')` with `.bob` 3D models, `.ktx` textures, and `.ogg` voice files.
* **Custom UI Windows:** Built using `bauiv1.Window` to let players toggle mod settings inside the game menu:

```python
# ba_meta require api 9
from __future__ import annotations
import babase
import bauiv1 as bui

class ModSettingsWindow(bui.Window):
    def __init__(self) -> None:
        super().__init__(root_widget=bui.containerwidget(size=(400, 250), transition='in_scale'))
        bui.textwidget(parent=self._root_widget, text='EXTRAX8 Mod Settings', position=(100, 190))
        bui.buttonwidget(parent=self._root_widget, label='Close', position=(150, 40), size=(100, 40),
                         on_activate_call=lambda: bui.containerwidget(edit=self._root_widget, transition='out_scale'))
```

---

## 🔄 4. Legacy Translation Table (`v1.4` ➔ `v1.8+`)

Use this table to convert any mod type above to older BombSquad versions:

| Element | Classic `v1.4.x` (Python 2.7) | Mid-Gen `v1.5 – v1.7.19` (API 6/7) | Modern `v1.8.x` (API 9) |
| :--- | :--- | :--- | :--- |
| **Plugin Export** | *(Auto-loaded)* | `# ba_meta export ba.Plugin` | `# ba_meta export babase.Plugin` |
| **Game Export** | `bsGetAPIVersion()` | `# ba_meta export ba.GameActivity` | `# ba_meta export bascenev1.GameActivity` |
| **Map Export** | `bs.registerMap(...)` | `# ba_meta export ba.Map` | `# ba_meta export bascenev1.Map` |
| **Player Class** | `bs.PlayerSpaz` | `bastd.actor.playerspaz.PlayerSpaz` | `bascenev1lib.actor.playerspaz.PlayerSpaz` |
| **Bots Module** | `bsSpaz.BotSet` | `bastd.actor.spazbot.SpazBotSet` | `bascenev1lib.actor.spazbot.SpazBotSet` |
| **Timers** | `bs.gameTimer(1000, f)` *(ms)* | `ba.timer(1.0, f)` *(sec)* | `bs.timer(1.0, f)` *(sec)* |

---

<div align="center">

### 💥 Build Your Mod & Share It in Boom-Vault-BS! 💥
[⬅️ Back to Boom-Vault-BS Main Page](../README.md)

</div>
