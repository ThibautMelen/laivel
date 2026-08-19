# Methode

La grille officielle: **un niveau n'est atteint que si tous ses axes le sont**.

Laivel est un seul workflow Nika. Pas de script, pas d'autre runtime.

## 1. Extraire

OpenAI (`openai/gpt-5-mini`) lit chaque profil **et la grille**
(`levels/aidd.yaml`). Il sort des signaux types, avec citations.
Il n'ecrit pas de niveau. Schema ferme, retry. Un fichier illisible
devient `unknown` (`recover: null`).

Les fixtures structurees prouvent la loi. Les profils `held/` sont
de la prose de lead tech, sans enums: c'est le e2e qui ressemble
au sujet de vendredi.

## 2. La loi (jq)

Le plus haut palier dont tous les minima sont tenus. `unknown` ne
satisfait aucun minimum. Une contradiction (XL sans harness, never +
prompts, 3 chantiers en taille S, agents sans boucles) baisse la
confiance et plafonne.

Silver et Gold partagent les 4 axes. Gold exige en plus `agents_pick`
et `multi_pr_day`.

## 3. Publier ou s'abstenir (`nika:decide`)

Le bundle `decisions/aidd-publish.bundle.json` recoit le nombre
d'unknowns et le flag contradiction.

- `recommend` · assez de preuves pour afficher le niveau
- `defer` · trop de trous · le niveau reste un plafond, pas une note
- `human_required` · deux sources font autorite et se contredisent

C'est le critere « assume quand il n'est pas sur », en contrat.

## 4. Raconter

Le modele recit le geste que jq a deja choisi. Il ne peut pas changer
le niveau (le champ n'est plus dans son schema).

## 5. Equipe

Un verdict par profil, un `out/team.md`, un `out/team.svg`.

## Pourquoi pas 0-100

La grille n'est pas une moyenne. Un harness Gold avec des PR taille S
est Red. 73/100 ment au lead tech.
