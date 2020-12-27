# these

Ce dépôt contient 3 versions du solveur SMT veriT, développées au cours de ma thèse au laboratoire INRIA-LORIA, au sein de l'équipe veridis.

Une fois extrait chaque version du solveur peut être complilée sur une architecture Linux de la façon suivante:

autoconf


./configure


make -j7


Puis veriT peut-être exécuté par la commande ./veriT

Pour la version Machine learning il est conseillé de compiler les modèles indépendamment 
(src/symbolic/xgboost_classifier2.c et src/symbolic/xgboost_classifier.c), puis d'ajouter les binaires au reste pour l'édition de liens.
La commande suivante peut être utilisée pour compiler plus rapidement ces deux fichiers :

gcc -lgmp -DWITH_OPENSLL -DWITH_COOKIES -fPIC -E xgboost_classifier.c -o xgboost_classifier.i


gcc -lgmp -DWITH_OPENSLL -DWITH_COOKIES -fPIC -c xgboost_classifier.i -o xgboost_classifier.o

Ces trois versions implémentent les techniques décrites dans mon manuscrit de thèse.

L'archive nommée verit-cade.tar.xz,correspond au code source du solveur veriT pour 
la logique d'ordre supérieur, et dont les évaluations sont données, dans ma thèse (chapitre 3),
et sur cette page : http://homepage.divms.uiowa.edu/~hbarbosa/papers/hosmt/
L'implémentation de la fermeture de congruence se trouve dans le fichier src/congruence/simpl_congruence.c
Le travail d'instanciation est quant à lui, effectuée dans les fichiers se trouvant dans le répertoire src/instantiation.

L'archive nommée HOSMT_full.tar.xz, correspond au code source du solveur veriT pour 
la logique d'ordre supérieur. Cette version du solveur utilise un module d'instanciation qui s'appuie 
sur une version curryfié du framework CCFV (la première version de HOCCFV).
Cette version de CCFV est évoquée dans ma thèse.


L'archive nommée veriTML-COMPILINGvers.zip, correspond au code source du solveur veriT 
utilisant l'approche de séléctions d'instances décrite dans ma thèse dans le chapitre 4.
Cette archive contient le code source du solveur veriT, ainsi que les deux modèles utilisés 
(src/symbolic/xgboost_classifier.c, et  src/symbolic/xgboost_classifier2.c) pour les évaluations décrites en section 4.4. 
L'encodage des features, ainsi que la sélection des instances, sont implémentées dans les fichiers src/symbolic/DAGstat.c, src/ml.c, src/veriT.c.
