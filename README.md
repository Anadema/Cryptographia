# 🔐 Cryptographia — Web Edition

> **An interactive journey through 3,500 years of cryptography history.**<bR><br>

Cryptographia is an educational web game featuring **16 progressive cryptographic puzzles**, spanning from ancient Hebrew traditions to the digital age. Each challenge immerses the player in a real historical era and encryption system, with an immersive cyberpunk design and full **bilingual support (🇫🇷 French / 🇺🇸 English)**.

<img width="648" height="565" alt="Cryptographia preview" src="https://github.com/user-attachments/assets/954ca4c5-7a94-4c40-8633-46173ebaa09c" />

## 🎮 How to Play

1. Open the site: **[anadema.github.io/Cryptographia](https://anadema.github.io/Cryptographia/)**
2. Choose your language using the 🇫🇷/🇺🇸 selector in the top-right corner
3. Pick a challenge from the 16 available (in chronological order)
4. Read the **📜 History** of the code (hints are hidden in the text!)
5. Solve the puzzle to obtain a secret **flag**
6. Collect all 16 flags to become **Code Master**

## 🎮 Hard mode

See **[Hacker Guide](https://github.com/Anadema/Cryptographia/blob/main/Hacker_guide.md)**

## 🏛️ The 16 Challenges

| # | Era | Cipher | Concept 
|---|-----|--------|---------|
| I | 1500 BC | **Atbash** ↔ | Alphabet inversion (A↔Z, B↔Y...) 
| II | 500 BC | **Scytale** 𓂀 | Column transposition (Sparta) 
| III | 150 BC | **Polybius Square** ⊞ | Coordinates in a 5×5 grid (Greece) 
| IV | 50 BC | **Caesar Cipher** ♜ | Letter shift substitution (Rome) 
| V | 1586 | **Vigenère Cipher** ⚜ | Polyalphabetic encryption (France) 
| VI | 1844 | **Rail Fence** ⚡ | Zigzag transposition + Morse code (USA) 
| VII | 1854 | **Playfair Cipher** ♛ | 5×5 grid + Greek alphabet coordinates (UK) 
| VIII | 1917 | **XOR Cipher** ⊕ | Bitwise XOR operation (Cryptography)
| IX | 1940 | **Enigma** ⚙ | Rotor-based code breaking (Bletchley Park) 
| X | 1960 | **Hexadecimal** #️⃣ | Base 16 encoding (Computing) 
| XI | 1963 | **Binary Code** 💾 | ASCII / 8-bit encoding (Computing) 
| XII | 1980 | **ROT13** 🔄 | Caesar cipher with 13-position shift (Internet/Usenet) 
| XIII | 1985 | **Steganography** ◉ | Message hidden in image bytes (Digital era)
| XIV | 1987 | **Base64** 📧 | Binary-to-text encoding (Web/MIME)
| XV | 1991 | **MD5 Hash** 🔒 | One-way fingerprint cracking with rainbow tables
| XVI | 1994 | **QR Code** 📱 | 2D barcode invented by Denso Wave (Japan)

### 📚 Challenge Details

#### I — Atbash (1500 BC) 🇮🇱
One of the oldest known ciphers from Hebrew tradition. The principle is radically simple: reverse the alphabet. A↔Z, B↔Y, C↔X... Mentioned in the Bible's Book of Jeremiah where "Sheshakh" is Atbash for "Babel".

#### II — Scytale (500 BC) 🇬🇷
Spartan generals wrapped a leather strip around a cylindrical rod called a scytale. The message was written horizontally, then the strip was unwound. Without the right rod diameter, the message was unreadable. Used famously by King Leonidas.

#### III — Polybius Square (150 BC) 🇬🇷
Greek historian Polybius arranged 25 letters in a 5×5 grid. Each letter is identified by its (row, column) position. Used with torches on hills for long-distance communication, and later by prisoners tapping on cell walls.

#### IV — Caesar Cipher (50 BC) 🇮🇹
Julius Caesar's deceptively simple system: shift each letter by a fixed number of positions. Reported by Suetonius. The famous "VENI VIDI VICI" message from his Gallic conquest is encoded with a shift of 3 (III in Roman numerals).

#### V — Vigenère Cipher (1586) 🇫🇷
Blaise de Vigenère's polyalphabetic system. Unlike Caesar (fixed shift), Vigenère uses a secret keyword that modifies each letter differently. Nicknamed "**le chiffre indéchiffrable**" for 300 years until Babbage and Kasiski cracked it in the 19th century.

#### VI — Rail Fence + Morse (1844) 🇺🇸
Letters are written in zigzag across multiple "rails", then read row by row. Combined with Samuel Morse's revolutionary code (dots and dashes) which enabled instant long-distance communication for the first time in history.

#### VII — Playfair Cipher (1854) 🇬🇧
Charles Wheatstone's 5×5 grid system, promoted by Lord Playfair. Used by the British Army during the Boer War and WWI. This challenge adds a twist: positions are encoded using **Greek alphabet letters** (α=0, β=1, γ=2, δ=3, ε=4).

#### VIII — XOR Cipher (1917) 🔢
The fundamental operation of modern cryptography. XOR compares two bits: same → 0, different → 1. Self-inverse: applying XOR twice with the same key restores the original. Foundation of the unbreakable "one-time pad" encryption.

#### IX — Enigma (1940) ⚙️
Nazi Germany's electromechanical rotor machine with 158 quintillion combinations. Cracked at Bletchley Park by Alan Turing's team using the "Bombe" machine. Estimated to have shortened WWII by 2 to 4 years.

#### X — Hexadecimal (1960) #️⃣
Base 16 system using digits 0-9 and letters A-F. Two hex digits = one byte = one ASCII character. The compact language of computers, used in memory addresses, web colors (#FF0000), and forensic analysis.

#### XI — Binary Code (1963) 💾
ASCII standard adopted in 1963: every character receives a unique number (0-127) encoded in 8 bits (one byte). The foundation of all modern computing — every file, message, and image is ultimately a sequence of 0s and 1s.

#### XII — ROT13 (1980) 🔄
A Caesar cipher with a fixed shift of 13. Its unique property: applying it twice returns the original text (because 13 × 2 = 26 = alphabet length). Popularized by Usenet for hiding spoilers and offensive content.

#### XIII — Steganography (1985) ◉
While the concept dates back to antiquity (Herodotus reported messages tattooed on slaves' scalps), modern digital steganography was born in 1985 with **Gustavus Simmons**' "Prisoners' Problem". The challenge: hide text in the raw bytes of a PNG image, invisible to the eye but discoverable with a hex editor.

#### XIV — Base64 (1987) 📧
Not encryption but an encoding scheme. Transforms binary data into 64 "safe" text characters (A-Z, a-z, 0-9, +, /). Invented for the MIME email standard to send binary attachments through text-only protocols.

#### XV — MD5 Hash (1991) 🔐
Ronald Rivest's 128-bit hash function. One-way: you can't reverse it. But "rainbow tables" allow brute-forcing common passwords. This challenge simulates an attacker cracking a hash from a candidate word list — illustrating why MD5 is now considered broken.

#### XVI — QR Code (1994) 📱
Invented by Masahiro Hara at **Denso Wave** (Toyota subsidiary) for automotive parts tracking. Stores data in two dimensions with error correction (readable even when 30% damaged). Today ubiquitous and used in modern steganography.

## 🎯 Target Audience

Designed for **non-technical trainees** in cybersecurity awareness contexts. Challenges are accessible without prior computer knowledge — each puzzle teaches a historical cryptography concept while testing logic and deduction. Perfect for:

- 🏢 Corporate cybersecurity training sessions
- 🎓 Educational workshops on cryptography history
- 🎮 Personal entertainment for puzzle enthusiasts
- 🧠 Logic and deduction practice

## ✨ Features

- **🌍 Full bilingual support** — Switch between French 🇫🇷 and English 🇺🇸 anytime
- **📜 History popups** with era miniatures and subtle in-text hints
- **🏆 Flag collection system** — each solved challenge reveals a historical treasure
- **🔗 URL-encoded session** — progress is saved and shareable (Base64 + XOR encoding)
- **📱 Mobile-first design** — optimized for iPhone/Android with responsive layouts
- **🎨 Cyberpunk aesthetics** — neon glows, glassmorphism, animated background symbols
- **🔗 Helper links** — online decoders (dcode.fr, hexed.it, rapidtables, base64decode, etc.)
- **🔒 Security** — input sanitization, no localStorage, no eval(), no external API for game logic
- **♿ Accessibility** — interactive widgets (Enigma rotors, column selector, etc.) for hands-on learning

## 🚀 Deployment

### GitHub Pages (automatic)

1. Fork or push this repo to your GitHub account
2. Go to **Settings → Pages → Source → GitHub Actions**
3. The `.github/workflows/deploy.yml` workflow auto-deploys on every push to `main`
4. Your site will be available at `https://your-username.github.io/Cryptographia`

### Local deployment

No dependencies, no build step. Just open `index.html` in a browser.

```bash
# Or serve it with a local server
python3 -m http.server 8000
# → http://localhost:8000
```

## 🏗️ Technical Architecture

- **Single HTML file** — all code in one `index.html`
- **React 18** via CDN (unpkg)
- **Tailwind CSS** via CDN
- **Babel standalone** for in-browser JSX compilation
- **React Context API** for bilingual support (LangContext)
- **Google Fonts** — Orbitron, Rajdhani, Share Tech Mono
- **Canvas API** for image generation (steganography challenge)
- **Wikipedia API** for fetching historical images dynamically
- **Zero server dependencies** — 100% static, fully client-side

## 📁 Repository Structure

```
cryptographia/
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions for Pages
├── .nojekyll               # Bypass Jekyll processing
├── index.html              # Complete application (all 16 challenges)
├── README.md               # This file
└── LICENSE                 # Apache 2.0 License
```

## 🌐 Internationalization

The application supports **full bilingual rendering** (French/English) through:

- React `LangContext` provider wrapping all views
- Translation tables for UI elements (`T.en` dictionary)
- Per-challenge `en:{}` objects with `nm`, `cv`, `fm`, `hi`, `lore` fields
- Helper functions (`tr`, `cn`, `cc`, `cf`, `ch_`, `cl`) for clean conditional rendering
- Persistent language selection during the session

## 🎨 Design Tokens

Each challenge has a unique color identity:

| Color | Challenges |
|-------|-----------|
| 🟣 Indigo (#6366f1) | Atbash |
| 🔵 Cyan (#00f0ff) | Scytale |
| 🟢 Green (#00ff41) | Polybius |
| 🩷 Pink (#ff2d95) | Caesar |
| 🟡 Gold (#ffd700) | Vigenère |
| 🟠 Orange (#ff6b00) | Rail Fence |
| 🟣 Purple (#a855f7) | Playfair |
| 🔵 Blue (#3b82f6) | XOR |
| 🔴 Red (#ef4444) | Enigma |
| 🟣 Violet (#8b5cf6) | Hexadecimal |
| 🟢 Emerald (#10b981) | Binary |
| 🟡 Amber (#f59e0b) | ROT13 |
| 🔷 Cyan (#06b6d4) | Steganography |
| 🩷 Pink (#ec4899) | Base64 |
| 🔴 Dark Red (#dc2626) | MD5 |
| 🟢 Teal (#14b8a6) | QR Code |

## 🐛 Known Limitations

- The Enigma challenge uses simplified single-rotor logic (not the full historical Enigma)
- Wikipedia images require an internet connection on first load
- The QR Code challenge requires either a mobile device or an online QR reader

## 📜 License

**Apache 2.0** — Free for use, modification, and distribution.

## 🙏 Credits

- Historical content: research from Wikipedia, dcode.fr, and academic sources
- Design inspiration: cyberpunk aesthetics, retro-futurism
- Cryptographic algorithms: implementations following standard specifications
- Wikipedia API for historical imagery
- QR Code generation via api.qrserver.com

---

*Cryptographia · MMXXVI · From Hebrew traditions to the digital age*

**🇫🇷 [Version française disponible dans l'application — cliquez sur 🇫🇷]**
