# Vidéo · 2 minutes

Script parlé, tutoiement. Filmer le terminal + deux notes `held/`.
Pas de slide. Les crochets sont des consignes d'écran, pas à lire.

**Officiel · le jury publie la vidéo MUETTE** (formulaire `rendu.yml`:
« elle sera publiée muette » · GIF accepté). Chaque carton ci-dessous
DOIT être tapé à l'écran (caption overlay ou `echo` plein terminal).
La voix est un bonus, pas le canal.

## 0:00–0:20 · Qu'est-ce que c'est

[écran: `README.md`, puis `laivel.nika.yaml` ouvert]
[carton: NIKA ONLY · LE MODELE N'ECRIT PAS LA CEINTURE]

Laivel place un dev sur la grille AIDD, White jusqu'à Gold.
Un seul workflow Nika. Pas d'autre runtime.
OpenAI extrait des faits. jq pose le niveau: tous les axes ou rien.
Le modèle n'écrit jamais la ceinture.

## 0:20–0:50 · Le chemin live

[écran: lancer]
[carton: GLOB → EXTRACT → JQ LOI → DECIDE → RECUS]

```
nika run laivel.nika.yaml --var profiles=./held/*.md --max-cost-usd 1
```

Je lance `nika run`. Nika glob les notes, les lit.
L'extract sort taille, harness, intervention, parallèle, avec citations.
Schéma cassé: retry. Toujours vide: unknown.
jq: le plus haut palier dont tous les minima sont tenus. Contradiction: White.
`nika:decide` publie ou s'abstient.
Puis le récit — il ne peut plus changer le niveau.
Charts, reçu blake3, `JURY.md`. Zéro script à côté.

## 0:50–1:20 · White/defer vs Gold

[écran: `held/paradox.md`, puis `out/verdicts/`]
[carton: PARADOX · WHITE · DECIDE DEFER]

Paradox. Il raconte une refonte 100 % IA, plus jamais la main.
En même temps: zéro AGENTS.md, zéro agent, tous les commits sont les siens.
Récit contre repo. White. `nika:decide`: defer. On n'invente pas un cran.

[écran: `held/amina.md`]
[carton: AMINA · GOLD · RECOMMEND]

Amina. Les agents piochent tout seuls, cinq PR mergées, zéro commit humain,
rules et boucle versionnés, trois chantiers finis. Gold. recommend.

## 1:20–1:45 · Incomplet / unknown

[écran: `held/inconnu.md`]
[carton: INCONNU · UNKNOWN → WHITE · DEFER]

« Kevin utilise Claude. » Pas de repo, pas d'historique.
Extract: unknown partout. jq: White. decide: defer.
Incomplet, ça ne plante pas. Ça assume: plafond, pas une note.

## 1:45–2:00 · Relancer

Pour rejouer chez toi:

```
brew install supernovae-st/tap/nika
export OPENAI_API_KEY=...
nika run laivel.nika.yaml
```

Clone le dépôt **seul**. Un `nika.yaml` parent intercepterait le run.
MIT. La loi est dans le jq, pas dans le modèle.
