# Methode

La grille officielle: **un niveau n'est atteint que si tous ses axes le sont**.

Laivel est un seul workflow Nika. Pas de script, pas d'autre runtime.

## Extraire

OpenAI (`openai/gpt-5-mini`) lit chaque profil **et la grille**
(`levels/aidd.yaml`). Il sort des signaux types, avec citations.
Il n'ecrit pas de niveau. Schema ferme, retry.

`parallele` accepte entier ou string (`-1 | 0 | 1 | 3`). Un enum
string seul cassait des que le modele renvoyait `3` (nombre) —
l'extrait tombait en `null`, puis White. Evidence est optionnelle:
un champ oublie ne doit pas tuer l'extrait.

« Jamais deux chantiers » / « un ticket a la fois » = parallele **1**,
pas 0. 0 = aucune livraison.

Premier passage rate → second infer, schema encore plus petit.
Toujours `null` → `unknown` (`recover: null`). Si l'extract rate
encore, `nika:decide` defer White. Ne pas inventer un cran.

Les fixtures structurees prouvent la loi. Les profils `held/` sont
de la prose de lead tech, sans enums: c'est le e2e qui ressemble
au sujet de vendredi.

## La loi (jq)

Le plus haut palier dont tous les minima sont tenus. `unknown` ne
satisfait aucun minimum. Une contradiction (flag `conflict`, XL sans
harness, never + prompts, 3 chantiers en taille S, agents sans
boucles) **force White** et baisse la confiance.

Silver et Gold partagent les 4 axes. Gold exige en plus `agents_pick`
et `multi_pr_day`.

Avant de scorer, jq corrige deux lectures: ChatGPT colle sans fichier
= `prompts` (pas `none`) · hook CI + plus de diff = `never` (pas
`key_steps`).

## Publier ou s'abstenir (`nika:decide`)

Le bundle `decisions/aidd-publish.bundle.json` recoit le nombre
d'unknowns et le flag contradiction.

- `recommend` · assez de preuves pour afficher le niveau
- `defer` · trop de trous · le niveau reste un plafond, pas une note
- `human_required` · deux sources font autorite et se contredisent

C'est le critere « assume quand il n'est pas sur », en contrat.

## Raconter, puis sceller

Le modele recit le geste que jq a deja choisi. Il ne peut pas changer
le niveau (le champ n'est plus dans son schema).

Ensuite, uniquement des builtins Nika: glob `exclude: "**/README.md"`,
verdicts, roster (`nika:convert`), 3 charts, recu (`nika:date` +
`nika:uuid` + `nika:hash` blake3), `nika:validate` contre
`decisions/team.schema.json`, `nika:assert` cards vs glob, `nika:log`
des actions decide + effectifs par ceinture, `nika:emit`
`laivel.roster`, `out/JURY.md` (jq, pas le modele). Self-test:
`nika:json_diff` → `out/self-test.patch.json`. Extract rate → unknown
→ White + defer.

## Held (prose, zero enum)

| note | belt |
|---|---|
| camille | White |
| samir | Red |
| noor | Blue |
| lea | Green |
| ines | Copper |
| marc | Silver |
| amina | Gold |
| inconnu | White · rumor |
| paradox | White · recit vs repo |
| lou | White · rumor 3 lignes |
| theo | White · recit vs depot |
| chloe | White · boucle CI vs cadrage |
| felix | White · ChatGPT sans fichier |

## Pourquoi pas 0-100

La grille n'est pas une moyenne. Un harness Gold avec des PR taille S
est Red. 73/100 ment au lead tech.
