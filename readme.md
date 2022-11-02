# Preparing your IDE
You can find a way to configure your IDE to use PlantUML:

https://www.youtube.com/watch?v=xXYQGl2XFdE
https://github.com/esteinberg/plantuml4idea#plantuml4idea
https://plantuml.com/es/
https://crashedmind.github.io/PlantUMLHitchhikersGuide/

# C4 model
https://mattjhayes.com/2020/05/10/diagrams-with-c4-model/
# AWS symbols
https://github.com/awslabs/aws-icons-for-plantuml/blob/master/AWSSymbols.md

# The Kata

1. Our on-premise system => first MVP

This is a system which is composed of a website where users can consult information related
to movies. You will need to design it taking into account:
- Technologies
- Users
- Features

You could create a list of basic features to help to understand the system.

SOLUTION in the folder: onpremisemvp:
* systemcontext.puml
* features.puml
* containers.puml


We need to create the most simple solution. This is an MVP (Minimum Valuable Product)

2. Scaling our on-premise system

Our system has increased the volume of users which are using it. And we will need a new architecture to support it.

In addition, we want to improve the security and access to the Front.

It should be neccesary to detect certain technical features you will need in order to adapt the software to the new scenario.


SOLUTION in the folder: increasing users:
* containers.puml

- approach on-premise
- Using a Gateway to access 
- Using a Load Balancer with two Host. Balancer of traffic


3. Migrating to the cloud.

We want to migrate to the cloud (AWS), so we will need to do the changes to make a easy migration in order to save money.

SOLUTION:
* Change the server with the Gateway with Amazon Gateway
* Change the balancer with AWS balancer
* Change the virtual hosts with EC2 instances

Some easy improvements you could valorate it:

* Use a Elastik EC2 between 2-10 instances
* Improve the reading of the Secondary DB with a AWS - Elastik Cache - Redis - You need a change in your code (You need to valorate this change)
* Change MySQL to Aurora - MySQL (better speed and consistency)


5. Optimizing for the cloud.


# Explaination

## Context
A context diagram is the highest level view in C4 Model, where the system is abstracted to a simple rectangle in the middle of the diagram, surrounded users and other systems. We can see how the system interacts, free from detail of how it works. This type of diagram is a great starting point for someone unfamiliar with the system and also works in a top-down architecture approach as a starting point for green-field concepts.

Here we see the context diagram for our online hat retailer: systemcontext.puml
## Container
The second ‘c’ is for container, and it’s not the type popularised by Docker. A container diagram breaks apart the system box into ‘containers’ that represent things that execute code or store data, such as applications, databases and file systems.

Many things in life are hierarchical, with layers that expose ever-increasing detail, and this is where we go after the C4 model context diagrams – we need to choose what to drill down into. In this example we choose the eComm (e-commerce) System for a container diagram, however to document the whole solution a context diagram should be done for the fulfilment system too.

Here we zoom in on the eComm System from the above diagram, expanding it to show the ‘containers’ within:


