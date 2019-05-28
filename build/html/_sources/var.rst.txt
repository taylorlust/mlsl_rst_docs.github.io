Environment Variables
=====================

MLSL_ROOT
---------
**Syntax**

*MLSL_NUM_SERVERS=<nservers>*

**Arguments**

.. list-table:: 
   :widths: 25 50
   :align: left
   
   * - <path> 
     - Installation directory of the Intel® MLSL.

**Description**

Set this environment variable to specify the installation directory of the Intel® MLSL.


MLSL_NUM_SERVERS
----------------
**Syntax**

*MLSL_NUM_SERVERS=<nservers>*

**Arguments**

.. list-table:: 
   :widths: 25 50
   :header-rows: 1
   :align: left
   
   * - <nservers> 
     - The number of servers per node.
   * - >= 0  
     - The default value is 4. The maximum value is 16.

**Description**

Set this environment variable to define the number of endpoint servers per node.

.. note:: Each server is a separate process, which uses CPU resources. Take that into account when setting the
       OMP_NUM_THREADS variable for OpenMP*. The recommended value for OMP_NUM_THREADS is
       max_cores - num_servers, where max_cores is the maximum number of cores, and num_servers
       is the number of endpoint servers per node