Supported Machine Learning Frameworks
=====================================

Most machine learning frameworks are located in the /glob/deep-learning/ directory. Each directory points to the newest version of the compiler or interpreter that is available on the cluster. If you need a specific version, look in the "versions" directory.

If the framework you require is not listed, you can try installing them locally on your home directory.

TensorFlow
----------

TensorFlow 1.10.0
~~~~~~~~~~~~~~~~~

TensorFlow 1.10.0 is already built into the Intel Distribution for Python installed on the cluster.
The easiest way to access TensorFlow is to add the following lines to the '~/.bash_profile' script.

>>> export PATH=/glob/intel-python/python2/bin/:/glob/development-tools/gcc/bin:$PATH
>>> export LD_LIBRARY_PATH=/glob/development-tools/gcc/lib64:$LD_LIBRARY_PATH

.. Note::
   Beware To use python 3 instead, change python2 to python3 in the first line.

You will have to either log out/back in or run the following for the changes to take effect:

>>> [u21356@c009 ~] source ~/.bash_profile

Conda users can install the latest Intel optimized Tensorflow by issuing the command below in their environment:

>>> [u21356@c009 ~] conda install -c intel tensorflow

TensorFlow 1.7.0 and Multi-Node Training Support
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section discusses how to install TensorFlow 1.7.0 with multi-node training support

First, we need to add a few paths to some environment variables. Add the followig lines to ~/.bash_profile:

>>> export CC=/glob/development-tools/versions/gcc-6.4.0/bin/gcc
>>> export LD_LIBRARY_PATH=/glob/development-tools/versions/gcc-6.4.0/lib64/:$LD_LIBRARY_PATH
>>> source /glob/development-tools/parallel-studio/compilers_and_libraries/linux/mpi/bin64/mpivars.sh

By default, you will be using and installing TF 1.7.0 on with Python 3. If you prefer to use Python 2 instead, change the following line so that python2 comes before python3:

>>> export PATH=/glob/intel-python/python3/bin/:/glob/intel-python/python2/bin/:${PATH}

You will have to either log out/back in or run the following for the changes to take effect:

>> [u21356@c009 ~] source ~/.bash_profile

The .whl file is precompiled for your convenience and available in /glob/. You can install this locally on your account by running the following command:

>>> [u21356@c009 ~] pip install --user /glob/deep-learning/versions/intel-tensorflow/tensorflow-1.7.0/tensorflow-1.7.0-cp36-cp36m-linux_x86_64.whl

If you only require single-node, you are done! Your python should now use TensorFlow 1.7.0. Just remember that if you switch python versions, you will have to reinstall the .whl file using the corresponding version of pip.

If you need multi-node support, there are few more dependencies you must install. First, install horovod using the following command.

>>> [u21356@c009 ~] CFLAGS="-D_GLIBCXX_USE_CXX11_ABI=0" pip install --user horovod

The CFLAGS argument is important, and will give you errors if you do not include it.
Furthermore, there is currently an issue between TensorFlow 1.7.0 and the numpy package used by Intel Distribution of Python. So install numpy locally using the following command.

>> [u21356@c009 ~] pip install --user numpy==1.14.3

Caffe
-----

Caffe is already built into the Intel Distribution for Python installed on the cluster.

By default, Caffe uses Intel Distribution for Python 2. If Python 3 is preferred, change the following line in the '~/.bash_profile' script from 'python2' to 'python3'

>>> export PATH=/glob/intel-python/python2/bin/:$PATH

You will have to either log out/back in or run the following for the changes to take effect:

>>> [u21356@c009 ~]# source ~/.bash_profile

Torch
-----

The easiest way to access Torch is to add the following lines to the '~/.bash_profile' script.

>>> [u21356@c009 ~] source /glob/deep-learning/torch/install/bin/torch-activate

You will have to either log out/back in or run the following for the changes to take effect:

>>> [u21356@c009 ~] source ~/.bash_profile

Torch available on the cluster uses the Intel git repository for Torch.

Theano
------

To use Theano, run the following to copy the '.theanorc' file.

>>> [u21356@c009 ~] cp /glob/deep-learning/versions/intel-theano/theanorc_icc_mkl ~/.theanorc

Theano available on the cluster uses the Intel git repository for Theano.


Mxnet
-----

Mxnet is already built into the Intel Distribution for Python installed on the cluster.

By default, Mxnet uses Intel Distribution for Python 2. If Python 3 is preferred, change the following line in the '~/.bash_profile' script from 'python2' to 'python3'

>>> export PATH=/glob/intel-python/python2/bin/:$PATH

You will have to either log out/back in or run the following for the changes to take effect:
>>> [u21356@c009 ~] source ~/.bash_profile

Chainer
-------

To learn how to use Chainer for machine learning, go to :ref:`chainer-usage`.





