# Most often used design patterns

### Repository

The Repository provides an abstraction of data, so that your application can work with a simple abstraction that has an interface approximating that of a collection. Adding, removing, updating, and selecting items from this collection is done through a series of straightforward methods, without the need to deal with database concerns like connections, commands, cursors, or readers.

Purpose:  loose coupling and can keep domain objects persistence ignorant.

Two types of implementations:

* Repository Per Entity or Business Object Create a new Repository implementation for each business object you need to store to or retrieve from your persistence layer. Further, you should only implement the specific methods you are calling in your application. The biggest benefit of this approach is [ ](http://deviq.com/yagni)– you won’t waste any time implementing methods that never get called.
* Generic Repository Interface Create a simple, generic interface for your Repository. The advantage of this approach is that it ensures you have a common interface for working with any of your objects.

### Service Locator Pattern

The service locator pattern is a design pattern or anti-pattern used in software development to encapsulate the processes involved in obtaining a service with a strong abstraction layer.

![](../../.gitbook/assets/image%20%28102%29.png)

Advantages:

* The "service locator" can act as a simple run-time linker.
* Large sections of a library or application can be completely separated. The only link between them becomes the registry.
* The solution may be simpler with service locator \(vs. dependency injection\) in applications with well-structured component/service design.

Disadvantages:

* The registry hides the class' dependencies, causing run-time errors instead of compile-time errors when dependencies are missing \(similar to using Dependency injection\).
* The registry makes the code more difficult to maintain \(similar to using Dependency injection\), because it becomes unclear when you would be introducing a breaking change. 
* The registry makes code harder to test, since all tests need to interact with the same global service locator class to set the fake dependencies of a class under test.

### Unit of Work

Unit of Work is referred to as a single transaction that involves multiple operations of insert/update/delete and so on kinds.

![](../../.gitbook/assets/image%20%28155%29.png)

During a single operation, that involves more then one entities, all of them use the same DbContext instance. This will ensure that even if one of them breaks, the other one is also not saved, thus maintaining the database consistency.

### Rules Pattern

Rules Pattern helps to reduce complexity and duplication of code, which is full of conditions.

![](../../.gitbook/assets/image%20%28105%29.png)

With the Rules Pattern there is an Evaluator class that loops through a collection of rules and executes them. It evaluates the result and decides what action to take.

### Specification Pattern

Specification pattern is a pattern that allows us to encapsulate some piece of domain knowledge into a single unit – specification – and reuse it in different parts of the code base.

There are 3 main use cases for the Specification pattern:

* Looking up data in the database. That is finding records that match the specification we have in hand.
* Validating objects in the memory. In other words, checking that an object we retrieved or created fits the spec.
* Creating a new instance that matches the criteria. This is useful in scenarios where you don’t care about the actual content of the instances, but still need it to have certain attributes.

![](../../.gitbook/assets/image%20%28129%29.png)

### Event Aggregator

The Event Aggregator pattern tries overcome the limitation of traditional event handling approach by providing a central place to publish and subscribe for events which is nothing but an Event Aggregator.

![](../../.gitbook/assets/image%20%2824%29.png)

**Intent of pattern**

* Simplify subscribing and unsubscribing to events
* Decouple publishers from subscribers allowing both to change without effecting the other.
* Reduce wastage of system resources, but may depend on support from development framework or environment.
* Makes it easy to add new events.
* Centralized handling of events.

### Lazy Load Pattern

An object that doesn't contain all of the data you need but knows how to get it.

![](../../.gitbook/assets/image%20%2841%29.png)

For loading data from a database into memory it's handy to design things so that as you load an object of interest you also load the objects that are related to it. This makes loading easier on the developer using the object, who otherwise has to load all the objects he needs explicitly. There are four main varieties of lazy load. 

**Lazy Initialization** uses a special marker value \(usually null\) to indicate a field isn't loaded. Every access to the field checks the field for the marker value and if unloaded, loads it. 

**Virtual Proxy** is an object with the same interface as the real object. The first time one of its methods are called it loads the real object and then delegates. 

**Value Holder** is an object with a getValue method. Clients call getValue to get the real object, the first call triggers the load. A **ghost** is the real object without any data. The first time you call a method the ghost loads the full data into its fields.

### Model View Controller \(MVC\) Pattern

Model-View-Controller \(MVC, «Модель-Представление-Контроллер», «Модель-Вид-Контроллер»\) — схема разделения данных приложения, пользовательского интерфейса и управляющей логики на три отдельных компонента: модель, представление и контроллер — таким образом, что модификация каждого компонента может осуществляться независимо.

**Model** предоставляет данные и реагирует на команды контроллера, изменяя своё состояние.

**View** отвечает за отображение данных модели пользователю, реагируя на изменения модели.

**Controller** интерпретирует действия пользователя, оповещая модель о необходимости изменений.

![](../../.gitbook/assets/image%20%28134%29.png)

### Model View Presenter \(MVP\) Pattern

MVP — шаблон проектирования пользовательского интерфейса, который был разработан для облегчения автоматического модульного тестирования и улучшения разделения ответственности в презентационной логике \(отделения логики от отображения\).

**Model** — хранит в себе всю бизнес-логику, при необходимости получает данные из хранилища.

**View** — реализует отображение данных \(из Модели\), обращается к Presenter за обновлениями.

**Presenter** — реализует взаимодействие между Моделью и Видом.

![](../../.gitbook/assets/image%20%2897%29.png)

Как видно на этой диаграмме, Presenter занял место контроллера и отвечает за перемещение данных, введенных пользователем, а также за обновление представления при изменениях, которые происходят в модели. Presenter общается с представлением через интерфейс, который позволяет увеличить тестируемость, так как модель может быть заменена на специальный макет для модульных тестов.

### Model View ViewModel \(MVVM\) Pattern

MVVM \(Model-View-ViewModel\) - это шаблон, который появился для обхода ограничений паттернов MVC и MVP, и объединяющий некоторые из их сильных сторон.

Шаблон MVVM имеет три основных компонента: **модель**, которая представляет бизнес-логику приложения, **представление** пользовательского интерфейса XAML, и **представление-модель**, в котором содержится вся логика построения графического интерфейса и ссылка на модель, поэтому он выступает в качестве модели для представления.

![](../../.gitbook/assets/image%20%284%29.png)

### Null Object Pattern

Целью Null-object является инкапсулирование отсутствия объекта путём замещения его другим объектом, который ничего не делает.

Данный шаблон проектирования рекомендуется использовать, когда:

* Объект требует взаимодействия с другими объектами. Null Object не устанавливает нового взаимодействия — он использует уже установленное взаимодействие. 
* Какие-то из взаимодействующих объектов должны бездействовать.
* Требуется абстрагирование «общения» с объектами, имеющими NULL-значение.

![](../../.gitbook/assets/image%20%2815%29.png)



