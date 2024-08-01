# design-pattern-in-detailed-in-c#

Design patterns are general reusable solutions to common problems in software design. They provide templates for how to solve specific types of problems in various contexts. Here’s a broad overview of some key design patterns, divided into three main categories:

### 1. **Creational Patterns**

These patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.

- **Singleton**: Ensures a class has only one instance and provides a global point of access to it.
- **Factory Method**: Defines an interface for creating an object but allows subclasses to alter the type of objects that will be created.
- **Abstract Factory**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
- **Builder**: Separates the construction of a complex object from its representation so that the same construction process can create different representations.
- **Prototype**: Creates new objects by copying an existing object, known as the prototype.

### 2. **Structural Patterns**

These patterns deal with object composition, creating relationships between objects to form larger structures.

- **Adapter**: Allows incompatible interfaces to work together by converting the interface of a class into another interface that a client expects.
- **Bridge**: Separates an abstraction from its implementation, allowing the two to vary independently.
- **Composite**: Composes objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual objects and compositions uniformly.
- **Decorator**: Adds new functionality to an object dynamically without altering its structure.
- **Facade**: Provides a unified interface to a set of interfaces in a subsystem, making it easier to use.
- **Flyweight**: Reduces the cost of creating and managing a large number of similar objects by sharing as much data as possible.
- **Proxy**: Provides a surrogate or placeholder for another object to control access to it.

### 3. **Behavioral Patterns**

These patterns focus on communication between objects, defining how objects interact and how responsibilities are distributed.

- **Chain of Responsibility**: Passes a request along a chain of handlers, allowing multiple handlers to process the request.
- **Command**: Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.
- **Interpreter**: Defines a grammatical representation for a language and provides an interpreter to interpret the sentences of the language.
- **Iterator**: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
- **Mediator**: Defines an object that encapsulates how a set of objects interact, promoting loose coupling.
- **Memento**: Captures and externalizes an object’s internal state without violating encapsulation, allowing the object to be restored to that state later.
- **Observer**: Defines a dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
- **State**: Allows an object to alter its behavior when its internal state changes, appearing as if it has changed its class.
- **Strategy**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable.
- **Template Method**: Defines the skeleton of an algorithm in a method, deferring some steps to subclasses.
- **Visitor**: Defines a new operation to a group of objects without changing the classes of the objects on which it operates.

Each pattern serves a particular purpose and can be adapted to fit various situations. By using these patterns, developers can create more flexible, reusable, and maintainable code.


Creational patterns are design patterns focused on the process of object creation. They abstract the instantiation process, making it easier to manage and extend object creation. Here’s a detailed look at each of the main creational patterns:

### 1. **Singleton Pattern**

**Purpose**: Ensures a class has only one instance and provides a global point of access to that instance.

**Structure**:
- **Singleton**: The class itself is responsible for maintaining a single instance.
- **Private Constructor**: Prevents other classes from creating instances directly.
- **Static Method**: Provides a global access point to the single instance.

**Implementation Example**:
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // private constructor
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

**Use Cases**:
- When exactly one instance of a class is needed, such as a configuration manager.
- To control access to shared resources, like a database connection.

**Considerations**:
- Can be a bottleneck in multi-threaded environments if not implemented properly.
- May hinder testing and flexibility due to its global access nature.

### 2. **Factory Method Pattern**

**Purpose**: Defines an interface for creating objects but lets subclasses alter the type of objects that will be created.

**Structure**:
- **Product**: Defines the interface of objects the factory method creates.
- **ConcreteProduct**: Implements the `Product` interface.
- **Creator**: Declares the factory method, which returns an object of type `Product`.
- **ConcreteCreator**: Implements the factory method to return an instance of `ConcreteProduct`.

**Implementation Example**:
```java
interface Product {
    void use();
}

class ConcreteProductA implements Product {
    public void use() {
        // Implementation
    }
}

class ConcreteProductB implements Product {
    public void use() {
        // Implementation
    }
}

abstract class Creator {
    public abstract Product factoryMethod();
}

class ConcreteCreatorA extends Creator {
    public Product factoryMethod() {
        return new ConcreteProductA();
    }
}

class ConcreteCreatorB extends Creator {
    public Product factoryMethod() {
        return new ConcreteProductB();
    }
}
```

**Use Cases**:
- When a class can’t anticipate the type of objects it must create.
- When a class wants its subclasses to specify the objects it creates.

**Considerations**:
- Increases the number of classes in the system.
- Can be overkill if the type of objects is known in advance.

### 3. **Abstract Factory Pattern**

**Purpose**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

**Structure**:
- **AbstractFactory**: Declares a set of methods for creating abstract products.
- **ConcreteFactory**: Implements the methods to create concrete products.
- **AbstractProduct**: Defines an interface for a type of product.
- **ConcreteProduct**: Implements the `AbstractProduct` interface.

**Implementation Example**:
```java
interface ProductA {
    void use();
}

interface ProductB {
    void use();
}

class ConcreteProductA1 implements ProductA {
    public void use() {
        // Implementation
    }
}

class ConcreteProductA2 implements ProductA {
    public void use() {
        // Implementation
    }
}

class ConcreteProductB1 implements ProductB {
    public void use() {
        // Implementation
    }
}

class ConcreteProductB2 implements ProductB {
    public void use() {
        // Implementation
    }
}

interface AbstractFactory {
    ProductA createProductA();
    ProductB createProductB();
}

class ConcreteFactory1 implements AbstractFactory {
    public ProductA createProductA() {
        return new ConcreteProductA1();
    }
    public ProductB createProductB() {
        return new ConcreteProductB1();
    }
}

class ConcreteFactory2 implements AbstractFactory {
    public ProductA createProductA() {
        return new ConcreteProductA2();
    }
    public ProductB createProductB() {
        return new ConcreteProductB2();
    }
}
```

**Use Cases**:
- When a system needs to create multiple families of related products.
- To enforce constraints that products from the same family must be used together.

**Considerations**:
- Can be complex to set up and maintain.
- Useful when you have multiple product families with complex interdependencies.

### 4. **Builder Pattern**

**Purpose**: Separates the construction of a complex object from its representation so that the same construction process can create different representations.

**Structure**:
- **Builder**: Defines an abstract interface for creating parts of a `Product`.
- **ConcreteBuilder**: Implements the `Builder` interface to construct and assemble parts of the `Product`.
- **Product**: Represents the complex object under construction.
- **Director**: Constructs an object using the `Builder` interface.

**Implementation Example**:
```java
class Product {
    private String partA;
    private String partB;
    
    public void setPartA(String partA) {
        this.partA = partA;
    }
    
    public void setPartB(String partB) {
        this.partB = partB;
    }
    
    @Override
    public String toString() {
        return "Product [partA=" + partA + ", partB=" + partB + "]";
    }
}

abstract class Builder {
    public abstract void buildPartA();
    public abstract void buildPartB();
    public abstract Product getResult();
}

class ConcreteBuilder extends Builder {
    private Product product = new Product();
    
    public void buildPartA() {
        product.setPartA("Part A");
    }
    
    public void buildPartB() {
        product.setPartB("Part B");
    }
    
    public Product getResult() {
        return product;
    }
}

class Director {
    private Builder builder;
    
    public Director(Builder builder) {
        this.builder = builder;
    }
    
    public void construct() {
        builder.buildPartA();
        builder.buildPartB();
    }
}
```

**Use Cases**:
- When an object needs to be created with many optional components.
- When a construction process must allow for different representations of the object.

**Considerations**:
- Can lead to complex builder classes.
- Useful when the construction process is complex and needs to be separated from the actual representation.

### 5. **Prototype Pattern**

**Purpose**: Creates new objects by copying an existing object, known as the prototype.

**Structure**:
- **Prototype**: Declares an interface for cloning itself.
- **ConcretePrototype**: Implements the cloning operation to create a copy of itself.
- **Client**: Uses the prototype to create new objects.

**Implementation Example**:
```java
interface Prototype extends Cloneable {
    Prototype clone();
}

class ConcretePrototype implements Prototype {
    private String attribute;
    
    public ConcretePrototype(String attribute) {
        this.attribute = attribute;
    }
    
    public Prototype clone() {
        try {
            return (Prototype) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);
        }
    }
    
    @Override
    public String toString() {
        return "ConcretePrototype [attribute=" + attribute + "]";
    }
}
```

**Use Cases**:
- When object creation is costly or complex.
- When you need to create a lot of similar objects efficiently.

**Considerations**:
- Requires that the prototype class implements cloning, which can be complex if the object has mutable fields or deep copy requirements.
- Can be challenging if prototypes need to be extended or modified frequently.

Creational patterns help manage object creation in flexible and reusable ways, allowing systems to handle new types of objects and change object creation without affecting the system's structure.

Structural patterns deal with the composition of classes and objects, focusing on how to compose objects to form larger structures. These patterns help to ensure that if one part of a system changes, the entire system doesn’t need to change. Here's a detailed look at the main structural patterns:

### 1. **Adapter Pattern**

**Purpose**: Allows objects with incompatible interfaces to work together by converting the interface of a class into another interface that a client expects.

**Structure**:
- **Target**: Defines the domain-specific interface that the client uses.
- **Client**: Collaborates with objects conforming to the `Target` interface.
- **Adaptee**: Defines an existing interface that needs adapting.
- **Adapter**: Implements the `Target` interface and translates requests to the `Adaptee`.

**Implementation Example**:
```java
// Target
interface Target {
    void request();
}

// Adaptee
class Adaptee {
    void specificRequest() {
        // Specific implementation
    }
}

// Adapter
class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    public void request() {
        adaptee.specificRequest();
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Target target = new Adapter(new Adaptee());
        target.request();
    }
}
```

**Use Cases**:
- When integrating with third-party libraries that have incompatible interfaces.
- When dealing with legacy code where you can’t change the original code but need it to work with new code.

**Considerations**:
- Can add complexity due to the additional layer.
- Provides a way to keep classes from needing to know about the detailed implementation of other classes.

### 2. **Bridge Pattern**

**Purpose**: Separates an abstraction from its implementation, allowing both to vary independently.

**Structure**:
- **Abstraction**: Defines the abstraction’s interface and maintains a reference to the `Implementor`.
- **RefinedAbstraction**: Extends the interface defined by `Abstraction`.
- **Implementor**: Defines the interface for implementation classes.
- **ConcreteImplementor**: Implements the `Implementor` interface.

**Implementation Example**:
```java
// Implementor
interface Implementor {
    void operationImpl();
}

// ConcreteImplementor
class ConcreteImplementorA implements Implementor {
    public void operationImpl() {
        // Implementation A
    }
}

class ConcreteImplementorB implements Implementor {
    public void operationImpl() {
        // Implementation B
    }
}

// Abstraction
abstract class Abstraction {
    protected Implementor implementor;

    protected Abstraction(Implementor implementor) {
        this.implementor = implementor;
    }

    public abstract void operation();
}

// RefinedAbstraction
class RefinedAbstraction extends Abstraction {
    public RefinedAbstraction(Implementor implementor) {
        super(implementor);
    }

    public void operation() {
        implementor.operationImpl();
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Implementor implementor = new ConcreteImplementorA();
        Abstraction abstraction = new RefinedAbstraction(implementor);
        abstraction.operation();
    }
}
```

**Use Cases**:
- When you need to decouple an abstraction from its implementation so that both can vary independently.
- To avoid a permanent binding between an abstraction and its implementation.

**Considerations**:
- Useful when there are multiple implementations and you want to keep them separate from the abstractions.
- Helps manage complexity by separating concerns.

### 3. **Composite Pattern**

**Purpose**: Composes objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual objects and compositions uniformly.

**Structure**:
- **Component**: Defines the interface for objects in the composition and can be a leaf or composite.
- **Leaf**: Represents leaf objects in the composition. It has no children.
- **Composite**: Defines behavior for components with children and stores child components.

**Implementation Example**:
```java
// Component
interface Component {
    void operation();
}

// Leaf
class Leaf implements Component {
    public void operation() {
        // Leaf operation
    }
}

// Composite
class Composite implements Component {
    private List<Component> children = new ArrayList<>();

    public void add(Component component) {
        children.add(component);
    }

    public void remove(Component component) {
        children.remove(component);
    }

    public void operation() {
        for (Component child : children) {
            child.operation();
        }
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Component leaf1 = new Leaf();
        Component leaf2 = new Leaf();
        Composite composite = new Composite();
        composite.add(leaf1);
        composite.add(leaf2);
        
        composite.operation();
    }
}
```

**Use Cases**:
- When you need to represent part-whole hierarchies of objects.
- When clients need to ignore the difference between compositions of objects and individual objects.

**Considerations**:
- Can make the design overly complex if not used properly.
- Useful for tree-like structures where operations are uniformly applied.

### 4. **Decorator Pattern**

**Purpose**: Adds new functionality to an object dynamically without altering its structure.

**Structure**:
- **Component**: Defines an interface for objects that can have responsibilities added dynamically.
- **ConcreteComponent**: Defines an object to which additional responsibilities can be added.
- **Decorator**: Maintains a reference to a `Component` object and defines an interface that conforms to `Component`.
- **ConcreteDecorator**: Adds responsibilities to the `Component`.

**Implementation Example**:
```java
// Component
interface Component {
    void operation();
}

// ConcreteComponent
class ConcreteComponent implements Component {
    public void operation() {
        // Base operation
    }
}

// Decorator
abstract class Decorator implements Component {
    protected Component component;

    public Decorator(Component component) {
        this.component = component;
    }

    public void operation() {
        component.operation();
    }
}

// ConcreteDecorator
class ConcreteDecoratorA extends Decorator {
    public ConcreteDecoratorA(Component component) {
        super(component);
    }

    public void operation() {
        super.operation();
        addedBehavior();
    }

    private void addedBehavior() {
        // Additional behavior
    }
}

class ConcreteDecoratorB extends Decorator {
    public ConcreteDecoratorB(Component component) {
        super(component);
    }

    public void operation() {
        super.operation();
        anotherAddedBehavior();
    }

    private void anotherAddedBehavior() {
        // Another additional behavior
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Component component = new ConcreteComponent();
        Component decoratedComponent = new ConcreteDecoratorA(new ConcreteDecoratorB(component));
        decoratedComponent.operation();
    }
}
```

**Use Cases**:
- When you need to add responsibilities to objects dynamically.
- When extending functionality of a class in a flexible and reusable way.

**Considerations**:
- Can lead to a large number of small classes.
- Helps in adding responsibilities in a controlled manner.

### 5. **Facade Pattern**

**Purpose**: Provides a unified interface to a set of interfaces in a subsystem, making it easier to use.

**Structure**:
- **Facade**: Provides a simplified interface to the subsystem.
- **Subsystem Classes**: The classes that implement the complex functionality.

**Implementation Example**:
```java
// Subsystem Classes
class Subsystem1 {
    void operation1() {
        // Implementation
    }
}

class Subsystem2 {
    void operation2() {
        // Implementation
    }
}

class Subsystem3 {
    void operation3() {
        // Implementation
    }
}

// Facade
class Facade {
    private Subsystem1 subsystem1;
    private Subsystem2 subsystem2;
    private Subsystem3 subsystem3;

    public Facade() {
        subsystem1 = new Subsystem1();
        subsystem2 = new Subsystem2();
        subsystem3 = new Subsystem3();
    }

    public void operation() {
        subsystem1.operation1();
        subsystem2.operation2();
        subsystem3.operation3();
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.operation();
    }
}
```

**Use Cases**:
- When you need to provide a simple interface to a complex subsystem.
- When you want to decouple a client from a subsystem.

**Considerations**:
- Can obscure the functionality of the subsystem if overused.
- Simplifies client interaction with the subsystem by hiding its complexity.

### 6. **Flyweight Pattern**

**Purpose**: Reduces the cost of creating and managing a large number of similar objects by sharing as much data as possible.

**Structure**:
- **Flyweight**: Defines an interface for the flyweight objects and includes methods to manage intrinsic state.
- **ConcreteFlyweight**: Implements the `Flyweight` interface and stores intrinsic state.
- **FlyweightFactory**: Creates and manages flyweight objects, ensuring that they are shared correctly.
- **Client**: Uses flyweights and maintains references to them.

**Implementation Example**:
```java
// Flyweight
interface Flyweight {
    void operation();
}

// ConcreteFlyweight
class ConcreteFlyweight implements Flyweight {
    private String intrinsicState;

    public ConcreteFlyweight(String intrinsicState) {
        this.intrinsicState = intrinsicState;
    }

    public void operation() {
        // Use intrinsic state
    }
}

// FlyweightFactory
class FlyweightFactory {
    private Map<String, Flyweight> flyweights = new HashMap<>();

    public Flyweight getFlyweight(String key) {
        if (!flyweights.containsKey(key)) {


            flyweights.put(key, new ConcreteFlyweight(key));
        }
        return flyweights.get(key);
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        FlyweightFactory factory = new FlyweightFactory();
        Flyweight flyweight1 = factory.getFlyweight("A");
        Flyweight flyweight2 = factory.getFlyweight("B");
        Flyweight flyweight3 = factory.getFlyweight("A"); // Shared with flyweight1
        
        flyweight1.operation();
        flyweight2.operation();
        flyweight3.operation();
    }
}
```

**Use Cases**:
- When dealing with a large number of objects that have shared state.
- To optimize memory usage by sharing common parts of objects.

**Considerations**:
- Can add complexity due to the need to manage shared state.
- Works well for applications with many similar objects that share common state.

### 7. **Proxy Pattern**

**Purpose**: Provides a surrogate or placeholder for another object to control access to it. This can be used to add functionality such as lazy initialization, access control, logging, etc.

**Structure**:
- **Subject**: Defines the interface that the proxy and real subject share.
- **RealSubject**: The actual object that the proxy represents.
- **Proxy**: Controls access to the `RealSubject` and may add additional behavior.

**Implementation Example**:
```java
// Subject
interface Subject {
    void request();
}

// RealSubject
class RealSubject implements Subject {
    public void request() {
        // Real implementation
    }
}

// Proxy
class Proxy implements Subject {
    private RealSubject realSubject;

    public void request() {
        if (realSubject == null) {
            realSubject = new RealSubject();
        }
        realSubject.request();
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Subject proxy = new Proxy();
        proxy.request();
    }
}
```

**Use Cases**:
- When you need to control access to an object.
- To add additional behavior such as logging, caching, or access control.

**Considerations**:
- Can add an additional layer of complexity.
- Provides a way to control access and extend functionality without modifying the original object.

Structural patterns help ensure that complex systems are composed in a way that maintains flexibility and reduces dependency, making it easier to manage and extend the system as it evolves.


Behavioral patterns focus on how objects interact and communicate with each other, and how responsibilities are distributed among objects. They help to define clear, flexible communication between objects and manage complex control flows. Here’s a detailed look at the main behavioral patterns:

### 1. **Chain of Responsibility Pattern**

**Purpose**: Allows an object to pass a request along a chain of handlers, where each handler can either process the request or pass it to the next handler in the chain.

**Structure**:
- **Handler**: Defines an interface for handling requests and an optional link to the next handler.
- **ConcreteHandler**: Implements the handling logic and either processes the request or forwards it to the next handler.
- **Client**: Initiates the request.

**Implementation Example**:
```java
// Handler
abstract class Handler {
    private Handler next;

    public void setNext(Handler next) {
        this.next = next;
    }

    public abstract void handleRequest(int request);
}

// ConcreteHandlerA
class ConcreteHandlerA extends Handler {
    public void handleRequest(int request) {
        if (request < 10) {
            System.out.println("Handler A processed request " + request);
        } else if (next != null) {
            next.handleRequest(request);
        }
    }
}

// ConcreteHandlerB
class ConcreteHandlerB extends Handler {
    public void handleRequest(int request) {
        if (request >= 10 && request < 20) {
            System.out.println("Handler B processed request " + request);
        } else if (next != null) {
            next.handleRequest(request);
        }
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Handler handlerA = new ConcreteHandlerA();
        Handler handlerB = new ConcreteHandlerB();
        handlerA.setNext(handlerB);

        handlerA.handleRequest(5); // Handled by Handler A
        handlerA.handleRequest(15); // Handled by Handler B
    }
}
```

**Use Cases**:
- When you have multiple objects that can handle a request but you want to decouple the sender from the receiver.
- When you need to process a request with a series of handlers that can be dynamically changed.

**Considerations**:
- Can lead to a long chain if not properly managed.
- The order of handlers is significant and must be correctly configured.

### 2. **Command Pattern**

**Purpose**: Encapsulates a request as an object, thereby allowing parameterization of clients with queues, requests, and operations. It also supports undoable operations.

**Structure**:
- **Command**: Declares an interface for executing a particular operation.
- **ConcreteCommand**: Implements the `Command` interface and defines the binding between a receiver and an action.
- **Receiver**: Knows how to perform the operations to satisfy a request.
- **Invoker**: Asks the command to execute the request.
- **Client**: Creates a command object and sets its receiver.

**Implementation Example**:
```java
// Command
interface Command {
    void execute();
}

// Receiver
class Light {
    void turnOn() {
        System.out.println("Light is ON");
    }

    void turnOff() {
        System.out.println("Light is OFF");
    }
}

// ConcreteCommand
class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOn();
    }
}

class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOff();
    }
}

// Invoker
class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Light light = new Light();
        Command lightOn = new LightOnCommand(light);
        Command lightOff = new LightOffCommand(light);

        RemoteControl remote = new RemoteControl();
        remote.setCommand(lightOn);
        remote.pressButton(); // Light is ON
        remote.setCommand(lightOff);
        remote.pressButton(); // Light is OFF
    }
}
```

**Use Cases**:
- When you need to parameterize objects by an action to perform.
- When you need to support undo/redo operations or queue requests.

**Considerations**:
- Can lead to a proliferation of command classes if not managed properly.
- Encapsulates requests but can increase the number of objects in the system.

### 3. **Interpreter Pattern**

**Purpose**: Defines a grammatical representation for a language and provides an interpreter to interpret sentences of the language.

**Structure**:
- **AbstractExpression**: Declares an abstract `interpret` method.
- **TerminalExpression**: Implements the `interpret` method for terminal symbols in the grammar.
- **NonTerminalExpression**: Implements the `interpret` method for non-terminal symbols in the grammar.
- **Context**: Contains information that is global to the interpreter.

**Implementation Example**:
```java
// Expression
interface Expression {
    boolean interpret(String context);
}

// TerminalExpression
class TerminalExpression implements Expression {
    private String data;

    public TerminalExpression(String data) {
        this.data = data;
    }

    public boolean interpret(String context) {
        return context.contains(data);
    }
}

// NonTerminalExpression
class AndExpression implements Expression {
    private Expression expr1;
    private Expression expr2;

    public AndExpression(Expression expr1, Expression expr2) {
        this.expr1 = expr1;
        this.expr2 = expr2;
    }

    public boolean interpret(String context) {
        return expr1.interpret(context) && expr2.interpret(context);
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Expression isMale = new TerminalExpression("Male");
        Expression isMarried = new TerminalExpression("Married");
        Expression isMarriedMale = new AndExpression(isMale, isMarried);

        System.out.println("John is married male? " + isMarriedMale.interpret("John Male Married"));
        System.out.println("Anna is married male? " + isMarriedMale.interpret("Anna Female Single"));
    }
}
```

**Use Cases**:
- When you need to interpret sentences in a language or evaluate expressions.
- When the grammar of the language can be defined and the interpretations can be implemented.

**Considerations**:
- Can become complex with a large grammar.
- Useful for designing and implementing domain-specific languages.

### 4. **Iterator Pattern**

**Purpose**: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

**Structure**:
- **Iterator**: Defines an interface for accessing elements in the collection.
- **ConcreteIterator**: Implements the iterator interface and keeps track of the current position.
- **Aggregate**: Defines an interface for creating an iterator.
- **ConcreteAggregate**: Implements the aggregate interface and returns an instance of `ConcreteIterator`.

**Implementation Example**:
```java
// Iterator
interface Iterator {
    boolean hasNext();
    Object next();
}

// Aggregate
interface Aggregate {
    Iterator createIterator();
}

// ConcreteIterator
class ConcreteIterator implements Iterator {
    private ConcreteAggregate aggregate;
    private int current = 0;

    public ConcreteIterator(ConcreteAggregate aggregate) {
        this.aggregate = aggregate;
    }

    public boolean hasNext() {
        return current < aggregate.size();
    }

    public Object next() {
        return aggregate.get(current++);
    }
}

// ConcreteAggregate
class ConcreteAggregate implements Aggregate {
    private List<Object> items = new ArrayList<>();

    public void add(Object item) {
        items.add(item);
    }

    public Object get(int index) {
        return items.get(index);
    }

    public int size() {
        return items.size();
    }

    public Iterator createIterator() {
        return new ConcreteIterator(this);
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        ConcreteAggregate aggregate = new ConcreteAggregate();
        aggregate.add("Item 1");
        aggregate.add("Item 2");
        aggregate.add("Item 3");

        Iterator iterator = aggregate.createIterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

**Use Cases**:
- When you need to provide a standard way to traverse a collection.
- When you want to access elements in a collection without exposing its internal structure.

**Considerations**:
- Simplifies access to elements but can lead to multiple iterators if not managed carefully.
- Useful for collections where traversal needs to be decoupled from the actual structure.

### 5. **Mediator Pattern**

**Purpose**: Defines an object that encapsulates how a set of objects interact, promoting loose coupling by keeping objects from referring to each other explicitly.

**Structure**:
- **Mediator**: Defines an interface for communication between components.
- **ConcreteMediator**: Implements the `Mediator` interface and coordinates communication between components.
- **Colleague**: Defines an interface for components that communicate through the mediator.
- **ConcreteColleague**: Implements the `Colleague` interface and communicates with other colleagues through the mediator.

**Implementation Example**:
```java
// Mediator
interface Mediator {
    void notify(Object sender, String event);
}

// ConcreteMediator
class ConcreteMediator implements Mediator {
    private Colleague1 colleague1;
    private Colleague2 colleague2;

    public void setColleague1(Colleague1 colleague1) {
        this.colleague1 = colleague1;
    }

    public void setColleague2(Colleague2 colleague2) {
        this.colleague2 = colleague2;
    }



    public void notify(Object sender, String event) {
        if (sender == colleague1) {
            colleague2.handleEvent(event);
        } else if (sender == colleague2) {
            colleague1.handleEvent(event);
        }
    }
}

// Colleague1
class Colleague1 {
    private Mediator mediator;

    public Colleague1(Mediator mediator) {
        this.mediator = mediator;
    }

    public void send(String event) {
        mediator.notify(this, event);
    }

    public void handleEvent(String event) {
        System.out.println("Colleague1 received event: " + event);
    }
}

// Colleague2
class Colleague2 {
    private Mediator mediator;

    public Colleague2(Mediator mediator) {
        this.mediator = mediator;
    }

    public void send(String event) {
        mediator.notify(this, event);
    }

    public void handleEvent(String event) {
        System.out.println("Colleague2 received event: " + event);
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        ConcreteMediator mediator = new ConcreteMediator();

        Colleague1 colleague1 = new Colleague1(mediator);
        Colleague2 colleague2 = new Colleague2(mediator);

        mediator.setColleague1(colleague1);
        mediator.setColleague2(colleague2);

        colleague1.send("Hello");
        colleague2.send("Hi");
    }
}
```

**Use Cases**:
- When you need to centralize communication between objects to avoid tight coupling.
- When you want to manage complex communication flows between multiple objects.

**Considerations**:
- Can become complex if not carefully managed.
- Useful for managing complex interactions by centralizing control.

### 6. **Memento Pattern**

**Purpose**: Captures and externalizes an object's internal state without violating encapsulation, so that the object can be restored to this state later.

**Structure**:
- **Memento**: Stores the internal state of the `Originator`.
- **Originator**: Creates a memento containing a snapshot of its current state and can restore its state from a memento.
- **Caretaker**: Maintains the memento but does not examine or modify its contents.

**Implementation Example**:
```java
// Memento
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

// Originator
class Originator {
    private String state;

    public void setState(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }

    public Memento saveStateToMemento() {
        return new Memento(state);
    }

    public void getStateFromMemento(Memento memento) {
        state = memento.getState();
    }
}

// Caretaker
class Caretaker {
    private Memento memento;

    public void saveState(Originator originator) {
        memento = originator.saveStateToMemento();
    }

    public void restoreState(Originator originator) {
        originator.getStateFromMemento(memento);
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        originator.setState("State 1");
        caretaker.saveState(originator);

        originator.setState("State 2");
        System.out.println("Current State: " + originator.getState());

        caretaker.restoreState(originator);
        System.out.println("Restored State: " + originator.getState());
    }
}
```

**Use Cases**:
- When you need to save and restore the state of an object.
- When you want to support undo functionality.

**Considerations**:
- Can lead to increased memory usage due to storing state snapshots.
- Useful for managing object state and supporting undo/redo features.

### 7. **Observer Pattern**

**Purpose**: Defines a dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

**Structure**:
- **Subject**: Maintains a list of observers and notifies them of any state changes.
- **Observer**: Defines an update interface for objects that need to be notified of changes.
- **ConcreteSubject**: Implements the subject and stores the state.
- **ConcreteObserver**: Implements the observer and reacts to state changes in the subject.

**Implementation Example**:
```java
// Observer
interface Observer {
    void update(String message);
}

// Subject
interface Subject {
    void attach(Observer observer);
    void detach(Observer observer);
    void notifyObservers();
}

// ConcreteSubject
class ConcreteSubject implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String state;

    public void attach(Observer observer) {
        observers.add(observer);
    }

    public void detach(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(state);
        }
    }

    public void setState(String state) {
        this.state = state;
        notifyObservers();
    }
}

// ConcreteObserver
class ConcreteObserver implements Observer {
    private String name;

    public ConcreteObserver(String name) {
        this.name = name;
    }

    public void update(String message) {
        System.out.println(name + " received message: " + message);
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        ConcreteSubject subject = new ConcreteSubject();
        ConcreteObserver observer1 = new ConcreteObserver("Observer 1");
        ConcreteObserver observer2 = new ConcreteObserver("Observer 2");

        subject.attach(observer1);
        subject.attach(observer2);

        subject.setState("New State");
    }
}
```

**Use Cases**:
- When you need to notify multiple objects about changes in another object’s state.
- When you want to implement distributed event handling systems.

**Considerations**:
- Can lead to a large number of updates if not managed carefully.
- Useful for implementing event-driven systems.

### 8. **State Pattern**

**Purpose**: Allows an object to change its behavior when its internal state changes, appearing to change its class.

**Structure**:
- **State**: Defines an interface for encapsulating the behavior associated with a particular state.
- **ConcreteState**: Implements the behavior associated with a state.
- **Context**: Maintains an instance of a `ConcreteState` subclass that represents the current state.

**Implementation Example**:
```java
// State
interface State {
    void handle(Context context);
}

// ConcreteStateA
class ConcreteStateA implements State {
    public void handle(Context context) {
        System.out.println("Handling state A");
        context.setState(new ConcreteStateB());
    }
}

// ConcreteStateB
class ConcreteStateB implements State {
    public void handle(Context context) {
        System.out.println("Handling state B");
        context.setState(new ConcreteStateA());
    }
}

// Context
class Context {
    private State state;

    public Context() {
        state = new ConcreteStateA();
    }

    public void setState(State state) {
        this.state = state;
    }

    public void request() {
        state.handle(this);
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Context context = new Context();
        context.request(); // Handling state A
        context.request(); // Handling state B
        context.request(); // Handling state A
    }
}
```

**Use Cases**:
- When an object’s behavior depends on its state and it must change its behavior at runtime.
- When you want to encapsulate state-specific behavior in different classes.

**Considerations**:
- Useful for managing state-dependent behavior in a clean, extensible way.
- Can lead to many state classes if not managed properly.

### 9. **Strategy Pattern**

**Purpose**: Defines a family of algorithms, encapsulates each algorithm, and makes them interchangeable. The algorithm can vary independently from the clients that use it.

**Structure**:
- **Strategy**: Defines an interface for a family of algorithms.
- **ConcreteStrategy**: Implements the algorithm using the `Strategy` interface.
- **Context**: Maintains a reference to a `Strategy` object and can delegate work to it.

**Implementation Example**:
```java
// Strategy
interface Strategy {
    void execute();
}

// ConcreteStrategyA
class ConcreteStrategyA implements Strategy {
    public void execute() {
        System.out.println("Strategy A");
    }
}

// ConcreteStrategyB
class ConcreteStrategyB implements Strategy {
    public void execute() {
        System.out.println("Strategy B");
    }
}

// Context
class Context {
    private Strategy strategy;

    public void setStrategy(Strategy strategy) {
        this.strategy = strategy;
    }

    public void executeStrategy() {
        strategy.execute();
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Context context = new Context();
        context.setStrategy(new ConcreteStrategyA());
        context.executeStrategy(); // Strategy A

        context.setStrategy(new ConcreteStrategyB());
        context.executeStrategy(); // Strategy B
    }
}
```

**Use Cases**:
- When you have multiple algorithms for a specific task and want to select an algorithm at runtime.
- When you need to define a family of algorithms and encapsulate them.

**Considerations**:
- Useful for encapsulating and varying algorithms.
- Can lead to many strategy classes if not managed carefully.

### 10. **Template Method Pattern**

**Purpose**: Defines the skeleton of an algorithm in a base class, allowing subclasses to provide specific implementations for certain steps of the algorithm.

**Structure**:
- **AbstractClass**:

 Defines the template method and some steps of the algorithm.
- **ConcreteClass**: Implements the steps defined in the abstract class.

**Implementation Example**:
```java
// AbstractClass
abstract class AbstractClass {
    public void templateMethod() {
        stepOne();
        stepTwo();
        stepThree();
    }

    protected abstract void stepOne();
    protected abstract void stepTwo();
    private void stepThree() {
        System.out.println("Step Three");
    }
}

// ConcreteClass
class ConcreteClass extends AbstractClass {
    protected void stepOne() {
        System.out.println("Step One");
    }

    protected void stepTwo() {
        System.out.println("Step Two");
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        AbstractClass concrete = new ConcreteClass();
        concrete.templateMethod();
    }
}
```

**Use Cases**:
- When you have a fixed sequence of steps and need to allow variations in some of the steps.
- When you want to define the structure of an algorithm and allow subclasses to redefine specific parts.

**Considerations**:
- Useful for defining and enforcing a sequence of operations.
- Subclasses need to provide specific implementations for the steps.

### 11. **Visitor Pattern**

**Purpose**: Defines a new operation to a set of objects without changing the classes of the elements on which it operates. 

**Structure**:
- **Visitor**: Defines an interface for operations to be performed on elements.
- **ConcreteVisitor**: Implements the visitor interface and defines specific operations.
- **Element**: Defines an accept method that takes a visitor.
- **ConcreteElement**: Implements the accept method to allow the visitor to visit.

**Implementation Example**:
```java
// Visitor
interface Visitor {
    void visit(ConcreteElementA element);
    void visit(ConcreteElementB element);
}

// ConcreteVisitor
class ConcreteVisitor implements Visitor {
    public void visit(ConcreteElementA element) {
        System.out.println("Visiting Element A");
    }

    public void visit(ConcreteElementB element) {
        System.out.println("Visiting Element B");
    }
}

// Element
interface Element {
    void accept(Visitor visitor);
}

// ConcreteElementA
class ConcreteElementA implements Element {
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

// ConcreteElementB
class ConcreteElementB implements Element {
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        Element elementA = new ConcreteElementA();
        Element elementB = new ConcreteElementB();

        Visitor visitor = new ConcreteVisitor();

        elementA.accept(visitor); // Visiting Element A
        elementB.accept(visitor); // Visiting Element B
    }
}
```

**Use Cases**:
- When you need to perform operations on a set of objects with different types.
- When you want to add new operations without modifying existing classes.

**Considerations**:
- Useful for adding operations to objects without modifying their classes.
- Can lead to a proliferation of visitor classes if not managed carefully.

Behavioral patterns facilitate communication and control between objects and help manage complex behaviors, making it easier to design and implement systems with varied and dynamic interactions.
