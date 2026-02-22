# 🔒 MeetingScribe — Secure IAM Meeting Tool

Application 100% locale de transcription et compte rendu de réunions IAM.  
**Aucune donnée ne quitte votre navigateur.**

![Privacy](https://img.shields.io/badge/Privacy-100%25%20Local-brightgreen)
![Cost](https://img.shields.io/badge/Cost-Free-blue)
![AI](https://img.shields.io/badge/AI-WebLLM%20(In--Browser)-purple)

## 🏗️ Architecture de sécurité

```
┌─────────────────────────────────────────┐
│           VOTRE NAVIGATEUR              │
│                                         │
│  ┌──────────┐  ┌──────────┐  ┌───────┐ │
│  │ Interface │  │  WebLLM  │  │ Audio │ │
│  │  React    │  │  (WebGPU)│  │ Local │ │
│  └────┬─────┘  └────┬─────┘  └───┬───┘ │
│       │              │            │     │
│       └──────┬───────┘            │     │
│              ▼                    │     │
│       ┌────────────┐             │     │
│       │ localStorage│◄────────────┘     │
│       │ (chiffré)   │                   │
│       └─────────────┘                   │
└─────────────────────────────────────────┘
         ▲
         │ HTTPS (fichiers statiques uniquement)
         ▼
┌─────────────────┐
│  GitHub Pages   │  ← Ne sert que le HTML/JS
│  (hébergement)  │  ← Aucune donnée reçue
└─────────────────┘
```

| Composant | Où ça tourne | Données partagées |
|---|---|---|
| Interface web | Navigateur | ❌ Aucune |
| Stockage | localStorage | ❌ Aucune |
| IA (CR) | WebLLM / WebGPU | ❌ Aucune |
| Enregistrement audio | MediaRecorder | ❌ Aucune |
| Transcription manuelle | Navigateur | ❌ Aucune |
| Transcription vocale | Web Speech API | ⚠️ Opt-in (Google) |
| Hébergement | GitHub Pages | ❌ Fichiers statiques |

## 🚀 Déploiement sur GitHub Pages

### Option A : Via l'interface GitHub (simple)

1. Créez un nouveau repository sur github.com
2. Uploadez les fichiers (`index.html`, `README.md`, `.nojekyll`)
3. Settings → Pages → Source: **main** / **/ (root)** → Save
4. Attendez 2 min → votre app est sur `https://VOTRE_USER.github.io/REPO_NAME/`

### Option B : Via Git (recommandé)

```bash
cd meetingscribe
git init
git add .
git commit -m "🎙️ MeetingScribe - Secure IAM Meeting Tool"
git branch -M main
git remote add origin https://github.com/VOTRE_USER/meetingscribe.git
git push -u origin main
```

Puis activez GitHub Pages dans Settings → Pages.

## 💻 Prérequis

### Navigateur compatible WebGPU
- ✅ Chrome 113+ (recommandé)
- ✅ Edge 113+
- ✅ Chrome Android 121+ (mobile)
- ⚠️ Safari : support limité
- ❌ Firefox : pas encore supporté

### Premier lancement
Au premier accès, le modèle IA (~700 MB - 2 GB) est **téléchargé et mis en cache** dans le navigateur. Les lancements suivants sont instantanés.

### Modèles disponibles

| Modèle | Taille | Qualité FR | RAM requise |
|---|---|---|---|
| Llama 3.2 1B | ~700 MB | ⭐⭐ | 4 GB |
| Qwen 2.5 1.5B | ~1 GB | ⭐⭐⭐ | 6 GB |
| Phi 3.5 Mini | ~2.3 GB | ⭐⭐⭐⭐ | 8 GB |

## 📱 Usage mobile

L'application fonctionne sur mobile (Chrome Android 121+) :
- Enregistrement audio local ✅
- Transcription manuelle ✅
- Génération IA dans le navigateur ✅
- Export des CR ✅

> ⚠️ Sur mobile, privilégiez le modèle Llama 3.2 1B (plus léger).
> La génération prend ~30-60 secondes selon l'appareil.

## 🔐 Sécurité

- **Aucun serveur backend** — tout tourne dans le navigateur
- **Aucune API externe** — l'IA est embarquée via WebAssembly/WebGPU
- **Aucune télémétrie** — pas de tracking, pas d'analytics
- **GitHub Pages** ne sert que les fichiers statiques HTML/JS
- **Web Speech API** est désactivée par défaut (opt-in avec avertissement)

## 📄 Licence

MIT — Usage libre, y compris commercial.
