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
##  Extrait du fichier de données

| doc_id              | titre                                        | type           | difficulté    | coût         | ingrédients                                  | recette  |
|---------------------|---------------------------------------------|---------------|--------------|-------------|----------------------------------------------|----------|
| recette_221358.xml  | Feuilleté de saumon et de poireau, sauce aux crevettes | Plat principal | Facile       | Moyen       | 1 pavé de saumon, 100g crevettes, 2 poireaux... | Couper finement les poireaux... |
| recette_48656.xml   | Cake poulet/moutarde/amandes               | Entrée        | Très facile  | Bon marché  | 3 œufs, 150g farine, levure, moutarde...    | Couper finement l'échalote... |



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
###  **Run 1: Baseline (Classe Majoritaire)**

**Descripteurs utilisés**  
- Aucun descripteur NLP.  
- La seule information utilisée est **la fréquence des classes** dans `train.csv`.
 - On prédit cette classe **pour toutes les recettes** de `test.csv`, sans analyser le texte. 
- On prédit uniquement **la classe majoritaire** sans analyser le texte.

 **Classifieur utilisé**  
- **Règle conditionnelle** : prédire systématiquement **la classe majoritaire** du jeu de train.  
- Il ne s'agit pas d'un modèle de Machine Learning, mais d'une **référence triviale**.

 **Résultat obtenu**  
- **Précision obtenue** : **46,4%**  
- **Explication** : En classant toutes les recettes dans **la catégorie majoritaire**, on obtient une précision de **46,4%**, mais sans aucune compréhension du texte.  

###  **Run 2: TF-IDF + SVM**

 **Descripteurs utilisés**  
- **TF-IDF (Term Frequency - Inverse Document Frequency)**
- **Suppression des stopwords avec spaCy**
- **Lemmatisation des mots**
- **N-grammes**

 **Classifieur utilisé**  
- **SVM (Support Vector Machine) avec noyau linéaire**
- **Gestion des classes déséquilibrées avec `class_weight='balanced'`**

 **Résultats obtenus**  
| Classe           | Precision | Recall | F1-score | Support |
|-----------------|-----------|--------|----------|---------|
| **Dessert**     | 0.99      | 1.00   | 0.99     | 407     |
| **Entrée**      | 0.70      | 0.84   | 0.77     | 337     |
| **Plat principal** | 0.91  | 0.82   | 0.86     | 644     |
| **Moyenne (accuracy)** | **0.87** | **0.88** | **0.87** | **1388** |

 **Conclusion**  
- **Amélioration significative** par rapport à la baseline.  
- **Les classes "Entrée" et "Plat principal" sont plus difficiles à séparer**.  

### Run3: LSTM - Word2vec
Nous avons entraîné un **modèle LSTM** utilisant les **embeddings Word2Vec** pour classifier les recettes en **Entrée, Plat principal ou Dessert**.

####  **Entraînement du modèle**
Nous avons utilisé **Word2Vec** pour convertir chaque mot en un vecteur de 300 dimensions, puis nous avons construit un modèle **LSTM** avec la structure suivante :
-  **Couche d'Embedding Word2Vec** (300 dimensions).
-  **LSTM avec 128 unités** pour capturer les relations locales entre les mots.
-  **Dropout (0.5)** pour éviter le surapprentissage.
-  **Deuxième LSTM avec 64 unités** pour capturer les relations globales.
-  **Dense (32 unités, activation ReLU)** pour l’apprentissage des représentations.
-  **Softmax** pour classifier en `Entrée`, `Plat principal` ou `Dessert`.

####  **Résultats obtenus**
| **Classe**          | **Précision** | **Recall** | **F1-score** | **Support** |
|---------------------|--------------|------------|--------------|------------|
| **Dessert**        | 0.93         | 0.99       | 0.96         | 407        |
| **Entrée**         | 0.73         | 0.61       | 0.67         | 337        |
| **Plat principal** | 0.83         | 0.87       | 0.85         | 644        |
| **Moyenne (accuracy)** | **0.84**  | **0.82**   | **0.82**     | **1388**  |

####  **Analyse des résultats**
 **Le modèle fonctionne très bien pour classer les `Desserts` (96% de F1-score).**  
 **Les `Plats principaux` sont bien reconnus (85% de F1-score).**  
 **Le modèle confond parfois les `Entrées` avec les plats principaux (67% de F1-score).**  
### Run4: BERT 



## Résultats

**Comparaison avec la baseline**  
| Méthode            | F1-Score (%) |
|--------------------|--------------|
| **Baseline (Classe Majoritaire)** | ~40-50  |
| **TF-IDF + SVM**  | **87.0**|
| **LSTM + word2vec**   |  **** |
| **BERT**  |  **85** |

### Analyse de résultats

	

	Pistes d'analyse:

	* Combien de documents ont un score de 0 ? de 0.5 ? de 1 ? (Courbe ROC)

	* Y-a-t-il des régularités dans les document bien/mal classifiés ?

	* Où est-ce que l'approche se trompe ? (matrice de confusion)

	* Si votre méthode le permet: quels sont les descripteurs les plus décisifs ?
