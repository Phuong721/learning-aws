---
title: "Blog 3"
date: 2025-08-21
weight: 3
chapter: false
pre: " Artificial Intelligence, Customer Solutions, Generative AI, Open Source "
---

 ### Open Protocol for Agent Interoperability Part 4: A2A Agent Communication

## Introduction:
Welcome to Part 4 of our Open Protocols for Agent Interoperability blog series where we will cover the Agent-to-Agent (A2A) protocol, AWS's involvement with the Linux Foundation-based open standard, and our support for A2A in the Strands Agents SDK. Here's what we've covered so far:

- Part 1: How the Model Context Protocol (MCP) facilitates communication between agents and how AWS has worked to improve the MCP specification to better support agent-to-agent communication.

- Part 2: Details on recent MCP specification updates related to Authentication.

- Part 3: How to build inter-agent systems with the new Strands Agents SDK and MCP

Standard protocols are the primary way to connect network services. Typically, there are different protocols to address different types of network connectivity. At the network layer, there are two main protocols: TCP and UDP. Each protocol is suited to specific needs, and neither protocol is universal. This is also true when connecting AI agents. In part 4 of our agent-to-agent communication series, we will introduce A2A, how it can be used for agent-to-agent communication, and how AWS helps customers build systems with A2A.

MCP was originally created to connect agents to tools, but can also be used to connect agents to each other. A2A was created to connect agents to each other, and can also be used in conjunction with MCP for agents to communicate with tools. Which protocol to use for agent-to-agent communication depends on your needs. AWS supports both protocols, allowing customers to deploy their code on AWS using MCP, A2A, or a combination of both.

As inter-agent protocols and the frameworks around them evolve, they will likely become more like TCP & UDP, where most developers focus more on building their agents rather than the underlying protocols. The first step towards that is for agent frameworks to support the protocols and build ecosystems around them. At AWS, we have taken this first step by joining the A2A standards community and adding support for A2A in our open-source Strands Agents SDK. Swami Sivasubramanian, Vice President of AWS Agentic AI, summarizes this effort:

At AWS, we believe agentic AI will be critical to nearly every customer experience. We welcome A2A to the Linux Foundation and expect this to create more opportunities for anyone building AI applications. We plan to support the community with project contributions and access to the broadest and deepest set of agentic frameworks, protocols, and services.

Similar to how we are supporting the development of MCP, we are supporting the development of A2A to meet customer needs. We plan to focus on several areas to make A2A work well on AWS, including support for Amazon Bedrock AgentCore, extending the A2A protocol for temporary task storage and SigV4, improving multi-task management, and improving the Java A2A SDK.


## Overview of A2A
The A2A protocol addresses a key challenge in the AI ​​landscape. It enables AI agents built on diverse platforms, operated by different companies on separate servers, to communicate and collaborate effectively—as agents, not just tools. A2A represents a significant step forward in creating interoperable AI systems that work together across organizational boundaries. The protocol is supported by a growing partner ecosystem, including more than 50 technology companies such as Google, Atlassian, Confluent, Salesforce, SAP, and MongoDB.

Before A2A, organizations faced significant challenges in deploying multi-agent AI systems at scale. Without a standardized protocol, each pair of agents required custom integration code, leading to excessive development costs and maintenance complexity. This creates siloed AI systems where specialized agents cannot easily share capabilities or coordinate on complex tasks. The protocol provides agents with a common language, allowing them to maintain their autonomy and specialized skills while collaborating—agents communicate with each other as peers, not just tools. This distinction is important because it allows agents to engage in complex back-and-forth interactions, negotiate task requirements, and maintain independent decision-making while working toward common goals.

For AWS customers, A2A offers a number of compelling features that align with enterprise requirements. The protocol enables enterprise capabilities including secure agent discovery through standardized agent tags, authentication and authorization mechanisms for controlled access, support for multiple communication methods (text, forms, media), and the ability to allow agents to collaborate on long-running tasks without revealing their internal state or implementation details.

A2A addresses the unique challenges of multi-agent collaboration through features that enable complex workflows, handling complex real-world business processes with the observability and control required by production environments. Specifically, it supports agent tags, structured tasks, multiple transport options, and authentication/authorization primitives.

## Agent Tags
Effective multi-agent communication requires agents to discover and understand each other’s capabilities. A2A supports this through Agent Tags — metadata documents that capture semantic meaning about what each agent can do, how it prefers to operate, and what types of tasks it is good at. Agent Tags enable other agents to make intelligent decisions about when and how to cooperate. Agent Tags also describe an agent’s authentication/authorization requirements and support incrementally expanded capabilities after authentication, using Authenticated Extended Agent Tags.

## Structured Task Execution
Agents work together to solve problems by leveraging tasks to structure their communication; they organize their messages into intelligent units of work, carry context, track progress, and store output artifacts. Through tasks, agents can reference previously created artifacts, understand dependencies between tasks in a workflow, and make informed decisions based on the entire conversation history. Tasks support both sequential and parallel execution for complex workflows. Agents can create multiple subsequent tasks simultaneously and create dependent activity chains. This gives application developers the flexibility to model real-world business processes.

By leveraging task IDs and context, applications can trace task origins, tracing task chains back to their roots to recover information about how outputs are produced. This improves observability by providing agents with the ability to generate rich activity logs for debugging and auditing.

## Multiple Transport Options
A2A empowers application developers by supporting three core protocols with equivalent capabilities: JSON-RPC 2.0, gRPC, and REST. This allows developers to choose the transport that best fits their team’s expertise, existing infrastructure, and performance requirements. For long-running operations, A2A enhances each transport with Server-Sent Events (SSE) for streaming and sending webhook-based push notifications. Developers have intuitive options for handling asynchronous task updates and real-time progress monitoring without complex polling logic.

## A2A Security
Enterprise-grade security is a non-negotiable requirement for agent systems. A2A enables a robust security architecture by supporting a number of authentication protocols; including OAuth 2.0, OpenID Connect, and mTLS, allowing organizations to integrate agents with their existing identity infrastructure, while skill-specific authorization metadata and secondary authentication support allow for fine-grained access control policies that can be enforced at the application level.

A2A’s decision to keep agents opaque to each other supports a zero-trust architecture by treating each agent as an independent security boundary, and the protocol’s support for task auditing provides the foundation for comprehensive security monitoring and compliance reporting.

## Inter-Agent with Strands Agents & A2A
The unique features of A2A make it perfect for interoperability between agent platforms. Several open source agent platforms already support it. The open source Strands Agents SDK recently added support for A2A so agents can easily communicate with other agents.

Strands Agents takes a model-driven approach to building and operating AI agents in just a few lines of code. Strands scales from simple to complex agent use cases, and from local development to production deployment. Many teams at AWS have used Strands for AI agents in production, including Amazon Q Developer, AWS Glue, and VPC Reachability Analyzer.

With built-in A2A support in Strands Agents, you can easily use an agent as an A2A server and communicate from one Strands Agent to other A2A agents. To illustrate this, consider the example of a Human Resources (HR) agent that can answer questions about employees. To do this, you can imagine the HR agent communicating with several other agents such as an employee data agent, an Enterprise Resource Planning (ERP) agent, a performance agent, a goals agent, etc. For this example, let's start with a basic architecture, where a REST API provides access to an HR agent that connects to an Employee Info agent: The architecture of the inter-agent system consists of two agents (HR & Employee Info), connected using A2A.

Note: The complete, working version of the following example is available in our Agentic AI samples repo.

- Our employee information tool uses Amazon Bedrock and the MCP tool to retrieve employee data (see full code for those aspects):
employee_agent = Agent(
    model=bedrock_model,
    name="Employee Agent",
    description="Answers questions about employees",
    tools=tools,
    system_prompt="you must abbreviate employee first names and list all their skills"
)

- To expose this agent via A2A, we just need to create an A2A server and start it when the program runs:
a2a_server = A2AServer(agent=employee_agent, host=urlparse(EMPLOYEE_AGENT_URL).hostname, port=urlparse(EMPLOYEE_AGENT_URL).port)

if __name__ == "__main__":
a2a_server.serve(host="0.0.0.0", port=8001)

Note that we pass EMPLOYEE_AGENT_URL via an environment variable. This helps our infrastructure definition know the endpoint URL that can set the host and port used in the A2A agent tag (used by the A2A client to discover the agent).

- Now we can access the Employee Info agent via A2A and we can create the HR agent:
provider = A2AClientToolProvider(known_agent_urls=[EMPLOYEE_AGENT_URL])

agent = Agent(model=bedrock_model, tools=provider.tools)

This agent can now be invoked in a variety of ways. In this example, we invoke it from a REST request. See the full code for the REST aspects. Here's what happens when a REST request is made:
- The user (possibly via a web or mobile app) sends a query like "list employees with AI-related skills"
- The HR agent uses the Amazon Nova model to understand the user's query and decides that it should be sent to the employee information agent.
- Using A2A, the query is sent to the Employee Information agent.
- The Employee Information agent uses the Amazon Nova model to understand the query and decides that it should call the Employee Data MCP server.
- The Employee Information agent calls the Employee Data MCP server to query the employee database and return the data to the Nova model.
- Given a system requirement to abbreviate employee names, the model takes a list of employees, formats the list nicely, abbreviates the names, and returns the text to the Employee Info agent.

- The Employee Info agent returns the text to the HR agent, which returns the text in a REST response.

Of course, all of this can run on AWS using a variety of runtime environments (Amazon Elastic Kubernetes Service (Amazon EKS), Amazon Elastic Container Service (Amazon ECS), Amazon Bedrock AgentCore, AWS Lambda, etc.). This example contains an AWS CloudFormation deployment template that deploys the agents and MCP servers on Amazon ECS (all in a VPC) and an Application Load Balancer to expose the REST service.

- We can experiment with curl:
curl -X POST --location "http://something.us-east-1.elb.amazonaws.com/inquire" \
-H "Content-Type: application/json" \
-d '{"question": "list employees that have skills related to AI programming"}'

And we are back: Here are the employees with skills related to AI programming:

- A. Rosalez - Machine Learning, REST API
- E. Owusu - DevOps, Machine Learning, Python
- J. Doe- Machine Learning, JavaScript
- K. Mensah - REST API, Kubernetes, Machine Learning, Node.js
- M. Rivera - AWS, Kubernetes, GraphQL, Machine Learning
- M. Major - MongoDB, Angular, Kotlin, Machine Learning, REST API
- C. Salazar - React, Machine Learning, SQL, Kotlin
- N. Wolf - SQL, Machine Learning, Docker, DevOps, Git

If you need more If you need detailed information about any of these employees or require further assistance, please let me know!

Get the complete source for this example.

With Strands Agents, it takes just a few lines of code to expose agents as A2A servers and communicate between agents using A2A. In future posts, we will cover more advanced agent types such as Swarms, Graphs, and Workflows.

## Customer Perspectives
We’ve heard from a number of customers and partners who are excited about our A2A support. Here are some of their thoughts:

“At Autodesk, we are committed to driving open standards for agent AI and interoperability as we shape the future of design and engineering. Through our collaboration with AWS and the A2A community, we are excited to help build an ecosystem where intelligent agents can communicate seamlessly across Autodesk platforms. As we continue to enhance Autodesk Platform Services with generative AI capabilities, we see tremendous potential in how interoperable AI agents can transform workflows across architecture, engineering, construction, and manufacturing. Working with AWS, we are committed to creating solutions that enable secure and efficient agent collaboration while maintaining enterprise-grade standards.” – Ritesh Bansal, Vice President of Data Analytics, Insights and AI/ML Platform, Autodesk

“Our commitment to developing Agentic AI, open protocols, and interoperability is at the core of our vision for secure and intelligent networks. By collaborating with AWS and the A2A community, we are driving innovation to set new standards for AI-based security, enabling organizations to operate with greater resilience and confidence in the rapidly evolving AI era.” – Raj Chopra, Senior Vice President and Chief Product Officer, Security, Cisco

“As organizations design increasingly sophisticated agentic AI systems, coordination between agents and tools is becoming essential. We are excited to see AWS accelerate efforts like A2A, supporting better interoperability architectures that help organizations and Datadog customers build more observable, reliable, and secure agent-based applications.” — Yrieix Garnier, Vice President of Product, Datadog

“MongoDB and AWS are committed to building an open, interoperable ecosystem that gives developers greater freedom to innovate. Adopting open standards like A2A is an important step toward this vision, simplifying how agents interact with MongoDB's rich document model, built-in vector search, and Voyage AI models.” – Abhinav Mehla, Vice President of Global Partner Programs & Ecosystem, MongoDB

“Interoperability is critical for AI agents to work seamlessly and efficiently across enterprise systems and tools, which is why we collaborated with the industry to develop the A2A standard, and why we will support open standards like A2A and MCP in Agentforce. AWS’s support for A2A will continue to help break down barriers between vendors, drive innovation, and deliver significant value to our mutual customers by enabling agents to work across the company’s entire infrastructure and ecosystem of tools and agents.” — Gary Lerhaupt, Vice President of Product Architecture, Salesforce

“It’s exciting to see industry leaders like AWS back the Agent2Agent protocol. What started as a bold idea is now quickly becoming an industry standard – one based on openness, security, and cross-platform interoperability. With support from AWS and other partners, the A2A ecosystem is truly thriving, and ServiceNow is proud to lead this trend by making enterprise-grade, interoperable AI agents a reality.” – Joe Davis, Executive Vice President of Platform Engineering & AI Technologies at ServiceNow.

Snowflake firmly believes that some of the industry’s biggest innovations come from open protocols and the communities that support them. Maximizing the potential of agentic AI depends on open protocols like A2A, as well as the shared knowledge and best practices they provide. We are excited to see AWS demonstrate their commitment to open protocols for agent interoperability by adding A2A support to Strands Agents. Together with the support of the broader technology community, the industry will be able to automate knowledge work with secure agentic systems like Strands Agents and Snowflake Cortex Agents. – Dwarak Rajagopal, Vice President of AI Engineering & Research, Snowflake

“In the future, a fragmented workforce of humans and AI agents will inevitably hinder growth. We believe that open protocols, particularly Agent-to-Agent (A2A) Protocols, play a critical role in the evolution of this hybrid workforce. They enable secure, collaborative communication, ensuring interoperability across diverse agent ecosystems. Workday’s Agent System of Record (ASOR) uniquely extends our trusted platform to manage people, finances, and agents together. Working with AWS and the A2A community, we are committed to enabling secure, interoperable agent communication. This isn’t just about new technology; it’s about securely unlocking new levels of productivity and innovation across the enterprise, while maintaining complete control.” —Dean Arnold, Vice President of System of Record, Workday


## Getting Started and Providing Feedback
To get started building interactive AI agents using A2A, check out the Strands Agents A2A docs. We'd love to hear your feedback on using A2A with Strands Agents! Join the discussions on the open source Strands Agents Python SDK repo to let us know what else you need to know when building an inter-agent system.

- Nick Aldridge is a Principal Engineer at AWS. Over the past 6 years, Nick has been involved in multiple AI/ML initiatives, including Amazon Lex and Amazon Bedrock. Most recently, he led the launch of Amazon Bedrock Knowledge Bases. Currently, he works on generative AI and AI infrastructure, focusing on agent collaboration and function invocation. Before joining AWS, Nick earned his Master's degree from the University of Chicago.

- James Ward is a Principal Developer Advocate at AWS. James travels the world helping enterprise developers learn how to build reliable systems. His current focus is on helping developers build systems of AI agents using Spring AI, Embabel, Strands Agents, Amazon Bedrock, MCP, and A2A.