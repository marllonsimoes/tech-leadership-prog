# Solution Architecture Documenting Practical Task

## Overview
The purpose of this module is to practise:
* decomposing design documentation into **views**
* maximising the value and maintainability of design using **decision log**

## Task 1 - initial design
### Sub-task 1.1 - analyse requirements
**Plan**:
* Read the requirements below.
* Build a list of any gaps/unclear requirements.

**Requirements**
Development team is going to elaborate REST Service manipulating Event resource.

Event entity contains following fields:
* id;
* title;
* place;
* speaker;
* eventType;
* dateTime.

Team leader should choose the most suitable data storage implementation for REST Service providing following functionality:
* CRUD operations
* Filtering
* Search
* Sorting
* Aggregation by specified field value

Take into account the following:
* Data storage for REST service should provide support multi-tenant content storage.
* Data Storage should scale so that:
  * up to 100 000 000 of records are stored
  * CRUD operations and typical search queries should execute within 1 second
* Data storage should support automated data backup every 30 days.
* Event Model for Data Storage Schema mapping complexity should be minimized.
* Data storage should support detailed logging for troubleshooting.
* The infrastructure should support two European regions: east and west.

### Sub-task 1.2 - define components
**Plan**
* Based on those requirements you see as most important, decompose your solution into components, or tiers, or layers.
* **Note** that it's not necessary to account for all the non-functional requirements at this point.
* Visualise the decomposition (UML class/package/component diagram or an informal diagram with a legend is recommended).
* Choose technologies/frameworks for every component/tier/layer from the decomposition and **log the rationale** behind the choice
  * 1-2 sentences is enough
  * include links to any docs/product sites/articles you feel relevant
* **Discuss** the choices with your peer or mentor.

### Sub-task 1.3 - define a flow
**Plan**
* Based on the decomposition from task 1.2, pick any major use case from the requirements.
* Visualise the use case (UML sequence/activity or BPMN diagram is recommended).

## Task 2 - DB choice
**Plan**
* On your projects, you might need to make major decisions that affect both functions and quality of the system.
Here, you need to choose a DB for the underlying storage.
* Pick any 3 DB options you have experience with, but make sure they are different enough 
(cloud-managed service vs self-hosted, SQL vs NoSQL, search engine vs DB, or else).
* Compare the DB options and choose one using the following decision log template:
```
  a.   Title
  b.   Status
  c.   Background
  d.   Glossary
  e.   Functional requirements
  f.   Non-functional requirements
  g.   Constraints
  h.   Quality attributes
  i.   Solution Options
  j.   Decision criteria
  k.   Decision
  l.   Sources
  m.   Tickets
  n.   References
```

## (Optional) Task 2 - context view
**Plan**
* Oftentimes, especially when you have to work with developing brand-new services or major components, it's useful
to define the context shared across all the docs/decisions you make for the solution.
* Prepare a C4 context view describing the relationships of your system with external systems and users.

## (Advanced) Task 3 - infrastructure view
**Plan**
* Pick a cloud provider you feel most comfortable with.
* Define a deployment diagram for your solution (e.g. using AWS diagram).
* Make as many decisions related to the non-functional requirements above as possible and log them
  * 1-2 sentences is enough
  * include links to any docs/product sites/articles you feel relevant