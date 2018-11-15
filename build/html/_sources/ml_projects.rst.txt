Included Machine Learning Projects
==================================

Some machine learning projects have been installed in the /glob/deep-learning/ directory.

py-faster-rcnn
--------------

py-faster-rcnn (https://github.com/rbgirshick/py-faster-rcnn) has been installed at /glob/deep-learning/py-faster-rcnn/. To use py-faster-rcnn on Intel® AI DevCloud, first create a local working directory.

>>> [u21356@c009 ~] mkdir -p py-faster-rcnn/data && cd py-faster-rcnn

Then create a file config.yml and add the following lines:

.. code-block:: bash

	ROOT_DIR: /home/u21356/py-faster-rcnn/
	DATA_DIR: /home/u21356/py-faster-rcnn/data/

When downloading data for your training, make sure to place it in the DATA_DIR above. It is also recommended to add the following:

.. code-block:: bash

	TRAIN:
	  BG_THRESH_LO: 0.0
	TEST:
	  HAS_RPN: True

Finally, create a symbolic link for the models directory.

>>> [u21356@c009 py-faster-rcnn] ln -s glob/deep-learning/py-faster-rcnn/models/

To when running train_faster_rcnn scripts, use the config.yml to set the default output and data directory to the working directory. For example for the pascal VOC data:

>>> [u21356@c009 py-faster-rcnn] python /glob/deep-learning/py-faster-rcnn/tools/train_faster_rcnn_alt_opt.py  --net_name ZF --weights ./faster_rcnn_models/ZF_faster_rcnn_final.caffemodel --imdb voc_2007_trainval --cfg faster_rcnn_alt_opt.yml

.. note:: 
	the above assumes that the dataset is downloaded to DATA_DIR form above, and the caffemodels to /home/u21356/py-faster-rcnn/faster_rcnn_models/.

These steps are required because py-faster-rcnn tries to write to the install directory by default. The install directory, /glob/deep-learning/py-faster-rcnn/ is read-only as it is a shared directory, and so the above changes the output directory to the working directory.
