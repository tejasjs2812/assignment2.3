# assignment2.3
Ans :


Hadoop consists of mainly two parts HDFS(Hadoop Distributed File System) and MAp and Reduce
HDFS in Hadoop version 1.x mainly has 3 daemons which are Name Node, Secondary Name Node and Data Node.

Name Node-
There is only single instance of this process runs on a cluster and that is on a master node
It manages information like location of file blocks across cluster and it’s permission
This process reads all the metadata from a file named fsimage and keeps it in memory
After this process is started, it updates metadata for newly added or removed files in RAM
It time after time writes the changes in one file called edits 
This process is a heart of HDFS, if it is down HDFS cant be accessed

Secondary Name Node-
This process can run on a master node or can run on a separate node depends on the size of the cluster
One misinterpretation from name is “This is a backup Name Node” but thats not the case!!!!!
It manages the metadata for the Name Node. In the sense, it reads the information written in edit logs (by Name Node) and creates an updated file of current cluster metadata
Than it transfers that file back to Name Node so that fsimage file can be updated
So, whenever Name Node daemon is restarted it can always find updated information in fsimage file

Data Node-

It is responsible for storing the individual file blocks on the slave nodes in Hadoop cluster
Based on the replication factor, a single block is replicated in multiple slave nodes(only if replication factor is > 1) to prevent the data loss
Whenever required, this process handles the access to a data block by communicating with Name Node
This process periodically sends heart bits to Name Node to make Name Node aware that slave process is running
Hadoop 1.x has a Single Point Of Failure


MapReduce –
It is a Distributed Computation
MapReduce component is responsible for distributed computing on Hadoop Cluster. Basically it uses two daemons named Job Tracker and Task Tracker. 
Hadoop MapReduce algorithm basically has two phases Map and Reduce.

Job Tracker-
Only one instance of this process runs on a master node same as Name Node
Any MapReduce job is submitted to Job Tracker ,thenJob Tracker checks for the location of file blocks used in processing
and then starts the separate tasks on different Data Nodes by communicating with Task Tracker.

Task Tracker-
It receives the job information from Job Tracker daemon and initiates a task on that slave node
mostly, Task Tracker initiates the task on the same node where physical data block is there.
 this process also sends heart bits to Job Tracker to make Job Tracker aware that slave process is going on.

Limitations of Hadoop 1.x Architecture-
In case of system failure, hadoop admin need to take control and restart the job, which usually takes 45 minutes as there is no
HIGH AVAIBILITY like hadoop2.x.
the  major drawback of Hadoop 1.x Architecture is Single Point of Failure as there is no backup Name Node.
Job scheduling, resource management and job monitoring are being done by Job Tracker which is tightly coupled with Hadoop. 
Job Tracker has to coordinate with all task tracker so in a very big cluster it will be difficult to manage huge number of task trackers altogether.
Due to single Name Node, there is no concept of namespaces in Hadoop 1.x. So everything is being managed under single namespace.
Using Hadoop 1.x architecture, Hadoop Cluster can be scaled upto ~4000 nodes. 
