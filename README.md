# RecipClassify

## Travail à effectuer

- Prendre en main les données
- Analyser l'ensemble d'entraînement
  * Attention, le fichier de test, lui, ne doit être conservé que pour l'évaluation de vos approches !
- Lire l'article de présentation de la compétition
 * Vous pouvez aussi regarder ce qu'on fait les participant·es dans l'onglet "Actes"
- Mettre en place une baseline (méthode de référence simple à laquelle vous comparer)
 * Par exemple, prédire de manière aléatoire, prédire toujours la classe majoritaire, ...
- Mettre en place 3 ou 4 méthodes différentes pour résoudre la tâche
- Analysez vos résultats pour comprendre les prédictions de vos approches (choisissez par exemple seulement la meilleure et la moins bonne)

# DEFT2013 Tâche 2 : SONY (optionnel)

OULBOUB Safaa - NAFYSSATA Mohamed



## Description de la tâche



	1 ou 2 exemples de documents (avec leur identifiant)



## Statistiques corpus



	Nombre de document de train/dev/test

	Répartition des étiquettes dans chacun des sous-ensemble



## Méthodes proposées



### Run1: baseline (méthode de référence)



	Description de la méthode:

	- descripteurs utilisés

	- classifieur utilisé



### Run2: IDF-TF 

### Run3: RNN - Word2vec

### Run4: 



## Résultats



| Run      | f1 Score |

| -------- | --------:|

| baseline |  15,2 |

| IDF-TF   |   6,8 |

| RNN   |  50,8 |

| METH 4   |  70,2 |



### Analyse de résultats

	

	Pistes d'analyse:

	* Combien de documents ont un score de 0 ? de 0.5 ? de 1 ? (Courbe ROC)

	* Y-a-t-il des régularités dans les document bien/mal classifiés ?

	* Où est-ce que l'approche se trompe ? (matrice de confusion)

	* Si votre méthode le permet: quels sont les descripteurs les plus décisifs ?
