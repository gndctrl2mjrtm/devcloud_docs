How to Connect
==============

Access to Resources
-------------------
The cluster consists of multiple compute servers, which we call compute nodes, storage servers, and the login node. You can run a Jupyter Notebook session on one of the compute nodes. You can also access the login node using an SSH client in a text-based terminal. In both cases, if you want to use the full power of the cluster, you will need to submit jobs to a queue.

Access via a Jupyter Notebook
-----------------------------
Your Jupyter Notebook instance runs on one of the compute nodes. When you execute the Notebook cells, they run on an Intel Xeon Scalable processor. There may be other people connecting to your compute node, which reduces the available compute power. However, you can reserve a full node for your job and even use multiple nodes at once by submitting scripts to the job queue. For more information,  open the Welcome.ipynb file in your home directory.

If you Connect with the Terminal
--------------------------------
Eight-word summary: **do not run jobs on the login node**
When you log in, you will find yourself on the host c009, which is your login node. This node is intended only for code development and compilation, but NOT for computation. That is because it does not have much compute power, and, additionally, there are limitations on CPU time and RAM usage on the login node; your workload will be killed if it exceeds the limit. To run computational workloads on powerful compute nodes, you must submit a job through the Torque job queue. See next section for a sample job script.
