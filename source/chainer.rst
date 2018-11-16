.. _chainer-usage:

Chainer Usage
=============

Chainer is a flexible framework for neural networks. It uses dynamic computational graph that uses define by run scheme, instead of the traditional define and run scheme. In define by run approach, network is defined dynamically via the actual forward computation. It stores the computation history instead of programming logic which enables us to fully leverage the power of programming logic in Python (Reference link: https://docs.chainer.org/en/stable/guides/define_by_run.html ). Chainer is useful in cases where there is a variation in input, for example, unstructured data like text. It is notably faster than other Python-oriented frameworks. Please refer https://docs.chainer.org/en/stable/ for further details.

The detailed instructions to install Chainer on Linux can be referred from: https://github.com/Intel/chainer . 

Pre-requisite: Numpy>1.9 need to be installed using below command

>>> pip install numpy 

Please refer https://docs.chainer.org/en/stable/install.html for further details.

Chainer is integrated with the latest release of Intel® Math Kernel Library (Intel® MKL) for Deep Neural Networks optimized for Intel® AVX and Intel® AVX-512 instructions. These are supported in Intel® Xeon® and Intel® Xeon Phi™ processors. Please refer https://github.com/Intel/chainer for more information.

What is imperative programming?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Imperative programming is a programming paradigm in which the commands explain how the computation takes place, step by step. The commands enable the computer to accomplish the computation.

How to use the GAN that is available in Chainer?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The GAN available with Chainer is a DCGAN, which is an evolved form of GAN. The network provided here accepts a fixed size of input, 32x32x3. If an input of a different size is required for training, the network must be changed. You can find the implementation details from https://github.com/intel/chainer/tree/master/examples/dcgan .

What are the differences between Chainer and PyTorch?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Chainer and PyTorch use dynamic computational graphs. Chainer is much more customizable as it is entirely written in Python, which makes it more mass appealing. For instance, to define a custom neural network layer only using python, it is much simpler to do so in Chainer than a framework with C/C++ as backend where one might need to hack the framework itself to modify/implement the custom function. Given this, all the python norms are inherently supported in Chainer. PyTorch is the python version of Torch (lua framework) and uses the same C backend. PyTorch actually started out as a fork of Chainer only with a different backend. The auto differentiation parts in PyTorch are based on Chainer.
For further details, please refer to: https://docs.chainer.org/en/stable/comparison.html 

What are the differences between Chainer and Tensorflow?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The differences between Chainer and Tensorflow are explained here: https://docs.chainer.org/en/stable/comparison.html 

What is ChainerCV?
~~~~~~~~~~~~~~~~~~

ChainerCV is a collection of tools to train and run neural networks for computer vision tasks using Chainer. Please refer to https://github.com/chainer/chainercv.git .

Logging can be customized in Chainer using chainer.Reporter module. The observed current variables values can be reported using chainer.Reporter.report() function. For example:

.. code :: python 

	chainer.reporter.report({'rpn_loc_loss': rpn_loc_loss,
	                         'rpn_cls_loss': rpn_cls_loss,
	                         'roi_loc_loss': roi_loc_loss,
	                         'roi_cls_loss': roi_cls_loss,
	                         'rpn_cls_accuracy':rpn_cls_accuracy,
	                         'roi_cls_accuracy':roi_cls_accuracy,
	                         'loss': loss},
	                        self)

Where values without quotes are the variable that are calculated.
Please go through https://docs.chainer.org/en/stable/guides/report.html# for more details.

What are the different forms to save the model?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We can save a model in chainer using chainer.serializers module. Serializer is a simple interface to serialize or deserialize an object. Model saving can be done in two formats:
- NPZ 
- HDF5

Saving and loading in NPZ Format
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Save using the following command:

.. code :: python 

	from chainer import serializers
	serializers.save_npz('mymodel.npz', model)

Load using the following command:

.. code :: python 

	serializers.load_npz('mymodel.npz', model)

Saving and loading in HDF5 format
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Save using the following command:

.. code :: python

	from chainer import serializers
	serializers.save_hdf5('mymodel.hdf5', model)

Load using the following command:

.. code :: python

	serializers.load_hdf5('mymodel.hdf5', model)

For more information, refer to https://docs.chainer.org/en/stable/guides/serializers.html .

What is iDeep? How much performance improvement can we achieve with the use of iDeep in Chainer?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

iDeep is a module that provides NumPy-like API and DNN acceleration using MKL-DNN for Intel® CPUs. It utilizes vector instructions of CPU. Please refer to https://github.com/intel/ideep for more details.
For MNIST Classifier which is using MLP (Multi-layer Perceptron), we got around 16% performance improvement whereas for CIFAR-10 Classifier which is using CNN, it is around 94%.

How to configure iDeep with Chainer?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Please refer to https://docs.chainer.org/en/stable/tips.html#how-do-i-accelerate-my-model-using-ideep-on-Intel®-cpu for configuring iDeep with Chainer. 

What is Chainer RL?
~~~~~~~~~~~~~~~~~~~

It is a deep RL library that implements various state-of-the-art deep reinforcement algorithms in Python using Chainer.
You can use this link to quickstart Chainer RL: https://github.com/chainer/chainerrl/blob/master/examples/quickstart/quickstart.ipynb

How to perform Object Detection in ChainerCV for a custom data?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Object Detection in Chainer can be achieved using inbuilt Chainer module called ChainerCV. Here we are considering Oxford pets dataset (http://www.robots.ox.ac.uk/~vgg/data/pets/ )
Pets Dataset contains both xml and jpeg files. All the xml files has name which contain either cat or dog not with the breed names. So modified all xml files with breed names at name tag.
In pets dataset there are predefined shuffled jpeg and xml files for both test and train which are saved in the form of trainval.txt and test.txt. But either trainval.txt or test.txt are in the format of file name, xmin, ymin, xmax, ymax where as our file expects input in the form of just file name.  So modified the files accordingly.

Follow below steps to download ChainerCV.

>>> cd ~
>>> git clone https://github.com/chainer/chainercv.git
>>> cd ~/chainercv

For loading customized data the following need to be updated
Modify pascal voc 2007 and 2012 datasets with customized data.
Paths in ` chainercv/examples/ssd/train.py` file. Modify below lines

.. code :: python 

	train = TransformDataset(ConcatenatedDataset(VOCBboxDataset(year='2007', split='trainval'), VOCBboxDataset(year='2012', split='trainval') ), Transform(model.coder, model.insize, model.mean)) 

To below code

.. code :: python

	train = TransformDataset(ConcatenatedDataset(VOCBboxDataset(split='trainval')), Transform(model.coder, model.insize, model.mean)) 

Modify labels variable in ~/.conda/envs/<conda_env_name>/lib/python3.6/site-packages/chainercv/datasets/voc/voc_utils.py as below

.. code :: python

	voc_bbox_label_names = ('aeroplane',..,etc)

To customized class labels like below

.. code :: python

	voc_bbox_label_names = (' abyssinian', 'american_bulldog'..,etc)

Modify below lines in ~/.conda/envs/<conda_env_name>/lib/python3.6/site-packages/chainercv/datasets/voc/voc_bbox_dataset.py 
Data_dir parameter in init function need to be updated with customized data located path like below

.. code :: python

	data_dir='/home/<user_id>/chainer/data'

Path of id_list_file need to updated with customized split file like below

.. code :: python

	id_list_file = os.path.join(data_dir, 'annotations/{0}.txt'.format(split))

In the above example, trainval.txt is stored in /home/<user_id>/chainer/data/annotations/ where trainval can be passed at split variable while calling VOCBboxDataset()

Few .xml files of trainval.txt are missed in pets data which interrupts the training. So adding below code will help to skip and continue with training even if there are no .xml files.

.. code :: python

	self.data_dir = data_dir # this line need to be remove from the below and add above self.ids line as mentioned
	self.ids = [id_.strip() for id_ in open(id_list_file)]

After this below line need to be added

.. code :: python

	self.ids=[ i for i in self.ids if(Path(os.path.join(self.data_dir,'annotations/xmls_bkp/', i +'.xml')).is_file())] 

Update Images path in _get_image function as below

.. code :: python

	img_path = os.path.join(self.data_dir, 'images/', id_ + '.jpg')

where .jpegs are in images/ directory having parent directory /home/<user_id>/chainer/data

Update Annotations path in _get_annotations function as below

.. code :: python

	anno = ET.parse(os.path.join(self.data_dir, 'annotations/xmls_bkp/', id_ + '.xml'))

Add below lines to avoid error while reading .xml files 

.. code :: python

	name = obj.find('name').text.lower().strip()

Modify it to below lines

.. code :: python

	for ex in anno.findall('filename'):
    	filename = ex.text.lower().strip()
	name=filename.rsplit('_',1)[0]

How to tweak code to get “N” boundary boxes for each object?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To draw “N” boundary boxes, modify the code in /home/<user_id>/.conda/envs/<conda_env_name> /lib/python3.6/site-packages/chainercv/visualizations/vis_bbox.py

.. code :: python

	for i, bb in enumerate(bbox):

Change line to:

.. code :: python

	for i, bb in enumerate(bbox[:N,:]):

How to tweak code to get boundary boxes when model inference accuracy is poor?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We can do it by changing the threshold value.

For example, if you are using Faster- RCNN, in the file /home/<user_id>/.conda/envs/<conda_env_name>/lib/python3.6/site-packages/chainercv/links/model/faster_rcnn/faster_rcnn.py, you need to change the value of self.score_thresh

.. code :: bash

	if preset == 'visualize':
	        self.nms_thresh = 0.3
	        #self.score_thresh = 0.7 (line to be changed as below)
	        self.score_thresh = 0.45 (set based on the model accuracy)















