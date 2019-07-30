# Levels of Requirements

![](../../.gitbook/assets/image%20%28149%29.png)

### Business

{% hint style="success" %}
defines the business problems or opportunities about the product. Business requirements define why the software product is being developed. They are the objectives of the customer requesting the development of the software.
{% endhint %}

**Business requirements** describe why the organization is undertaking the project. They state some benefits that the developing organization or its customers expect to receive from the product. Business requirements may be delineated in several documents such as a project charter, business case, or in a project vision and scope statements. Business requirements bring the project owner, stakeholders and the project team on the same song sheet. But you can’t build software from such high-level information.

* Problem Statement
* Project Vision
* Project Constraints \(Budget, Schedule, and Resources\)
* Project Objectives
* Project Scope Statements
* Business Process Analysis
* Stakeholder Analysis

**A business requirement is not something a system must do. It is something that the business needs to do or have in order to stay in business.** For example, a business requirement can be:

* a process they must complete
* a piece of data they need to use for that process
* a business rule that governs that process and that data

Your business requirements change less \(in most businesses\) than your functional requirements, and are typically more objective. 

Remember, “The system shall do this or that…” describes the how \(or the functionality\). It is the manifestation of the business requirement in a system.

Understanding the true problem or business need \(Business Requirement\) will ensure that you are delivering the highest value to your customer. Once we understand the true business needs, we can start determining the best way to approach building a solution \(whether automation is involved or not\) and how to implement that solution.

### User

{% hint style="success" %}
defines functionality of the software product from the user’s perspective. They define what the software has to do in order for the users to accomplish their objectives.
{% endhint %}

**User requirements**, often referred to as user needs, describe what the user does with the system, such as what activities that users must be able to perform. User requirements are generally documented in a User Requirements Document \(URD\) using narrative text. User requirements are generally signed off by the user and used as the primary input for creating system requirements.

An important and difficult step of designing a software product is determining what the user actually wants it to do. This is because the user is often not able to communicate the entirety of their needs and wants, and the information they provide may also be incomplete, inaccurate and self-conflicting. The responsibility of completely understanding what the customer wants falls on the business analyst. This is why user requirements are generally considered separately from system requirements. The business analyst carefully analyzes user requirements and carefully constructs and documents a set of high quality system requirements ensuring that that the requirements meet certain quality characteristics.

### Functional requirements

{% hint style="success" %}
define the software functionality must be built into the product to enable users to accomplish their tasks. This includes the entire external, database, functional/non-functional requirements.
{% endhint %}

Some of the more typical functional requirements include:

* Business Rules
* Transaction corrections, adjustments and cancellations
* Administrative functions
* Authentication
* Authorization levels
* Audit Tracking
* External Interfaces
* Certification Requirements
* Reporting Requirements
* Historical Data
* Legal or Regulatory Requirements

**Functional requirements** provide a very detailed description of all of the functions your future product will have, how it should behave, and how it should respond to different user commands and gestures.

The functional requirements are mostly about how the system should act when the user interacts with it. How the login process should look like, what kind of information the user will be able to retrieve/have access to with what type of membership, what the user journey will be like, etc.

While there are different ways to write down functional specifications, one of the most popular ways is just by plain text. It is also common to draw a diagram to visually show the relationships between the user and the system but this approach has its drawbacks: it’s easy to misunderstand the issue or omit the context of the situation.

Today, there’re two key methods of creating functional requirements: through **use cases** and **user stories**.

When you describe requirements not as separate functions, but as a whole while considering the current context and simulating how users will interact with the entire system, you have a better chance to ensure the completeness and non-redundancy of requirements.

A regular use case should include:

* _**Actors**_ – Users that interact with a system.
* _**System**_ – The system that is built according to the specifications.
* _**Goals**_ – What makes user interact with a system and what they want to achieve as a final result.

Another way to structure functional requirements is by writing them in the form of user stories. User stories tend to better emphasize the end user and their goals. The typical structure of a user story looks as follows:

* As a **type of user**, I want **some goal** so that **some reason**.

For example: _**As a user I want to have my Google account connected to my profile so that I will be able to log in with the Google account**_.

Every user story should be accompanied by the **acceptance criteria** that define the conditions the feature should meet/satisfy in order to be accepted by your product owner and stakeholders. One user story should have at least one acceptance criterion, each being testable and transparent to all of the stakeholders.

For example, the acceptance criteria for a login feature might be as follows:

* User can use an email or a mobile phone number to log in;
* The lengths of the password should be between 6 and 20 symbols;
* Symbols in a password may include letters, numbers and special signs.

