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
- Instead of scaling with virtual machine, scaling with docker and kubernetes: 
  - Front - Pod
  - Catalog service - Pod
  - CRUD service - Pod (this service could need a change in the code)
- We only need a set of EC2 with Docker and kubernetes
We would need to evaluate this change:
- We could change the database with DynamoDB because, really we need relations in the DB? we could need some refactoring in the services
- We could include DynamoDB accelerator
```
