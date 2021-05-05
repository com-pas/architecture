<!--
SPDX-FileCopyrightText: 2021 Alliander N.V.

SPDX-License-Identifier: Apache-2.0
-->

## Technnology Survey
An initial survey was taken to determine some technologies we could use:

| Technology                     | Name Technology | Benfits | Challenges | Reference Project | Opinion Rob | Opinion RTE | Optinion GE  |
| ------------------------------ |:---------------:| -------:| ----------:| -----------------:| -------:| ----------------------:|----------------------------------------------------------:|
| Microservices (cross-platform) | Java Spring or Python Flask | Isolation of features in microservices speed up the development | Limiting number of microservices to a manageable number. | | I don't have experience with Python Flask, development is also not very active. I do have experience with Java Spring, and I think it's a great choice!| |By Spring we mean Spring Boot which is the framwork to create microservices architecture, Is a good candidate if we want to reuse code. I don't have experiece about python flesk |
|                                | NestJS with NodeJS | | | | No experience, but NodeJS is a good candidate. NodeJS seems to have some performance issues with heavy computing (downside) | In my opinion, it's a weak argument saying just because NodeJs uses C library to process XML means it's better that Java. Binding/Wrapping could bring performance issues. May be I don't get it, but NodeJs is not mono thread otherwise asynchronous is impossible, though it provides developper the ability to only deal with a single thread. I don't think either that dealing with repetitive and independent blocks with single thread is faster than multithread | Nodejs combined with typescript acceletate a microservices architecture development, for performance issue for reading/write xml document, Nodejs is better then Java (because it use C lib wrappers), Also the big advantage of NodeJs is weak typing (dynamic types) which simplify the communication between services, And JSON is natively supported (performance). Another advantage is mono thread, no-blocking and Nodejs community  |
|                                | Go Micro | | | | No experience, but very active development. Looks interesting! I also have some experience with the Go language. | |  a PoC done using Go Micro, it is great framework but not mature, we need to write a lot of code :) |
| Scripting                      | Python | Flexible. Object oriented. Cross platform. | No standard libraries, need to agree on subset. | | Fast, easy language. Lots of experience with Python, so ready to use. | | python is the one to choose for shell scripting|
|                                | No code technology | Non developper user can build their own user story built on predevelopped blocks | No many opensource solution and most of them are proprietary | | |
|                                | Typescript or Javascript | | | | No experience with Typescript, but it seems richer than Python for example. I don't know how easy it is in setting up related to Python. | | to create Job, Worker, Intermediate service, I recommand Typescript which contains a lot of ready to use libs|
|                                | Bash | | | | It depends on the tasks to do, but bash can do most of the scripting tasks. Easy and fully integrated in Linux. | | Better to use python/Typescript to be Os agnostic |
|                                | Groovy | | | | |  | Java based VM, no experience. |
| APIs                           | REST, Message queue such as Kafka? | | | | REST is a good standard, yes. Depends on the tasks of the APIs. | | Depends on The needs |
|                                | OpenAPI for REST | | | | | | The standard that we must implment to share our APIs  |
|                                | GraphQL | | | | | |Another standard that we may implment to share our APIs to reduce the payload size  |
|                                | WebSocket | | | | | | For configuration purpose, the WebSocket support is more than recommanded |
| XML processing & file database | sax.js             | Memory efficient. Don't need to have XML file sized RAM | Needs to track state while parsing due to streaming nature of API | https://github.com/StevenLooman/saxpath | | | |
|                                | xQuery, XSLT, XPath|    Standard technologies for XML processing and XML DB querying | Overlapping use cases of very different technologies | https://github.com/BaseXdb/basex | | |
|                                | RiseClipse | Validates SCL files more precisely than with XSD (using rules expressed in OCL - Object Constraint Language) also validates CIM files | | https://github.com/riseclipse | RiseClipse has proven itself, been working with it in past projects. Good candidate! Also dedicated to IEC standards, so perfect. | It's plateform dependent. Plus XSD is a structure-based grammar for XML. Even though it gives some features for defining rules, I don't think it should be compared to OCL. XML comes with other schema language to define any kind of constrains : SCHEMATRON.| |
|                                | xerces? | fast, work well with big files | | | | | |
|                                | Schematron | Schematron is a simple and powerful rule-based Schema Language for making assertions about patterns found in XML documents. It relies almost entirely on XPath query patterns for defining rules and checks.| | | http://schematron.com/, http://xml.coverpages.org/schematron.html, https://github.com/Schematron| For manipulating XML, it can do anything OCL can do, and more. In term of handling xml, there's nothing better than xml technologies, in my opinion| |
|                                | Node - fastXML | | | | | | Good library to parse xml file to Javascript Object if we use NodeJS|
| Managing microservices         | container based Microservices using Kubernetes? | | | | To keep microservices managed, a containerized architecture is definitely the way to go. | |  For development, we must use docker-compose (by experience k8s is to heavy to manage for development )|
| XML versioning                 | Version through file repository or database, see below | Versioning is automatic if file repo or database are chosen to include this feature | | | | |SemVer is good standard of versionning|
|                                | Something similar to CGMES? Each file hasa header with identification, type and version information of the file. | Files are uniquely identified | | | | |
| Securing SCL XML files         | GPG Encryption | Industry standard (PGP) text encryption, for transport and storage | | https://github.com/StackExchange/blackbox | Don't have much experience with Encryption of files. Why do we want to do this? | |
| File repository vs database    | GIT SCM vs Datomic | Both technologies model time meaningfully, Datomic with schema and git with unstructured data | | https://git-scm.com/ vs https://www.datomic.com/ | | | |
|                                | SQLite | Embedded in app. No separate server needed. | Not as powerful as database server. | https://sqlite.org/index.html | I think a graph database is the way to go here.  | | |
|                                | I would go with file repository for big XML files. | | | | OK. | |
|                                | PostgreSQL | | | | I think a graph database is the way to go here. | PostgreSQL has XML type (Oracle has its own XML TYPE). It can store XML as it is. One can quiries directly in stored XML with basic SELECT and PostgreSQL provided routines based on XPATH| Postgres is good condidate because it support XML, and it have extention for graph (AgensGraph) | 
|                                | Neo4J | | | | Good candidate, native XML database. | | |
|                                | MongoDB | | | | MongoDB doesn't support XML, it supports BSON. Not handy. it's possible, but demands extra work. | | Limit of 16Mb can be problem |
|                                | InfluxDB | | | | Database build for time series such as operations monitoring, application metrics, Internet of Things sensor data, and real-time analytics.  | | Not for this purpose|
|                                | Minio Storage object | | | | Saving files  | | Good way to save xml files as it is|

