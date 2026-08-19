# Note de 1:1 · Marc

Un hook relance l'agent tant que la CI est rouge. Sur ses trois
branches du jour (auth, billing, docs), aucun commit n'est signe
de sa main. Il ne rouvre plus le diff. Context, rules, agents et
la boucle sont dans le repo. C'est encore lui qui lance chaque
boucle le matin, le board ne dispatch rien tout seul. Un merge
par jour, pas plus.
