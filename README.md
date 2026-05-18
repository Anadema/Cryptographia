# 🔐 Cryptographia — Web Edition

> **Un voyage interactif à travers 2500 ans d'histoire de la cryptographie.**

Cryptographia est un jeu web éducatif composé de **8 énigmes cryptographiques** progressives, allant de l'Antiquité à l'ère numérique. Chaque challenge plonge le joueur dans une époque et un système de chiffrement réel, avec un design immersif.

<img width="648" height="565" alt="image" src="https://github.com/user-attachments/assets/954ca4c5-7a94-4c40-8633-46173ebaa09c" />


## 🎮 Comment jouer

1. Ouvrez le site : **[anadema.github.io/cryptographia](https://anadema.github.io/Cryptographia/)**
2. Choisissez un challenge parmi les 8 disponibles
3. Lisez l'**📜 Histoire** du code (des indices sont cachés dans le texte !)
4. Résolvez l'énigme pour obtenir un **flag** secret
5. Collectez les 8 flags pour devenir **Maître des Codes**

## 🏛️ Les 8 Challenges

| # | Époque | Code | Concept |
|---|--------|------|---------|
| I | −500 av. J.-C. | **La Scytale** | Transposition par colonnes (Sparte) |
| II | −50 av. J.-C. | **Le Chiffre de César** | Substitution par décalage (Rome) |
| III | −150 av. J.-C. | **Le Carré de Polybe** | Coordonnées dans une grille (Grèce) |
| IV | 1586 | **Le Chiffre de Vigenère** | Chiffrement polyalphabétique (France) |
| V | 1844 | **Le Rail Fence** | Transposition en zigzag + Code Morse (USA) |
| VI | 1854 | **Le Chiffre de Playfair** | Grille + alphabet grec (Royaume-Uni) |
| VII | 1940 | **Enigma** | Cassage de code à rotors (Bletchley Park) |
| VIII | 2026 | **Stéganographie** | Message caché dans une image (Internet) |

## 🎯 Public cible

Conçu pour des **stagiaires non-techniques** dans un contexte de sensibilisation à la cybersécurité. Les challenges sont accessibles sans connaissances préalables en informatique — chaque énigme enseigne un concept historique de cryptographie tout en testant la logique et la déduction.

## ✨ Fonctionnalités

- **📜 Popups historiques** avec miniatures d'époque et indices subtils
- **🏆 Système de flags** : chaque challenge résolu révèle un trésor historique
- **🔗 Session encodée dans l'URL** : progression sauvegardée et partageable (base64 + XOR)
- **📱 Mobile-first** : optimisé pour iPhone/Android
- **🔗 Liens d'aide** : décodeurs en ligne (dcode.fr, hexed.it, rapidtables)
- **🔒 Sécurité** : sanitization des inputs, pas de localStorage, pas d'eval

## 🚀 Déploiement

### GitHub Pages (automatique)

1. Forkez ou poussez ce repo sur votre compte GitHub
2. Allez dans **Settings → Pages → Source → GitHub Actions**
3. Le workflow `.github/workflows/deploy.yml` déploie automatiquement à chaque push sur `main`
4. Votre site sera disponible à `https://votre-username.github.io/cryptographia`

### Déploiement local

Aucune dépendance, aucun build. Ouvrez simplement `index.html` dans un navigateur.

```bash
# ou servez-le avec un serveur local
python3 -m http.server 8000
# → http://localhost:8000
```

## 🏗️ Architecture technique

- **HTML unique** : tout le code dans un seul fichier `index.html`
- **React 18** via CDN (unpkg)
- **Tailwind CSS** via CDN
- **Babel standalone** pour la compilation JSX
- **Google Fonts** : Orbitron, Rajdhani, Share Tech Mono
- **Canvas API** pour la génération d'images (stéganographie)
- **Aucune dépendance serveur** : 100% statique

## 📁 Structure du repo

```
cryptographia/
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions pour Pages
├── .nojekyll               # Bypass Jekyll
├── index.html              # Application complète
├── README.md               # Ce fichier
└── LICENSE                 # MIT License
```

## 📜 Licence

Apache 2.0 — Libre d'utilisation, modification et distribution.

---

*Cryptographia · MMXXVI · De Sparte à l'ère numérique*
