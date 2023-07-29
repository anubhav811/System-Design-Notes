# System-Design-Notes


- Reliability : The system should be fault tolerant and working when faults/error happen. It’s measured in terms of robustness, failures and effect analysis of the sub systems of the larger system.
- Scalability : Should should be able to cater to the growing users, traffic and data. It’s measured in terms of resources allocation, utilization, serviceability and availability.
- Availability : It’s measured by the percentage of time in a given period that a system is available to perform the assigned task without any failure(s).
- Efficiency : It’s measured in terms of reusability of components, simplicity and productivity.

And all of it bottles down to three things — **Cost, Speed and Failures.**

**Maintainability** means even after adding new functionalities and features as per the new requirements, the system and the existing code should work.

![[Pasted image 20230728094757.png]]


APIs
READ API
WRITE API
SEARCH API
	- _takes a query string as input and returns a list of documents that match the query_


**Services**
Services are commonly used in the context of microservices architecture, where a large application is broken down into smaller, manageable services. Each service handles a specific business capability and can be developed, deployed, and scaled independently.

For example, in a web-based e-commerce application, you might have services such as:

1. User Service: Manages user registration, authentication, and profile information.
2. Product Service: Handles product catalog, inventory, and pricing.
3. Cart Service: Manages user shopping carts and checkout process.
4. Payment Service: Handles payment processing and transaction management.
5. Recommendation Service: Provides personalized product recommendations to users.
6. Notification Service: Sends notifications and emails to users.


## User Info Service
In a system, the User Info Service would be responsible for managing the following tasks:

- _Creating new user accounts_
- _Authenticating users and validating their credentials_
- _Retrieving user profile information (e.g. name, email address, profile picture, etc.)_
- _Updating user profile information_
- _Deleting user accounts_

## User Graph Service
A user graph service is a component in a system design that manages and maintains the relationships between users in a network. It is responsible for storing and updating information about user connections, such as friend lists, followers, or other types of relationships.

## Timeline Service
A timeline service in system design is responsible for managing and presenting a chronological list of events or activities

## Notification Service
A notification service in system design is a mechanism that allows a system to send notifications to users or other systems about events or changes in the system. In order to implement a notification service, you will need to define the message format, the delivery mechanism, and the logic for handling incoming notifications.

**Redis Pub/Sub** (Publish/Subscribe) is a messaging system or messaging pattern provided by Redis, an open-source, in-memory data structure store. It allows for real-time message distribution among multiple subscribers. The Pub/Sub mechanism is often used to build scalable and event-driven architectures.

It's essential to note that Redis Pub/Sub follows a "fire-and-forget" approach. This means that Redis doesn't keep track of whether a subscriber received a message or not. If a subscriber is not actively listening (e.g., offline at the moment of publishing), the message is lost, and the subscriber won't receive it when it comes back online.

Keep in mind that while Redis Pub/Sub is straightforward and effective for certain use cases, it lacks some advanced features like message persistence and guaranteed message delivery, which can be crucial for more complex messaging systems. For such requirements, using dedicated message brokers like RabbitMQ or Apache Kafka might be more appropriate.

## Full text search service
A full text search service in system design is a mechanism that allows a system to search for and retrieve documents or other data based on keyword or phrase searches. It is often used in systems that have large amounts of unstructured or semi-structured data, such as text documents or web pages. In order to implement a full text search service, you will need to define the data model and indexing strategy, the search API, and the logic for querying and retrieving results.

Elasticsearch is a popular and powerful open-source search and analytics engine built on top of Apache Lucene. It is commonly used as a full-text search service and offers various capabilities for searching, analyzing, and visualizing data.

Here are some key features and concepts of Elasticsearch as a full-text search service:

1. Full-Text Search: Elasticsearch is designed to handle full-text search efficiently. It can index and search through large volumes of text data in real-time, making it suitable for applications that require fast and accurate text-based searches.
    
2. Indexing: In Elasticsearch, data is organized into indices, which can be thought of as collections of documents. Each document represents a single data entry and is in JSON format. When you index data into Elasticsearch, it automatically creates an index and stores the documents accordingly.
    
3. Analysis: Elasticsearch performs text analysis during the indexing process. This includes tasks like tokenization (breaking text into individual words or tokens), stemming (reducing words to their root form), and lowercasing. This analysis helps in creating an inverted index, which significantly speeds up text search operations.
    
4. Query DSL: Elasticsearch provides a powerful Query Domain-Specific Language (DSL) that allows you to construct complex queries to search for specific text patterns or perform aggregations on the data.
    
5. Real-time Search: As soon as you index data into Elasticsearch, it becomes available for searching. This real-time capability makes it suitable for applications that require up-to-date search results.
    
6. Scalability: Elasticsearch is designed to scale horizontally, meaning you can add more nodes to the cluster to handle increasing data and query loads. This allows for high availability and performance even with large datasets.
    
7. RESTful API: Elasticsearch exposes a RESTful API, making it easy to interact with the service using simple HTTP requests. You can perform indexing, searching, and administrative operations through the API.
    
8. Distributed Architecture: Elasticsearch is a distributed system by nature, which means it can be deployed across multiple nodes to ensure fault tolerance and improved performance.
    
9. Text Relevance Scoring: Elasticsearch calculates a relevance score for each document based on how well it matches the query. This score helps in ranking the search results in order of relevance.

It's important to note that while Elasticsearch is a powerful search engine, setting up and managing a production-ready Elasticsearch cluster can be complex. For simpler use cases, hosted Elasticsearch solutions are available from cloud service providers, which handle the infrastructure management for you.

## Caching Service
Caching works by storing data in a fast-access storage area that is close to the data consumer. When data is requested, the system checks the cache first to see if the data is already available. If the data is available in the cache, it is retrieved and returned to the consumer. If the data is not available in the cache, the system retrieves the data from the original source and stores it in the cache for future use.

## Fan Out Service
It’s the process of distributing requests or messages from a single source to multiple destinations.
This is a common pattern in distributed systems, where a service or application needs to send information to multiple downstream systems.

_One way to implement a fan out service is to use a message queue. The service would receive requests or messages from the source system, and then publish those messages to a message queue. Each downstream system would then subscribe to the message queue and receive a copy of the message._

**RabbitMQ** is an open-source message broker software that facilitates communication between different applications or components by implementing the Advanced Message Queuing Protocol (AMQP). It provides a flexible and scalable messaging system, enabling decoupling of producers and consumers of messages.

Key concepts and features of RabbitMQ include:

1. Message Broker: RabbitMQ acts as an intermediary or message broker between applications. Producers send messages to RabbitMQ, and RabbitMQ routes those messages to the appropriate consumers.
    
2. Queues: Messages are placed into queues within RabbitMQ. Queues hold the messages until they are consumed by the intended recipients. This decouples message production from consumption, allowing for asynchronous communication.
    
3. Exchange: Producers send messages to exchanges, which are responsible for routing messages to the correct queues based on defined rules or bindings. Different types of exchanges (e.g., direct, topic, fanout) determine how messages are routed.
    
4. Consumers (Subscribers): Consumers, also known as subscribers or workers, retrieve messages from queues and process them. They can consume messages at their own pace, and RabbitMQ ensures messages are delivered to only one consumer at a time.
   
5. Publishers: Applications that send messages to RabbitMQ are known as publishers. They publish messages to exchanges, which then route the messages to the appropriate queues.


# Components

## Memory Cache
In a system, the memory cache would be responsible for managing the following tasks:

- _Storing and retrieving data from memory_
- _Expiring or invalidating cached data after a certain amount of time or under certain conditions_
- _Maintaining cache consistency and preventing data corruption_
- _Managing cache capacity to avoid running out of memory_

## DNS (Domain Name System)

It is a system used to translate human-readable domain names into IP addresses. It acts as a directory for the internet, allowing users to easily access websites and other internet services without needing to remember IP addresses.

In a system, a DNS server would be responsible for managing the following tasks:

- _Resolving domain names into IP addresses_
- _Caching resolved IP addresses to improve performance_
- _Load balancing between multiple IP addresses for a given domain name_
- _Handling domain name registration and management_

## Real-time message Ingestion

Real-time message ingestion is the process of capturing and processing messages as they are generated in real-time.

In a system, real-time message ingestion would be responsible for managing the following tasks:

- _Capturing messages as they are generated_
- _Storing messages in a way that allows for efficient retrieval and querying_
- _Processing messages in real-time to perform actions such as notifications or real-time analytics_
- _Scaling to handle high message volume and ensure high availability_


## Load Balancer
A load balancer is a system component that distributes incoming network traffic across multiple servers to improve performance, reliability, and availability.

In a system, a load balancer would be responsible for managing the following tasks:

- _Monitoring server health and availability_
- _Distributing traffic across available servers_
- _Managing session persistence (i.e. ensuring that subsequent requests from a client are routed to the same server)_
- _Handling SSL termination (i.e. decrypting encrypted traffic and forwarding it to the appropriate server)_

## Content Delivery Network (CDN)

A Content Delivery Network (CDN) is a distributed network of servers that helps to deliver content faster and more efficiently to end-users by caching content closer to the user’s location.

A CDN can be used in a system design to improve website performance and reliability by reducing latency, improving website availability and scalability, and reducing bandwidth costs.

Amazon CloudFront is a content delivery network (CDN) service provided by Amazon Web Services (AWS). It is designed to deliver static and dynamic web content, including images, videos, applications, and APIs, to users with low latency and high data transfer speeds. CloudFront helps improve the performance, availability, and scalability of web applications and content distribution by caching and delivering content from edge locations closer to end-users.

# Job Server

A job server in system design is responsible for managing and executing background jobs or tasks asynchronously. It can be used in various applications such as web scraping, data processing, or batch processing.

The implementation of a job server can be done using the following steps:

1. _Job queue: Define a job queue to store the jobs to be executed. This can be a message queue such as RabbitMQ, a database table, or a simple in-memory data structure such as a list._
2. _Job producer: Define a job producer to add jobs to the job queue. This can be a user interface, a REST API endpoint, or any other application logic that generates jobs._
3. _Job consumer: Define a job consumer to fetch jobs from the job queue and execute them. This can be a worker process that runs continuously in the background, or a scheduler that runs periodically to check for new jobs._
4. _Job executor: Define the logic for executing the jobs. This includes processing input data, performing the necessary calculations or operations, and generating output data._


## Workers

Workers in system design refer to background processes that perform tasks asynchronously and independently of the main system flow.
They are often used to perform tasks that are time-consuming or resource-intensive, such as processing large files, sending emails, or performing data analysis.

## App servers
An application server in system design is a server that provides a platform for running and managing applications, often in a distributed or scalable environment. It typically includes features such as load balancing, caching, and session management, and is often used to deploy web applications or APIs.
They act as intermediaries between the front-end user interface (client-side) and the backend databases and services (server-side).

## Queues
Queues are an important part of many system designs, allowing you to process tasks and messages in a distributed or asynchronous manner

## Object storage

Object storage is a method of storing and retrieving unstructured data in the form of objects. It is often used to store large amounts of data, such as media files, and can be accessed over a network using APIs.

How Object Storage and CDN are related:

1. Origin Storage: Object Storage often serves as the "origin storage" for the CDN. The original web content, such as images, videos, and other static assets, are stored in the object storage system.
    
2. Content Distribution: When a user requests content from a website or web application, the CDN fetches the requested content from the object storage system. The content is then cached in the CDN's edge locations (edge caching) for subsequent requests from other users. Caching the content closer to the end-users reduces the need to fetch the same content repeatedly from the origin storage, resulting in faster load times and reduced load on the origin server.
    
3. Global Content Delivery: CDNs use their distributed network of edge servers to deliver content to users from the nearest edge location. Object storage, on the other hand, can be located in a centralized or distributed manner. The combination of object storage and CDN ensures that content is efficiently delivered to users worldwide with low latency.
    
4. Scalability: Both Object Storage and CDN are designed to handle large-scale data distribution and high volumes of content delivery. This makes them suitable for serving content to a global user base without compromising performance.
    

By combining Object Storage with a CDN, organizations can effectively deliver large-scale, media-rich content and web assets to users worldwide with low latency, high availability, and improved overall performance.


## Authentication
Authentication is the process of verifying the identity of a user, typically by requiring them to provide credentials such as a username and password.

## Batch processing
Batch processing is a data processing method used in system design to process large volumes of data as a group or "batch." Instead of processing data in real-time, batch processing collects, stores, and processes data in discrete batches at scheduled intervals or when a predefined volume of data is reached. It is commonly used for data-intensive tasks that do not require immediate processing or response.

Key characteristics and concepts of batch processing in system design include:

1. Data Accumulation: Batch processing systems accumulate data over time until a specific batch size or time window is reached. The collected data is then processed together as a group.
    
2. Scheduled Execution: Batch jobs are scheduled to run at specific intervals, such as hourly, daily, or weekly, depending on the system's requirements. These schedules are often chosen based on the data volume, processing complexity, and business needs.
    
3. Data Transformation: Batch processing typically involves transforming and processing raw data into a format suitable for analysis, reporting, or storage. Common data transformations include aggregations, filtering, sorting, and joining datasets.
    
4. Reduced Real-time Requirements: Unlike real-time processing systems, batch processing systems do not require immediate results. This makes batch processing suitable for tasks that can tolerate some delay between data collection and processing.
    
5. Scalability: Batch processing can handle large volumes of data efficiently by leveraging distributed processing and parallelization techniques, making it suitable for big data processing scenarios.
    
6. Error Handling: Batch processing systems should have mechanisms to handle errors and exceptions that may occur during data processing. Logging and error reporting are essential for diagnosing and resolving issues.
    
7. ETL (Extract, Transform, Load): Batch processing is commonly used in Extract, Transform, Load (ETL) processes, where data is extracted from various sources, transformed to fit the target format, and then loaded into a data warehouse or another storage system for analysis.


## Cloud storage
Cloud storage is a method of storing data in a remote server or a network of servers that are accessible over the internet.

It is commonly used in systems that require scalable, flexible, and reliable storage solutions.

Cloud storage has become an integral part of modern data management, enabling individuals, businesses, and organizations to store, share, and back up their data in a convenient and cost-effective manner. It also plays a significant role in supporting other cloud-based services, such as cloud computing, content delivery networks (CDNs), and file sharing platforms.

Amazon S3 (Amazon Simple Storage Service) is a highly scalable and secure cloud storage service provided by Amazon Web Services (AWS). It is designed to store and retrieve any amount of data from anywhere on the web, making it a popular choice for businesses and developers looking for reliable and cost-effective storage solutions.

Key features and characteristics of Amazon S3 include:

1. Object Storage: Amazon S3 stores data as objects, each consisting of data, a unique identifier (key), and optional metadata. These objects can range in size from a few bytes to multiple terabytes.
    
2. Data Durability and Availability: Amazon S3 provides a high level of data durability by replicating objects across multiple data centers within an AWS Region. This redundancy ensures that data is protected against hardware failures or other issues, offering a 99.999999999% (11 nines) durability guarantee.
    
3. Scalability: S3 is highly scalable, allowing users to store virtually unlimited amounts of data without worrying about storage capacity limits. It automatically scales to accommodate growing data needs.
    
4. Global Accessibility: S3 objects can be accessed from anywhere in the world through a unique URL, making it easy to distribute content globally.
    
5. Data Security: Amazon S3 offers various security features, including data encryption in transit and at rest, access control policies, and integration with AWS Identity and Access Management (IAM) for managing user access.
    
6. Data Lifecycle Management: S3 allows users to define lifecycle policies to automatically transition data between storage classes (e.g., from Standard to Glacier for archival) or expire data after a specified period.
    
7. Versioning: S3 supports object versioning, which allows users to preserve, retrieve, and restore every version of an object stored in the bucket.
    
8. Events and Triggers: S3 can be integrated with AWS Lambda to trigger custom actions or event notifications when certain events, such as object uploads or deletions, occur in the bucket.
    
9. Data Transfer Acceleration: S3 Transfer Acceleration enables faster data uploads and downloads by utilizing Amazon CloudFront's content delivery network for transferring data over long distances.
    

Amazon S3 is widely used for various purposes, such as website hosting, media storage and delivery, data backup and archival, content distribution, and serving as a data lake for big data analytics. Its pay-as-you-go pricing model and ease of use make it a popular choice for organizations of all sizes, from startups to large enterprises, seeking scalable and reliable cloud storage solutions.


CDNs are often used in conjunction with cloud storage services like Amazon S3. Here's how they are related:

- Origin Storage: Amazon S3 can serve as the "origin storage" for a CDN. The original web content, such as images and videos, can be stored in Amazon S3 buckets. When a user requests this content, the CDN can fetch it from the S3 bucket and cache it in the edge locations.
    
- Edge Caching: CDNs cache content at their edge locations to reduce the need for repeated requests to the origin server (in this case, Amazon S3). By caching content closer to end-users, CDNs improve the delivery speed and reduce the load on the origin server.
    
- Global Content Delivery: CDNs have a distributed network of edge servers worldwide. When a user requests content, the CDN delivers it from the nearest edge location, minimizing latency and ensuring fast content delivery globally.
    

By combining Amazon S3's object storage capabilities with a CDN's edge caching and global content delivery, system designers can create scalable, high-performance architectures for serving web content efficiently to users around the world.



## Stream processing
Stream processing is a critical component of many modern system designs, allowing applications to process large volumes of data in real-time. In stream processing, data is processed as it is generated, allowing for faster analysis and insights. Unlike traditional batch processing, where data is collected and processed in discrete batches at scheduled intervals, stream processing deals with data as a continuous flow or "stream" of events.

1. Real-time Processing: Stream processing systems analyze and respond to data in real time, allowing for immediate insights, actions, or reactions to emerging events.
    
2. Continuous Data Streams: Stream processing systems handle data as a continuous and potentially infinite sequence of events. These events can come from various sources, such as sensors, logs, user interactions, or IoT devices.
    
3. Low Latency: Stream processing is optimized for low latency, ensuring that data is processed quickly and efficiently as it arrives, often in milliseconds or sub-milliseconds.
    
4. Event Time and Processing Time: Stream processing considers two timelines: event time (when the event occurred in the real world) and processing time (when the event is received and processed by the system). Event time is crucial for tasks like windowing and handling out-of-order events.
    
5. Data Windowing: Stream processing allows developers to define time-based or count-based windows to group and process a subset of events for specific time intervals.
    
6. Stateful Processing: Stream processing systems can maintain stateful information about the ongoing data stream, enabling complex operations and analysis that depend on historical context.
    
7. Fault Tolerance: Stream processing systems often incorporate fault-tolerant mechanisms to ensure the system's resilience and to handle failures gracefully.

Stream processing finds applications in various use cases, including:

- Real-time analytics: Analyzing and aggregating data in real time to gain insights and make data-driven decisions.
    
- Fraud detection: Identifying and reacting to fraudulent activities as they happen.
    
- IoT data processing: Handling data generated by IoT devices and sensors in real time.
    
- Monitoring and alerting: Continuously monitoring events and raising alerts based on predefined conditions.
    
- Real-time recommendation systems: Providing personalized recommendations to users in real time.

Popular stream processing frameworks and technologies include Apache Kafka Streams, Apache Flink, Apache Spark Streaming, AWS Kinesis, and Google Cloud Dataflow
