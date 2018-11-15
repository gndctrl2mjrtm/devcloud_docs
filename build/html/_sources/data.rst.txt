Data Management
===============

- Do not use /tmp.
- Home folder is NFS-shared between the login node and the compute nodes.
- Some machine learning datasets can be found in /data/

Storage Quota
-------------

Your account on Intel® AI DevCloud will have a storage quota. You can view your current usage with the following command:

>>> [u21356@c009 ~] getquota
23.06 GB out of 200.00 GB (11.53%) used

You are free to write data up to this limit, but note that if you reach this quota your applications will no longer be able to write any more data to your home directory. To reduce your usage, simply remove unwanted files. For special cases, you can request additional quota by emailing with the requested value and the details of the workload that requires this additional quota.


If you reach 90% of your quota, we send a courtesy email to let you know that you are approaching the limit. Once again, it is perfectly okay to use all the quota space available to you. Just remember that you will not be able to write any more data once you reach it.

Scratch Space
-------------
When you submit a job through qsub, or if you are using JupyterNotebook, you will have access to a local scratch directory on the compute node. The location of this directory is stored in environment variable PBS_SCRATCHDIR

>>> [u21356@c009-nXXX ~] echo $PBS_SCRATCHDIR
/local/12345/

This is a temporary scratch directory that you can use to get additional I/O bandwidth for applications that uses heavy I/O operations. However, there are two things to keep in mind when using this directory


This directory is deleted at the end of your job (or JupyterNotebook session). If there are data that you wish to keep, make sure to copy it back to your home directory.


This directory is local and not shared by other nodes. If you have requested multiple nodes in your job, each compute node will have their own local scratch directory.
