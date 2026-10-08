# TW-Tiny-Bootstrap — contexte projet pour Claude

> **Avant toute tâche sur ce plugin, consulter d'abord le `CLAUDE.md` du workspace** (`../CLAUDE.md`) et ses `guides/` : outillage de dev commun (pnpm, `dev.cjs`/HMR, Ctrl+C, git push), pièges PowerShell/Windows, `publishFilter`, symlink. Ci-dessous : uniquement le spécifique à TW-Tiny-Bootstrap.

## Ce que c'est
Plugin TiddlyWiki (`$:/plugins/nikorion/tiny-bootstrap`) qui embarque les classes CSS utilitaires/composants de Bootstrap 5.3.3 — extraites du dossier `styles/bs/` de [Shiraz](https://github.com/kookma/TW-Shiraz) (Shiraz les reconditionne depuis le CSS officiel de Bootstrap, MIT). Aucun JS, aucune procédure wikitext, que du CSS. **Auto-désactivation si Shiraz est installé et actif** (voir mécanisme plus bas) — pensé pour les wikis/plugins (ex. TW-Table) qui veulent ces classes sans dépendre de Shiraz en entier.

## Mécanisme d'auto-désactivation (le seul point non trivial du plugin)
Les 24 tiddlers CSS sources (`styles/*.css`, un fichier Bootstrap = un tiddler) sont **volontairement pas tagués `$:/tags/Stylesheet`** — seul `styles/gate.tid` l'est. `gate.tid` est un tiddler `text/vnd.tiddlywiki` (donc wikifié, pas servi tel quel) qui :
1. teste la présence + activation de Shiraz via `\function tiny-bootstrap-shiraz-active() [[$:/plugins/kookma/shiraz]!is[missing]] :filter[lookup:no[$:/config/Plugins/Disabled/]match[no]]` (même idiome que `due-date.tid` de TW-Table pour Pikaday) ;
2. si la fonction est vide (Shiraz absent ou désactivé), transclut le champ `text` de chacun des 24 tiddlers sources en `$mode="block"`, produisant le CSS final concaténé dans la feuille de style de la page.

Validé empiriquement en direct dans un wiki de dev (`$tw.wiki.addTiddler` + lecture de `getComputedStyle`) : CSS actif sans Shiraz, CSS neutralisé dès que `$:/plugins/kookma/shiraz` existe et n'est pas dans `$:/config/Plugins/Disabled/`. Réactif : pas besoin de reload, `$:/tags/Stylesheet` se réévalue au changement de tiddlers.

**Ne jamais tagger un des 24 fichiers sources `$:/tags/Stylesheet` directement** — ça court-circuiterait le gate et casserait l'auto-désactivation.

## Renommages vs Shiraz
Aucun — ce plugin ne fait que republier du CSS statique sous un autre titre de tiddler (`$:/plugins/nikorion/tiny-bootstrap/styles/<nom>` au lieu de `$:/plugins/kookma/shiraz/styles/bs/<nom>`). Les classes CSS elles-mêmes (`w-100`, `btn-primary`, etc.) sont **volontairement identiques** à celles de Shiraz/Bootstrap — c'est le but (compatibilité avec tout code qui les utilise déjà).

## Structure
```
src/tiny-bootstrap/
  plugin.info
  readme.tid / history.tid / licence.tid   ← sélecteurs de langue
  settings.tid                              ← placeholder "Coming soon."
  language/
    lingo.tid                               ← tiny-bootstrap-lingo (tag $:/tags/Global)
    en-GB|fr-FR/{readme,history,license}.tid, settings.multids, playground.multids
  styles/
    gate.tid                    ← seul tiddler tagué $:/tags/Stylesheet, voir § auto-désactivation
    root.css(.meta)             ← variables CSS --bs-* (chargé en premier, les autres en dépendent)
    sizing/spacing/border/rounded/shadow/float/clearfix/text-*.css(.meta)  ← utilitaires
    alert/badge/breadcrumb/button/card/card-group/image/progress/rulers.css(.meta)  ← composants

wiki/                      ← wiki TW de dev : Playground.tid (i18n) démontrant chaque groupe de classes + note Shiraz
dist/                      ← généré par pnpm build, gitignored
docs/                      ← démo générée par `pnpm build` (`index.html` + moteur externe), gitignorée, publiée par la CI
```

## Spécificités dev
- Aucun module JS → pas de `pnpm lint`.
- HMR : tout est `.css`/`.tid`/`.multids`, poussé à chaud. Un changement de `plugin.info` reboote (nodemon).
- `pnpm build` → `dist/TW-Tiny-Bootstrap-Plugin.json` + démo `docs/` (publiée par la CI : `../guides/publication.md`).
- Pour tester l'auto-désactivation en dev : installer Shiraz dans `wiki/tiddlywiki.info` (`plugins`) ou glisser son `.json` dans le wiki de dev, recharger, vérifier que le Playground garde le même rendu (classes fournies par Shiraz) puis le retirer pour voir Tiny Bootstrap reprendre la main.
