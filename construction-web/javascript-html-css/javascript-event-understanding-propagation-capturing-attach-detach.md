# JavaScript: Event Understanding \(propagation, capturing, attach/detach\)

### Event handling \(bubbling and capturing\) <a id="event-handling-bubbling-and-capturing"></a>

* При наступлении события – элемент, на котором оно произошло, помечается как «целевой» \(event.target\).
* Далее событие сначала двигается вниз от корня документа к event.target, по пути вызывая обработчики, поставленные через addEventListener\(...., true\).
* Далее событие двигается от event.target вверх к корню документа, по пути вызывая обработчики, поставленные через on\* и addEventListener\(...., false\).

### Объект события

* event.type \('click'\)
* event.target \(самый глубокий, на котором произошло событие\)
* event.currentTarget \(Элемент, на котором сработал обработчик\)
* event.clientX / event.clientY

### Стадии

* Событие сначала идет сверху вниз. Эта стадия называется «стадия перехвата» \(capturing stage\)
* Событие достигло целевого элемента. Это – «стадия цели» \(target stage\)
* После этого событие начинает всплывать. Это – «стадия всплытия» \(bubbling stage\)

### **bubbling \(всплытие\)**

> исключение focus - не всплывает

* При наступлении события обработчики сначала срабатывают на самом вложенном элементе, затем на его родителе, затем выше и так далее, вверх по цепочке вложенности.
* event.stopPropagation\(\) - прекратить всплытие
* event.stopImmediatePropagation\(\) - прекратить немедленно \(для одного уровня \)

### **capturing \(погружение\)**

* редко используется

Note that the word event is not itself a technical word that requires definition. **Events** are simply occurrences that a web browser will notify your program about. Events are not JavaScript objects and have no manifestation in the source code of your program.

The **event type** is a string that specifies what kind of event occurred. The type “mousemove”, for example, means that the user moved the mouse. The type “keydown” means that a key on the keyboard was pushed down. And the type “load” means that a document \(or some other resource\) has finished loading from the network. Because the type of an event is just a string, it is sometimes called an event name, and indeed, we use this name to identify the specific kind of event we’re talking about.

The **event target** is the object on which the event occurred or with which the event is associated. When we speak of an event, we must specify both the type and the target. A load event on a Window, for example, or a click event on a  Element. Window, Document, and Element objects are the most common event targets in client-side JavaScript applications, but some events are triggered on other kinds of objects.

An **event handler or event listener** is a function that handles or responds to an event.1 Applications register their event handler functions with the web browser, specifying an event type and an event target. When an event of the specified type occurs on the specified target, the browser invokes the handler. When event handlers are invoked for an object, we sometimes say that the browser has “fired”, “triggered”, or “dispatched” the event.

An **event object** is an object that is associated with a particular event and contains details about that event.

**Event propagation** is the process by which the browser decides which objects to trigger event handlers on. For events that are specific to a single object \(such as the load event on the Window object\), no propagation is required. When certain kinds of events occur on document elements, however, they propagate or “bubble” up the document tree. If the user moves the mouse over a hyperlink, the mousemove event is first fired on the  element that defines that link.

In another form of event propagation, known as **event capturing**, handlers specially registered on container elements have the opportunity to intercept \(or “capture”\) events before they are delivered to their actual target.

