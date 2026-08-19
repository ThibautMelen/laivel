# Referentiel AIDD

Source: https://github.com/ai-driven-dev/laivel-up/blob/main/levels/aidd.md

Sept niveaux. Ils se cumulent. **Un niveau n'est atteint que si tous ses axes le sont.**

## Axes

- **Taille** · plus grosse feature livree avec l'IA · S peu de complexite · M moyenne · L multi-etapes · XL multi-modules
- **Harness** · autour du modele · context (memoire, conventions) · behavior (rules, agents, hooks) · boucles (relance tant que la CI echoue)
- **Intervention** · quand l'humain reprend · apres coup majorite · apres coup une partie · etapes cles · jamais
- **En parallele** · 0 · 1 · 3 chantiers meres le meme jour

## Grille

| Niveau | Taille | Harness | Intervention | Parallele |
| --- | --- | --- | --- | --- |
| White | — | rien | — | 0 |
| Red | S | prompts | apres coup, majorite | 1 |
| Blue | M | context | apres coup, une partie | 1 |
| Green | L | context + behavior | etapes cles | 1 |
| Copper | L-XL | context + behavior | etapes cles | 3 |
| Silver | L-XL | context + behavior + boucles | jamais | 3 |
| Gold | L-XL | context + behavior + boucles | jamais | 3 + agents autonomes + plusieurs PR/jour |

Hors perimetre: seniorite, qualite du code (pre-requis), volume de tokens.
