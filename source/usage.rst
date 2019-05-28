Using Intel® Machine Learning Scaling Library
=============================================

Prerequisites
*************

Before you start using the Intel® MLSL, make sure to set up the library environment. Use the command:
``$ source <install_dir>/intel64/bin/mlslvars.sh``
This is sets up the environment both for the C/C++ and Python* bindings.
Here and below, ``<install_dir>`` is the Intel MLSL installation directory, which is ``/opt/intel/mlsl``
by default.

Generic Workflow
****************

Below is a generic flow of using the Intel® MLSL in C++:

1. Initialize the library:

.. code-block::

   Environment::GetEnv().Init(&argc, &argv);

2. Create a Session and a Distribution objects:

.. code-block::
  
   Session *s = Environment::GetEnv().CreateSession();
   Distribution *d = Environment::GetEnv().CreateDistribution(<args>);

3. Set the global mini-batch size (equal to the sum of local batch sizes):

.. code-block::

   s->SetGlobalMinibatchSize(<args>);

Launching Sample Application
****************************

Intel® MLSL supplies a sample application, ``mlsl_test.cpp`` or ``mlsl_test.py``, which demonstrates
the usage of Intel MLSL API.

Launching the Sample
--------------------

1. For the C++ sample, build ``mlsl_test.cpp``:

.. code-block::
   $ cd <install_dir>/test
   $ icpc -O2 –I<install_dir>/intel64/include/ -L<install_dir>/intel64/lib
   -lmlsl -lmpi -ldl -lrt -lpthread -o mlsl_test mlsl_test.cpp
   
2. Launch the mlsl_test binary or the mlsl_test.py script with mpirun on the desired number of nodes (N).

Sample Description
------------------
The application is set up to run a test for two layers. It sets output on the 1st layer and checks input for
the 2nd layer in an fprop() call. Similarly, for the bprop() call, it sets a gradient with respect to input
for the 2nd layer and checks the gradient with respect to output for the 1
st layer. For weights, it sets gradients with respect to weights, checks the gradients accumulation, modifies weights in a wtinc()
call, and then verifies the expected values in an fprop() call for both layers.
The application prints parameters for input and output feature maps and weights, whether the
communication is required, and what type of communication is required. The test status is printed as
PASSED or FAILED. You can grep for FAILED to see if a test failed.
