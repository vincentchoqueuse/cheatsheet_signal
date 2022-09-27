Introduction
============

Un filtre permet de "sculpter" un signal en supprimant ou en accentuant certaines composantes fréquentielles. 
Alors que les filtres analogiques reposent sur la conception de circuits électroniques, les filtres numériques sont souvent plus simples à mettre en oeuvre car ils reposent sur des algorithmes pouvant être codés dans n'importe quel langage de programmation. 

Dans cette section, nous allons nous intéresser à la synthèse de filtres numériques linéaires et invariants dans le temps (LTI) à une entrée et une sortie (SISO). Ces filtres sont couramment utilisés dans un large panel d'applications. 

Modélisation
------------

Un filtre numérique SISO peut être modélisé par une transformation (ou un opérateur) prenant en entrée un signal numérique et renvoyant en sortie un signal numérique. 

Mathématiquement, un signal numérique est représenté par une suite de nombres où le :math:`n^{ieme}` nombre de la suite est noté :math:`x[n]` (:math:`n \in \mathbb{Z}`). Le lien entre l'entrée et la sortie peut être décrit par 

.. math ::

    y[n] = T\{x[n]\}

* :math:`x[n]`: :math:`n^{ieme}` entrée du filtre, 
* :math:`y[n]`: :math:`n^{ieme}` sortie du filtre,
* :math:`T\{.\}`: opérateur décrivant le filtre.

Dans ce document, nous allons nous intéresser à la classe des filtres dits linéaires et invariant dans le temps (LTI). 

Définitions 
```````````

Un filtre LTI respecte les deux propriétés suivantes:

* Linéarité: Si l'entrée du filtre est égale à :math:`x[n]=\alpha x_1[n]+\beta x_2[n]`, alors la sortie sera égale à :math:`y[n]=\alpha y_1[n]+\beta y_2[n]`.
* Invariance dans le temps: Si l'entrée du filtre est égale à :math:`x[n]=x_1[n-\tau]` (:math:`\tau \in \mathbb{Z}`), alors la sortie sera égale à :math:`y[n]=y_1[n-\tau]`.

Un filtre LTI peut être entièrement décrit par sa réponse à une entrée de type impulsion. Cette réponse est appelée réponse impulsionnelle et est notée :math:`h[n]` où 

.. math ::

    h[n]=T\{\delta[n]\}.

Propriétés 
``````````

Lorsqu'un signal :math:`x[n]` est envoyé à l'entrée d'un filtre LTI, la sortie s'exprime sous la forme

.. math ::

    y[n]=h[n] * x[n] \triangleq \sum_{k=-\infty}^{\infty}x[k]h[n-k]

* :math:`*` désigne le produit de convolution,
* :math:`h[n]=T\{\delta[n]\}` correspond à la réponse impulsionnelle du filtre.

Equation de récurrence
``````````````````````

Une grande partie des filtres LTI peut s'exprimer à partir d'une équation de récurrence à coefficients constants

.. math ::
    
    y[n]=\sum_{m=0}^{M}b_m x[n-m]-\sum_{l=1}^{L}a_l y[n-l]

* les coefficients réels :math:`b_m` (:math:`m=0,\cdots,M`) correspondent aux coefficients de la partie non récursive du filtre,
* les coefficients réels :math:`a_l` (:math:`l=1,\cdots,L`) correspondent respectivement aux coefficients de la partie récursive du filtre. 

Notons que le coefficient multipliant :math:`y[n]` est implicitement égal à :math:`a_0=1`. 
L'ordre du filtre est défini comme étant la plus grande valeur entre :math:`M` et :math:`L`. 

La réponse impulsionnelle d'un filtre décrit par une équation de récurrence peut s'obtenir en posant :math:`x[n]=\delta[n]` et en calculant les échantillons de sortie les uns après les autres à partir de l'équation de récurrence.
En fonction des coefficients :math:`a_k`, il est alors possible de définir deux grandes catégories de filtres:

* les filtres à Réponse Impulsionnelle Finie (FIR) pour lesquels :math:`a_l=0` pour tout :math:`l>0`,
* les filtres à Réponse Impulsionnelle Infinie (IIR) pour lesquels il existe au moins une valeur de :math:`l` (:math:`l>0`) telle que :math:`a_l\ne 0`.

Problématiques 
--------------

Dans les sous-sections suivantes, nous allons traiter les problématiques suivantes.

* Connaissant la valeur des coefficients :math:`b_m` et :math:`a_l`, est-il possible de comprendre l'effet d'un filtre sur une entrée quelconque :math:`x[n]`  ? 
* Est-il possible de déterminer les coefficients :math:`b_m` et :math:`a_l` d'un filtre à partir d'un ensemble de spécifications (fréquentielles ou temporelles) ?

