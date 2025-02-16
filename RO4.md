# **RO4: Intégrales**

## **Définition**  

Une intégrale définie est une somme continue permettant de calculer l’aire sous une courbe :  

\[
I = \int_{a}^{b} f(x) \,dx
\]

- **\( a \) et \( b \)** : bornes d’intégration  
- **\( f(x) \)** : fonction à intégrer  
- **\( dx \)** : élément infinitésimal de la variable  

Les intégrales se notent de cette manière, avec **\( f(x) \) la fonction à intégrer** et **\( F(x) \) sa primitive**.

\[
\int_{a}^{b} f(x) \, dx = [F(x)]_{a}^{b}
\]

---

## **1. Intégrales Classiques**  

| Fonction | Primitive |
|----------|-----------|
| \( \int x^n \,dx \) | \( \frac{x^{n+1}}{n+1} \) si \( n \neq -1 \) |
| \( \int e^x \,dx \) | \( e^x \) |
| \( \int \frac{1}{x} \,dx \) | \( \ln |x| \) |
| \( \int \cos(x) \,dx \) | \( \sin(x) \) |
| \( \int \sin(x) \,dx \) | \( -\cos(x) \) |
| \( \int \frac{1}{1+x^2} \,dx \) | \( \arctan(x) \) |
| \( \int \frac{1}{\sqrt{1-x^2}} \,dx \) | \( \arcsin(x) \) |

---

## **Intégration par Parties (IPP)**  

### **Formule Générale**  

\[
\int_{a}^{b} u v' \,dx = [u v]_{a}^{b} - \int_{a}^{b} u'v \,dx
\]

avec :  

- \( u \) : fonction choisie qui devient plus simple après dérivation  
- \( v' \) : fonction facile à intégrer  

### **Exemple**  

Calculer \( I = \int_{0}^{1} x (e^x+e^{-x}) \,dx \).  

1. Choisir \( u = x \) et \( v' = e^x+e^{-x} \), alors on pose:
\[
\left\{
\begin{array}{ll}
    u = x, & u' = 1 \\
    v' = e^x+e^{-x}, & v = e^x-e^{-x}
\end{array}
\right.
\]

2. Appliquer la formule :  
    \[
    I = [u v]_{a}^{b} - \int_{a}^{b} u'v \,dx
    \]

    \[
    I = [x (e^x-e^{-x})]_{0}^{1} - \int_{0}^{1} 1(e^x-e^{-x}) \,dx
    \]

    \[
    I = [x (e^x-e^{-x}) - e^x-e^{-x}]_{0}^{1}
    \]

3. Remplacer \( x \) par 1 et 0 dans l'expression :
    \[
    I = \left[ 1 (e^1 - e^{-1}) - (e^1 - e^{-1}) \right] - \left[ 0 (e^0 - e^0) - (e^0 - e^0) \right]
    \]

4. Simplification :
    \[
    I = 2 - \frac{2}{e}
    \]

---

## **3. Changement de Variable**  

### **Formule Générale**  

Si \( x = g(t) \), alors :

\[
dx = g'(t) dt
\]

et l’intégrale devient :

\[
\int f(x) \,dx = \int f(g(t)) g'(t) \, dt
\]

### **Exemple**  

Calculer \( I = \int_{0}^{1} \frac{2x}{1 + x^2} \,dx \).  

1. **Poser le changement de variable :**  
On choisit \( u = 1 + x^2 \), donc on pose:
\[
\left\{
\begin{array}{ll}
    u = 1 + x^2 \\
    u' = 2x\,dx
\end{array}
\right.
\]

On applique u sur les 2 bornes.
\[
\left\{
\begin{array}{ll}
    \text{Quand } x = 0 & u = 1 + 0^2 = 1 \\
    \text{Quand } x = 1 & u = 1 + 1^2 = 2
\end{array}
\right.
\]

2. **Transformer l'intégrale :**  
   Etant donné que \( u' = 2x \,dx \), on observe que l'on peut écrire :  

   \[
   I = \int_{1}^{2} \frac{u'}{u}
   \]

3. **Calculer l'intégrale :**  
On sait que 
   \[
   (\ln(u))' = \frac{u'}{u}
   \]
Donc la primitive est `ln(u)`, ainsi:
   \[
   I = [\ln(u)]_{1}^{2}
   \]

   \[
   I = \ln(2) - \ln(1)
   \]

   \[
   I = \ln(2) - \ln(1)
   \]
   Puisque \( \ln 1 = 0 \), on a :  
   \[
   I = \ln 2
   \]

### **Exemple 2**  

Calculer \( I = \int_{0}^{\frac{\pi}{2}} \sin^3 t \cos t \, dt \).  

1. **Poser le changement de variable :**  
On choisit \( u = \sin t \), donc on pose :
\[
\left\{
\begin{array}{ll}
    u = \sin t \\
    u' = \cos t \, dt
\end{array}
\right.
\]

On applique \( u \) sur les bornes :
\[
\left\{
\begin{array}{ll}
    \text{Quand } t = 0, & u = \sin 0 = 0 \\
    \text{Quand } t = \frac{\pi}{2}, & u = \sin \frac{\pi}{2} = 1
\end{array}
\right.
\]

2. **Transformer l'intégrale :**  
   Étant donné que \( u' = \cos t \, dt \), on observe que l'on peut écrire :  

   \[
   I = \int_{0}^{1} u^3 \, du
   \]

3. **Calculer l'intégrale :**  
   On utilise la formule de l'intégration des puissances :

   \[
   \int u^n \, du = \frac{1}{n+1} u^{n+1}
   \]


   \[
   I = \left[ \frac{1}{4}u^{4} \right]_{0}^{1}
   \]

4. **Remplacer les bornes :**  
   \[
   I = \frac{1^4}{4} - \frac{0^4}{4}
   \]

   \[
   I = \frac{1}{4} - 0
   \]

   \[
   I = \frac{1}{4}
   \]

---

## **Résumé des Méthodes**  

| Méthode | Quand l'utiliser ? | Étapes clés |
|---------|--------------------|-------------|
| **Intégrales classiques** | Fonction simple ou directe | Utiliser les formules courantes |
| **Intégration par parties (IPP)** | Produit de fonctions (\( x e^x, x \ln x, x \sin x \)) | Choisir \( u \) et \( v' \), appliquer la formule |
| **Changement de variable** | Présence de \( (1+x^2) \), \( (1-x^2) \), \( e^x \), \( \sqrt{x} \), etc. | Poser \( u = g(x) \), dériver \( du \), transformer l’intégrale |

