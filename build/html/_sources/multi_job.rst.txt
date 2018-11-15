Running Multiple Jobs
=====================

For most machine learning workloads, reserve 1 node per job (this is the default). If you reserve more nodes, your application will not take advantage of them, unless you explicitly use a distributed training library such as MLSL. Most people do not. Reserving extra nodes, whether your application uses them or not, reduces the queue priority of your future jobs.

Instead, to take advantage of multiple nodes available to you, submit multiple single-node jobs with different parameters. For example, you can submit several jobs with different values of the learning rate like this:

Your application "my_application.py" should use the command-line arguments to set the learning rate:

.. code-block:: python

	import sys
	print("Running with learning rate %s"%sys.argv[1])
	learning_rate=float(sys.argv[1])

Your job file "myjob" may contain the following:

>>> cd $PBS_O_WORKDIR 
>>> python my_application.py $1

You will submit several jobs like this:

>>> [u21356@c009 ~]# qsub myjob -F "0.001"
>>> [u21356@c009 ~]# qsub myjob -F "0.002"
>>> [u21356@c009 ~]# qsub myjob -F "0.005"
>>> [u21356@c009 ~]# qsub myjob -F "0.010"

If resources are available, all 4 jobs will start at the same time on different compute nodes. This workflow will produce results up to 4 times faster than if you had only one compute node.
