# Fiche de Révision : Théorie des probabilités et statistique mathématique

## 1. Notions de base

### Probabilité d'un événement

La probabilité \( P(A) \) d’un événement \( A \) est un nombre entre 0 et 1 qui mesure la chance que cet événement se produise. Les règles fondamentales sont :
- \( P(A) \geq 0 \) : une probabilité ne peut pas être négative.
- \( P(\Omega) = 1 \) : la probabilité que **quelque chose** se produise est 1 (l'univers \( \Omega \)).
- La somme des probabilités de tous les événements possibles doit être égale à 1.

### Événement complémentaire

Si \( A \) est un événement, son **complémentaire** \( \bar{A} \) est l’événement "A ne se produit pas". On a la relation :
\[
P(\bar{A}) = 1 - P(A)
\]
**Exemple :** Si la probabilité qu’il pleuve demain est \( P(\text{pluie}) = 0.3 \), la probabilité qu’il ne pleuve pas est \( P(\text{pas de pluie}) = 1 - 0.3 = 0.7 \).

### Événements incompatibles

Deux événements sont **incompatibles** si les deux ne peuvent pas se produire en même temps. Cela signifie que :
\[
P(A \cap B) = 0
\]
Si deux événements \( A \) et \( B \) sont incompatibles, alors la probabilité que l’un ou l’autre se produise est donnée par :
\[
P(A \cup B) = P(A) + P(B)
\]

### Probabilité conditionnelle

La **probabilité conditionnelle** permet de calculer la probabilité qu’un événement \( B \) se produise sachant qu’un autre événement \( A \) s’est déjà produit. Elle est notée \( P(B \mid A) \) et définie par :
\[
P(B \mid A) = \frac{P(A \cap B)}{P(A)}, \text{ à condition que } P(A) > 0
\]
Cela signifie que l’on divise la probabilité que \( A \) et \( B \) se produisent en même temps par la probabilité que \( A \) se produise.

### Indépendance des événements

Deux événements \( A \) et \( B \) sont **indépendants** si la survenue de l’un n’affecte pas la probabilité de l’autre. Dans ce cas :
\[
P(A \cap B) = P(A) \times P(B)
\]
et
\[
P(B \mid A) = P(B)
\]

---

## 2. Relations entre les événements et opérations sur les événements

### Union et intersection d’événements

- **Union** (\( A \cup B \)) : Cela correspond à la survenue de **l’un ou l’autre** des événements \( A \) ou \( B \). La probabilité de l’union est :
  \[
  P(A \cup B) = P(A) + P(B) - P(A \cap B)
  \]
  On retire \( P(A \cap B) \) car il est compté deux fois dans la somme.

- **Intersection** (\( A \cap B \)) : Cela correspond à la survenue **simultanée** des deux événements \( A \) et \( B \). Si les événements sont incompatibles, alors \( P(A \cap B) = 0 \).

### Tribu d’événements

Une **tribu** (ou σ-algèbre) est un ensemble structuré d'événements qui obéit à trois règles :
1. L'univers \( \Omega \) doit appartenir à la tribu.
2. Le complémentaire de tout événement de la tribu doit également être dans la tribu.
3. L'union et l'intersection de tout sous-ensemble d'événements de la tribu doivent également être des événements de la tribu.

### Système complet d’événements

Un **système complet d'événements** est un ensemble d'événements qui couvrent tous les résultats possibles d'une expérience et qui sont mutuellement exclusifs. Cela signifie que chaque résultat appartient à un seul événement du système.

**Exemple :** Si l’on lance un dé, un système complet d’événements peut être :
- \( A_1 \) : "le dé montre 1 ou 2",
- \( A_2 \) : "le dé montre 3 ou 4",
- \( A_3 \) : "le dé montre 5 ou 6".

---

## 3. Notions de base de la combinatoire et du dénombrement

### P-listes

> **Quand l’utiliser ?** : Lorsque **l'ordre compte** et que la **répétition est autorisée**.

Une **p-liste** est une suite ordonnée de \( p \) éléments tirés d'un ensemble de \( n \) éléments, **avec répétition**. Cela signifie que chaque élément peut être sélectionné plusieurs fois, et l'ordre compte.

La formule pour calculer le nombre de p-listes est :
\[
n^p
\]
où \( n \) est le nombre total d'éléments dans l'ensemble, et \( p \) est la longueur de la liste.

#### Exemple

Si tu dois former une liste de 3 lettres à partir de l'alphabet \( \{A, B, C, D\} \) (donc \( n = 4 \)) avec répétition, le nombre de p-listes possibles est :
\[
4^3 = 4 \times 4 \times 4 = 64.
\]
Cela inclut des listes comme \( AAA, AAB, BAC, DDD \), etc.

Les p-listes sont utilisées lorsque l'ordre des éléments est important et qu'il est possible de répéter des éléments.

### Permutations

> **Quand l’utiliser ?** : Lorsque **l'ordre compte** et que la **répétition n’est pas autorisée**. On organise tous les éléments disponibles.

Les **permutations** concernent l’organisation d’éléments où **l’ordre compte**. Le nombre de permutations de \( n \) objets est donné par \( n! \) (factorielle de \( n \)).

**Exemple :** Le nombre de façons d’organiser 3 livres sur une étagère est \( 3! = 6 \).

### Combinaisons

> **Quand l’utiliser ?** :  Lorsque **l'ordre ne compte pas** et que la **répétition n’est pas autorisée**. On choisit des éléments **sans tenir compte de l'ordre**.

Les **combinaisons** concernent la sélection d’éléments où **l’ordre ne compte pas**. Le nombre de combinaisons de \( k \) objets parmi \( n \) est donné par :
\[
C(n, k) = \frac{n!}{k!(n-k)!}
\]
**Exemple :** Le nombre de façons de choisir 3 livres parmi 8, sans se soucier de l'ordre, est :
\[
C(8, 3) = \frac{8!}{3!(8-3)!} = 56.
\]

### Arrangements

> **Quand l’utiliser ?** : Lorsque **l'ordre compte** mais que l’on ne prend **que quelques éléments** d’un ensemble, **sans répétition**.

Les **arrangements** concernent la sélection d’éléments où **l’ordre compte**. Le nombre d’arrangements de \( k \) éléments parmi \( n \) est donné par :
\[
A(n, k) = \frac{n!}{(n - k)!}
\]
**Exemple :** Le nombre de façons d’organiser 2 boules parmi 8 est :
\[
A(8, 2) = \frac{8!}{6!} = 56.
\]

---

## 4. Probabilités des événements

### Calcul des probabilités

La probabilité d’un événement est calculée en divisant le **nombre de résultats favorables** par le **nombre total de résultats possibles**.

**Exemple** : La probabilité d’obtenir un nombre pair en lançant un dé est :
\[
P(\text{nombre pair}) = \frac{3}{6} = 0.5.
\]

### Probabilité conditionnelle

La probabilité qu'un événement \( B \) se produise sachant qu'un autre événement \( A \) s'est déjà produit est donnée par :
\[
P(B \mid A) = \frac{P(A \cap B)}{P(A)}.
\]

### Formule des probabilités totales

Si \( A_1, A_2, \dots, A_n \) forment un système complet d’événements, la probabilité d’un événement \( B \) est donnée par la **formule des probabilités totales** :
\[
P(B) = \sum_{i=1}^{n} P(A_i) \times P(B \mid A_i) = P(B \mid A_1) \times P(B \mid A_2) \times ... P(B \mid A_n)
\]

### Formule de Bayes

La **formule de Bayes** permet d’inverser les probabilités conditionnelles. Elle est donnée par :
\[
P(A_i \mid B) = \frac{P(A_i) \times P(B \mid A_i)}{P(B)}
\]

**Exemple :** Si tu veux connaître la probabilité que quelqu’un vienne d’un certain département dans une entreprise sachant qu’il a été promu, tu peux utiliser la formule de Bayes pour l'inverser à partir des probabilités conditionnelles.

---

# Fiche de Révision : Séries et Convergence

## 1. Définition d'une série

Une **série** est la somme infinie des termes d'une suite. Si la suite est notée \( u_n \), la série associée est :
\[
S = \sum_{n=0}^{\infty} u_n
\]
L'objectif est de déterminer si cette somme infinie **converge** (tend vers une valeur finie) ou **diverge**.

---

## 2. Sommes partielles

Pour étudier la convergence d'une série, on commence par examiner les **sommes partielles** \( S_n \), qui représentent la somme des premiers \( n \) termes de la série :
\[
S_n = \sum_{k=0}^{n} u_k
\]
Si, lorsque \( n \) tend vers l'infini, \( S_n \) se rapproche d'une limite \( l \), on dit que la série **converge** vers \( l \). Sinon, elle **diverge**.

---

## 3. Convergence d'une série

Une série est **convergente** si la suite des sommes partielles tend vers une limite finie :
\[
\lim_{n \to \infty} S_n = l
\]
Si cette limite n'existe pas ou est infinie, la série est **divergente**.

---

## 4. Critères de convergence

### a) Critère de Leibniz (Séries alternées)

Le **critère de Leibniz** concerne les **séries alternées**, c'est-à-dire des séries où les termes changent de signe à chaque itération, comme dans :
\[
S = \sum_{n=1}^{\infty} (-1)^{n+1} u_n
\]
Ce critère stipule que la série **converge** si les deux conditions suivantes sont remplies :
1. Les termes \( u_n \) sont décroissants, c'est-à-dire \( u_{n+1} \leq u_n \).
2. Les termes tendent vers 0 : \( \lim_{n \to \infty} u_n = 0 \).

**Exemple** : La série alternée \( \sum_{n=1}^{\infty} \frac{(-1)^n}{n} \) converge car \( \frac{1}{n} \) est décroissant et tend vers 0.

### b) Test de D'Alembert (Critère du rapport)

Le **test de d'Alembert** examine le rapport entre deux termes consécutifs de la série. Si \( u_n \) est le terme général de la série, on calcule le rapport \( \frac{u_{n+1}}{u_n} \) et on étudie sa limite quand \( n \to \infty \) :
\[
r = \lim_{n \to \infty} \left|\frac{u_{n+1}}{u_n}\right|.
\]
- Si \( r < 1 \), la série est **convergente**.
- Si \( r > 1 \), la série est **divergente**.
- Si \( r = 1 \), le test est **inconclusif** (il faut utiliser un autre critère).

**Exemple** : La série géométrique \( \sum_{n=0}^{\infty} q^n \) avec \( |q| < 1 \) est convergente. En appliquant le test de d'Alembert, on trouve que \( \frac{q^{n+1}}{q^n} = q \), et si \( |q| < 1 \), la série converge.

### c) Règle de Cauchy (Critère de convergence)

Le **critère de Cauchy**, ou critère de la racine, permet de déterminer la convergence d'une série en étudiant la limite de la racine n-ième des termes de la série. Ce critère est particulièrement utile lorsque la série a des termes qui deviennent très petits au fur et à mesure que \( n \) augmente.

Le critère se base sur la limite :
\[
L = \lim_{n \to \infty} \sqrt[n]{|u_n|}
\]
- Si \( L < 1 \), la série **converge**.
- Si \( L > 1 \), la série **diverge**.
- Si \( L = 1 \), le critère est **inconclusif** et il faut utiliser un autre test pour déterminer la convergence.

#### Interprétation :
Le critère de Cauchy dit que si, en prenant la racine n-ième des termes \( u_n \), ceux-ci deviennent de plus en plus petits et tendent vers une valeur inférieure à 1, la série converge. Si les termes ne décroissent pas assez vite (c'est-à-dire que \( L > 1 \)), la série diverge.

---
---

## 5. Séries de référence

### a) Série géométrique

La série géométrique est de la forme :
\[
S = \sum_{n=0}^{\infty} q^n
\]
Elle converge si \( |q| < 1 \), et sa somme est donnée par :
\[
S = \frac{1}{1 - q}.
\]

**Exemple** : Si \( q = \frac{1}{2} \), la série géométrique \( \sum_{n=0}^{\infty} \left(\frac{1}{2}\right)^n \) converge vers 2.

### b) Série de Riemann

La série de Riemann est de la forme :
\[
S = \sum_{n=1}^{\infty} \frac{1}{n^p}
\]
Elle converge si et seulement si \( p > 1 \). Pour \( p = 2 \), c'est la célèbre **série des carrés inverses**.

**Exemple** : La série harmonique \( \sum_{n=1}^{\infty} \frac{1}{n} \) diverge car \( p = 1 \).

---

## 6. Exemples de convergence et divergence

### a) Série harmonique

La **série harmonique** \( \sum_{n=1}^{\infty} \frac{1}{n} \) est un exemple classique de série divergente, même si les termes tendent vers 0.

### b) Série géométrique

La série géométrique avec \( |q| < 1 \) converge. Par exemple :
\[
\sum_{n=0}^{\infty} \left(\frac{1}{2}\right)^n = 2.
\]

### c) Série alternée

La série alternée \( \sum_{n=1}^{\infty} \frac{(-1)^n}{n} \) converge par le critère de Leibniz.

---

### Rappels sur les Puissances

\[
a^m \times a^n = a^{m+n}
\]
\[
\frac{a^m}{a^n} = a^{m-n}
\]
\[
(a^m)^n = a^{m \times n}
\]
\[
(a \times b)^n = a^n \times b^n
\]
\[
\left(\frac{a}{b}\right)^n = \frac{a^n}{b^n}
\]
\[
a^b = e^{b \cdot \ln(a)}
\]
\[
\sqrt[n]{a} = a^{\frac{1}{n}}
\]

### Suites équivalentes:

\[
\sin(u_n) \sim u_n
\]
\[
\cos(u_n)-1 \sim \frac{-u_n^2}{2}
\]
\[
\tan(u_n) \sim u_n
\]
\[
\ln(1 + u_n) \sim u_n
\]
\[
e^{u_n} - 1 \sim u_n
\]
\[
(1 + u_n)^p \sim 1 + p u_n
\]

### Croissances comparées:
- **Condition** : \( a > 0 \)
\[
\ln(n) \ll n^a
\]
- **Condition** : \( a > 1 \)
\[
n^a \ll a^n
\]
- **Condition** : \( a > 0 \)
\[
a^n \ll n!
\]
\[
n! \ll n^n
\]
- **Condition** : \( a > 0 \), \( b > 0 \)
\[
ln(n)^b \ll n^a
\]
- **Condition** : \( 1 < a < b \)
\[
a^n \ll b^a
\]
- **Condition** : \( a < b \)
\[ 
a^n \ll b^a 
\]