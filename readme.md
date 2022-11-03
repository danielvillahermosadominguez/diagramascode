# Preparing your IDE

For this kata you will need to install in IntelliJ-IDEA the PlantUML integration plugin.

You can find a way to configure your IDE to use PlantUML:
https://www.youtube.com/watch?v=xXYQGl2XFdE

Here you have more information:
https://github.com/esteinberg/plantuml4idea#plantuml4idea
https://plantuml.com/es/
https://crashedmind.github.io/PlantUMLHitchhikersGuide/

# C4 model
You have information about this model here:

https://mattjhayes.com/2020/05/10/diagrams-with-c4-model/
# AWS symbols

If you need information about AWS symbols:
https://github.com/awslabs/aws-icons-for-plantuml/blob/master/AWSSymbols.md

# The Kata : Movies website

I'm creating this "Kata" to train skills with "Diagram as Design" with the objective to learn about Macro-Architecture and Cloud (AWS in this case). 
The approach is to describe a simple web app (The "fizzbuzz" for this context :-)). The steps would be:


## Requirements for product:
This is a system which is composed of a website where users can consult information related
to movies
## Steps of the Kata:
* Use C4 for your first MVP (Minimum Viable Product). Restriction  = on premise

* Now you have a lot active users and you need to improve your Software architecture and infrastructure architecture. Evolve it. In addition, you need to improve the security. Describe the new technical features to adapt the software to the new system.

* You are going to do the migration to the cloud (AWS), what could be the first approach?
* At the end, you want to optimize it for the cloud (AWS). Describe the new features you would need.
* Based on it, I think two or more people could join in a pair/mob session and evolve this architecture.


# The Kata : Steps and help to solve it

## 1. Our on-premise system => first MVP

This is a system which is composed of a website where users can consult information related
to movies. You will need to design it taking into account:
- Technologies
- Users
- Features

You could create a list of basic features to help to understand the system.
```
A possible solution in the folder: onpremisemvp:
* systemcontext.puml
* features.puml
* containers.puml
```

We need to create the most simple solution. This is an MVP (Minimum Valuable Product)

## 2. Scaling our on-premise system

Our system has increased the volume of users which are using it. And we will need a new architecture to support it.

In addition, we want to improve the security and access to the Front.

It should be neccesary to detect certain technical features you will need in order to adapt the software to the new scenario.

```
A possible solution in the folder: increasing users:
* containers.puml

- approach on-premise
- Using a Gateway to access 
- Using a Load Balancer with two Host. Balancer of traffic
```

## 3. Migrating to the cloud.

We want to migrate to the cloud (AWS), so we will need to do the changes to make a easy migration in order to save money.
```
A possible solution in the folder awsmigration:
* Change the server with the Gateway with Amazon Gateway
* Change the balancer with AWS balancer
* Change the virtual hosts with EC2 instances

Some easy improvements you could valorate it:

* Use a Elastik EC2 between 2-10 instances
* Improve the reading of the Secondary DB with a AWS - Elastik Cache - Redis - You need a change in your code (You need to valorate this change)
* Change MySQL to Aurora - MySQL (better speed and consistency)
```

## 4. Optimizing for the cloud.
We want to optimize for the cloud and include monitoring. What kind of changes could we do?

```
A possible solution in the folder awsoptimization:
- Backend scaling with a balancer and EC2 machines
- Instead of scaling with virtual machine, scaling with docker and kubernetes: 
  - Front - Pod
  - Catalog service - Pod
  - CRUD service - Pod (this service could need a change in the code)
  - We could based on this picture: https://aws.amazon.com/es/getting-started/hands-on/deploy-kubernetes-app-amazon-eks/
- We only need a set of EC2 with Docker and kubernetes


We would need to evaluate this change:
- We could change the database with DynamoDB because, really we need relations in the DB? we could need some refactoring in the services: In our case
  we need to compare and think we could implement in the future a feature for filtering movies:
    * Backups: DynamoDB provides constants backups and the user can restore the database table to any point in time. On the other hand RDS you can enable
      automatic backup for your database instance. The user-initiated backups are stored as database snapshopts in S3 until you delete it. So, I don't find
      any motive to use DynamoDB in this point.
    * Scalability: Amazon DynamoDB is highly scalable but RDS is also scalable and support auto-scaling. So, I don't see a motive here.
    * Performance: DynamoDB is known for high-performance. There is less latency and response time when reading and writing data because the IO is SSD. In
                   addition, the in-memory cache of DynamoDB Acceleator (DAX) cand enhance the read performance. So this could a motive to remove a RDIS cache
                   and the replication of DB and use just DynamoDB.
                   On the other hand, RDS is running en SSD too.
                   RDS has a high-performance too and is a solution for OLTP (online transaction processing). This could be a motive to use RDS because we will
                   have concurrency and atomicity. multiple user could alterate the same data. However, Amazon DynamoDB works with transactions too.
    * Availability and Durability: DynamoDB is replicated across three availabiltiy zones automatically. RDS uses Multi-AZ deployments to enhance the availability.
                   This has an additional cost because we will need multiple instances.
    * Security: DynamoDB integrates well with IAM and RDS too. The encryption with KMS (Key Management Service) ensure the DynamoDB security. Amazon RDS also
                includes AWS KMS. User can use SSL to enhance the security of data.
                
    The recommended uses cases for DynamoDB:
        * Real-time bidding
        * Shopping carts
        * Mobile applications
        * Content management
        * High I/O needs
        * Unstructured data in gamming applications.
    Uses cases for Amazon RDS:
        * Any relational backend database
        * Traditional applications
        * Enterprise-grade applications
        * CRM and e-commerce solutions.
        * Data warehouses
    So, in this case, it is better use RDS - Aurora with replication. But if we include in the future a mobile client to improve the experience for the user,
    we will need to evaluate again this part of the architecture.                
```
