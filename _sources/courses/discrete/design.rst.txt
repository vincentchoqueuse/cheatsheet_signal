Synthèse de Filtres
===================


Filtre FIR 
----------

Principe 
++++++++

Considérons le cas où nous souhaitons synthétiser un filtre FIR d'ordre N à phase linéaire dont la réponse fréquentielle est donnée par 

.. math :: 
    
    H_d(e^{j\omega})=|H_d(e^{j\omega})|e^{-j\omega N/2}

Pour obtenir les coefficient du filtre FIR, nous allons procéder de la manière suivante :

* Calcul de la réponse impulsionnelle théorique :math:`h_d[n]`,
* Troncature temporelle de la réponse impulsionnelle pour ne conserver que :math:`N` éléments,
* [optionnel] Application d'une fenêtre de pondération temporelle pour limiter l'effet de la troncature temporelle.

Exemple 
+++++++

Cahier des charges 
``````````````````

Pour illustrer cette partie, nous allons synthétiser le filtre dont le module de la réponse fréquentielle est donné par :

.. math ::

    |H_d(e^{j\omega})|&=\left\{\begin{array}{cl}
    1&\textrm{, pour } |\omega| \le \omega_c\\
    0 &\textrm{, ailleurs}\end{array}\right.

où :math:`\omega_c` désigne la pulsation de coupure normalisée par rapport à la pulsation d'échantillonnage :math:`\omega_e`.

Ce filtre est un filtre passe-bas **en mur de briques** (pente infinie). En imposant une phase linéaire, la 
réponse fréquentielle de ce filtre est donnée par :math:`H_d(e^{j\omega})=|H_d(e^{j\omega})|e^{-j\omega N/2}`

Réponse Impulsionnelle
``````````````````````

La réponse impulsionnelle du filtre s'obtient en utilisant l'expression

.. math ::

    h_d[n]= \frac{1}{2\pi}\int_{-\pi}^{\pi} H(e^{j\omega})e^{j\omega n}d\omega

Après quelques calculs, nous obtenons

.. math ::

    h_d[n] =\frac{\sin\left(\omega_c (n-N/2)\right)}{\pi (n-N/2)}

En pratique, nous allons conserver uniquement N échantillons. La réponse impulsionnelle utilisée s'exprime alors sous la forme 

.. math ::

    h[n] = w[n]h_d[n]

où :math:`w[n]` est une fenêtre de pondération telle que :math:`w[n]=0` si :math:`n<0` ou :math:`n\ge N`. 

Fenêtres de pondération 
```````````````````````


.. list-table::
   :widths: 33 33 33
   :header-rows: 1

   * - Nom
     - Fonction scipy
     - :math:`w[n]`
   * - Rectangulaire
     - :code:`boxcar`
     - :math:`1`
   * - Hamming
     - :code:`hamming`
     - :math:`0.54 - 0.46 cos\left(\frac{2\pi n}{N-1}\right)`
   * - Blackman
     - :code:`blackman`
     - :math:`0.42 - 0.5 cos\left(\frac{2\pi n}{N}\right)+ 0.08 cos\left(\frac{4\pi n}{N}\right)`

.. plot::
    :context: close-figs
    :include-source:

    from scipy.signal import get_window
    import matplotlib.pyplot as plt

    N = 101
    window_name_list = ["boxcar", "hamming", "blackman"]

    for window_name in window_name_list:
        w = get_window(window_name, N)
        plt.plot(w, label=window_name)

    plt.grid()
    plt.xlim([0, N-1])
    plt.legend()

Réponse fréquentielle
`````````````````````

La figure suivante présente l'allure de la réponse fréquentielle obtenue avec les paramètres suivants :

* ordre: :math:`N=101`
* pulsation de coupure : :math:`\omega_c=f_c/F_e` avec `f_c=5000`Hz et `f_e=44100` Hz,
* fenêtre de pondération: :code:`boxcar` ou :code:`hamming` ou :code:`blackman`.

Le script suivant présente l'allure des réponses fréquentielles. Notons que la fenêtre rectangulaire (:code:`boxcar`) ne permet pas d'obtenir 
une attenuation importante dans la bande rejetée à cause de la présence de lobes importants.

.. plot::
    :context: close-figs
    :include-source:

    import numpy as np
    from scipy.signal import freqz, get_window
    import matplotlib.pyplot as plt

    N = 101
    f_c = 5000
    fs = 44100

    w_c = 2*np.pi*(f_c/fs)
    window_name_list = ["boxcar", "hamming", "blackman"]

    n_vect = np.arange(N)
    # be careful to the definition of the sinc function (see documentation)
    h_d = (w_c/np.pi)*np.sinc((w_c/np.pi)*(n_vect-int(N/2)))

    for window_name in window_name_list:
        w = get_window(window_name, N)
        h = w*h_d
        f, Hjw = freqz(h, fs=fs)
        plt.semilogy(f, np.abs(Hjw), label=window_name)
    
    plt.ylabel("Module $H(e^{j\omega})$")
    plt.xlabel("Frequence [Hz]")
    plt.xlim([0, fs/2])
    plt.ylim([10**-6, 10])
    plt.grid()
    plt.legend()
