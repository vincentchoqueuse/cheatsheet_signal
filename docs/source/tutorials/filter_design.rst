Synthèse d'un Filtre Numérique
==============================

Ce tutorial montre comment implémenter un filtre numérique. 

Cahier des charges
------------------

Le cahier des charges du filtre est spécifié ci-dessous :

* Fréquence de coupure: 4 kHz,
* Fréquence d'échantillonnage: 44.1 kHz,
* Type: Passe-bas, 
* Ordre: 4.

Synthèse de filtre
------------------

Dans ce tutorial, nous allons utiliser la technique de synthèse de Butterworth.

.. note :: 

    Documentation: https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.butter.html


.. plot::
    :context: close-figs
    :include-source:

    from scipy import signal
    import matplotlib.pyplot as plt

    Fe = 44100
    b, a = signal.butter(4, 4000, fs=Fe)

    # affichage de la reponse frequentielle
    w, h = signal.freqz(b, a, fs=Fe)
    plt.semilogx(w, 20 * np.log10(abs(h)))
    plt.xlabel('Frequence [Hz]')
    plt.ylabel('Amplitude [dB]')
    plt.axvline(4000, color='green')
    plt.axhline(-3, color='green')
    plt.ylim([-60, 10])
    plt.grid()


En utilisant la fonction :code:`butter`, nous obtenons les coefficients du filtres ci-dessous :

.. code ::

    b = [0.00345416, 0.01381663, 0.02072494, 0.01381663, 0.00345416]
    a = [1., -2.5194645 ,  2.56083711, -1.20623537,  0.22012927]


Simulation
----------

Pour vérifier le bon comportement du filtre, le script suivant montre l'allure de la sortie lorsqu'une sinusoïde de 4kHz est envoyé en entrée du filtre.
Nous observons bien une réduction de l'amplitude de -3dB lorsque la fréquence est égale à la fréquence de coupure du filtre.

.. plot::
    :context: close-figs
    :include-source:

    from scipy.signal import lfilter
    import numpy as np
    import matplotlib.pyplot as plt

    Fe = 44100

    # generation du signal d'entrée
    t = np.arange(0, 0.005, 1/Fe)
    x = np.sin(2*np.pi*4000*t)

    # filtrage
    b = [0.00345416, 0.01381663, 0.02072494, 0.01381663, 0.00345416]
    a = [1., -2.5194645 ,  2.56083711, -1.20623537,  0.22012927]
    y = lfilter(b, a, x)

    # affichage de la sortie du filtre
    plt.plot(t, x, label="input")
    plt.plot(t, y, label="output")
    plt.xlabel('Temps [s]')
    plt.xlim([0, 0.005])
    plt.grid()
    plt.legend()