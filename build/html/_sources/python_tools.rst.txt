Python Tools
============

pip
---

pip command is installed and supported on this cluster, however you can only install packages locally on your account. To do this, run pip with the argument --user.

>>> [u21356@c009 ~] pip install --user numpy

With Intel Distribution of Python, the pip is just pip for both Python 2 and Python 3 (as opposed to pip3). So running pip will install for distribution in the default python, which is Python 3. To check which pip you are using, run the following.

>>> [u21356@c009 ~] which pip
/glob/intel-python/python3/bin/pip

If Python 2 is preferred, swap the ordering of the two on the following line in the '~/.bash_profile' script so that python2/bin directory comes first.

>>> export PATH=/glob/intel-python/python3/bin/:/glob/intel-python/python2/bin/:${PATH}

You will have to either log out/back in or run the following for the changes to take effect:

>>> [u21356@c009 ~] source ~/.bash_profile
pyopencl

CPU version of OpenCL is supported in this cluster. You can use this through pyopencl module, but you must install it locally on your account. To install pyopencl locally, use the following.

>>> [u21356@c009 ~] export LIBRARY_PATH=${LIBRARY_PATH}:/glob/supplementary-software/opencl/lib64/
>>> [u21356@c009 ~] pip install --user pyopencl

To use the pyopencl module, add the following lines to your ~/.bash_profile script.
..code:: bash

	export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/glob/supplementary-software/opencl/lib64/
	export PYOPENCL_CTX='0'

Then run the following to apply the new environment variables.

>>> [u21356@c009 ~] source ~/.bash_profile

PYOPENCL_CTX environment varible disables the user prompt of pyopencl that asks which OpenCL context (device) to use. Without this variable, your job script will hang as it will wait for a user input that will never come. The cluster only supports the CPU context, which is 0.
