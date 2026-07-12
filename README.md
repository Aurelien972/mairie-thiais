# Ville de Thiais — Maquette interactive du site internet

Maquette fonctionnelle réalisée dans le cadre de la **consultation n° 26PA12SE**
(refonte du site internet de la Ville de Thiais), pour le **critère 2.1 (25 % de
la note)**. Le jury peut cliquer, naviguer, filtrer l'agenda, ouvrir le menu et
dialoguer avec le chat simulé « Thiais GPT ».

> Version 1 — juillet 2026 · Réponse de **Digital Freedom Caraïbe**.

## 🔗 Pages

| Page | Fichier | Description |
|------|---------|-------------|
| Accueil | `site/index.html` | Page d'accueil (M1) : accès rapides, actualités, agenda, kiosque, vidéos, menu overlay, chat « Thiais GPT ». |
| Agenda | `site/agenda.html` | Agenda « Que faire à Thiais ? » (M4) : vue liste + fiche événement, filtres temporels et catégories. |
| Article | `site/article.html` | Article & page type (M3) : fil d'Ariane, accordéons, bandeaux d'alerte, colonne latérale. |
| Présentation | `site/presentation.html` | Note de présentation (format A4) reliant chaque exigence du CCTP à sa réponse dans la maquette. |

Les pages se lient entre elles (le logo ramène à l'accueil, boutons « Voir tout
l'agenda », « Toutes les actualités », etc.).

## 🏗️ Technique

- **100 % statique**, rendu **côté client**. Chaque page HTML est interprétée par
  le runtime **Claude Design** (`site/support.js`), qui charge React/ReactDOM
  depuis un CDN puis rend le template.
- **Aucune étape de build.** Il suffit de servir le dossier `site/`.
- Typographie **Public Sans** (Google Fonts), palette bleue de la charte de la
  Ville, loader « lys de Thiais », micro-interactions sobres — conformément à la
  direction artistique du cahier des charges.
- Quelques visuels sont chargés depuis `ville-thiais.fr` ; le logo est servi en
  local (`site/assets/logo-thiais.jpg`).

> ⚠️ Le rendu nécessite un accès réseau sortant (CDN React + Google Fonts).

## ▶️ Lancer en local

Servez le dossier `site/` avec n'importe quel serveur statique, par exemple :

```bash
cd site
python3 -m http.server 8000
# puis ouvrir http://localhost:8000
```

Ouvrir directement le fichier via `file://` ne fonctionne pas (le runtime charge
des scripts par requêtes HTTP).

## 🚀 Déploiement — Netlify

Le site est publié sur Netlify. La configuration se trouve dans
[`netlify.toml`](./netlify.toml) :

- `publish = "site"` — seul le dossier `site/` est mis en ligne ;
- pas de commande de build (site statique) ;
- en-tête `X-Robots-Tag: noindex` pour éviter l'indexation de la maquette.

**Déploiement continu (recommandé) :** connecter ce dépôt GitHub à Netlify
(*Add new site → Import an existing project*). Netlify détecte `netlify.toml` et
publie automatiquement `site/` à chaque `push` sur la branche de production.

## 📁 Structure

```
.
├── site/                 # ← dossier publié
│   ├── index.html        # Accueil (M1)
│   ├── agenda.html       # Agenda (M4)
│   ├── article.html      # Article & page type (M3)
│   ├── presentation.html # Note de présentation A4
│   ├── support.js        # Runtime Claude Design
│   ├── doc-page.js       # Composant document paginé (présentation)
│   ├── robots.txt
│   └── assets/logo-thiais.jpg
├── netlify.toml
└── README.md
```

> Le cahier des charges interne des maquettes est conservé hors dépôt (dépôt
> public) et ignoré par git.
