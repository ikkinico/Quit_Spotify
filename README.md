# Comment s'échapper de Spotify 🎵

> Payer un abonnement pour écouter de la musique, sans jamais pouvoir la posséder ?

Défions le modèle des plateformes de streaming en reprenant le contrôle de sa musique.
Découvrons comment héberger sa bibliothèque musicale chez soi, l'enrichir avec des sources
externes, et y accéder depuis n'importe où, comme avec un abonnement de streaming.
En sortant de cette présentation, vous saurez construire votre propre alternative :
souveraine, portable, et sans abonnement imposé.

Ce dépôt contient la stack Docker Compose utilisée pendant la conférence, les slides
et les liens cités.

## Replay

🎬 _Le lien vers la vidéo sera ajouté ici après la première session._

## Contenu du dépôt

```
├── docker-compose.yml           # Tailscale + Docktail + Navidrome + Audiobookshelf
├── .env.example                 # Variables à personnaliser
└── slides/                      # Le diaporama
```

## La stack

| Service                                           | Rôle                                                                             | Accès                                          |
|---------------------------------------------------|----------------------------------------------------------------------------------|------------------------------------------------|
| [Tailscale](https://tailscale.com/)               | VPN mesh WireGuard : expose les services sur votre tailnet sans ouvrir de port   | `https://console.tailscale.com/admin/machines` |
| [Navidrome](https://www.navidrome.org/)           | Serveur de musique, compatible [OpenSubsonic](https://opensubsonic.netlify.app/) | `https://navidrome.your-tailnet.ts.net`        |
| [Audiobookshelf](https://www.audiobookshelf.org/) | Serveur de livres audio (et podcasts)                                            | `https://audiobookshelf.your-tailnet.ts.net`   |

## Prérequis

- Une machine qui tourne à la maison (NAS, Raspberry Pi, vieux PC, VM…) avec Docker et Docker Compose.
- Un compte [Tailscale](https://login.tailscale.com/) (gratuit jusqu'à 3 utilisateurs / 100 appareils).
- La configuration de docktail dans Tailscale : [Installation](https://docktail.org/docs/#installation)
- Des fichiers audio à vous : FLAC/MP3 pour la musique, MP3/M4B pour les livres audio.

## Installation

1. Cloner le dépôt (idéalement dans le dossier des stacks de Dockge) :

   ```bash
   git clone https://github.com/ikkinico/Quit_Spotify.git /opt/stacks/quit-spotify
   cd /opt/stacks/quit-spotify
   ```

2. Créer la configuration :

   ```bash
   cp .env.example .env
   ```

- Renseigner `TS_AUTHKEY` (console Tailscale > *Settings* > *Keys* > *Generate auth key*,
- Renseigner `TAILSCALE_OAUTH_CLIENT_ID` (console Tailscale > *Settings* > *Trust credentials* > *Credential*,
- Renseigner `TAILSCALE_OAUTH_CLIENT_SECRET` (console Tailscale > *Settings* > *Trust credentials* > *Credential*)

4. Démarrer :

   ```bash
   docker compose up -d
   ```

5. Depuis n'importe quel appareil connecté au tailnet :
   - Navidrome : <https://navidrome.your-tailnet.ts.net> (créer le compte admin au premier lancement)
   - Audiobookshelf : <https://audiobookshelf.your-tailnet.ts.net>

## Les apps
Toutes les apps compatibles OpenSubsonic fonctionnent : <https://www.navidrome.org/apps/>

| Plateforme | Musique (Navidrome)                                            | Livres audio (Audiobookshelf)                                                                                                             | Podcasts                                     |
|------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| Android    | [Symfonium](https://symfonium.app/)                            | [Symfonium](https://symfonium.app/) ou l'app [Audiobookshelf](https://play.google.com/store/apps/details?id=com.audiobookshelf.app&hl=fr) | [AntennaPod](https://antennapod.org/)        |
| iOS        | [Arpeggi](hhttps://apps.apple.com/fr/app/arpeggi/id6503619183) | [AudioBooth](https://apps.apple.com/fr/app/audiobooth-audiobooks-player/id6753017503)                                                     | Apple Podcasts                               |
| PC / Mac   | [Feishin](https://github.com/jeffvli/feishin)                  | Interface web                                                                                                                             | [radio-podcast.fr](https://radio-podcast.fr) |

## Aller plus loin
- [Qobuz](https://www.qobuz.com/) — acheter sa musique en Hi-Res, sans DRM
- [Vivlio](https://shop.vivlio.com/) — acheter ses livres audio sans DRM
- [Headscale](https://github.com/juanfont/headscale) — alternative libre au serveur de coordination Tailscale
