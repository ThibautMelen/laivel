# Profil · Marc

Un hook relance l'agent tant que la CI est rouge. Zero commit humain
sur les PR. Il ne relit plus le diff.

- taille: XL
- harness: context_behavior_loops
- intervention: never
- parallele: 3
- autonomy: human_starts (c'est lui qui lance chaque boucle, pas le board)
- throughput: one (un merge par jour)
