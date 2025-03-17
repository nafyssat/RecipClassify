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
L'objectif est de classifier automatiquement des recettes de cuisine en trois catégories :
- **Entrée**  
- **Plat principal**  
- **Dessert**  
## Extrait du fichier de données

Voici un exemple de structure du fichier contenant les recettes de cuisine :
```csv
doc_id,titre,type,difficulte,cout,ingredients,recette
recette_221358.xml,"Feuilleté de saumon et de poireau, sauce aux crevettes",Plat principal,Facile,Moyen,"- 1 gros pavé de saumon<br>- 100 g de crevettes décortiquées<br>- 2 poireaux moyens","Couper finement le blanc de poireaux...<br>Faire revenir dans l'huile..."
recette_48656.xml,"Cake poulet/moutarde/amandes",Entrée,Très facile,Bon marché,"- 3 œufs<br>- 150 g de farine<br>- 1 sachet de levure","Préchauffer le four...<br>Mélanger les ingrédients..."

## Statistiques corpus
###  Nombre de documents dans chaque ensemble (train/dev/test) :
- **Total (train + validation)** : 12 473 recettes
- **Train** : 9 978 recettes
- **Validation** *(utilisée uniquement avec LSTM + Word2Vec)* : 2 495 recettes
- **Test** *(réservé à l'évaluation finale)* : 1 388 recettes

##  Répartition des étiquettes dans chacun des sous-ensembles

Voici la distribution des catégories (`Entrée`, `Plat principal`, `Dessert`) dans chaque ensemble.

### **Train (80% des données)**
- **Plat principal** : 4 642 recettes
- **Dessert** : 3 009 recettes
- **Entrée** : 2 327 recettes

### **Validation (20% des données, utilisé uniquement avec LSTM)**
- **Plat principal** : 1 160 recettes
- **Dessert** : 753 recettes
- **Entrée** : 582 recettes

### **Test (évaluation finale)**
- **Plat principal** : 644 recettes
- **Dessert** : 407 recettes
- **Entrée** : 337 recettes


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
