This document describes the dependencies of PCS and IoT Suite, the driving requirements and the criteria used to select the technical implementations.
Since PCS is in active development, we are updating this document as we design and develop the microservices used in Remote Monitoring PCS first.

Summary
=======
* Reuse existing open source and Azure cloud solutions meeting a selection criteria
* Apply the same selection criteria to all the solutions
* Must have:
  1. Security
  2. Simplicity
  3. Meet Requirements
* Other metrics:
  1. Maturity, Documentation, Community size, Licensing
  2. Reliability, Scalability
  3. Performance
  4. Cost
* Third Party components used by PCS:
  * Application Framework (e.g. MVC and distributed services)
  * Dependency Injection
  * Application Configuration
  * Logging
  * Storage
  * others TBD

[NIH] Not Invented Here
=======================
When facing a new set of scenarios and requirement, there is a tendency of translating these to new software engineering tasks, the creation of one or more solutions tailored to the specific needs.

On the contrary, it is often the case that someone has already faced requirements and scenarios with similar patterns, designed and developed a solution, and either shared it as Open Source Software or as an Azure cloud Service.

When one of these shared solutions meet the **Selection Criteria** below, it is our goal not to reimplement, but rather to reuse what the open source community or Azure platform provides.

It follows that we also aim to be part of the open source community, providing feedback and sharing our work created on top of these open source components.

Selection Criteria
==================
When selecting a technology/solution/component we apply the same selection criteria, in particular we have defined a framework that allows to drive our decisions with comparable metrics.
The criteria applies to software details, components and services, for example it applies to Programming languages, MVC frameworks, Continuous Integration platforms, Storage types etc.

When choosing dependencies, we classify and prioritize by:
* P1 Must have: security - Yes/No
* P1 Must have: simplicity - Yes/No
* P1 Must have: meet requirements - Yes/No
* P2 (Score 1 to 3): maturity, known patterns, licensing, active community + size, documentation
* P3 (Score 1 to 3): reliability, scalability
* P3 (Score 1 to 3): performance
* P3 (Score 1 to 3): cost

When using a score from 1 to 3, 3 is better.

### [SEC] Security (yes/no)
The component uses well known security patterns and solutions. It does not use custom/proprietary encryption algorithms.

Secrets can be injected by the user, as opposed to hard coded ones, and there are documented mechanisms to protect these secrets from third parties.

The solution is not a risk to the hosting platform (Azure) and business (Microsoft and IoT users). To assess this metric we analyze online reports and updates, looking for recent security issues

### [KISS] Simplicity (yes/no) - (KISS = keep it short and simple)
The component is simple to adopt and to understand. It has a clear architecture, and a well defined scope of application (single responsibility principle).

Setting up and integrating with the component/service is straightforward, possibly automated, and well documented.
For instance it's simple for a developer to use/setup the dependency in the development environment.

Within the scope of one microservice, the dependent solution can be replaced by an alternative, without affecting the implementation of other microservices.

To assess this metric we read online how-to's covering PCS scenarios, and possibly create proof-of-concepts to compare difficulty and complexity for our requirements.

### [REQ] Meet requirements (yes/no)
The component meets all the requirements, possibly allows extensibility and offers features which will be in scope in the next 6-12 months.

For instance, all .NET components must support .NET Core. Another example is scalability, e.g. solutions should allow to scale to millions, even if not in the current development scope.

### [MAT] Maturity, License and Community (1..3)
We measure maturity with several metrics, taking into consideration whether the component is supported, under development, documented and established among the software engineering community.

Under this metric we look also at the licensing model, preferring open source solutions with an OSS friendly license, like MIT. With regard to open source, we consider GitHub our primary source, so we look at metrics like git activity (commits, forks, issues, docs) and stars in the GitHub repository of these components.

Some metrics:
* Count Stackoverflow results, better if dedicated label
* Count Google+Bing results
* Count tutorials, examples, videos
* Relevant features, incl. NET Core support
* Breaking changes
* Flexibility, conventions vs configurations
* Commercial support
* MIT license
* Code in GitHub
* GitHub stars
* GitHub results
* Months since last dev. spike
* IRC, Gitter, Slack, Discourse

### [REL] Reliability and Scalability (1..3)
The solution is stable for production use, and for long term adoption.
It also allows to scale PCS to serve thousands to millions of connected devices, with millions to billions of telemetry messages.

To measure reliability and scalability, we look for documentation explaining how the component would be used when distributing over multiple nodes, what kind of extra requirements/assumptions are in place to scale. For instance, some solutions requires extra components in order to scale, to manage state, to load balance network traffic, or might affect the overall architecture design. We prioritize components that can scale without affecting the overall design and the cost of deployment.

### [PERF] Performance (1..3)
This metric does not apply to every dependency, however we try to look for data to compare alternatives. Since we cannot compare every option in a timely fashion, we look at this metric only if other metrics don't provide an indication already, or if the dependency could have a major impact overall (e.g. storage options).

In most cases we prioritize scalability over performance, i.e. PCS is designed to scale horizontally.
Latency though is an important metric for connected devices, so in some scenarios we prioritize performance, e.g. serialization formats, IoT protocols, etc.

Where possible, we also look for reasonably recent benchmarks.

### [COST] Cost (1..3)
We aim to allow demos and small deployments at very low price, even for free, e.g. a developer should be able to test and showcase a PCS on a laptop without incurring in major costs.

# Criteria applications

1. [Microservices](Microservice-Principles.md)
2. [Frontend](Frontend.md)