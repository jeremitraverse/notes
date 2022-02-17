# BAYE THEORIE

Compared theories on data proven values 

All ML algorithm tries to find the most probable class

P(C|x) = probability of C with the attributs vector of x

p(x) = probability to observe a 10% yellow pixels on a Homer picture

P(C) [a priori] = estimate without looking at the data

### Lost and risk

#### Rejection
Add verification step after the decision model to see if the certainty of the prediction is higher than a threshold. 

### Classification



### Classification parametrique
1. Choisir une distribution de probabilite (Bernouillis, normale ou multinomiale)
  - Normal : Lorsque nous avons un X numerique
  - Bernouillis : Lorsque x peut seulement prendre deux valeurs
2. 
  - Normal : Calculer la moyenne et variances pour chaque labels
3. On remplace ces valeurs dans des fonctions discriminentes (1 fonctions par classe)
  - Dans les fonction discriminentes nous avons seulement une variable pour tester la valeurs donnee
4. Remplacer la valeur donnee dans chaques fonction discriminente et choisir la valeur la plus elevee recu
