Analyse de filtres
==================

Une grande partie des filtres LTI peut s'exprimer à partir d'une équation aux différences

.. math ::
    
    y[n]=\sum_{m=0}^{M}b_m x[n-m]-\sum_{l=1}^{L}a_l y[n-l]


Dans cette section, nous allons introduire les outils nécessaires pour analyser ce type de filtre.

Transformée en Z
----------------

Définition 
``````````

La transformée en :math:`\mathcal{Z}` d'une suite numérique :math:`x[n]`` est définie par l'équation

.. math ::

    X(z) \triangleq \sum_{n=-\infty}^{\infty}x[n]z^{-n}

où :math:`z` est une variable complexe.

Il est important de noter que la transformée de 2d'un signal ne converge pas nécessairement pour toutes les valeurs :math:`z \in \mathbb{Z}`.
Il est alors nécessaire de préciser la région de convergence (ROC) pour laquelle la série converge c-à-d les valeurs de :math:`z`` telles que :math:`|X(z)|<\infty`. 

Tables des transformées 
```````````````````````

A titre d'illustration, le tableau suivant présente les transformées en Z de plusieurs signaux et leurs regions de convergence associées.

.. list-table:: Quelques transformées en Z
   :widths: 33 33 33
   :header-rows: 1

   * - Signal 
     - Transformée en Z 
     - ROC
   * - :math:`\delta[n]`
     - :math:`1`
     - :math:`z \in \mathbb{Z}`
   * - :math:`u[n]`
     - :math:`\frac{1}{1-z^{-1}}`
     - :math:`|z| > 1`
   * - :math:`\delta[n-m]`
     - :math:`z^{-m}`
     - :math:`z \ne 0`
   * - :math:`à^n u[n]`
     - :math:`\frac{1}{1-az^{-1}}`
     - :math:`|z| > |à|`
   * - :math:`na^n u[n]`
     - :math:`\frac{az^{-1}}{(1-az^{-1})^2}`
     - :math:`|z| > |à|`
   * - :math:`\cos (\omega_0 n)u[n]`
     - :math:`\frac{1-\cos(\omega_0)z^{-1}}{1-2\cos(\omega_0)z^{-1}+z^{-2}}`
     - :math:`|z| > 1`
   * - :math:`\sin (\omega_0 n)u[n]`
     - :math:`\frac{\sin(\omega_0)z^{-1}}{1-2\cos(\omega_0)z^{-1}+z^{-2}}`
     - :math:`|z| > 1`
   * - :math:`r^n\cos (\omega_0 n)u[n]`
     - :math:`\frac{1-r\cos(\omega_0)z^{-1}}{1-2r\cos(\omega_0)z^{-1}+r^2z^{-2}}`
     - :math:`|z| > r`
   * - :math:`r^n\sin (\omega_0 n)u[n]`
     - :math:`\frac{r\sin(\omega_0)z^{-1}}{1-2r\cos(\omega_0)z^{-1}+r^2z^{-2}}`
     - :math:`|z| > r`

Propriétés 
``````````

La transformée en 2 possède les propriétés suivantes (les réciproques étant également vraies):

* Linéarité: Si :math:`y[n]=\alpha x_1[n]+\beta x_2[n]`, alors :math:`Y(z)=\alpha X_1(z)+\beta X_2(z)`.
* Décalage temporel: Si :math:`y[n]=x[n-m]` (:math:`m \in \mathbb{Z}`), alors :math:`Y(z)=X(z)z^{-m}`.
* Multiplication par une fonction exponentielle: Si :math:`y[n]= à^n x[n]`, alors :math:`Y(z)=X(z/à)`.
* Convolution: Si :math:`y[n]= h[n]*x[n]`, alors :math:`Y(z)=H(z)X(z)`.
* Théorème de la valeur finale: :math:`\lim_{n\to \infty} x[n]=\lim_{z\to 1}(z-1)X(z)`.


La propriété liée au décalage temporel indique qu'un retard d'un échantillon dans le domaine temporel revient à multiplier la transformée en Z par :math:`z^{-1}`.
En utilisant cette propriété, l'équation aux différences peut être représentée graphiquement par un schéma bloc où les blocs de fonction de transfert :math:`z^{-1}` introduisent un retard d'un échantillon. 
A titre d'exemple, la figure suivante présente le schéma bloc du filtre 1.


La propriété liée à la convolution montre l'importance de la transformée en Z de la réponse impulsionnelle, :math:`H(z)`.
Cette transformée en Z est appelée fonction de transfert du filtre. 

Fonction de transfert 
---------------------

La fonction de transfert d'un filtre correspond à la transformée en Z de sa réponse impulsionnelle c-à-d

.. math ::

    H(z) =\sum_{n=-\infty}^{\infty}h[n]z^{-n}

La propriété liée à la convolution montre que la fonction de transfert d'un filtre s'exprime également sous la forme :math:`H(z)=Y(z)/X(z)`.
Pour un filtre décrit par une équation aux différences, cette propriété permet d'exprimer la fonction de transfert du filtre en fonction des coefficients des parties récursive :math:`a_l` et non-recursive :math:`b_m`` du filtre.

Forme polynomiale 
`````````````````

La fonction de transfert d'un filtre numérique décrit par une équation aux différences s'exprime sous la forme:

.. math ::

    H(z)=\frac{B(z)}{A(z)}=\frac{\sum_{m=0}^{M}b_m z^{-m}}{\sum_{l=0}^{L}a_l z^{-l}}

Exemple 
```````
Considérons le filtre décrit par l'équation de récurrence suivante :

.. math ::

        y[n]=0.065x[n]+0.13 x[n-1]+0.065x[n-2])+1.143y[n-1]-0.413y[n-2]

Il est possible de montrer que la fonction de transfert de ce filtre est donnée par 

.. math ::

    H(z)=\frac{0.065+0.13 z^{-1}+0.065z^{-2}}{1-1.143z^{-1}+0.413z^{-2}}.

Par exemple, si l'entrée du filtre est un échelon unitaire, la transformée en Z de la sortie sera égale à 
:math:`Y(z)=H(z)/(1-z^{-1})`. En utilisant le théorème de la valeur finale, nous pouvons alors anticiper qu'en temporel 
la valeur finale sera égale à :math:`\lim_{n\to\infty}y[n]=H(1)=0.962`. La figure suivante présente la réponse du filtre 1 
lorsqu'un échelon unitaire est envoyé en entrée. Nous pouvons constater qu'effectivement la valeur finale est bien égale à :math:`0.962`.

.. plot::
    :context: close-figs
    :include-source:

    from scipy.signal import dlti
    import matplotlib.pyplot as plt

    num = [0.065, 0.13, 0.065]
    den = [1, -1.143, 0.413]
    H = dlti(num, den)
    n, y = H.step()

    # affichage de la reponse indicielle
    plt.step(n, np.squeeze(y))
    plt.axhline(y=0.962, color="r", linestyle="--")
    plt.grid()
    plt.xlabel("n")
    plt.ylabel("Réponse Indicielle")
    plt.xlim([-1, 50])

Forme factorisée 
````````````````

La fonction de transfert :math:`H(z)` peut présenter des "pics" et des "vallées" pour certaines valeurs de :math:`z`.
Pour mettre en évidence ces comportements singuliers, il est possible de réexprimer la fonction de transfert sous une forme factorisée. 

La forme factorisée donne explicitement les valeurs de :math:`z`` pour lesquelles :math:`H(z)` tend vers 0 (zéros) 
et les valeurs de :math:`z` pour lesquelles :math:`H(z)`` tend vers l'infini (pôles). 

.. math ::
    
    H(z)=\left(\frac{b_0}{a_0}\right)\frac{\prod_{m=1}^{M}(1-z_m z^{-1})}{\prod_{l=1}^{L}(1-p_l z^{-1})}

* les valeurs :math:`z_m` correspondent respectivement aux zéros de la fonction de transfert,
* les valeurs :math:`p_l` correspondent respectivement aux pôles de la fonction de transfert.

En pratique, les valeurs des pôles et des zéros s'obtiennent le plus souvent en utilisant des algorithmes numériques.
A titre d'illustration, la fonction Python :code:`root` permet d'établir que le filtre 1 possède un zéro double en :math:`z=-1` et deux pôles complexes conjugués en :math:`z=0.57\pm 0.29j`.
Notons que comme les coefficients :math:`a_l` et :math:`b_m` sont réels, les pôles et zéros complexes sont nécessairement réels ou complexe-conjugués. 

Il est courant de représenter la localisation des pôles et des zéros dans le plan complexe. Par convention, les pôles sont indiqués avec un :math:`\times` et les zéros avec un :math:`\circ`.
La figure suivante présente la localisation des pôles et des zéros pour le filtre 1.

.. plot::
    :context: close-figs
    :include-source:

    from scipy.signal import dlti
    import matplotlib.pyplot as plt

    num = [0.065, 0.13, 0.065]
    den = [1, -1.143, 0.413]
    H = dlti(num, den)
    poles = H.poles
    zeros = H.zeros

    # affichage des poles et zeros
    plt.plot(np.real(zeros), np.imag(zeros),"o", label="zeros")
    plt.plot(np.real(poles), np.imag(poles),"x", label="poles")
    plt.grid()
    plt.axis("equal")
    plt.legend()
    plt.xlim([-2, 2])
    plt.xlabel("Real Part")
    plt.ylabel("Imag part")

Stabilité 
---------

La localisation des pôles joue un rôle de premier plan sur la propriété de stabilité du filtre. De manière formelle, un filtre est dit stable si sa réponse impulsionnelle est absolument sommable c-à-d 

.. math :: 
    
    \sum_{n=-\infty}^{\infty}|h[n]|<\infty

Propriété 
`````````

Un filtre est stable si tous les pôles de sa fonction de transfert sont inclus dans le cercle de rayon unité c-à-d si pour tout :math:`l`` 

.. math ::

    |p_l|\le 1

Exemple 
```````

La figure suivtante présente la localisation des pôles et des zéros ainsi que la réponse impulsionnelle de deux filtres IIR. 


.. plot::
    :context: close-figs
    :include-source:

    from scipy.signal import dlti
    import matplotlib.pyplot as plt

    # enter zero pole gain transfert function
    H1 = dlti([1, -0.75], [-0.5, 0.2+0.3j, 0.2-0.3j], 5)
    H2 = dlti([1, -0.75], [-0.5, 1.2+0.3j, 1.2-0.3j], 5)
    H_list = [H1, H2]

    plt.figure()

    for index, H in enumerate(H_list):
        
        # affichage des poles et zeros
        ax1 = plt.subplot(2, 2, 1+2*index)
        plt.plot(np.real(H.zeros), np.imag(H.zeros),"o")
        plt.plot(np.real(H.poles), np.imag(H.poles),"x")
        plt.grid()
        plt.axis("equal")
        plt.xlim([-2, 2])
        plt.xlabel("Real Part")
        plt.ylabel("Imag part")

        # affichage de la reponse impulsionnelle
        n, y = H.impulse(n=80)
        ax2 = plt.subplot(2, 2, 2+2*index)
        plt.step(n, np.squeeze(y))
        plt.grid()
        plt.xlim([0, 80])
        plt.xlabel("n")
        plt.ylabel("Réponse Indicielle")

    plt.tight_layout()
        
* Le premier filtre est stable car tous ses pôles sont inclus dans le cercle de rayon unité. 
* Le second filtre est instable car il possède deux pôles pour lesquels le module est supérieur à 1. Pour ce second filtre, nous constatons que la réponse impulsionnelle semble tendre vers des valeurs infinies ( :math:`10^8` !)

Analyse Fréquentielle 
---------------------

Le domaine fréquentielle est très utilisé pour analyser le comportement des filtres LTI. 
Le succès de ce domaine d'analyse est principalement lié au fait que la réponse d'un filtre à une exponentielle complexe de pulsation :math:`\omega`
est une exponentielle complexe de même pulsation mais multipliée par un coefficient complexe. 
Ce coefficient multiplicateur s'obtient à partir de la transformée de Fourier de la réponse impulsionnelle.

Transformée de Fourier discrète
+++++++++++++++++++++++++++++++


Définition 
``````````

Une suite numérique :math:`x[n]` peut se décomposer sous la forme 

.. math ::

    x[n]= \frac{1}{2\pi}\int_{-\pi}^{\pi} X(e^{j\omega})e^{j\omega n}d\omega

* la quantité :math:`X(e^{j\omega})` correspond à la transformée de Fourier (à temps discret) de :math:`x[n]`. La transformée de Fourier est définie par

.. math ::

    X(e^{j\omega})\triangleq \sum_{n=-\infty}^{\infty}x[n]e^{-j\omega n}.

Propriétés
``````````

* La transformée de Fourier d'un signal s'obtient en évaluant sa transformée en Z sur le cercle de rayon unité c-à-d :math:`z=e^{j\omega}`.
* Comme :math:`X(e^{j\omega})=X(e^{j(\omega+2k\pi)})` (:math:`k \in \mathbb{Z}`), la transformée de Fourier à temps discret est :math:`2\pi`-périodique. De plus lorsque :math:`x[n]\in \mathbb{R}`, il est possible de démontrer que :math:`X(e^{j\omega})=X^{*}(e^{-j\omega})`` (symétrie hermitienne). Pour ces deux raisons, la transformée de Fourier est couramment représentée dans l'intervalle :math:`[0,\pi]`.
* La transformée de Fourier du signal de sortie d'un filtre LTI s'obtient en multipliant la transformée de Fourier de la réponse impulsionnelle du filtre par la transformée de Fourier de l'entrée c-à-d :math:`Y(e^{j\omega})=H(e^{j\omega})X(e^{j\omega})`. La transformée de Fourier de la réponse impulsionnelle est appelée réponse fréquentielle du filtre.

Réponse Fréquentielle 
+++++++++++++++++++++

Définition 
``````````

La réponse fréquentielle d'un filtre correspond à la transformée de Fourier de sa réponse impulsionnelle c-à-d

.. math ::

    H(e^{j\omega})=\sum_{n=-\infty}^{\infty}h[n]e^{-j\omega n}

Représentation
``````````````

La réponse frequentielle :math:`H(e^{j\omega})` est généralement une quantité complexe qu'il est possible de décomposer sous la forme

.. math ::

    H(e^{j\omega})=|H(e^{j\omega})| e^{j Arg[H(e^{j\omega})]},

* :math:`|H(e^{j\omega})|` désigne le module de la réponse fréquentielle,
* :math:`Arg[H(e^{j\omega})]` désigne l'argument de la réponse fréquentielle.

Pour analyser le comportement d'un filtre, il est utile de représenter le module et l'argument de la réponse fréquentielle en fonction de :math:`\omega`.
L'affichage du module et de l'argument permet d'avoir une interprétation concrète de l'effet du filtre sur une entrée quelconque. 
En effet à la pulsation :math:`\omega`, le filtre va appliquer un gain :math:`|H(e^{j\omega})|` et un déphasage (retard) :math:`Arg[H(e^{j\omega})]`.

A titre d'illustration, la figure suivante présente le module et l'argument de la réponse fréquentielle d'un filtre. 

.. plot::
    :context: close-figs
    :include-source:

    from scipy.signal import dlti
    import matplotlib.pyplot as plt

    num = [0.065, 0.13, 0.065]
    den = [1, -1.143, 0.413]
    H = dlti(num, den)
    w, Hjw = H.freqresp()

    # affichage du module
    ax1 = plt.subplot(2, 1, 1)
    plt.plot(w, np.abs(Hjw))
    plt.ylabel("Module $H(e^{j\omega})$")
    plt.grid()
    plt.xlim([0, np.pi])

    ax1 = plt.subplot(2, 1, 2)
    plt.plot(w, np.angle(Hjw))
    plt.xlabel("Pulsation normalisée [rad/sample]")
    plt.ylabel("Argument $Arg[H(e^{j\omega})]$ [deg]")
    plt.grid()
    plt.xlim([0, np.pi])

    plt.tight_layout()


Nous observons ici que le filtre se comporte comme un filtre passe-bas. Lorsque l'argument est égal à :math:`Arg[H(e^{j\omega})]=-\omega \tau`, ce qui n'est pas le cas ici, le filtre est dit **à phase linéaire**. 
En pratique, cette propriété est souvent recherchée car elle évite la présence de distorsion de phase.

Lien avec l'équation aux différences
````````````````````````````````````

Pour les filtres décrits par une équation aux différences, la réponse fréquentielle peut s'exprimer en fonction de la transformée de Fourier des coefficients :math:`a_l` et :math:`b_m` du filtre.
Spécifiquement, nous obtenons :

.. math ::

    H(e^{j\omega})=\frac{Y(e^{j\omega})}{X(e^{j\omega})}=\frac{\sum_{k=0}^{M}b_m e^{-j\omega k}}{\sum_{l=0}^{N}a_l e^{-j\omega l}}=\frac{B(e^{j\omega})}{A(e^{j\omega})}

