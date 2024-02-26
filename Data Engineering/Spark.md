---
banner: "![[Spark.png]]"
---

Contents

- [Hadoop vs Spark](#Hadoop%20vs%20Spark)
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
		- [Client Mode vs Cluster mode](#Client%20Mode%20vs%20Cluster%20mode)
		- [Spark Submit](#Spark%20Submit)

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





#### Spark Submit 

Links - https://medium.com/@mojtaba81/introduction-to-spark-submit-d22cde2dfa86

