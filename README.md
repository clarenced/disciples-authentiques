# Disciple Authentique

Deck Slidev pour le message *Disciple Authentique* (série *Serviteurs du Roi*,
Marc 3.7-35), avec sketchnotes qui se révèlent au clic.

## Structure

- `slides.md` — le deck, slide par slide.
- `layouts/` — layouts Slidev (`full-bleed` pour les slides 1 et 8 rendues en
  image, `background` pour le fond texture + halo, `verse` pour les slides de
  texte biblique).
- `components/Background.vue` — le fond partagé (texture pierre + halo),
  utilisé par tous les layouts sauf `full-bleed`.
- `style.css` — styles globaux (fond, sketchnotes empilées, transitions).
- `public/` — toutes les images statiques, référencées dans les slides par
  chemin absolu (`/nom.png`).

## Où déposer les images

Tout va dans `public/` :

| Fichier(s) | Rôle |
| --- | --- |
| `texture.png`, `halo.png` | fond partagé (texture pierre + halo lumineux) |
| `slide-title.png`, `slide-plan.png` | slides 1 et 8, rendues en plein cadre depuis le PPTX |
| `intro-01.png` à `intro-03.png` | sketchnote d'intro (aucun calque de base — la slide démarre vide) |
| `00-consommateur.png` + `01-`, `02-`, `03-consommateur.png` | groupe 1 : « N'est pas un consommateur » |
| `10-projet-jesus.png` + `11-`, `12-`, `13-projet-jesus.png` | groupe 2 : « Participe au projet de Jésus » |
| `20-puissance-jesus.png` + `21-`, `22-`, `23-puissance-jesus.png` | groupe 3 : « Reconnaît la puissance de Jésus » |
| `30-famille-jesus.png` + `31-famille-jesus.png` | groupe 4 : « Fait partie de la famille de Jésus » |

Dans chaque groupe, le fichier `x0` est la base (visible sans clic, déjà
trouée aux emplacements des éléments) et `x1`, `x2`, `x3`... sont les clics
successifs, empilés dans `slides.md` avec `v-click="1"`, `v-click="2"`, etc.

Si tu dois refaire un découpage : les calques exportés par Photoshop sont
souvent rognés à leur bounding box plutôt qu'au format plein canevas. Un
calque plus petit que la référence doit être repositionné (recalé par
corrélation d'image ou repositionné manuellement) avant d'être posé dans
`public/` — sinon il ne s'alignera pas avec `inset: 0`.

## Développement

```bash
npm install
npm run dev        # ouvre le deck en local avec rechargement à chaud
```

## Présenter depuis le téléphone (mode présentateur distant)

```bash
npm run present -- --remote=motdepasse
```

Ouvre `http://<ip-locale>:3030/presenter` depuis le téléphone (même réseau
Wi-Fi), avec le mot de passe choisi. Ça donne les notes orateur, l'aperçu de
la slide suivante et le contrôle des clics.

**Important** : cette synchronisation distante repose sur un WebSocket porté
par le serveur de dev (`slidev --remote`). Elle ne fonctionne **pas** sur la
version déployée sur GitHub Pages, qui ne sert que des fichiers statiques —
pas de serveur, pas de WebSocket. Pour présenter en salle avec le
téléphone en présentateur, il faut lancer `npm run present` sur la machine
qui projette.

## Déploiement (GitHub Pages)

Le workflow `.github/workflows/deploy.yml` construit et déploie le deck à
chaque push sur `main`. Il n'y a rien à faire manuellement une fois le dépôt
poussé sur GitHub, avec Pages activé sur la source « GitHub Actions ».

## PDF de secours

En cas de souci de projection ou de réseau, exporter un PDF avec toutes les
étapes de clic :

```bash
npm run pdf
```

C'est un alias de `slidev export --with-clicks`. **Le flag `--with-clicks`
est indispensable** : sans lui, Slidev exporte une seule page par slide avec
les animations désactivées (donc les sketchnotes complètes, sans les
révélations progressives). Avec le flag, chaque étape de clic devient sa
propre page PDF.

`npm run export` (sans `--with-clicks`) reste disponible si un jour un export
simple, une page par slide, est utile pour autre chose qu'une présentation en
direct.

## Build

```bash
npm run build
```

Produit le site statique dans `dist/`.
