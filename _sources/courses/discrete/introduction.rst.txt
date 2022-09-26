Introduction
============



Un filtre permet de "sculpter" un signal en supprimant ou en accentuant certaines composantes fréquentielles. 
Alors que les filtres analogiques reposent sur la conception de circuits électroniques, les filtres numériques eux sont souvent plus simples à mettre en oeuvre car ils reposent sur des algorithmes pouvant être codés dans n'importe quel langage de programmation 
(même si le C reste la norme pour les applications embarquées). Dans cette section, nous allons nous intéresser à la synthèse de filtres numériques à une entrée et une sortie. Ces filtres sont couramment utilisés dans un large panel d'applications. 

Modélisation
------------

Un filtre numérique peut être modélisé par une fonction mathématique prenant en entrée un signal numérique et renvoyant en sortie un signal numérique. 

Mathématiquement, un signal numérique est représenté par une suite de nombres où le :math:`n^{ieme}` nombre de la suite est noté :math:`x[n]` (:math:`n \in \mathbb{Z}`).

Dans ce document, nous allons nous intéresser à la classe des filtres dits linéaires et invariant dans le temps (LTI). 

Définitions 
```````````

Un filtre LTI respecte les deux propriétés suivantes:

* Linéarité: Si l'entrée du filtre est égale à :math:`x[n]=\alpha x_1[n]+\beta x_2[n]`, alors la sortie sera égale à :math:`y[n]=\alpha y_1[n]+\beta y_2[n]`.
* Invariance dans le temps: Si l'entrée du filtre est égale à :math:`x[n]=x_1[n-\tau]` (:math:`\tau \in \mathbb{Z}`), alors la sortie sera égale à :math:`y[n]=y_1[n-\tau]`.

Un filtre LTI est entièrement décrit par sa réponse à une entrée de type impulsion (:math:`x[n]=\delta[n]`). La réponse à une entrée de type impulsion est appelée réponse impulsionnelle et est notée :math:`h[n]`. 

Propriétés 
``````````

Lorsqu'un signal :math:`x[n]` est envoyé à l'entrée d'un filtre LTI, la sortie s'exprime sous la forme

.. math ::

    y[n]=x[n]*h[n] \triangleq \sum_{k=-\infty}^{\infty}x[k]h[n-k]


où :math:`*` désigne le produit de convolution et :math:`h[n]` correspond à la réponse impulsionnelle du filtre.

Equation aux différences 
````````````````````````

Une grande partie des filtres LTI peut s'exprimer à partir d'une équation aux différences

.. math ::
    
    y[n]=\sum_{m=0}^{M}b_m x[n-m]-\sum_{l=1}^{L}a_l y[n-l]

* les coefficients réels :math:`b_m` (:math:`m=0,\cdots,M`) correspondent aux coefficients de la partie non récursive du filtre,
* les coefficients réels :math:`a_l` (:math:`l=1,\cdots,L`) correspondent respectivement aux coefficients de la partie récursive du filtre. 

Notons que le coefficient multipliant :math:`y[n]` est implicitement égal à :math:`a_0=1`. 
L'ordre du filtre est défini comme étant la plus grande valeur entre :math:`M` et :math:`L`. 

La réponse impulsionnelle d'un filtre décrit par une équation aux différences s'obtient en posant :math:`x[n]=\delta[n]`
dans l'équation aux différences. En fonction des coefficients :math:`a_k`, il est alors possible de définir deux grandes catégories de filtres:

* les filtres à Réponse Impulsionnelle Finie (FIR) pour lesquels :math:`a_l=0` pour tout :math:`l>0`,
* les filtres à Réponse Impulsionnelle Infinie (IIR) pour lesquels il existe au moins une valeur de :math:`l` (:math:`l>0`) telle que :math:`a_l\ne 0`.

Problématiques 
--------------

Dans les pages suivantes, nous allons traiter les problématiques suivantes.

* Connaissant la valeur des coefficients :math:`b_m` et :math:`a_l`, est-il possible de comprendre l'effet d'un filtre sur une entrée quelconque :math:`x[n]``  ? 
* Est-il possible de déterminer les coefficients :math:`b_m` et :math:`a_l` d'un filtre à partir d'un ensemble de spécifications (fréquentielles ou temporelles) ?

