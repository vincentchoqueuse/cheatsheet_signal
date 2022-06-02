Signaux Analogique
==================

Décomposition en séries de Fourier
----------------------------------

La décomposition en séries de Fourier d'un signal :math:`T_0`-périodique :math:`x(t)` est donnée par 

.. math:: 

    x(t) = \sum_{n=-\infty}^{\infty} c_n e^{2j\pi \frac{n}{T_0}t}


où :math:`c_n` désignent les coefficients de la décomposition en série de Fourier et sont donnés par 

.. math:: 

    c_n = \frac{1}{T_0}\int_{[T_0]} x(t) e^{-2j\pi \frac{n}{T_0}t}dt


Propriétés
++++++++++

* Parseval :

.. math:: 

    \frac{1}{T_0}\int_{[T_0]} |x(t)|^2dt =  \sum_{n=-\infty}^{\infty} |c_n|^2


Transformée de Fourier
----------------------

La transformée de Fourier d'un signal :math:`x(t)` est donnée par 

.. math:: 

    X(f) = \mathcal{F}\left[x(t)\right]=\int_{-\infty}^{\infty} x(t) e^{-2j\pi ft}dt


La transformée de Fourier Inverse est donnée par 

.. math:: 

    x(t) = \mathcal{F}^{-1}\left[X(f)\right]=\int_{-\infty}^{\infty} X(f) e^{2j\pi ft}df

Propriétés
++++++++++

* Linéarité: :math:`\mathcal{F}\left[\alpha x_1(t)+\beta x_2(t)\right] = \alpha X_1(f)+\beta X_2(f)`

* Dilatation / Compression: :math:`\mathcal{F}\left[x(\alpha t)\right] = \frac{1}{|\alpha|} X\left( \frac{f}{\alpha} \right)`

* Décalage Temporel: :math:`\mathcal{F}\left[x(t-\tau)\right] = X(f)e^{-2j\pi f \tau}`

* Convolution : La transformée de Fourier du produit de convolution est égale au produit des transformées de Fourier, c-à-d

.. math:: 

    \mathcal{F}\left[(x*y) (t)\right] = X(f)Y(f)

où 

.. math:: 

    (x*y) (t) = \int_{-\infty}^{\infty} x(t-\tau) y(\tau) dt




Exemples
++++++++

Porte rectangulaire 
^^^^^^^^^^^^^^^^^^^

* Définition : 

.. math:: 

    x(t)=\Pi(t)=\left\{\begin{array}{cc}
    1,&|t|<\frac{1}{2}\\
    0,&\text{ailleurs}
    \end{array}\right.

* Transformée de Fourier: 

.. math :: 

    X(f)=\frac{\sin(\pi f)}{\pi f}=\text{sinc}(\pi f)


Porte triangulaire
^^^^^^^^^^^^^^^^^^^

* Définition : 

.. math:: 

    x(t)=\Delta(t)=\left\{\begin{array}{cc}
    1-|t|,&|t|\le \frac{1}{2}\\
    0,&\text{ailleurs}
    \end{array}\right.

* Transformée de Fourier: 

.. math :: 

    X(f)=\text{sinc}^2(\pi f)

Exponentielle Décroissante (unilaterale)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* Définition : 

.. math :: 

    x(t)=\left\{\begin{array}{cc}
    0,&t<0\\
    e^{-at},&t\ge 0
    \end{array}\right.

* Transformée de Fourier: 

.. math :: 

    X(f)=\frac{1}{a+2j\pi f}

Exponentielle Décroissante (bilaterale)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Définition : 

.. math :: 

    x(t)=e^{-a|t|}

* Transformée de Fourier:

.. math :: 

    X(f)=\frac{2a}{a^2+(2\pi f)^2}

Impulsion de Dirac 
^^^^^^^^^^^^^^^^^^

* Définition : 
  
.. math :: 

    x(t) = \delta(t)=\left\{\begin{array}{cc}
    \infty,&t=0\\
    0,&t\ne 0
    \end{array}\right.~\text{s.t.}\int_{-\infty}^{\infty} \delta(t)dt = 1


* Propriétés:

.. math :: 

    \int_{-\infty}^{\infty} f(t)\delta(t-\tau)dt = f(\tau)\\
    f(t)*\delta(t) = f(t)\\
    f(t)\delta(t) = f(0)\delta(t)


* Transformée de Fourier:

.. math :: 

    X(f)=1

Sinusoide (part 1)
^^^^^^^^^^^^^^^^^^

* Définition : 

.. math :: 

    x(t) = \cos(2\pi f_0 t)

* Transformée de Fourier:

.. math :: 

    X(f)=\frac{1}{2}\left(\delta(f-f_0)+\delta(f+f_0)\right)

Sinusoide (part 2)
^^^^^^^^^^^^^^^^^^

* Définition : 

.. math :: 

    x(t) = \sin(2\pi f_0 t)

* Transformée de Fourier :

.. math :: 

    X(f)=\frac{1}{2j}\left(\delta(f-f_0)-\delta(f+f_0)\right)

