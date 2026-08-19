# Méthode

La grille officielle dit: **un niveau n'est atteint que si tous ses axes le sont**.

Laivel n'en fait pas une moyenne. Trois étapes, dans cet ordre.

## 1. Extraire, ne pas juger

Un modèle lit le profil et sort uniquement des signaux typés:

- `taille` · none / S / M / L / XL
- `harness` · none / prompts / context / context+behavior / +loops
- `intervention` · after majority / after part / key steps / never
- `parallele` · 0 / 1 / 3
- `autonomy` + `throughput` · uniquement pour départager Silver et Gold

Chaque signal porte une citation. S'il n'y a pas de preuve, le signal est `unknown`.

Le modèle n'écrit pas de niveau.

## 2. Appliquer la loi

`jq` (pas le modèle) calcule le plus haut palier dont **tous** les minima sont tenus.

`unknown` ne satisfait aucun minimum. Un profil troué ne devient jamais Gold
par interpolation.

Silver et Gold partagent les quatre axes. Gold exige en plus que les agents
prennent les tâches et que plusieurs PR partent le même jour, sans commit humain.

## 3. Raconter le cran suivant

Le modèle revoit les preuves et l'axe qui **bloque** le palier au-dessus.
Il écrit comment monter. Il n'a pas le droit de changer le niveau.

## Incomplet

Un profil vide ou illisible sort `white` / `low` / `blocking_axis: all`.
Le process ne plante pas. L'incertitude est le verdict.

## Pourquoi pas un score 0–100

La grille n'est pas une moyenne. Un harness Gold avec des PR taille S
est Red. Cacher ça derrière 73/100 ment au lead tech.
