# Software Architecture Patterns \(structure, pros & cons\)

### Layered architecture

Components within the layered architecture pattern are organized into horizontal layers, each layer performing a specific role within the application \(e.g., presentation logic or business logic\). Although the layered architecture pattern does not specify the number and types of layers that must exist in the pattern, most layered architectures consist of four standard layers: presentation, business, persistence, and database.

![](../../.gitbook/assets/image%20%2819%29.png)

#### Overall agility 

_**Rating:**_ Low __

_**Analysis:**_ Overall agility is the ability to respond quickly to a constantly changing environment. While change can be isolated through the layers of isolation feature of this pattern, it is still cumbersome and time-consuming to make changes in this architecture pattern because of the monolithic nature of most implementations as well as the tight coupling of components usually found with this pattern. 

#### Testability 

_**Rating:**_ High _****_

_**Analysis:**_ Because components belong to specific layers in the architecture, other layers can be mocked or stubbed, making this pattern is relatively easy to test. A developer can mock a presentation component or screen to isolate testing within a business component, as well as mock the business layer to test certain screen functionality. 

#### Performance 

_**Rating:**_ Low __

_**Analysis:**_ While it is true some layered architectures can perform well, the pattern does not lend itself to high-performance applications due to the inefficiencies of having to go through multiple layers of the architecture to fulfill a business request. 

#### Scalability 

_**Rating:**_ Low 

_**Analysis:**_ Because of the trend toward tightly coupled and monolithic implementations of this pattern, applications build using this architecture pattern are generally difficult to scale. You can scale a layered architecture by splitting the layers into separate physical deployments or replicating the entire application into multiple nodes, but overall the granularity is too broad, making it expensive to scale. 

#### Ease of development 

_**Rating:**_ High 

_**Analysis:**_ Ease of development gets a relatively high score, mostly because this pattern is so well known and is not overly complex to implement. Because most companies develop applications by separating skill sets by layers \(presentation, business, database\), this pattern becomes a natural choice for most business-application development.

### Event-driven architecture

The event-driven architecture pattern consists of two main topologies, the mediator and the broker.

#### Mediator Topology

The event flow starts with a client sending an event to an event queue, which is used to transport the event to the event mediator. The event mediator receives the initial event and orchestrates that event by sending additional asynchronous events to event channels to execute each step of the process. Event processors, which listen on the event channels, receive the event from the event mediator and execute specific business logic to process the event.

![](../../.gitbook/assets/image%20%2876%29.png)

#### Broker Topology

The broker topology differs from the mediator topology in that there is no central event mediator; rather, the message flow is distributed across the event processor components in a chain-like fashion through a lightweight message broker. 

![](../../.gitbook/assets/image%20%2881%29.png)

The broker topology is all about the chaining of events to perform a business function. The best way to understand the broker topology is to think about it as a relay race. In a relay race, runners hold a baton and run for a certain distance, then hand off the baton to the next runner, and so on down the chain until the last runner crosses the finish line. In relay races, once a runner hands off the baton, she is done with the race_**.**_

#### Overall agility 

_**Rating:**_ High

_**Analysis:**_ Overall agility is the ability to respond quickly to a constantly changing environment. Since event-processor components are single-purpose and completely decoupled from other event processor components, changes are generally isolated to one or a few event processors and can be made quickly without impacting other components. 

#### Testability 

_**Rating:**_ Low

_**Analysis:**_ While individual unit testing is not overly difficult, it does require some sort of specialized testing client or testing tool to generate events. Testing is also complicated by the asynchronous nature of this pattern. 

#### Performance 

_**Rating:**_ High

_**Analysis:**_ While it is certainly possible to implement an event-driven architecture that does not perform well due to all the messaging infrastructure involved, in general, the pattern achieves high performance through its asynchronous capabilities; in other words, the ability to perform decoupled, parallel asynchronous operations outweighs the cost of queuing and dequeuing messages. 

#### Scalability 

_**Rating:**_ High

_**Analysis:**_ Scalability is naturally achieved in this pattern through highly independent and decoupled event processors. Each event processor can be scaled separately, allowing for fine-grained scalability. 

#### Ease of development 

_**Rating:**_ Low

_**Analysis:**_ Development can be somewhat complicated due to the asynchronous nature of the pattern as well as contract creation and the need for more advanced error handling conditions within the code for unresponsive event processors and failed brokers.

### Microkernel architecture

The microkernel architecture pattern consists of two types of architecture components: a _core system_ and _plug-in modules_. Application logic is divided between independent plug-in modules and the basic core system, providing extensibility, flexibility, and isolation of application features and custom processing logic.

![](../../.gitbook/assets/image%20%28162%29.png)

The plug-in modules are stand-alone, independent components that contain specialized processing, additional features, and custom code that is meant to enhance or extend the core system to produce additional business capabilities One great thing about the microkernel architecture pattern is that it can be embedded or used as part of another architecture pattern.

#### Overall agility 

_**Rating:**_ High

_**Analysis:**_ Overall agility is the ability to respond quickly to a constantly changing environment. Changes can largely be isolated and implemented quickly through loosely coupled plug-in modules. In general, the core system of most microkernel architectures tends to become stable quickly, and as such is fairly robust and requires few changes over time. 

#### Testability 

_**Rating:**_ High

_**Analysis:**_ Plug-in modules can be tested in isolation and can be easily mocked by the core system to demonstrate or prototype a particular feature with little or no change to the core system. 

#### Performance 

_**Rating:**_ High

_**Analysis:**_ While the microkernel pattern does not naturally lend itself to high-performance applications, in general, most applications built using the microkernel architecture pattern perform well because you can customize and streamline applications to only include those features you need. The JBoss Application Server is a good example of this: with its plug-in architecture, you can trim down the application server to only those features you need, removing expensive non-used features such as remote access, messaging, and caching that consume memory, CPU, and threads and slow down the app server. 

#### Scalability 

_**Rating:**_ Low

_**Analysis:**_ Because most microkernel architecture implementations are product based and are generally smaller in size, they are implemented as single units and hence not highly scalable. Depending on how you implement the plug-in modules, you can sometimes provide scalability at the plug-in feature level, but overall this pattern is not known for producing highly scalable applications. 

#### Ease of development 

_**Rating:**_ Low

_**Analysis:**_ The microkernel architecture requires thoughtful design and contract governance, making it rather complex to implement. Contract versioning, internal plug-in registries, plug-in granularity, and the wide choices available for plug-in connectivity all contribute to the complexity involved with implementing this pattern.

### Microservices architecture

Regardless of the topology or implementation style you chose, there are several common core concepts that apply to the general architecture pattern. The first of these concepts is the notion of separately deployed units. Each component of the microservices architecture is deployed as a separate unit, allowing for easier deployment through an effective and streamlined delivery pipeline, increased scalability, and a high degree of application and component decoupling within your application.

![](../../.gitbook/assets/image%20%2812%29.png)

Another key concept within the microservices architecture pattern is that it is a distributed architecture, meaning that all the components within the architecture are fully decoupled from one other and accessed through some sort of remote access.

Three main topologies stand out as the most common and popular: _**the API REST-based topology**_, _**application REST-based topology**_, and _**the centralized messaging topology**_. 

_**The API REST-based topology**_ is useful for websites that expose small, self-contained individual services through some sort of API \(applicationprogramming interface\).

![](../../.gitbook/assets/image%20%28135%29.png)

The application REST-based topology differs from the API REST-based approach in that client requests are received through traditional web-based or fat-client business application screens rather than through a simple API layer.

![](../../.gitbook/assets/image%20%2888%29.png)

Another common approach within the microservices architecture pattern is the centralized messaging topology. This topology  is similar to the previous application REST-based topology except that instead of using REST for remote access, this topology uses a lightweight centralized message broker \(e.g., ActiveMQ, HornetQ, etc.\)

![](../../.gitbook/assets/image%20%28128%29.png)

#### Overall agility 

_**Rating:**_ High

_**Analysis:**_ Overall agility is the ability to respond quickly to a constantly changing environment. Due to the notion of separately deployed units, change is generally isolated to individual service components, which allows for fast and easy deployment. 

#### Testability 

_**Rating:**_ High

_**Analysis:**_ Due to the separation and isolation of business functionality into independent applications, testing can be scoped, allowing for more targeted testing efforts. 

#### Performance 

_**Rating:**_ Low

_**Analysis:**_ While you can create applications implemented from this pattern that perform very well, overall this pattern does not naturally lend itself to high-performance applications due to the distributed nature of the microservices architecture pattern. 

#### Scalability 

_**Rating:**_ High

_**Analysis:**_ Because the application is split into separately deployed units, each service component can be individually scaled, allowing for fine-tuned scaling of the application. 

#### Ease of development 

_**Rating:**_ High

_**Analysis:**_ Because functionality is isolated into separate and distinct service components, development becomes easier due to the smaller and isolated scope.

