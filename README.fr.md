# TW-Tiny-Bootstrap

[English](README.md) · **Français**

![Status](https://img.shields.io/badge/status-experimental-orange)
![TiddlyWiki](https://img.shields.io/badge/TiddlyWiki-%E2%89%A55.3.5-blue)

Un plugin TiddlyWiki qui regroupe les classes CSS utilitaires et de composants de Bootstrap 5.3.3 — sans JavaScript, du style pur par `class="..."`. Il se désactive de lui-même quand [Shiraz](https://github.com/kookma/TW-Shiraz) est installé et activé, Shiraz fournissant déjà les mêmes classes.

## Présentation

Extrait du dossier `styles/bs/` de Shiraz (24 feuilles de style : dimensions, espacements, bordures, coins arrondis, couleurs, ombres, alertes, badges, boutons, cartes, etc.). Utilisable sur n'importe quel élément — tableaux, `<div>`, titres —, pas seulement sur les widgets de Shiraz.

## Installation

**Démo en ligne** : [https://nikorion.github.io/TW-Tiny-Bootstrap/](https://nikorion.github.io/TW-Tiny-Bootstrap/) — pour essayer le plugin avant de l'installer.

**Depuis la bibliothèque de plugins nikorion** (TiddlyWiki propose ensuite chaque nouvelle version en mise à jour) :

1. Sur [nikorion.github.io/tw-plugins](https://nikorion.github.io/tw-plugins/), glisser le bouton **Bibliothèque de plugins nikorion** sur votre wiki (une fois par wiki).
2. Ouvrir *Panneau de configuration → Plugins → Obtenir d'autres plugins → Ouvrir la bibliothèque de plugins*, choisir l'onglet nikorion et installer **Tiny Bootstrap**.

**À la main** : télécharger [`TW-Tiny-Bootstrap-Plugin.json`](https://nikorion.github.io/TW-Tiny-Bootstrap/TW-Tiny-Bootstrap-Plugin.json) et le glisser-déposer sur votre wiki.

Nécessite TiddlyWiki ≥ 5.3.5.

## Développement

```
pnpm install
pnpm dev      # wiki de dev + rechargement à chaud ; l'URL (port libre aléatoire) s'affiche au démarrage
pnpm build    # dist/TW-Tiny-Bootstrap-Plugin.json + docs/ (wiki de démo, publié par la CI)
```

Les sources sont dans `src/tiny-bootstrap/`.

## Fichiers

| Fichier | Rôle |
|---|---|
| `src/tiny-bootstrap/plugin.info` | Métadonnées du plugin |
| `src/tiny-bootstrap/styles/gate.tid` | Verrou d'auto-désactivation (détecte Shiraz), seul tiddler tagué `$:/tags/Stylesheet` |
| `src/tiny-bootstrap/styles/*.css` | Les 24 feuilles de style Bootstrap (non taguées, transcluses par `gate.tid`) |

## Historique des versions

**v0.1.0**

Première version — CSS utilitaire/composants de Bootstrap extrait de Shiraz dans un plugin à part, qui se désactive de lui-même.

## Crédits

Développé avec l'aide d'Anthropic Claude pour le code, la revue et la documentation.

## Licence

Licence MIT — voir `LICENSE`. Embarque un sous-ensemble de Bootstrap 5.3.3 (MIT), reconditionné via Shiraz (MIT).
