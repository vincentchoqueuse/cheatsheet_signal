Filtres FIR et IIR 
==================

Contexte
--------

Modélisation
++++++++++++

Filtre FIR
``````````

.. math ::
    
    y[n]=\sum_{m=0}^{M}b_m x[n-m]



Filtre IIR 
``````````

.. math ::
    
    y[n]=\sum_{m=0}^{M}b_m x[n-m]-\sum_{l=1}^{L}a_l y[n-l]


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


Propriétés 
----------

.. list-table:: Comparaison des filtres FIR et IIR
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

Le tableau montre que les filtres FIR possèdent moins d'inconvénients que les filtres IIR. Néanmoins, pour un même ordre N, les filtres IIR 
permettent généralement d'obtenir au niveau de la réponse fréquentielle des pentes nettement plus importantes. Pour un gabarit fréquentiel donné, l'implémentation
d'un filtre IIR présentera donc une complexité calculatoire moindre.
