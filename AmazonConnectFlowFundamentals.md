# Amazon Connect Flows Fundamentals

Find the course [here](https://explore.skillbuilder.aws/learn/courses/19837/amazon-connect-flows-fundamentals/lessons/131380/amazon-connect-flows-fundamentals)

## Introduction to Amazon Connect Flows

* Recognize Amazon Connect flow types.

### Introduction

Amazon Connect defines customer journeys.  

* Interactive Voice Response (IVR)
* Chatbot

It defines paths for both customers and agents.  

### Default and sample flows

Available in every new instance  

_Default flows_ are premade experiences that activate without a designer needing to take any action. For example, there is a "hold" flow for when agents put a caller on hold. More information is available [here](https://docs.aws.amazon.com/connect/latest/adminguide/contact-flow-default.html)  
_Sample flows_ are premade flows designed to help developers develop similar flows by example. They are not intended for production, but for learning. More information is available [here](https://docs.aws.amazon.com/connect/latest/adminguide/contact-flow-samples.html)  

### Flow types

There are nine types of flows:  

#### Inbound flow

The default flow type. This is the flow to initiate a customer experience prior to transfering them to a queue, and to create step-by-step guides, or specific treatments (like a survey) after the agent disconnects from the call.  

#### Customer queue flow

This is the flow that customers experience while waiting in a queue. This can include prompts like estimated time of wait, alternatives like chatbots.    

#### Customer hold flow

This is the flow customers experience while on hold. It can include audio prompts and music.  

#### Customer whisper flow

This is a flow customers can experience right before they connect to an agent. It can provide prompts, disclaimers and disclosures, "This call may be recorded..." is an example of what might happen in a customer whisper flow.  

#### Agent whisper flow

This is a flow agents experience before they are connected with a customer. It can explain things the agent needs to know about the call. For example, an agent whisper can tell an agent which queue a caller is being routed to them from.  

#### Agent hold flow

This is a flow agents experience when they place the caller on hold. It can include one or more audio prompts.  

#### Transfer to agent flow

This is the flow the agent experiences when transfering a caller to another agent. They can include messages.  

#### Transfer to queue flow

This is the flow the agent experiences when transfering a caller to another queue.  

#### Outbound whisper flow

This is the flow the customer experiences before connecting with an agent in an outbound call.  

#### Disconnect flow

This is the flow the customer experiences after the agent disconnects the call. It could include things like a post interaction survey.  

### Flow blocks

This is the visual representation of the flow that the designer uses to build the customer journey.  

## Flow Designer

* Explore the key capabilities of the flow designer.

### Introduction

The flow designer is a visual, drag-and-drop tool for building Amazon Connect flows.  

### Key capabilities of the flow designer

* _Design flows:_ Build flows using blocks like prompts, transfers, queues, and integrations with other AWS services (like lambdas).  
* _Configure flow logic:_ You can add conditional decision logic to your flows.  
* _Integrate with other AWS services:_ Integrate your flows with services like Lex and Lambda.  
* _Test and debug flows:_ Lets you test and debug before publishing.
* _Manage flow versions:_ Create and manage different versions.  
* _Import and export flows:_ This allows reuse across multiple instances of Amazon Connect.  

### Flow blocks

There are seven categories of flow blocks:  

* _Interact:_ Play messages, gather information.
* _Set:_ Set conditions or attributes in the flow.
* _Check:_ Check flow conditions or attributes.
* _Analyze:_ Set logging and recording behavior.
* _Logic:_ Insert logic into the routing behavior.
* _Integrate:_ Invoke a flow module or lambda.
* _Terminate:_ Either tranfer calls, terminate calls, or terminate flow processing.

### Flow management

#### Save, publish, and archive flows.  

Versions are supported for comparison and rollback. Flows can be saved and/or published.  

#### Import and export flows

Flows are reusable across environments/instances.  

#### Export flows

Flows can be exported using the GUI.

#### Import flows

Flows can be imported using the GUI.

## Enabling Additional Amazon Connect Functionality Using Flows

* Explore how to use flow blocks to activate Amazon Connect features.

### Introduction

Amazon Connect features include capabilities like:  

* Intelligent routing
* Self-service options
* Real-time analytics
* Integration with other business applications

### Amazon Connect call recording

Find "Set recording and analytics behavior" in the Blocks search panel. Drag to theflow designer canvas. Edit the settings. Save changes.  

### Amazon Connect Contact Lens

This block can improve customer experiences. It provides analytic and quality management tools to measure, monitor and improve contact quality.  

Be sure the administrator has enabled this feature in your instance before using.  

### Amazon Q in Connect

This feature provides agents with GenAI assistance.  

Be sure the administrator has enabled this feature in your instance before using.  

### Amazon Connect Cases

This feature helps track customer issues over multiple calls. Agents can document case details.  

Be sure the administrator has enabled this feature in your instance before using.  

### Amazon Connect Tasks

This feature helps prioritize, track, route, and automate tasks for agents.

### Amazon Connect Customer Profiles

This feature provides agents with up to date customer information for personalized interactions.  

Be sure the administrator has enabled this feature in your instance before using.  

### Amazon Connect Persistent Chat

This feature supports conversations that take place over longer periods of time, with breaks and restarts by persisting the history of the chat.  

## Operational Support Flow Blocks

* Explore the use of flow logs.
* Recognize the ability to distribute contacts by pre-configured percentage.

### Introduction

The AWS Well-Architected Framework is a set of architectural best practices toinsure operational excellence, security, reliability, performance efficiency, and cost optimization.  

### Distributed traffic by percentage

The Well-Architected **reliability** pillar includes strategies like blue/green deployment. For call centers, this involves slowly increasing traffic to the new flow. The _Distribute by percentage_ flow block can be used to implement this strategy. It works with the following types of flows:

* Inbound flow
* Customer queue flow
* Outbound whisper flow
* Transfer to agent flow
* Transfer to queue flow

### Flow logs

The Well-Architected **operational excellence** pillar recomends storing logs in a CloudWatch log group. This organizes streams from the Amazon Connect environemnt, and allows storage, monitoring, and access from a variety of sources. CloudWatch can be configured to send alerts when unexpected events occur.  

## Summary

Amazon Connect Flows are a feature of Amazon Connect. They define the customer journey using channels like chat, voice, and tasks.  



