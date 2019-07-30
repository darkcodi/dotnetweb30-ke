# Behavioral patterns

### **Strategy \(**Policy**\)**

визначає сімейство алгоритмів, інкапсулює кожен з них та робить їх взаємозамінними. Дозволяє змінювати алгоритми незалежно від коду клієнтів. Якщо в системі є алгоритми, які часто можуть використовуватися повторно в різних частинах програми, зручно їх виділити в окрему сутність, параметризувати та запускати там, де це потрібно, не дублюючи сам код.

_When should be used:_ 

* програма повинна забезпечувати різні варіанти алгоритму або поведінки;
* у наявності є багато споріднених класів, які відрізняються тільки поведінкою \(мають схожі інтерфейси, але різну логіку\);
* потрібно змінювати поведінку кожного екземпляра класу;
* необхідно змінити поведінку об'єктів на стадії виконання; 
* введення інтерфейсу дозволяє класам-клієнтам нічого не знати про класи, що реалізують цей інтерфейс і інкапсулюють в собі конкретні алгоритми \(метод “чорного ящика”\).

![](../../../.gitbook/assets/image%20%2877%29.png)

**Strategy** – оголошує загальний для всіх підтримуваних алгоритмів інтерфейс. Клас Context користується цим інтерфейсом для виклику конкретного алгоритму, визначеного в класі ConcreteStrategy.

**ConcreteStrategy** - реалізує алгоритм, що використовує інтерфейс, оголошений у класі Strategy. 

**Context**: конфігурується об'єктом класу ConcreteStrategy; зберігає посилання на об'єкт класу Strategy; може визначати інтерфейс, який дозволяє об'єкту Strategy отримати доступ до даних контексту.

### **Template method**  

визначає функціональність конкретних методів в рамках лише абстрактних сутностей. Визначає основу алгоритму та дозволяє підкласам перевизначити деякі кроки алгоритму, не змінюючи структуру в цілому.

_When should be used:_ 

*  необхідно забезпечити одноразову реалізацію інваріантних частин алгоритму, залишаючи реалізацію поведінки, що змінюється, на розсуд підкласів;
* треба відокремити та локалізувати в одному класі поведінку, що є загальною для усіх підкласів, щоб запобігти дублювання коду. Це хороший приклад техніки “винесення за лапки з метою узагальнення”;
* батьківські класи повинні мати змогу уніфіковано звертатися до поведінки підкласів; 
* необхідний дозвіл на розширення коду нащадками тільки в чітко визначених місцях.

![](../../../.gitbook/assets/image%20%28156%29.png)

**AbstractClass** – визначає абстрактні примітивні операції, що заміщуються у конкретних підкласах для реалізації кроків алгоритму; реалізує шаблонний метод, що визначає скелет алгоритму; **ConcreteClass** – реалізує примітивні операції, що виконують кроки алгоритму у спосіб, необхідний підкласу. ConcreteClass припускає,  що інваріантні \(зафіксовані\) кроки алгоритму будуть виконані в AbstractClass.

### **State** 

дозволяє об'єкту варіювати свою поведінку залежно від внутрішнього стану.

Часто називається динамічною Strategy. Передбачає реалізацію поведінки, асоційованої з певним станом об'єкту, а також забезпечення зміни поведінки відповідно до зміни внутрішнього стану.

_When should be used:_ 

*   поведінка об'єкта залежить від його стану і повинна змінюватися під час виконання;
* в коді операцій зустрічаються умовні оператори, які складаються з багатьох гілок і у яких вибір гілки залежить від стану \(зазвичай стан подається зліченними константами\);
* одна і та сама структура умовного оператора повторюється в кількох операціях, патерн “Стан” передбачає розміщення кожної гілки в окремому класі.  Це дозволяє трактувати стан об'єкту як самостійний об'єкт, який може змінюватися незалежно від інших; 
* переходи між станами об’єкту повинні бути явними.

![](../../../.gitbook/assets/image%20%28115%29.png)

**Context** – визначає інтерфейс, що представляє інтерес для клієнтів. Зберігає екземпляр підкласу ConcreteState, яким визначається поточний стан;

**State** – визначає інтерфейс для інкапсуляції поведінки, асоційованого з конкретним станом контексту Context; 

**ConcreteState** – кожен підклас реалізує поведінку, асоційовану з деяким станом контексту Context.

### **Chain of Responsibility**

призначений для організації в системі рівнів відповідальності.

Будує об’єкти складених частин програми зв’язаними між собою ланцюжком для передачі запиту на обробку від більш низьких, деталізованих прошарків до більш глобальних. Дозволяє уникнути зв’язування відправника запиту та його отримувача.

_When should be used:_ 

*   у розроблюваній системі є група об’єктів, які можуть оброблювати запит певного типу, причому справжній обробник запиту заздалегідь невідомий;
* набір об’єктів, які обробляють запит, повинен визначатися динамічно;
* потрібно відправити запит одному з декількох об’єктів, не вказуючи явно, якому саме;
* всі повідомлення повинні бути оброблені хоча б одним об’єктом системи; повідомлення в системі оброблюються за схемою “оброби сам або передай іншому”, тобто одні повідомлення обробляються на тому ж рівні, де вони були отримані, а інші – передаються об’єктам іншого рівня.

![](../../../.gitbook/assets/image%20%28116%29.png)

  
**Handler** – визначає інтерфейс для обробки запитів, реалізує зв’язок зі спадкоємцем \(необов’язково\);

**ConcreteHandler** –оброблює запит, за який відповідає. Має доступ до свого спадкоємця. Якщо може самостійно обробити запит – робить це, якщо ні – передає його своєму спадкоємцю;

**Client** – відправляє запит деякому об’єкту ConcreteHandler у ланцюжку.

Коли клієнт ініціює запит, він починає просуватися ланцюжком, поки якийсь об’єкт ConcreteHandler не візьме на себе відповідальність за його обробку.

### **The Command \(**Action or Transaction\)

інкапсулює різні алгоритми в єдину сутність \(об’єкт\), завдяки чому можна параметризувати клієнтів різними запитами, вести історію виконаних операцій та підтримувати скасування операцій.

Забезпечує обробку команди у вигляді об’єкту, що дозволяє зберігати її, передавати у якості параметра методам, а також повертати її як результат методу.

_When should be used:_ 

* треба параметризувати об’єкти виконуваною дією;
* потрібно визначати, ставити в чергу та виконувати запити у різний час;
* потрібно підтримати відміну операцій;
* треба підтримати протоколювання змін \(лог\);
* структурувати систему на основі високорівневих операцій, побудованих з примітивних; команди для різних отримувачів повинні бути оброблені у різний спосіб.

![](../../../.gitbook/assets/image%20%28139%29.png)

**Command** – визначає інтерфейс для виконання операцій;

**ConcreteCommand** – визначає зв’язок між об’єктом-отримувачем Receiver та дією; реалізує операцію Execute шляхом виклику відповідних операцій об’єкту Receiver;

**Client** – створює об’єкти класу ConcreteCommand та встановлює їх отримувачів;

**Invoker** – ініціатор. Звертається до команди для виконання запиту; 

**Receiver** – отримувач. Має інформацію про способи виконання операцій, необхідних для задоволення запиту. Отримувачем може бути будь-який клас.

### **Mediator** 

надає **єдиний центр взаємодії** певної групи об’єктів, які повинні бути взаємнопов’язаними між собою. Визначає об'єкт, що інкапсулює спосіб взаємодії множини об'єктів

_When should be used:_ 

* потрібно послабити зв’язність системи, позбавляючи об'єкти від необхідності явно посилатися один на одного і дозволяючи тим самим незалежно змінювати взаємодії між ними;
* існують об'єкти, зв'язки між котрими досить складні та чітко задані. Отримані при цьому залежності не структуровані та важкі для розуміння;
* не можна повторно використовувати об'єкт, оскільки він обмінюється інформацією з багатьма іншими об'єктами; 
* поведінка, розподілена між кількома класами, повинна піддаватися налагодженню без створювання множини підкласів

![](../../../.gitbook/assets/image%20%2849%29.png)

**Mediator** – визначає інтерфейс для обміну інформацією з об'єктами Colleague;

**ConcreteMediator** – реалізує кооперативне поведінку, координуючи дії об'єктів Colleague; володіє інформацією про колег і підраховує їх;

Класи **Colleague** – кожен клас Colleague «знає» про свій об'єкті Mediator; всі колеги обмінюються інформацією лише з посередником, так як за його відсутності їм довелося б спілкуватися між собою безпосередньо.

 Колеги посилають запити посереднику та отримують повідомлення від нього. Посередник реалізує кооперативну поведінку шляхом переадресації кожного запиту відповідному колезі \(або декільком колегам\).

### **Observer** 

Define a one-to-many dependency between objects where a state change in one object results in all its dependents being notified and updated automatically.

_When should be used:_ 

* A one-to-many dependency between objects should be defined without making the objects tightly coupled.
* It should be ensured that when one object changes state an open-ended number of dependent objects are updated automatically.
* It should be possible that one object can notify an open-ended number of other objects.

Defining a one-to-many dependency between objects by defining one object \(subject\) that updates the state of dependent objects directly is inflexible because it couples the subject to particular dependent objects. Tightly coupled objects are hard to implement, change, test, and reuse because they refer to and know about \(how to update\) many different objects with different interfaces.

![](../../../.gitbook/assets/image%20%2846%29.png)



* Define `Subject` and `Observer` objects.
* so that when a subject changes state, all registered observers are notified and updated automatically.

The sole responsibility of a subject is to maintain a list of observers and to notify them of state changes by calling their `update()` operation.   
The responsibility of observers is to register \(and unregister\) themselves on a subject \(to get notified of state changes\) and to update their state \(synchronize their state with subject's state\) when they are notified.   
This makes subject and observers loosely coupled. Subject and observers have no explicit knowledge of each other. Observers can be added and removed independently at run-time.  
This notification-registration interaction is also known as publish-subscribe.

### **Interpreter** 

Design pattern that specifies how to evaluate sentences in a language. The basic idea is to have a [class](https://en.wikipedia.org/wiki/Class_%28computer_science%29) for each symbol \(terminal or nonterminal\) in a specialized computer language. The syntax tree of a sentence in the language is an instance of the composite pattern and is used to evaluate \(interpret\) the sentence for a client.

Шаблон Інтерпретатор слід використовувати, коли є мова для інтерпретації, речення котрої можна подати у вигляді абстрактних синтаксичних дерев. Найкраще шаблон працює коли:

* граматика проста. Для складних граматик ієрархія класів стає занадто громіздкою та некерованою. У таких випадках краще застосовувати генератори синтаксичних аналізаторів, оскільки вони можуть інтерпретувати вирази, не будуючи абстрактних синтаксичних дерев, що заощаджує пам'ять, а можливо і час;
* ефективність не є головним критерієм. Найефективніші інтерпретатори зазвичай не працюють безпосередньо із деревами, а спочатку транслюють їх в іншу форму. Так, регулярний вираз часто перетворюють на скінченний автомат. Але навіть у цьому разі сам транслятор можна реалізувати за допомогою шаблону інтерпретатор.

![](../../../.gitbook/assets/image%20%2866%29.png)



**AbstractExpression** — абстрактний вираз: оголошує абстрактну операцію Interpret, загальну для усіх вузлів у абстрактному синтаксичному дереві;

**TerminalExpression** — термінальний вираз:

* реалізує операцію Interpret для термінальних символів граматики;
* необхідний окремий екземпляр для кожного термінального символу у реченні;

**NonterminalExpression** — нетермінальний вираз:

* по одному такому класу потребується для кожного граматичного правила;
* зберігає змінні екземпляру типу AbstractExpression для кожного символу;
* реалізує операцію Interpret для нетермінальних символів граматики. Ця операція рекурсивно викликає себе для змінних, зберігаючих символи;

**Context** — контекст:містить інформацію, глобальну по відношенню до інтерпретатору;

**Client** — клієнт:

* будує \(або отримує у готовому вигляді\) абстрактне синтаксичне дерево, репрезентуюче окреме речення мовою з даною граматикою. Дерево складено з екземплярів класів NonterminalExpression та TerminalExpression;
* викликає операцію Interpret.

### Iterator 

An iterator is used to traverse a container and access the container's elements. The iterator pattern decouples algorithms from containers; in some cases, algorithms are necessarily container-specific and thus cannot be decoupled.

For example, the hypothetical algorithm SearchForElement can be implemented generally using a specified type of iterator rather than implementing it as a container-specific algorithm. This allows SearchForElement to be used on any container that supports the required type of iterator.

_When should be used:_ 

* для доступу до змісту агрегованих об'єктів не розкриваючи їхнє внутрішнє улаштування;
* для підтримки декількох активних обходів одного й того ж агрегованого об'єкта;
* для подання уніфікованого інтерфейсу з метою обходу різноманітних агрегованих структур \(тобто для підтримки поліморфної ітерації\).

![](../../../.gitbook/assets/image%20%28157%29.png)

**Iterator** визначає інтерфейс для доступу та обходу елементів

**ConcreteIterator**

* реалізує інтерфейс класу Iterator;
* слідкує за поточною позицією під час обходу агрегату;

**Aggregate** визначає інтерфейс для створення об'єкта-ітератора;

**ConcreteAggregate** реалізує інтерфейс створення ітератора та повертає екземпляр відповідного класу ConcreteIterator

### Visitor 

A way of separating an algorithm from an object structure on which it operates. A practical result of this separation is the ability to add new operations to existent object structures without modifying the structures. It is one way to follow the open/closed principle.

In essence, the visitor allows adding new virtual functions to a family of classes, without modifying the classes. Instead, a visitor class is created that implements all of the appropriate specializations of the virtual function. The visitor takes the instance reference as input, and implements the goal through double dispatch.

_When should be used:_ 

* many unrelated operations on an object structure are required,
* the classes that make up the object structure are known and not expected to change,
* new operations need to be added frequently,
* an algorithm involves several classes of the object structure, but it is desired to manage it in one single location,
* an algorithm needs to work across several independent class hierarchies.

![](../../../.gitbook/assets/image%20%281%29.png)



**Відвідувач** \(зазвичай, абстрактний клас чи інтерфейс\) визначає дію над кожним класом конкретних елементів. Ім'я та сигнатура операції мають визначати конкретний клас даних, елемент якого треба відвідати. Це дає можливість відвідувачу доступатися до елементів через інтерфейс конкретного класу.

**Конкретний відвідува**ч \(конкретний клас, що наслідує Відвідувач\) реалізує чи перевизначає операції, визначені в базовому класі. Містить алгоритми, які виконуватимуться над об'єктами відповідного класу. Також даний клас утримує локальний стан алгоритмів \(цей стан, зазвичай, утримує проміжні результати під час обходу структури, та ін.\).

**Елемент** \(зазвичай, абстрактний клас чи інтерфейс\) визначає операцію, яка приймає об'єкт відвідувача як аргумент.

**Конкретний елемент** \(конкретний клас, що наслідує Елемент\) визначає операцію, що приймає об'єкт відвідувача як аргумент.

**Структура елементів** \(клас, що реалізує структуру елементів\)

* може перераховувати елементи, які містить.
* надає високорівневий інтерфейс, що дозволяє відвідувачу виконувати елементи.
* може бути Компонувальником чи колекцією \(як список або черга\).

###  **Memento** 

provides the ability to restore an object to its previous state \(undo via rollback\).

The memento pattern is implemented with three objects: the originator, a caretaker and a memento. The originator is some object that has an internal state. The caretaker is going to do something to the originator, but wants to be able to undo the change. The caretaker first asks the originator for a memento object. Then it does whatever operation \(or sequence of operations\) it was going to do. To roll back to the state before the operations, it returns the memento object to the originator. The memento object itself is an opaque object \(one which the caretaker cannot, or should not, change\). When using this pattern, care should be taken if the originator may change other objects or resources - the memento pattern operates on a single object.

Classic examples of the memento pattern include the seed of a pseudorandom number generator \(it will always produce the same sequence thereafter when initialized with the seed state\) and the state in a finite state machine.

_When should be used:_ 

* необхідно зберегти миттєвий знімок стану об'єкта \(або його частини\), щоб згодом об'єкт можна було відтворити у тому ж самому стані;
* безпосереднє вилучення цього стану розкриває деталі реалізації та порушує інкапсуляцію об'єкта.

![](../../../.gitbook/assets/image%20%2882%29.png)



* **Memento** — контекст:
  * зберігає внутрішній стан об'єкта Originator. Обсяг інформації, що зберігається, може бути різним та визначається потребами хазяїна;
  * забороняє доступ усім іншим об'єктам окрім хазяїна. По суті знімок має два інтерфейси. Опікун Caretaker користується лише вузьким інтерфейсом знімку — він може лише передавати знімок іншим об'єктам. Навпаки, хазяїн користується широким інтерфейсом, котрий забезпечує доступ до всіх даних, необхідних для відтворення об'єкта \(чи його частини\) у попередньому стані. Ідеальний варіант — коли тільки хазяїну, що створив знімок, відкритий доступ до внутрішнього стану знімку;
* **Originator** — хазяїн:
  * створює знімок, що утримує поточний внутрішній стан;
  * використовує знімок для відтворення внутрішнього стану;
* **CareTaker** — опікун:
  * відповідає за зберігання знімку;
  * не проводить жодних операцій над знімком та не має уяви про його внутрішній зміст.

