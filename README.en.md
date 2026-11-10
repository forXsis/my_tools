[🇷🇺 Читать на русском](./README.md)

# Termulin ❯

**Termulin** is an aesthetic, fast, and minimalist theme for Windows Terminal and PowerShell 7. Inspired by Linux environments and r/unixporn aesthetics, it transforms the standard Windows console into a modern, stylish tool for work.

This project is crafted with respect for the community and a love for code.

## ✨ Features

- 🚀 **Instant Launch**: System information (CPU, RAM, OS) is cached, so the terminal opens in milliseconds.
- 🎨 **4 Preset Themes**:
  - `TRL Snow` — Graphite tones (perfect for mountain backgrounds).
  - `TRL Angel` — Marble monochrome (for minimalist black-and-white backgrounds).
  - `TRL Sakura` — Ash-pink (soft pastel tones).
  - `Custom` — Create your own theme from scratch!
- 🌌 **Aesthetic Background**: Uses local images with an acrylic glass effect (transparency).
- 💻 **Smart Prompt**: Two-line prompt with clock, current folder, and PowerShell version.
- 🎬 **Boot Animation**: A separate shortcut launches the terminal with a simulated Linux kernel boot (log lines, 3D ASCII art).
- 🛠️ **Universal Installer**: `Setup.bat` automatically finds PowerShell 7 (even the Microsoft Store version), installs it if necessary, and configures everything.

---

## ⚙️ Requirements

- **Windows 10 or Windows 11**.
- **Windows Terminal** (Microsoft Store version recommended).
- **PowerShell 7** (`Setup.bat` will automatically install it via `winget` if missing).
- **Liberation Mono font** (recommended for the best look, but if not installed, the terminal will fall back to Cascadia Mono).

---

## 🚀 Installation (Step-by-step for beginners)

1. **Download the Project**
   - Click the green `Code` button at the top of this page and select `Download ZIP`.
   - Extract the archive to any convenient folder (e.g., `C:\Tools\Termulin`).

2. **Run the Installer**
   - Open the project folder and double-click **`Setup.bat`**.
   - If Windows shows a blue SmartScreen warning saying "Windows protected your PC," click **"More info"** -> **"Run anyway"** (this is normal for `.bat` files downloaded from the internet).

3. **Follow the Console Instructions**
   - The script will check for PowerShell 7. If it's not found, it will start installing via `winget`.
   - You will be prompted with a theme menu (enter a number from 1 to 4 and press `Enter`).
   - If you choose `4` (Custom theme), the script will ask for the image path, colors (in HEX format), and prompt template step-by-step.

4. **Done!**
   - Shortcuts will appear on your desktop.
   - Open a new terminal (or use the shortcut) and enjoy.

---

## 🗑️ How to Uninstall

If you want to completely remove the theme and revert your terminal settings to default:
1. Open Command Prompt (`cmd`) or PowerShell.
2. Navigate to the project folder: `cd C:\Tools\Termulin`.
3. Run the following command:
   ```cmd
   Setup.bat -Uninstall
   ```
4. The script will remove all created profiles, color schemes, and shortcuts. Restart Windows Terminal for the changes to take effect.

---

## 📂 What does each file do? (For advanced users)

| File | Purpose | What you can change |
| :--- | :--- | :--- |
| **`Setup.bat`** | Universal launcher. Finds PowerShell 7 (including the Store version), installs it if needed, and runs `Install.ps1` or `Uninstall.ps1`. | Shortcut name in `title`, `pwsh` search logic. |
| **`Install.ps1`** | Main installer. Creates profiles in Windows Terminal, configures colors, creates desktop shortcuts, and adds the module to your PowerShell profile. | Color schemes (HEX codes), background opacity (`opacity`), image paths in the `background/` folder. |
| **`Uninstall.ps1`** | Completely removes all traces of Termulin from Windows Terminal and your PowerShell profile. | List of shortcuts to delete. |
| **`Boot.ps1`** | Boot animation script. Outputs logs, 3D art, and launches the console. | Log text, ASCII art, delay speed (`Sleep-Ms`). |
| **`Theme.psd1`** | PowerShell module manifest (module description). | Author, version, description. |
| **`Theme.psm1`** | The theme engine. Draws the banner (info box) and prompt (input prompt). | Border colors, string length calculation logic (for Cyrillic), functions. |
| **`theme.json`** | Banner and prompt configuration. | Banner title (`title`), fields (`fields`), box width (`width`). |
| **`background/`** | Folder with background images for themes. | You can replace images with your own (keeping the filenames) to change the background. |

---

## 🎨 How to create your own theme (Custom)

If you selected option `4` during installation, the script will create a personal profile.

- **Colors**: Enter them in HEX format (e.g., `#1A1B26` for background and `#C0CAF5` for text). You can find beautiful color combinations on [coolors.co](https://coolors.co/).
- **Prompt Template**: In `theme.json` (or `Theme.psm1`), you can use the following variables:
  - `{time}` — Current time (HH:MM:SS)
  - `{folder}` — Current folder name (e.g., `Termulin`)
  - `{pwsh}` — PowerShell version (e.g., `v7`)
  - `{date}` — Current date
  - `{username}` — Username
  - `{hostname}` — Computer name

Example of a beautiful prompt:
```json
"prompt": "╭─[{time}]─[{folder}]─[{pwsh}]\n╰─❯ "
```

---

## ❓ Common Issues and Solutions

**1. `Setup.bat` outputs garbled characters (mojibake)**
- **Solution:** Make sure you are running the file from File Explorer (by double-clicking). The script contains `chcp 65001`, which enables UTF-8. If you run it from an old terminal, it may ignore the encoding.

**2. Error `0x80070057` when opening the terminal**
- **Cause:** A file is missing (such as a background image), or the path to `pwsh.exe` is constructed incorrectly, or the file is missing entirely.
- **Solution:** Open the folder where all files were extracted. Check the integrity of the structure and make sure the path to `pwsh.exe` is correct (usually, it's installed at `C:\Program Files\WindowsApps\Microsoft.PowerShell_7.6.9.0_x64_...`).

**3. Banner borders are misaligned (the right border shifts)**
- **Cause:** Windows Terminal calculates the width of Cyrillic characters and emojis differently.
- **Solution:** We added a compensating space at the end of each line. If the border still shifts, you can reduce the banner width in `theme.json` (`"width": 60`).

**4. The script cannot find PowerShell 7**
- **Solution:** Download and install PowerShell 7 manually from the [official website](https://aka.ms/powershell). Then run `Setup.bat` again.

**5. How to revert to the old console?**
- **Solution:** Run `Setup.bat -Uninstall`. If you also want to disable the theme in your PowerShell profile, open `$PROFILE` and delete the block `# >>> TRL-Theme >>> ... # <<< TRL-Theme <<<`.

---

## 📄 License

This project is distributed under the **MIT License**. You are free to use, modify, and distribute it, provided you include a link back to this repository and retain the copyright notice.

*Crafted with ❤️ and respect for the community.*
