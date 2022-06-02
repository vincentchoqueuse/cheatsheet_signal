Séries de Fourier 
=================

Implémentation
--------------

.. plot::
    :context: close-figs

    class Fourier_Synth():

        def __init__(self, f0, L):
            self.f0 = f0 
            self.L = L

        def get_c(self, n):
            if (n%2) == 0:
                c_n = 0
            else:
                c_n = 2/(1j*np.pi*n)
            return c_n

        def __call__(self, t):
            
            L = self.L
            x = np.zeros(len(t),dtype=complex)
            for n in range(-L, L+1):
                cn = self.get_c(n)
                x += cn*np.exp(2j*np.pi*n*self.f0*t)

            return x

    # main program
    t = np.arange(-0.5,0.5,0.0001)
    waveform = Fourier_Synth(5, 20)
    x = waveform(t)
    plt.plot(t,x)
    plt.grid()
    plt.xlabel("t [s]")