Programming Languages
=====================

All compilers and interpreters, such as Intel Compiler or Python interpreter, are located in the /glob/development-tools/ directory. Each directory points to the newest version of the compiler or interpreter that is available on the cluster. If you need a specific version, look in the "versions" directory.

Python (and Conda)
------------------

For best performance, use Intel Distribution for Python from /glob/intel-python/python3/bin/ and /glob/intel-python/python3/bin/. These paths are included in your environment by default.


Conda is available for users that want to easily manage their environments. For best performance, create new environments using Intel Distribution for Python.


To do this, first add Intel's channel into Conda:

>>> [u21356@c009 ~] conda config --add channels intel

When creating your environment, you have the option of picking between core or full versions of Python 2 and 3.

To create an environment with core Python 3:

>>> [u21356@c009 ~] conda create -n <nameofyourenv> intelpython3_core python=3

For core Python 2:

>>> [u21356@c009 ~] conda create -n <nameofyourenv> intelpython2_core python=2

To use the full version instead of core, replace "core" with "full".

>>> [u21356@c009 ~] conda create -n <nameofyourenv> intelpython2_full python=2

In order to use the newly created environment, users will need to activate it.

>>> [u21356@c009 ~] source activate <nameofyourenv>

To leave the environment:

>>> [u21356@c009 ~] source deactivate

The Intel channel provides a variety of Python versions. If a particular version is required, you can use the search option to see what is available. Intel distributed packages are tagged "[intel]".

>>> [u21356@c009 ~] conda search -f python

Using C/C++ or Fortran
----------------------

For best performance, Intel Compiler is recommended. The paths to the Intel compilers are included in your environment by default.
For GCC, your environment will point to the system gcc (v4.8.5) by default. Add the following to your "~/.bash_profile" file to use the newest version of GCC that is available.

>>> export PATH=/glob/development-tools/gcc/bin/:$PATH

Using R
-------

To use R, add the following to your "~/.bash_profile" file.

>>> export PATH=/glob/development-tools/R/bin/:$PATH

R available on the cluster uses Intel Math Kernel Library as the backend math library.

Others
------

If the tool you require is not available, try install them locally in your home directory. If this is not possible, put in a feature request by posting it on the `Intel® AI Academy Forum <https://communities.intel.com/community/tech/intel-ai-academy/overview>`_
