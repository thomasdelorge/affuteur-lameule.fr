# Affûteur LA MEULE

Site vitrine statique pour l'activité d'affûtage de **Jérémie JOUET** (camion-atelier, marchés, dépôts, déplacements).

Stack : [Hugo](https://gohugo.io/) + thème maison `themes/lameule` + déploiement [GitHub Pages](https://pages.github.com/).

## Infos entreprise

- Téléphone : 06 02 23 80 08
- E-mail : contact@affuteur-lameule.fr
- Zone : Maine-et-Loire & Deux-Sèvres (Lys-Haut-Layon / Nueil-les-Aubiers)
- [Google Maps](https://maps.app.goo.gl/6B8nehasxDr69eMj6)
- [Facebook](https://www.facebook.com/AffuteurLAMEULE)
- [Instagram](https://www.instagram.com/affuteur_lameule)

## Prérequis (développeur)

- [Hugo Extended](https://gohugo.io/installation/) ≥ 0.164

```bash
hugo version   # doit afficher +extended
```

## Développement local

```bash
hugo server -D
```

Ouvre http://localhost:1313/

Build de production :

```bash
hugo --minify
```

Le résultat est dans `public/` (servable derrière n'importe quel reverse proxy nginx/Caddy, ou dossier statique).

## Édition pour l'artisan

Le design est dans le thème ; le contenu métier est **hors code** :

| Fichier | Contenu |
|---------|---------|
| `hugo.toml` → `[params]` | Téléphone, e-mail, réseaux, iframe calendrier, ID YouTube |
| `data/hero.yaml` | Accroche d'accueil |
| `data/services.yaml` | Liste des services |
| `data/process.yaml` | Les 3 étapes |
| `data/audiences.yaml` | Particuliers / Pros / Collectivités |
| `data/location.yaml` | Marchés, domicile, dépôts, textes planning |
| `data/video.yaml` | Texte « le rémouleur en action » |
| `data/footer.yaml` | Pied de page |
| `data/marquee.yaml` | Bandeau défilant |
| `static/images/` | Photos et logos |
| `content/mentions-legales.md` | Mentions légales |

### Planning

L'iframe Google Calendar est dans `hugo.toml` (`params.calendarEmbed`).  
Les dates se gèrent dans Google Calendar ; elles apparaissent automatiquement sur le site.

Theming limité par Google (pas de CSS dans l'iframe). On pousse au max via l'URL :
`hl=fr`, `showTitle=0`, `showTz=0`, `bgcolor` crème, `color` ambre (`#FFAD46`, palette Google).

### Photos

Remplacer les fichiers dans `static/images/` en gardant les mêmes noms, ou mettre à jour les chemins dans les YAML.

### Interface visuelle (optionnel)

Un éditeur [Decap CMS](https://decapcms.org/) est préparé sous `/admin/`.  
Il nécessite un backend d'auth (Net  # YouTube video ID (section « Le rémouleur en action »)
  videoId = "PHYnX07F2QM"
  logo = "/images/logo.png"ify Identity + Git Gateway, ou backend GitHub avec OAuth).  
Sans ça, l'édition se fait directement via les fichiers YAML ci-dessus (Pull Request ou commit).

## Déploiement

### GitHub Pages (recommandé)

1. Pousser le dépôt sur GitHub.
2. Settings → Pages → Source : **GitHub Actions**.
3. Le workflow `.github/workflows/deploy.yml` build et publie à chaque push sur `main`.
4. Domaine custom : le fichier `static/CNAME` contient `affuteur-lameule.fr`. Pointer le DNS (A/AAAA ou CNAME) vers GitHub Pages.

### Reverse proxy (nginx, Caddy, etc.)

```bash
hugo --minify --baseURL "https://affuteur-lameule.fr/"
```

Servir le contenu de `public/` en fichiers statiques. Aucun PHP/Node requis à l'exécution.

## Structure

```text
├── content/           # Pages Markdown
├── data/              # Contenu éditable (YAML)
├── assets/images/     # Sources images (WebP/srcset via Hugo)
├── static/images/     # Miroir médias (Decap CMS)
├── static/admin/      # Decap CMS (optionnel)
├── themes/lameule/    # Thème (layouts + CSS)
├── hugo.toml          # Config + coordonnées
└── .github/workflows/ # CI/CD GitHub Pages
```

### Images & SEO

Les photos passent par le processing Hugo (`assets/images/`) : WebP, `srcset`, compression.  
Données structurées `LocalBusiness` (JSON-LD) générées dans le `<head>`.

Fichier [`/llms.txt`](https://llmstxt.org/) pour les agents / moteurs agentiques, plus versions Markdown des pages (`index.html.md`).
