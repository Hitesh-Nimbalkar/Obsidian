---
banner: "![[Spark.png]]"
---

Contents

Contents

- [Why Spark](#Why%20Spark)
- [Apache Spark Ecosystem](#Apache%20Spark%20Ecosystem)
- [Spark and Pyspark](#Spark%20and%20Pyspark)
		- [Local Mode vs Cluster Mode](#Local%20Mode%20vs%20Cluster%20Mode)
- [Client + Spark + HDFS](#Client%20+%20Spark%20+%20HDFS)
- [Spark Architecture](#Spark%20Architecture)
		- [SSH](#SSH)
		- [Driver Program](#Driver%20Program)
		- [Driver Program vs Spark Context](#Driver%20Program%20vs%20Spark%20Context)
		- [Spark context and Spark Session](#Spark%20context%20and%20Spark%20Session)
		- [Container](#Container)
		- [Resource manager](#Resource%20manager)
			- [YARN](#YARN)
			- [Node manager vs YARN](#Node%20manager%20vs%20YARN)
			- [Execution](#Execution)
		- [Application Execution](#Application%20Execution)
		- [Spark Application Execution:](#Spark%20Application%20Execution:)
		- [Resource Allocation + Executor + Partitioning](#Resource%20Allocation%20+%20Executor%20+%20Partitioning)
				- [Executor](#Executor)
		- [Client Mode vs Cluster mode](#Client%20Mode%20vs%20Cluster%20mode)
		- [Spark Submit](#Spark%20Submit)
		- [Partitioning](#Partitioning)
				- [1. **Partitioning:**](#1.%20**Partitioning:**)
				- [2. **Task Execution:**](#2.%20**Task%20Execution:**)
				- [3. **Data Locality:**](#3.%20**Data%20Locality:**)
				- [4. **Efficient Computation:**](#4.%20**Efficient%20Computation:**)
				- [5. **Task Scheduling:**](#5.%20**Task%20Scheduling:**)
				- [6. **Fault Tolerance:**](#6.%20**Fault%20Tolerance:**)
		- [Spark RDD](#Spark%20RDD)
			- [RDD + DAG](#RDD%20+%20DAG)
		- [Action and Transformations](#Action%20and%20Transformations)
			- [RDD Transformation](#RDD%20Transformation)
				- [Narrow Transformation](#Narrow%20Transformation)
				- [Wide Transformation](#Wide%20Transformation)
	- [Lazy Evaluation](#Lazy%20Evaluation)

- ## Hadoop vs Spark 
- Batch Processing 
- Slow Performance due to In Memory 
  
Hadoop and Spark are both open-source big data processing frameworks, but they have different architectures and use cases. Here are some key points of comparison:

1. **Data Processing Model:**
    
    - **Hadoop:** Primarily uses the MapReduce programming model, which involves dividing a task into smaller sub-tasks (map phase) and then aggregating the results (reduce phase).
    - **Spark:** Offers a more flexible and expressive data processing model. It supports batch processing, interactive queries, streaming, and iterative algorithms. Spark allows data to be cached in-memory between stages, making it faster than Hadoop's MapReduce for some workloads.
2. **Performance:**
    
    - **Hadoop:** Performs disk-based storage and processing, which can result in slower processing times due to frequent disk I/O.
    - **Spark:** Leverages in-memory processing, reducing the need for frequent disk I/O and leading to faster data processing. Spark is often faster than Hadoop's MapReduce, especially for iterative algorithms and interactive queries.
3. **Ease of Use:**
    
    - **Hadoop:** Typically involves writing MapReduce programs, which can be complex and require a good understanding of distributed computing concepts.
    - **Spark:** Provides high-level APIs in languages like Scala, Java, Python, and R, making it more user-friendly and accessible. It also supports SQL queries and includes libraries for various tasks, simplifying development.
4. **Fault Tolerance:**
    
    - **Hadoop:** Achieves fault tolerance through data replication across nodes. If a node fails, the data can be retrieved from another replica.
    - **Spark:** Implements fault tolerance through lineage information, allowing it to recompute lost data in case of a node failure. This can be more efficient than Hadoop's replication approach.
5. **Use Cases:**
    
    - **Hadoop:** Well-suited for batch processing of large datasets. Commonly used for tasks like log processing, data warehousing, and ETL (Extract, Transform, Load) operations.
    - **Spark:** Versatile and supports batch processing, interactive queries, streaming, and machine learning. Spark is often chosen for iterative algorithms, real-time processing, and situations where low-latency responses are crucial.

In summary, while both Hadoop and Spark can handle big data processing, Spark is often preferred for its speed, flexibility, and ease of use, especially in scenarios requiring iterative processing, interactive queries, and real-time analytics. However, the choice between Hadoop and Spark depends on the specific requirements and nature of the data processing tasks at hand.
- ![[Spark vs Mapreduce.png]]
- 
- 
- 



## Why Spark 
Apache Spark is an open-source, distributed computing system designed for big data processing and analytics. It provides a fast and general-purpose cluster computing framework that supports in-memory processing and can handle large-scale data processing tasks. 

Apache Spark is often chosen over Hadoop, specifically the Hadoop MapReduce framework, for several reasons. While Hadoop and Spark are both part of the big data ecosystem, Spark offers advantages in terms of performance, ease of use, and versatility. Here are some key reasons why Spark is preferred over Hadoop in certain scenarios:

1. **In-Memory Processing:**
    
    - **Spark:** Utilizes in-memory processing, allowing it to store intermediate data in memory between stages of computation. This reduces the need for frequent disk I/O, making Spark significantly faster than Hadoop MapReduce, which relies heavily on disk-based storage and processing.
2. **Ease of Use:**
    
    - **Spark:** Provides high-level APIs in multiple programming languages, including Scala, Java, Python, and R. These APIs are more expressive and user-friendly compared to the lower-level MapReduce programming model of Hadoop. Spark's API allows developers to write concise and readable code, making it easier to develop and maintain applications.
3. **Versatility:**
    
    - **Spark:** Offers a unified platform for batch processing, interactive queries (via Spark SQL), machine learning (via MLlib), graph processing (via GraphX), and stream processing (via Spark Streaming). This versatility allows users to perform various data processing tasks within the same framework, eliminating the need for different tools for different tasks.
4. **Iterative Processing:**
    
    - **Spark:** Excels in iterative algorithms, making it well-suited for machine learning and graph processing tasks. Spark can cache intermediate results in memory, reducing the computational cost of iterative algorithms. This is particularly beneficial for applications like iterative machine learning algorithms.
5. **Fault Tolerance:**
    
    - **Spark:** Implements fault tolerance through lineage information and resilient distributed datasets (RDDs). In case of a node failure, Spark can recompute lost data using lineage information. This mechanism can be more efficient than Hadoop's replication-based fault tolerance.
6. **Interactive Queries:**
    
    - **Spark:** Supports interactive queries through its SQL and DataFrame API, providing users with a more responsive experience when querying large datasets. Hadoop MapReduce is not designed for interactive querying.
7. **Community and Ecosystem:**
    
    - **Spark:** Has a vibrant and active open-source community. It also has a rich ecosystem with various libraries and tools, extending its capabilities for different use cases. While Hadoop has a mature ecosystem, Spark's more extensive range of libraries makes it attractive for a broader set of applications.
8. **Real-time Processing:**
    
    - **Spark:** Supports real-time data processing through Spark Streaming, enabling the processing of data streams with low-latency requirements. Hadoop MapReduce is primarily designed for batch processing and is not well-suited for real-time analytics.

It's important to note that Spark and Hadoop are not mutually exclusive, and they can be used together. In fact, Spark can run on Hadoop Distributed File System (HDFS) and can be integrated with other Hadoop ecosystem components. The choice between Spark and Hadoop depends on specific use cases, performance requirements, and the nature of the data processing tasks at hand.



## Apache Spark Ecosystem 
![[Spark Ecosystem.png]]

Apache Spark consists of several components that work together to provide a comprehensive and flexible big data processing framework. Here are the main components of Apache Spark:

1. **Spark Core:**
    
    - The foundational and essential component of Spark that provides the basic functionality for distributed data processing. It includes the core data structures, such as Resilient Distributed Datasets (RDDs), and the fundamental mechanisms for task scheduling, fault tolerance, and data distribution.
2. **Spark SQL:**
    
    - A module for structured data processing that allows users to execute SQL queries within Spark. Spark SQL provides a DataFrame API for working with structured and semi-structured data. It also supports reading data from various sources, including Hive, Parquet, JSON, and relational databases.
3. **Spark Streaming:**
    
    - An extension of the core Spark API that enables the processing of live data streams. Spark Streaming allows developers to build scalable and fault-tolerant stream processing applications that can process data in mini-batches or micro-batches.
4. **MLlib (Machine Learning Library):**
    
    - A scalable machine learning library for Spark that provides a wide range of machine learning algorithms and utilities. MLlib enables the development and deployment of machine learning models at scale, making it suitable for large-scale data analysis and predictive modeling.
5. **GraphX:**
    
    - A graph processing library for Spark that allows users to express graph computation tasks in a high-level API. GraphX provides a distributed graph processing framework for tasks such as graph analysis, computation, and iterative graph algorithms.
6. **SparkR:**
    
    - An R package that provides an R interface for Spark, allowing R users to leverage Spark's distributed computing capabilities. SparkR enables data scientists and analysts familiar with R to work with large-scale datasets in a distributed computing environment.
7. **Cluster Manager:**
    
    - Spark can run on various cluster management systems, such as Apache Mesos, Hadoop YARN, and its own standalone cluster manager. The cluster manager is responsible for allocating resources, scheduling tasks, and managing the overall execution of Spark applications across a cluster of machines.
8. **Spark Submit:**
    
    - A command-line tool that simplifies the submission of Spark applications to a cluster. It allows users to specify application parameters, resources, and dependencies when submitting Spark jobs.

## Spark and Pyspark 
![[spark + python.png]]
![[Spark vs pyspark.png]]



- 



#### Local Mode vs Cluster Mode 


## Client + Spark + HDFS 
1. **Spark Application Submission:**
    
    - A user or a developer writes a Spark application on the client machine. The Spark application is submitted to the Spark cluster for execution.
2. **Cluster Resource Allocation:**
    
    - If using a cluster manager (e.g., Apache Mesos, Hadoop YARN), the client communicates with the cluster manager to allocate resources for the Spark application. This includes determining the number of worker nodes and resources (CPU, memory) allocated to each node.
3. **SparkContext Initialization:**
    
    - The Spark application creates a `SparkContext` or `SparkSession` object. This serves as the entry point to Spark functionality and is used to coordinate the execution of tasks across the cluster.
4. **Data Processing Logic:**
    
    - The Spark application contains logic written in Spark's programming API (Scala, Java, Python, or R). This logic defines the series of transformations and actions that Spark will perform on the data.
5. **Data Sources, including HDFS:**
    
    - Spark applications can read data from various sources, and HDFS is a common data source. Spark provides built-in support for reading and writing data from and to HDFS.
6. **Distributed Data Processing:**
    
    - Spark distributes the data processing tasks across the worker nodes in the cluster. Each node processes a portion of the data in parallel, allowing for efficient and scalable data processing.
7. **Result Generation:**
    
    - The Spark application generates results based on the defined transformations and actions. These results may be aggregated, filtered, or transformed data, depending on the application's logic.
8. **Result Storage (Optional):**
    
    - The Spark application can optionally write the results back to HDFS or other storage systems. This is common in scenarios where the processed data needs to be persisted for future analysis or shared with other applications.
9. **Client Retrieval of Results (Optional):**
    
    - If necessary, the client machine can retrieve the final results from HDFS or other storage systems after the Spark application has completed its execution.

In summary, Spark processes the data from HDFS and other sources based on the logic defined in the Spark application. The distributed nature of Spark allows it to efficiently handle large-scale data processing tasks, making it well-suited for big data analytics and data processing workflows.
## Spark Architecture 
![[Spark A.png]]

**Key points of Spark Driver:**

- Manages the overall execution of a Spark application.
- There is only one Driver per Spark application.
- Responsible for coordinating tasks, scheduling, and interacting with the Cluster Manager.
- Initiates SparkContext, which represents a connection to a Spark cluster.
- Monitors the execution progress and ensures fault tolerance.

#### SSH 
SSH, which stands for Secure Shell, is a network protocol that provides a secure way to access and manage remote machines over an unsecured network. In the context of Apache Spark, SSH is often used for cluster management and coordination. Here's how SSH is relevant to Spark:

1. **Cluster Deployment:**
    
    - When deploying a Spark cluster, whether in standalone mode or on a cluster manager like Apache Mesos or Hadoop YARN, SSH is commonly used to access and manage the worker nodes. The Driver Program, running on the master node, uses SSH to communicate with and control the worker nodes in the cluster.
2. **Executor Launching:**
    
    - Spark applications run on a cluster of machines, with the Driver Program executing on the master node and worker nodes executing tasks in parallel. SSH is used to launch Spark executors (worker processes) on the worker nodes. The Driver Program communicates with these executors to distribute and execute tasks.
3. **Data Distribution:**
    
    - In a Spark cluster, data is often distributed across worker nodes. SSH is used to transfer data between nodes securely. This is important for ensuring the reliability and confidentiality of data during distributed computing tasks.
4. **Resource Allocation:**
    
    - When using a cluster manager like Apache Mesos or Hadoop YARN, SSH is employed to request and allocate resources for Spark applications. The Driver Program communicates with the cluster manager via SSH to acquire resources and manage the execution of tasks on the worker nodes.
5. **Communication and Coordination:**
    
    - SSH is utilized for secure communication between the Driver Program and the worker nodes. It enables the Driver Program to issue commands, transfer files, and manage the execution of Spark tasks on the distributed nodes.
#### Driver Program 
- The Spark driver program is the one that creates [SparkContext](https://sparkbyexamples.com/spark/spark-sparkcontext/) object in the application. 
- As soon as we submit the spark job, the driver program runs the main() method of your application and creates DAG’s representing the data flow internally.
-  Based on the DAG workflow, the driver requests the cluster manager to allocate the resources (workers) required for processing. 
- Once the resources are allocated, the driver then using spark context sends the serialized result (code+data) to the workers to execute as Tasks and their result is captured.

**Key points:**

- **Spark Context:** It connects to the cluster manager through the driver to acquire the executors required for processing. Then it sends the serialized result to the workers as tasks to run.
- RDD: Resilient Distributed Datasets are the group of data items that can be stored in memory on worker nodes.
- **Directed Acyclic Graph (DAG):** DAG is a graph that performs a sequence of computations on data.

Apache spark process data in the from of RDDs using the data flow represented in a Direct Acyclic Graph(DAG).


#### Driver Program vs Spark Context

#### Spark context and Spark Session 

#### Container 
In Apache Spark, the term "container" is often used in the context of cluster deployment, particularly when Spark is running on cluster managers like Apache Hadoop YARN or Apache Mesos. The concept of a container is more closely associated with YARN, as Mesos uses a different terminology.

#### Resource manager 


##### YARN 
![[Sparkoverview.png]]

https://www.youtube.com/watch/Pu9qgnebCjs

![[YARN Working.png]]

YARN Framework Overview

1. The YARN cluster comprises a master process (resource manager) and worker processes (node managers).
2. The resource manager runs on the master node, and node managers run on worker nodes.

Node Manager Configuration

3. Each node manager tracks local resources, including virtual cores and memory.
4. Recommended virtual cores = physical cores; Memory is the RAM of the node.
    - Node 1: 4 cores, 8GB RAM
    - Node 2: 4 cores, 16GB RAM
    - Node 3: 2 cores, 8GB RAM
5. Configuration is communicated to the resource manager, resulting in a total of 10 virtual cores and 32GB RAM.
Application Execution in YARN

6. Client runs an application program, consisting of tasks.
7. Application talks to the resource manager, which makes a container request on behalf of the application.
8. Containers are allocated on the cluster to start processes.
9. Container requests virtual cores and memory from the node manager.
    - Example: Container requests 2 virtual cores and 4GB RAM.
10. Once granted, the container uses these resources to start the application master.

Application Master and Task Coordination

11. Application master coordinates tasks on the cluster.
12. Subsequent container requests are made by the master to run tasks.
13. Tasks are run within containers, and the application master coordinates these tasks.
14. When tasks are completed, containers release acquired resources.
15. Application master exits when all tasks are completed.

Spark Running on YARN

16. Spark relies on YARN for resource management.
17. The Spark driver process manages the flow, involving the launch of applications and container requests.
18. Spark tasks are scheduled on executor processes started by node managers.
19. Executors keep running, reducing task start-up time and facilitating in-memory data processing.

Benefits of Executor Processes

1. Executors continue running, unlike the continuous startup of new task processes in MapReduce.
2. This approach in Spark reduces task start-up time and supports in-memory data processing.
3. 
##### Node manager vs YARN 
1. **Node Manager:**
    
    - **Function:** Node Manager is a component of the Hadoop YARN framework responsible for managing resources on individual nodes in a Hadoop cluster.
    - **Role:** It runs on each worker node and is responsible for launching and monitoring containers on that particular node.
    - **Tasks:** Manages resources (CPU, memory, etc.) on the node, starts and stops containers, and communicates with the Resource Manager.
2. **YARN (Resource Manager):**
    
    - **Function:** YARN is the overall resource management framework in Hadoop. It's responsible for managing and allocating resources across the entire cluster.
    - **Role:** It has a central role in the cluster and acts as a negotiator between different applications and Node Managers.
    - **Tasks:** Manages resources at the cluster level, allocates resources to applications, and makes decisions about where to run specific tasks based on the availability of resources.

**Difference:**

- **Scope:**
    
    - **Node Manager:** Manages resources at the individual node level.
    - **YARN (Resource Manager):** Manages resources at the cluster level.
- **Responsibility:**
    
    - **Node Manager:** Responsible for local resource management on a specific node.
    - **YARN (Resource Manager):** Responsible for global resource management across the entire cluster.
- **Role:**
    
    - **Node Manager:** Worker on individual nodes.
    - **YARN (Resource Manager):** Central manager and negotiator for the entire cluster.
- **Communication:**
    
    - **Node Manager:** Communicates with the Resource Manager.
    - **YARN (Resource Manager):** Communicates with all Node Managers and application masters.

In summary, Node Manager is responsible for managing resources on a specific node, while YARN (Resource Manager) oversees resource management at the cluster level, coordinating and allocating resources across all nodes based on the requirements of different applications.


Links https://youtu.be/6iSh62GB8TU

##### Execution
- **Spark's Purpose**
    
    - Processes data in-memory for batch processing, iterative algorithms, and interactive queries.
    - Supports Java, Scala, Python, and R.
- **Spark Application Execution**
    
    - Driver program runs the main function and creates a SparkContext.
    - Executors execute tasks and store data.
- **Architecture Requirements for Spark**
    
    - Supports standalone, Apache Mesos, and Hadoop YARN as cluster managers.
    - Cluster manager allocates resources and manages task distribution.
- **Master-Slave Architecture in Hadoop**
    
    - NameNode is the master for metadata, DataNode is the slave for storing data.
    - Secondary NameNode merges namespace and edits periodically.
- **Master-Slave Architecture in Spark**
    
    - Driver program is the master, executors are the slaves.
    - Executors run tasks and store data.
- **YARN's Role in Spark**
    
    - YARN acts as a resource manager and scheduler.
    - Efficiently shares and manages resources in a Hadoop cluster.
- **Components in YARN**
    
    - Resource Manager manages resource allocation.
    - Node Manager manages resources on a single node, executes tasks on containers.
    - Application Master negotiates resources and works with Node Managers.
- **Application Execution in YARN**
    
    - Spark application submission to YARN creates an Application Master.
    - Application Master negotiates resources with Resource Manager, executes tasks.
- **YARN High Availability**
    
    - Resource Manager High Availability prevents downtime in case of primary RM failure.
- **Conclusion**
    
    - Spark uses YARN for resource management and task distribution.
    - Master-slave architecture is maintained in both Spark and Hadoop YARN.


#### Application Execution  

#### Spark Application Execution:

> Overview

1. **Driver Program Initialization:**
    
    - A Spark application starts with a driver program. This program contains the application's main function and is responsible for creating a `SparkContext` object, which is the entry point for any Spark functionality.
    - The `SparkContext` coordinates with the Cluster Manager for resources and manages the overall execution of the application.
2. **Cluster Manager Connection:**
    
    - Spark supports multiple cluster managers, including standalone, Apache Mesos, and Hadoop YARN. The `SparkContext` connects to the chosen cluster manager to request resources for the application.
3. **Task Execution on Executors:**
    
    - The cluster manager allocates resources (CPU and memory) to the Spark application. These resources are distributed across the cluster nodes.
    - Executors are launched on the allocated resources. Executors are worker nodes responsible for running tasks and storing data.
4. **Task Submission:**
    
    - The driver program divides the Spark application into tasks, where each task represents a unit of work. These tasks are submitted to the Executors for parallel execution.
    - Tasks can be transformations (like map, filter) or actions (like reduce, collect).
5. **Data Distribution:**
    
    - The input data is divided into partitions, and each partition is processed by a separate task. Spark tries to keep the data local to the node where it resides to minimize data transfer.
6. **In-Memory Processing:**
    
    - Spark performs in-memory processing, keeping intermediate data in memory whenever possible. This helps in iterative algorithms and interactive queries by avoiding frequent disk I/O.
7. **Task Execution Flow:**
    
    - The driver program sends the tasks to the Executors, and each Executor runs its assigned tasks.
    - Executors can communicate with each other for shuffling and sorting operations.
8. **Result Aggregation:**
    
    - Once tasks are completed, the results are sent back to the driver program. Spark efficiently aggregates results across nodes.
9. **Driver Program Output:**
    
    - The final results are presented or saved by the driver program. Actions like `collect` or `save` trigger the execution of the Spark application.

- **Key Components Involved:**
    - **Driver Program:**
        - Initiates the Spark application, manages the `SparkContext`, and coordinates the execution.
    - **SparkContext:**
        - Manages the resources, coordinates with the Cluster Manager, and splits the application into tasks.
    - **Cluster Manager:**
        - Allocates resources to the Spark application. Examples include standalone, Mesos, or YARN.
    - **Executors:**
        - Worker nodes that execute tasks and store intermediate data. Multiple Executors run concurrently on cluster nodes.
    - **Tasks:**
        - Units of work representing transformations or actions. Tasks are executed in parallel across the cluster.

This process allows Spark to efficiently distribute computation across a cluster of machines, providing high-performance data processing capabilities. The ability to perform in-memory processing and parallelize tasks contributes to Spark's speed and versatility.


> **Working Process :**

- Let’s say a user submits a job using “spark-submit”.
- “spark-submit” will in-turn launch the Driver which will execute the main() method of our code.
- Driver contacts the cluster manager and requests for resources to launch the Executors.
- The cluster manager launches the Executors on behalf of the Driver.
- Once the Executors are launched, they establish a direct connection with the Driver.
- The driver determines the total number of Tasks by checking the Lineage.
- The driver creates the Logical and Physical Plan.
- Once the Physical Plan is generated, Spark allocates the Tasks to the Executors.
- Task runs on Executor and each Task upon completion returns the result to the Driver.
- Finally, when all Task is completed, the main() method running in the Driver exits, i.e. main() method invokes sparkContext.stop().
- Finally, Spark releases all the resources from the Cluster Manager.


#### Resource Allocation + Executor + Partitioning 
**Resource Allocation:**

- The Spark application starts with the driver program, initializing a `SparkContext`.
- The `SparkContext` communicates with the Cluster Manager to request resources.
- Various cluster managers (standalone, Mesos, YARN) are supported.
- The cluster manager allocates resources to the application, launching executors.

**Executor Initialization:**

- Executors start on worker nodes.
- Each executor has its allocated resources (CPU cores and memory).
- Multiple executors run concurrently on different nodes.

**Data Partitioning:**

- Input data is divided into partitions.
- Partitions are processed independently by tasks.
- The goal is even distribution across the cluster.

**Parallel Processing:**

- Spark operates on data in parallel.
- Tasks process multiple partitions simultaneously.
- Number of partitions impacts parallelism and efficiency.

**Shuffling:**

- Operations like grouping or joining may require data exchange.
- Shuffling involves redistributing and exchanging data.
- Impacts performance due to network and disk I/O.

**Task Submission:**

- Driver program breaks down the application into tasks.
- Tasks are submitted to executors for parallel execution.

**Task Execution Flow:**

- Executors execute tasks independently and in parallel.
- Tasks involve transformations or actions.

**Data Processing:**

- In-memory processing reduces disk I/O.
- Intermediate results stored in memory for efficiency.

**Result Aggregation:**

- Results are aggregated across nodes.
- Involves collecting and combining data.

**Driver Program Output:**

- Final results presented or saved.
- Marks completion of the Spark application.

**Key Components:**

- **Driver Program:** Initiates and manages the application.
- **SparkContext:** Manages resources and communication.
- **Cluster Manager:** Allocates resources.
- **Executors:** Execute tasks and store data.
- **Tasks:** Units of work executed in parallel.


###### Executor 

![[Saprk Executor.png]]
Executors in Apache Spark are located on each worker node in the Spark cluster. Each worker node typically runs one or more Executors, and these Executors are responsible for executing tasks assigned to them by the Spark Driver. The distribution of Executors across worker nodes enables parallel processing of data in a distributed fashion.

Here's a brief overview of how Executors are distributed in a Spark cluster:

1. **Worker Nodes:** In a Spark cluster, there are multiple worker nodes. Each worker node is a physical or virtual machine that contributes computational resources to the cluster.
    
2. **Executors on Worker Nodes:** Executors are launched on each worker node. The number of Executors on a node is configurable, and it depends on the available resources on that particular node.
    
3. **Task Execution:** When a Spark application is submitted, tasks are divided across the partitions of the data, and these tasks are sent to Executors for execution.
    
4. **Parallel Execution:** Executors on different nodes can execute tasks in parallel, processing data distributed across the cluster.
    
5. **Data Storage:** Executors on each node also manage the storage of data partitions in memory and on disk, contributing to Spark's ability to cache and reuse intermediate results for performance optimization.
    
6. **Fault Tolerance:** Executors play a role in fault tolerance by re-executing tasks in case of failures. The Spark Driver keeps track of the lineage information in the Directed Acyclic Graph (DAG) to recover lost data by re-computing tasks on available Executors.







#### Client Mode vs Cluster mode 

--- start-multi-column: ID_6kt3
```column-settings
Number of Columns: 3
Largest Column: standard
```

Aspect

Driver Location 

Resource Utilization 

communication 

Use case 

Advantages 


--- column-break ---

Cluster mode 

Driver program runs on one of the worker nodes within the cluster.

Cluster manager allocates resources for both the driver and executor programs, utilizing the entire cluster.

After submission, the client machine's involvement diminishes, and the cluster manager handles resource allocation.

More suitable for large-scale production deployments where cluster resources are required for efficient execution.

Efficient utilization of cluster resources; well-suited for scenarios where the client machine may lack sufficient resources.

--- column-break ---

Client mode

Driver program runs on the machine where the Spark application is submitted.

Client machine actively participates in execution, using its own resources for running the driver program.

Driver communicates directly with the cluster manager to request and allocate resources for executors.

Suitable for development, debugging, and scenarios where the client machine has sufficient resources.

Easier debugging and monitoring; suitable for scenarios where the client machine has enough resources for the driver

--- end-multi-column

Links - https://sparkbyexamples.com/spark/spark-deploy-modes-client-vs-cluster/
https://youtu.be/uvup4DIzVZ8
 

In the context of Apache Spark, "client mode" and "cluster mode" refer to the ways in which a Spark application can be executed in a distributed environment. The choice between these modes depends on how the Spark driver program is managed and where it runs. Let's delve into each mode:

1. **Client Mode:**
    
    - In client mode, the driver program runs on the machine where the Spark application is submitted.
    - The client machine is responsible for initiating the SparkContext and overseeing the execution of the application.
    - The driver program interacts with the cluster manager (such as YARN, Mesos, or Standalone) to request resources for task execution.
    - The application's output and logs are typically sent back to the client machine.
    - This mode is often used during development and debugging when the developer wants to have direct access to the Spark driver program.
    
    To submit a Spark application in client mode, you might use a command like:

    
    `spark-submit --master yarn --deploy-mode client your_app.py`
    
2. **Cluster Mode:**
    
    - In cluster mode, the driver program runs on one of the cluster's worker nodes rather than on the machine where the application was submitted.
    - The client machine is responsible for initiating the SparkContext, but the actual Spark driver runs within the cluster.
    - The driver program interacts with the cluster manager to request resources and manage the execution of tasks.
    - The application's output and logs are stored on the cluster, and the client machine typically only receives the final status.
    - This mode is commonly used in production environments for large-scale distributed processing.
    
    To submit a Spark application in cluster mode, you might use a command like:
    
    
    `spark-submit --master yarn --deploy-mode cluster your_app.py`
    

The choice between client and cluster mode depends on factors such as the development or production nature of the application, resource management preferences, and whether direct access to the driver program's logs and outputs is essential.

Both modes leverage Spark's ability to distribute computation across a cluster, but the distinction lies in where the Spark driver program is executed and where the application's output is managed.



#### Spark Submit 

Links - https://medium.com/@mojtaba81/introduction-to-spark-submit-d22cde2dfa86


#### Partitioning 
Spark is a cluster processing engine that allows data to be processed in parallel. Apache Spark's parallelism will enable developers to run tasks parallelly and independently on hundreds of computers in a cluster. All thanks to Apache Spark's fundamental idea, RDD.

![[RDD Partition.png]]

[Resilient Distributed Datasets](https://www.projectpro.io/article/working-with-spark-rdd-for-fast-data-processing/273 "Spark RDD") are collection of various data items that are so huge in size, that they cannot fit into a single node and have to be partitioned across various nodes. Spark automatically partitions RDDs and distributes the partitions across different nodes. A partition in spark is an atomic chunk of data (logical division of data) stored on a node in the cluster. Partitions are basic units of parallelism in Apache Spark. RDDs in Apache Spark are collection of partitions.

Resilient Distributed Datasets (RDDs) are a fundamental data abstraction that represents a distributed collection of data. RDDs are divided into partitions, and the efficient execution of RDDs in Spark involves the parallel processing of these partitions across a distributed cluster of machines. Here's how RDDs are partitioned and executed efficiently in Spark:

###### 1. **Partitioning:**

- **Division of Data:**
    
    - RDDs logically represent a collection of data, but in practice, the data is divided into partitions.
    - Partitions are the basic units of parallelism, allowing Spark to distribute the work across multiple nodes in the cluster.
- **User-Specified or Default:**
    
    - Partitioning can be user-specified when creating an RDD, or Spark can use a default partitioning strategy based on the underlying data source (e.g., HDFS blocks).
- **Independence of Partitions:**
    
    - Partitions are processed independently of each other, which enables parallel execution and scalability.

###### 2. **Task Execution:**

- **Task Distribution:**
    
    - RDD operations, such as transformations and actions, are broken down into tasks.
    - Each task operates on a single partition of the RDD.
- **Task Execution in Executors:**
    
    - Tasks are executed by Executors, which are distributed across the worker nodes in the Spark cluster.
    - Executors process tasks in parallel, each responsible for its assigned partition.

###### 3. **Data Locality:**

- **Minimizing Data Movement:**
    - Spark aims to execute tasks on the node where the corresponding data partition resides (data locality).
    - This minimizes data movement across the network, improving performance.

###### 4. **Efficient Computation:**

- **In-Memory Processing:**
    
    - Spark encourages in-memory processing by caching or persisting RDD partitions in memory.
    - This reduces the need to read data from disk repeatedly and speeds up iterative algorithms.
- **Lazy Evaluation:**
    
    - Spark uses lazy evaluation, meaning transformations on RDDs are not executed immediately but rather when an action is triggered.
    - This allows Spark to optimize the execution plan based on the sequence of transformations and actions.

###### 5. **Task Scheduling:**

- **Dynamic Task Scheduling:**
    - Spark schedules tasks dynamically, optimizing the execution plan based on the available resources in the cluster.
    - Executors may be added or removed based on the workload.

###### 6. **Fault Tolerance:**

- **Lineage Information:**
    
    - RDDs maintain lineage information, recording the sequence of transformations applied to derive the current RDD.
    - In case of data loss or task failure, Spark uses lineage information to recompute lost partitions.
- **Task Re-execution:**
    
    - Failed tasks can be re-executed on available Executors, ensuring fault tolerance and data reliability.

In summary, the efficient execution of RDDs in Spark involves the careful partitioning of data, parallel execution of tasks across distributed Executors, data locality to minimize data movement, and optimization through in-memory processing and lazy evaluation. These characteristics contribute to the scalability and performance of Spark applications.

#### Spark RDD 
Link - https://youtu.be/nH6C9vqtyYU
>  https://www.tutorialspoint.com/apache_spark/apache_spark_rdd.htm



RDD stands for Resilient Distributed Dataset, and it is a fundamental data structure in Apache Spark, a distributed computing framework. RDDs are designed to handle distributed data processing across a cluster of computers. Here are some key characteristics and aspects of RDDs:

1. **Distributed Computing:** RDDs allow data to be distributed across multiple nodes in a cluster. This enables parallel processing and can significantly improve the performance of data-intensive tasks.
    
2. **Resilience:** The term "resilient" in RDD refers to the ability to recover from node failures. RDDs achieve fault tolerance by keeping track of the transformations applied to the data, allowing them to be recomputed in case a partition of the dataset is lost due to a node failure.
    
3. **Immutability:** RDDs are immutable, meaning that once created, their content cannot be changed. Instead of modifying an RDD in place, you create a new RDD by applying transformations. This immutability simplifies fault recovery and enables some optimizations.
    
4. **Lazy Evaluation:** Transformations on RDDs are lazily evaluated, meaning that the execution is deferred until an action is triggered. This allows Spark to optimize the execution plan by combining multiple transformations and avoiding unnecessary computations.
    
5. **Transformation and Action Operations:**
    
    - **Transformations:** These are operations that create a new RDD from an existing one. Examples include `map`, `filter`, `flatMap`, and `groupByKey`.
    - **Actions:** These are operations that return a value to the driver program or write data to an external storage system. Examples include `count`, `collect`, `reduce`, and `saveAsTextFile`.
6. **Parallel Processing:** RDDs support parallel processing by dividing the data into partitions, each of which can be processed independently on different nodes of the cluster.
    
7. **Caching:** RDDs can be explicitly cached in memory to speed up iterative algorithms or to reuse them across multiple stages of a computation.
    

It's worth noting that while RDDs were a foundational abstraction in Spark, later versions of Spark introduced higher-level abstractions like DataFrames and Datasets, which provide a more structured and optimized API for working with distributed data. These abstractions build on the concepts of RDDs but offer additional optimizations and ease of use.


##### RDD + DAG 
Resilient Distributed Dataset (RDD) and Directed Acyclic Graph (DAG) are closely intertwined in the context of Apache Spark. RDDs serve as the foundational data structure, representing a distributed collection of data processed in parallel across a cluster of machines. RDDs are immutable and support transformations (e.g., `map`, `filter`) and actions (e.g., `count`, `collect`).

Transformations applied to RDDs create new RDDs, and RDDs maintain lineage information. This lineage information, essentially a record of transformations, is crucial for fault tolerance. In the event of data loss in a partition, Spark can utilize the lineage information to recompute the lost partition from the original data source.

The logical execution plan of Spark applications is represented by a Directed Acyclic Graph (DAG). The DAG captures the sequence of transformations and actions, providing a high-level view of the computation plan. Spark optimizes the execution plan based on the DAG, identifying common subexpressions, dependencies, and dividing the DAG into stages for parallel execution.

Tasks, representing the smallest unit of work, are derived from the stages in the DAG. Each task can be executed on individual partitions of the data. The dynamic task scheduling in Spark leverages the DAG to optimize task execution based on the available resources.

In essence, RDDs and DAGs in Spark are interdependent. RDDs provide the data abstraction, while the transformations on RDDs are logically represented by the DAG. The DAG, in turn, facilitates optimization, fault tolerance, and efficient parallel execution of Spark jobs.



#### Action and Transformations 
https://data-flair.training/blogs/spark-rdd-operations-transformations-actions/

 A **Transformation** is a function that produces new **RDD** from the existing RDDs but when we want to work with the actual dataset, at that point **Action** is performed. When the action is triggered after the result, new RDD is not formed like transformation
##### RDD Transformation

**Spark Transformation** is a function that produces new RDD from the existing RDDs. It takes RDD as input and produces one or more RDD as output. Each time it creates new RDD when we apply any transformation. Thus, the so input RDDs, cannot be changed since RDD are immutable in nature.

Applying transformation built an **RDD lineage**, with the entire parent RDDs of the final RDD(s). RDD lineage, also known as **RDD operator graph** or **RDD dependency graph.** It is a logical execution plan i.e., it is Directed Acyclic Graph (**[DAG](https://data-flair.training/blogs/directed-acyclic-graph-dag-in-apache-spark/)**) of the entire parent RDDs of RDD.

**[Transformations are lazy](https://data-flair.training/blogs/lazy-evaluation-in-apache-spark-guide/)** in nature i.e., they get execute when we call an action. They are not executed immediately. Two most basic type of transformations is a map(), filter().  
After the transformation, the resultant RDD is always different from its parent RDD. It can be smaller (e.g. filter, count, distinct, sample), bigger (e.g. flatMap(), union(), Cartesian()) or the same size (e.g. map).

###### Narrow Transformation 
 Narrow transformations are transformations where each partition of the resulting RDD depends on only one partition of the parent RDD. These transformations do not require shuffling or data exchange between partitions. As a result, they are more efficient and faster.
 Examples of Narrow Transformations:

1. **`map(func)` and `mapPartitions(func)`:**
    
    - Each element in the resulting RDD is a result of applying a function to a corresponding element or a partition of the parent RDD.
2. **`filter(func)`:**
    
    - Elements in the resulting RDD are filtered based on a condition without requiring information from other partitions.
3. **`union(otherDataset)`:**
    
    - Combines two RDDs without shuffling data between partitions. Each partition of the resulting RDD is derived independently._
![[NARROW TRANSFORMATION.png]]
###### Wide Transformation 
Wide transformations are transformations where each partition of the resulting RDD depends on multiple partitions of the parent RDD. These transformations often require shuffling or redistribution of data across the cluster, which can be a more resource-intensive operation.

 Examples of Wide Transformations:

1. **`groupByKey()`:**
    
    - Groups data based on a key, and this may require shuffling data across partitions.
2. **`reduceByKey(func)`:**
    
    - Aggregates values based on keys, involving shuffling of data to perform the reduction.
3. **`join(otherDataset)`:**
    
    - Combines two RDDs based on a common key, and it involves shuffling data to bring together related key-value pairs.

Working of Narrow Transformations:

- **Independence of Partitions:**
    
    - Each partition of the resulting RDD is computed independently of other partitions.
    - No data exchange or communication between partitions is needed during the execution.
- **Efficiency:**
    
    - Narrow transformations are generally more efficient as they don't require extensive data movement or shuffling.

Working of Wide Transformations:

- **Dependency on Multiple Partitions:**
    
    - Each partition of the resulting RDD depends on data from multiple partitions of the parent RDD.
    - This may involve the exchange of data across the network.
- **Shuffling:**
    
    - Shuffling occurs, where data is reorganized and redistributed among partitions, often leading to increased computation time.
- **Resource Intensiveness:**
    
    - Wide transformations are more resource-intensive compared to narrow transformations due to the need for inter-partition communication.
![[Wide Transformation.png]]



### Lazy Evaluation 
https://www.scaler.com/topics/lazy-evaluation-in-spark/


### RDD + DAG 
In Apache Spark, RDDs (Resilient Distributed Datasets) and Directed Acyclic Graphs (DAGs) are closely related concepts. RDDs are the fundamental data abstraction in Spark, representing distributed collections of data, while DAGs provide a logical representation of the sequence of transformations and actions applied to RDDs in a Spark application.

##### RDD (Resilient Distributed Dataset):

1. **Definition:**
    
    - RDD is a distributed collection of immutable data that can be processed in parallel across a cluster of machines.
2. **Characteristics:**
    
    - RDDs are divided into partitions, and each partition can be processed independently on different nodes in the cluster.
    - They support transformations (e.g., `map`, `filter`) and actions (e.g., `count`, `collect`).
3. **Lineage Information:**
    
    - RDDs maintain lineage information, recording the sequence of transformations applied to derive the current RDD.
    - Lineage information is crucial for fault tolerance and recomputing lost data.
4. **Transformation and Action Operations:**
    
    - Transformations on RDDs create new RDDs, and actions trigger the execution of these transformations, resulting in the materialization of the data.

##### DAG (Directed Acyclic Graph):

1. **Definition:**
    
    - DAG is a logical representation of the sequence of transformations and actions applied to RDDs in a Spark application.
2. **Characteristics:**
    
    - It is a directed acyclic graph where nodes represent RDDs, and edges represent the transformations or actions applied.
    - Transformations on RDDs contribute to the creation of the DAG.
3. **Optimization Opportunities:**
    
    - The DAG allows Spark to optimize the execution plan by rearranging operations, identifying common subexpressions, and dividing the computation into stages.
4. **Stages and Tasks:**
    
    - The DAG is divided into stages, where each stage represents a set of transformations that can be executed in parallel.
    - Tasks are the smallest units of work, executed on individual partitions of the data.

##### Relationship:

1. **Logical Flow of Operations:**
    
    - RDDs are created through transformations and actions, and the sequence of these operations is logically captured by the DAG.
2. **DAG Construction:**
    
    - As transformations are applied to RDDs, the DAG is constructed incrementally to represent the flow of data and operations.
3. **Optimization using DAG:**
    
    - The DAG provides Spark with a comprehensive view of the computation plan, allowing for optimization opportunities.
    - Spark can optimize the execution plan based on the DAG, rearranging operations for better performance.
4. **Fault Tolerance and Lineage:**
    
    - RDD lineage information, which contributes to fault tolerance, is reflected in the DAG.
    - If a partition is lost, Spark can use the lineage information in the DAG to recompute the lost data.

In summary, RDDs are the data abstraction in Spark, and DAGs are the logical representation of the computation plan. The creation and transformations of RDDs contribute to the construction of the DAG, providing Spark with the necessary information to optimize and execute the Spark job efficiently.

##### Lineage Graph
A lineage graph in Apache Spark is a directed acyclic graph (DAG) that represents the sequence of transformations and dependencies between RDDs (Resilient Distributed Datasets) in a Spark computation. It captures the lineage or the logical execution plan of a Spark application.

Here are the key aspects of the lineage graph:

1. **Definition:**
    
    - A lineage graph is a directed acyclic graph where each node represents an RDD, and each edge represents a transformation operation applied to derive a new RDD.
2. **Construction:**
    
    - The lineage graph is constructed as transformations are applied to RDDs in a Spark application.
    - Each RDD in the lineage graph is associated with the transformation that created it.
3. **Dependency Relationships:**
    
    - Nodes (RDDs) in the lineage graph have dependencies on the parent RDDs from which they were derived.
    - The edges in the graph represent the dependencies between RDDs, showing how data flows from one RDD to another through transformations.
4. **Fault Tolerance:**
    
    - The lineage graph is a key component of Spark's fault-tolerance mechanism.
    - If a partition of an RDD is lost due to node failure, Spark can use the lineage graph to recompute the lost partition by replaying the transformations from the original data source.
5. **Optimization:**
    
    - Spark uses the lineage graph for optimization purposes.
    - During the execution planning phase, Spark can optimize the DAG by identifying common subexpressions, reordering transformations, and dividing the computation into stages.
6. **DAG and Lineage Graph Relationship:**
    
    - The lineage graph is an integral part of the larger Directed Acyclic Graph (DAG) that represents the entire computation plan of a Spark application.
    - The lineage graph focuses specifically on the dependencies and transformations applied to RDDs.


### Job Execution 
.
Important - https://data-flair.training/blogs/how-apache-spark-works/


