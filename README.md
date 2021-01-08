# these

Ce dépôt contient 4 versions du solveur SMT veriT, développées au cours de ma thèse au laboratoire INRIA-LORIA, au sein de l'équipe veridis.

Une fois extrait chaque version du solveur peut être compilée sur une architecture Linux de la façon suivante:

autoconf


./configure


make -j7


Puis veriT peut-être exécuté par la commande ./veriT

Pour la version Machine learning, il est conseillé de compiler les modèles indépendamment 
(src/symbolic/xgboost_classifier2.c et src/symbolic/xgboost_classifier.c), puis d'ajouter les binaires au reste pour l'édition de liens, comme ceci :

gcc -E xgboost_classifier.c -o xgboost_classifier.i

gcc -c xgboost_classifier.i -o xgboost_classifier.o

Puis coller directement dans le répertoire src/symbolic xgboost_classifier.o (et xgboost_classifier2.o), et relancer make.

Ces quatre versions implémentent les techniques décrites dans mon manuscrit de thèse.

L'archive nommée verit-cade.tar.xz,correspond au code source du solveur veriT pour 
la logique d'ordre supérieur, et dont les évaluations sont données, dans ma thèse (chapitre 3),
et sur cette page : http://homepage.divms.uiowa.edu/~hbarbosa/papers/hosmt/
L'implémentation de la fermeture de congruence se trouve dans le fichier src/congruence/simpl_congruence.c
Le travail d'instanciation est quant à lui, effectué dans les fichiers se trouvant dans le répertoire src/instantiation.

L'archive nommée HOSMT_full.tar.xz, correspond au code source du solveur veriT pour 
la logique d'ordre supérieur. Cette version du solveur utilise un module d'instanciation qui s'appuie 
sur une version curryfiée du framework CCFV (la première version de HOCCFV).
Cette version de CCFV est évoquée dans ma thèse.


L'archive nommée veriTML.tar.xz , correspond au code source du solveur veriT 
utilisant l'approche de séléctions d'instances décrite dans ma thèse dans le chapitre 4.
Cette archive contient le code source du solveur veriT, ainsi que les deux modèles utilisés 
(src/symbolic/xgboost_classifier.c, et  src/symbolic/xgboost_classifier2.c) pour les évaluations décrites en section 4.4. 
L'encodage des features, ainsi que la sélection des instances, sont implémentés dans les fichiers src/symbolic/DAGstat.c, src/ml.c, src/veriT.c.

L'archive nommée veriT_heuristique_sk_I.xz , correspond au code source du solveur veriT 
utilisant l'heuristique de restriction d'instances issues soit de la Skolemisation, soit 
des stratégies de triggers ou d'énumération. Ce code correspond aux heuristiques présentées 
dans ma thèse dans le chapitre 5. Les fichiers concernés par cette extension sont veriT.c, 
inst-man.c, inst-triggers.c, pre.c et inst-create.c.
Pour exécuter l'heuristique de restriction des Skolem uniquement il faut utiliser veriT avec la commande suivante :

./veriT --disable-banner --disable-print-success --mdli --limit-sk-qform=9 --inst-sorts-threshold=100

--limit-sk-qform est le paramètre correspondant au seuil (nombre d'instances max/formules exists) que l'on 
souhaite accorder pour chaque formule existentiellement quantifiée, il peut être modifié.

Pour exécuter l'heuristique combinant la restriction des instances et des Skolems il faut utiliser 
veriT avec la commande suivante :

./veriT --disable-banner --disable-print-success --mdli --limit-sk-qform=9 --limit-qform=100 --inst-sorts-threshold=100

--limit-qform est le paramètre correspondant au seuil (nombre d'instances max/formules univ) que l'on souhaite accorder 
pour chaque formule quantifiée universellement, il peut être modifié.

Une remarque la valeur du paramètre --inst-sorts-threshold, permet de limiter le nombre de termes 
ground que l'on autorise pour chaque sorte, lorsqu'on utilise l'instanciation par énumération, la 
valeur donnée ici est celle qui a le mieux fonctionné lors de nos évaluations, cependant cette valeur 
peut être modifiée pour d'autres problèmes. Pour plus d'information vous pouvez aussi consulter le 
fichier portfolio.sh. 



