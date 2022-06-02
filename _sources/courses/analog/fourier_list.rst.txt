Liste des Transformées de Fourier
=================================

Signaux à Energie finie
-----------------------

Porte rectangulaire 
+++++++++++++++++++

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
++++++++++++++++++

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
++++++++++++++++++++++++++++++++++++++++

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
+++++++++++++++++++++++++++++++++++++++

* Définition : 

.. math :: 

    x(t)=e^{-a|t|}

* Transformée de Fourier:

.. math :: 

    X(f)=\frac{2a}{a^2+(2\pi f)^2}

Impulsion de Dirac 
++++++++++++++++++

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


Signaux Périodiques
-------------------

Sinusoide (part 1)
++++++++++++++++++

* Définition : 

.. math :: 

    x(t) = \cos(2\pi f_0 t)

* Transformée de Fourier:

.. math :: 

    X(f)=\frac{1}{2}\left(\delta(f-f_0)+\delta(f+f_0)\right)

Sinusoide (part 2)
++++++++++++++++++

* Définition : 

.. math :: 

    x(t) = \sin(2\pi f_0 t)

* Transformée de Fourier :

.. math :: 

    X(f)=\frac{1}{2j}\left(\delta(f-f_0)-\delta(f+f_0)\right)

