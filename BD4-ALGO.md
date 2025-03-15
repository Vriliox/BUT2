# Exemple d'utilisation de l'aglorithme de Synthèse en 3FN

## 1. Trouver une couverture minimale G de F

### 1.a. Initialiser la relation R avec tous les attributs et identifier toutes les dépendances fonctionnelles.

On considère la relation R(A, B, C, D, E, F, G), on considère l'ensemble $G_0$ des dépendances fonctionnelles suivantes:
- DF1: $AB \rightarrow EGD$
- DF2: $DE \rightarrow FGB$
- DF3: $C \rightarrow AG$
- DF4: $B \rightarrow EDF$
- DF5: $FB \rightarrow A$

### 1.b. Simplifier les DF à droite

> Développer les DF $X \rightarrow A_1, ..., A_n$ telles que $X \rightarrow A_1, X \rightarrow A_2, ..., X \rightarrow A_n$.

On obtient l'ensemble $G_1$ des dépendances fonctionnelles suivantes:
- DF1.1: $AB \rightarrow E$
- DF1.2: $AB \rightarrow G$
- DF1.3: $AB \rightarrow D$
- DF2.1: $DE \rightarrow F$
- DF2.2: $DE \rightarrow G$
- DF2.3: $DE \rightarrow B$
- DF3.1: $C \rightarrow A$
- DF3.2: $C \rightarrow G$
- DF4.1: $B \rightarrow E$
- DF4.2: $B \rightarrow D$
- DF4.3: $B \rightarrow F$
- DF5.1: $FB \rightarrow A$

### 1.c. Simplifier les DF à gauche

> Pour chaque attribut $B$ de $X$, si $B$ appartient à la fermeture suivante: $\{X-\{B\}\}^+_{G-\{X \rightarrow A\}}$.
         <br>C'est à dire que $B$ est atteignable par les autres attributs de X.
         <br>Alors on remplace $X \rightarrow A$ par $X-\{B\} \rightarrow A$.

Détaillons pour chaque DF:

1. DF1.1: $AB \rightarrow E$
    - Cherchons si $A$ est atteignable par $B$.
    - On a $B^+_{G_1 - \{AB \rightarrow E\}} = \{B,E,D,F,A...\}$.
    - On a $A \in B^+_{G_1 - \{AB \rightarrow E\}}$.
    - Donc on remplace $AB \rightarrow E$ par $B \rightarrow E$.
    - Or $B \rightarrow E$ est déjà dans $G_1$, on supprime donc la DF $AB \rightarrow E$.

2. DF1.2: $AB \rightarrow G$
    - Cherchons si $A$ est atteignable par $B$.
    - On a $B^+_{G_1 - \{AB \rightarrow G\}} = \{B,E,D,F,A...\}$.
    - On a $A \in B^+_{G_1 - \{AB \rightarrow G\}}$.
    - Donc on remplace $AB \rightarrow G$ par $B \rightarrow G$.
    - Or $B \rightarrow G$ est déjà dans $G_1$, on supprime donc la DF $AB \rightarrow G$.

3. DF1.3: $AB \rightarrow D$
    - Même raisonnement que pour DF1.1 et DF1.2.
    - On supprime la DF $AB \rightarrow D$.

4. DF2.1: $DE \rightarrow F$
   - Cherchons si $D$ est atteignable par $E$.
   - On a $E^+_{G_1 - \{DE \rightarrow F\}} = \{E\}$.
   - On a $D \notin E^+_{G_1 - \{DE \rightarrow F\}}$.
   - Donc on ne remplace pas $DE \rightarrow F$.
   - Cherchons si $E$ est atteignable par $D$.
   - On a $D^+_{G_1 - \{DE \rightarrow F\}} = \{D\}$.
   - On a $E \notin D^+_{G_1 - \{DE \rightarrow F\}}$.
   - Donc on ne remplace pas $DE \rightarrow F$.
   - On ne peut pas simplifier $DE \rightarrow F$.

5. DF2.2: $DE \rightarrow G$
    - Même raisonnement que pour DF2.1.
    - On ne peut pas simplifier $DE \rightarrow G$.

6. DF2.3: $DE \rightarrow B$
    - Même raisonnement que pour DF2.1.
    - On ne peut pas simplifier $DE \rightarrow B$.

Pour les autres DF, on ne peut pas les simplifier, excepté DF5.1:

7. DF5.1: $FB \rightarrow A$
    - Cherchons si $F$ est atteignable par $B$.
    - On a $B^+_{G_1 - \{FB \rightarrow A\}} = \{B,E,D,F...\}$.
    - On a $F \in B^+_{G_1 - \{FB \rightarrow A\}}$.
    - Donc on remplace $FB \rightarrow A$ par $B \rightarrow A$.

On obtient l'ensemble $G_2$ des dépendances fonctionnelles suivantes:
- DF1.2: $B \rightarrow G$
- DF2.1: $DE \rightarrow F$
- DF2.2: $DE \rightarrow G$
- DF2.3: $DE \rightarrow B$
- DF3.1: $C \rightarrow A$
- DF3.2: $C \rightarrow G$
- DF4.1: $B \rightarrow E$
- DF4.2: $B \rightarrow D$
- DF4.3: $B \rightarrow F$
- DF5.1: $B \rightarrow A$

### 1.d. Supprimer les DF redondantes

> Pour chaque DF $X \rightarrow A$, si $A$ appartient à $X^+_{G-\{X \rightarrow A\}}$, alors on peut supprimer $X \rightarrow A$.
         <br>C'est à dire que A est atteignable à partir des autres DF depuis X.

Détaillons pour chaque DF:

1. DF1.2: $B \rightarrow G$
    - On a $G \in B^+_{G_2 - \{B \rightarrow G\}} = \{B,E,D,F,A, G...\}$.
    - On peut supprimer $B \rightarrow G$.

2. DF2.1: $DE \rightarrow F$
    - On a $F \in DE^+_{G_2 - \{DE \rightarrow F\}} = \{D,E,G,B,F...\}$.
    - On peut supprimer $DE \rightarrow F$.

3. DF2.2: $DE \rightarrow G$
   - On a $G \in DE^+_{G_2 - \{DE \rightarrow G\}} = \{F,B,E,D,F,A\}$.
   - On ne peut pas supprimer $DE \rightarrow G$.

On ne peut supprimer aucune autre DF.

On obtient l'ensemble $G_3$ des dépendances fonctionnelles suivantes:
- DF2.2: $DE \rightarrow G$
- DF2.3: $DE \rightarrow B$
- DF3.1: $C \rightarrow A$
- DF3.2: $C \rightarrow G$
- DF4.1: $B \rightarrow E$
- DF4.2: $B \rightarrow D$
- DF4.3: $B \rightarrow F$
- DF5.1: $B \rightarrow A$

## 2. Edition des relations

> Pour chaque $X$ de $G$, créer une relation $\{X, A_1, ..., A_n\}$ avec les DF $X \rightarrow A_1, ..., X \rightarrow A_n$.
> <br> $X$ est la clé de la relation.

On obtient les relations suivantes:
- $R_1(D, E, G, B)$ avec la clé $DE$ et les DF $DE \rightarrow G$ et $DE \rightarrow B$.
- $R_2(C, A, G)$ avec la clé $C$ et les DF $C \rightarrow A$ et $C \rightarrow G$.
- $R_3(B, E, D, F, A)$ avec la clé $B$ et les DF $B \rightarrow E$, $B \rightarrow D$, $B \rightarrow F$ et $B \rightarrow A$.

## 3. Fusionner les relations

> Si les fermeture des clés sont équivalentes, alors les relations peuvent être fusionnées.

On a $DE^+_{G_3} = \{D,E,G,B,F,A\}$ et $C^+_{G_3} = \{C,A,G\}$ et $B^+_{G_3} = \{B,E,D,F,A,G\}$.

On observe que $DE^+_{G_3} = B^+_{G_3}$, donc on peut fusionner $R_1$ et $R_3$.

On obtient donc les relations finales suivantes:
- $R_1(D, E, G, B, F, A)$ avec la clé $DE$
- $R_2(C, A, G)$ avec la clé $C$ 
