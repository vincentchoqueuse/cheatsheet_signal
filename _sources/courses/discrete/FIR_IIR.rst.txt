Filtres FIR et IIR 
==================

Classification
--------------

Filtre FIR
++++++++++

Un filtre FIR (Finite Impulse Response) peut être décrit par :

.. math ::
    
    y[n]=\sum_{m=0}^{M}b_m x[n-m]

Ce type de filtre est dit fini, car sa réponse impulsionnelle se stabilisera ultimement à zéro. 
Un filtre FIR est non récursif, c'est-à-dire que la sortie dépend uniquement de l'entrée du signal, il n'y a pas de contre-réaction. 

Propriétés
``````````

* Les coefficients du filtre  sont égaux à la réponse impulsionnelle du filtre c-à-d :math:`b[n]=h[n]`. 
* La sortie du filtre est donnée par la convolution du signal d'entrée avec les coefficients (ou réponse impulsionnelle) du filtre c-à-d :math:`y[n] = b[n]*x[n]`.


Filtre IIR 
++++++++++

Un filtre IIR (Infinite Impulse Response) peut être décrit par :

.. math ::
    
    y[n]=\sum_{m=0}^{M}b_m x[n-m]-\sum_{l=1}^{L}a_l y[n-l]

Propriétés
``````````

La réponse impulsionnelle d'un filtre IIR ne s'annule jamais définitivement. Ce type de filtre est récursif car la sortie dépend à la fois du signal d'entrée et du signal de sortie. Nous parlons également de la présence d'une boucle de contre-réaction (feedback). 
Les filtres IIR sont principalement synthétisés en numérisant des filtres analogiques (Butterworth, Tchebychev, Bessel, Elliptique).

Implémentation
++++++++++++++

.. code ::

    from scipy.signal import dlti

    # fir 
    b_fir = [0.3, 0.1, 0.02]
    H_fir = dlti(b_fir, 1)

    # iir 
    b_iir = [0.3, 0.1, 0.02]
    a_iir = [1, -0.5, 0.1]
    H_iir = dlti(b_fir, a_iir)


Comparaison
-----------

.. list-table::
   :widths: 33 33 33
   :header-rows: 1

   * - Propriété
     - FIR
     - IIR
   * - Partie récursive
     - Non 
     - Oui
   * - Présence de pôles 
     - Non
     - Oui
   * - Stabilité
     - Oui
     - Oui si :math:`|p_l|<1`
   * - Phase linéaire
     - Oui si :math:`b_m=b_{M-k}`
     - Non

Le tableau montre que les filtres FIR semblent posséder moins d'inconvénients que les filtres IIR. Néanmoins, pour un même ordre N, les filtres IIR 
permettent généralement d'obtenir des pentes nettement plus importantes au niveau de la réponse fréquentielle. Pour un gabarit fréquentiel donné, l'implémentation
d'un filtre IIR présentera donc une complexité calculatoire plus faible.
