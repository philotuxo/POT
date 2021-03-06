

.. _sphx_glr_auto_examples_plot_OT_1D.py:


====================
1D optimal transport
====================

This example illustrates the computation of EMD and Sinkhorn transport plans
and their visualization.




.. code-block:: python


    # Author: Remi Flamary <remi.flamary@unice.fr>
    #
    # License: MIT License

    import numpy as np
    import matplotlib.pylab as pl
    import ot
    from ot.datasets import get_1D_gauss as gauss







Generate data
-------------



.. code-block:: python



    #%% parameters

    n = 100  # nb bins

    # bin positions
    x = np.arange(n, dtype=np.float64)

    # Gaussian distributions
    a = gauss(n, m=20, s=5)  # m= mean, s= std
    b = gauss(n, m=60, s=10)

    # loss matrix
    M = ot.dist(x.reshape((n, 1)), x.reshape((n, 1)))
    M /= M.max()








Plot distributions and loss matrix
----------------------------------



.. code-block:: python


    #%% plot the distributions

    pl.figure(1, figsize=(6.4, 3))
    pl.plot(x, a, 'b', label='Source distribution')
    pl.plot(x, b, 'r', label='Target distribution')
    pl.legend()

    #%% plot distributions and loss matrix

    pl.figure(2, figsize=(5, 5))
    ot.plot.plot1D_mat(a, b, M, 'Cost matrix M')




.. rst-class:: sphx-glr-horizontal


    *

      .. image:: /auto_examples/images/sphx_glr_plot_OT_1D_001.png
            :scale: 47

    *

      .. image:: /auto_examples/images/sphx_glr_plot_OT_1D_002.png
            :scale: 47




Solve EMD
---------



.. code-block:: python



    #%% EMD

    G0 = ot.emd(a, b, M)

    pl.figure(3, figsize=(5, 5))
    ot.plot.plot1D_mat(a, b, G0, 'OT matrix G0')




.. image:: /auto_examples/images/sphx_glr_plot_OT_1D_005.png
    :align: center




Solve Sinkhorn
--------------



.. code-block:: python



    #%% Sinkhorn

    lambd = 1e-3
    Gs = ot.sinkhorn(a, b, M, lambd, verbose=True)

    pl.figure(4, figsize=(5, 5))
    ot.plot.plot1D_mat(a, b, Gs, 'OT matrix Sinkhorn')

    pl.show()



.. image:: /auto_examples/images/sphx_glr_plot_OT_1D_007.png
    :align: center


.. rst-class:: sphx-glr-script-out

 Out::

    It.  |Err         
    -------------------
        0|8.187970e-02|
       10|3.460174e-02|
       20|6.633335e-03|
       30|9.797798e-04|
       40|1.389606e-04|
       50|1.959016e-05|
       60|2.759079e-06|
       70|3.885166e-07|
       80|5.470605e-08|
       90|7.702918e-09|
      100|1.084609e-09|
      110|1.527180e-10|


**Total running time of the script:** ( 0 minutes  1.198 seconds)



.. container:: sphx-glr-footer


  .. container:: sphx-glr-download

     :download:`Download Python source code: plot_OT_1D.py <plot_OT_1D.py>`



  .. container:: sphx-glr-download

     :download:`Download Jupyter notebook: plot_OT_1D.ipynb <plot_OT_1D.ipynb>`

.. rst-class:: sphx-glr-signature

    `Generated by Sphinx-Gallery <http://sphinx-gallery.readthedocs.io>`_
