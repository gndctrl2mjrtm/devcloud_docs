Basic Job Submission
====================

Submitting a job can be done through a job script file. Suppose that you have a Python application, 'my_application.py'. In the same folder, use your favorite text editor and create a file "myjob". Then add the following two lines.

>>> cd $PBS_O_WORKDIR

>>> python my_application.py

The first line ensures that the script runs in the same directory as where you have submitted it. And the second line runs the Python application.
You can submit this job with:

>>> [u21356@c009 ~]# qsub myjob

This command will return a Job ID, which is the tracking number for your job.
You can track the job with:

>>> [u21356@c009 ~]# qstat

Once it is complete, the output will be in the files:

>>> [u21356@c009 ~]# cat myjob.oXXXXXX
>>> [u21356@c009 ~]# cat myjob.eXXXXXX

Here 'XXXXXX' is the Job ID. The .o file contains the standard output stream, and .e file contains the error stream.
