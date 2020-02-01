Object Construction

1. never use -er names
2. make one primary constructor, many secondary constructors
    // A large number of methods leads to a lack of focus and a violation of the Single Responsibility Principle
    // A large number of constructors translates to flexibility
3. Keep constructors code-free
    // don't touch the arguments
    // Instead, it must wrap them, if necessary. or encapsulate them in a raw form.

Object Education

0. Object needs to be small
1. Encapsulate as little as possible
    // Recommended to encapsulate FOUR OBJECTS or LESS. If you need to encapsulate more, refactor it.
    // encapsulated objects all together also known as STATE or IDENTITY of the object. Lombok helps in this case
2. Encapsulate something at the very least
    // another extreme is an object that encapsulates nothing at all.
    // a class without properties is very similar to a static method, which is a terrible thing in oop. It has no state, no identity, just behaviour.
    
    // pure oop is without static methods and with strict separation of instantiation and execution.
    
    // instantiation should be isolated from execution:
        // operator NEW is allowed only inside constructors.
3. Always use interfaces
    // Cash4 and DefaultCash is an example.
    // Make sure that ALL methods in your class implement some interfaces
    // A properly designed class must not have any public methods that don't implement at least one interface
    // A class is there only because someone needs his service. This service must be documented somewhere - it's contract, an interface; - 
    // LOOSE COUPLING Each implementation of an interface must be easily replaceable
4. Choose METHOD NAMES carefully
    // builders are NOUNS, manipulators are VERBS.
    // Builders build, manipulators manipulate.
        // BUILDERS - method that build something and they return a new object
        // BUILDERS - always returns something, never return void
        // BUILDER names - always nouns
        
        // MANIPULATOR - method that makes modifications to the real world entity being abstracted by an object
        // MANIPULATOR - it always returns void
        // MANIPULATOR - names are always verbs
        
    // boolean results - use an adjective: if (name.empty()) {...}
5. Don't use public constants
    // Introduction of COUPLING
    // Loss of COHESION
6. Be immutable
    // mutable objects have no right to exist
    // IDENTITY MUTABILITY problem when using it
    // FAILURE ATOMICITY - we either have a complete and solid object, or a failure - nothing in between
    // Benefit - Lack of TEMPORAL COUPLING
    // Benefit - Side effect-free
    // No NULL references
    // Thread safety
    // Benefit - Smaller and simpler objects
7. Write tests instead of documentation
8. Don't mock; use fakes
    // nested fake class is part of the interface and is shipped together with the interface. 
    // It is a valuable part of Interface, because it helps everybody use Interface in unit tests
    // make sure your fake classes are serving your tests properly
    // Fake classes make tests shorter, which seriously improves their maintainability
    // Mocking on the other hand makes tests very verbose and very dificult to understand and refactor
    // Mocking turns assumptions into facts. and makes them hard to maintain.
    // Maiking our tests aware of internal implementation details of an object makes the test fragile and unmaintainable. And root of this problem is mocking
9. Keep interfaces short; use smarts
    // There can be many methods in this smart class that do something very obvious and very common.
        // This smart class doesn't know how the Exchange is implemented and how the rate is calculated, 
        // but it applies a certain functionality on top of it   
        // float rate = new Exchange.Smart(new NYSE()).toUsd("EUR");
    // extract shared functionality and avoid code duplication by making interfaces short and shipping them with "smart" classes together with them.
    // Smart classes are very close to composable decorators
    // Nested class Exchange.Fast is at the same time a decorator and a "smart" class.
        // First it overrides method rate, making it more powerful. It will skip the roundtrip to the exchange if both currencies are the same
        // Second it adds a nes method toUsd(), which makes conversion to USD more convenient

Object Employment

1. Expose fewer than five public methods
    // all classes under 250 lines of code
    // Use number of public methods as primary metric of class size.
    // constructors and private methods not included in this calculation
2. Don't use static methods
2.1. Object vs computer/procedural thinking
    // Number x = new Max(5, 9);        vs  int x = Math.max(5, 9);
2.2 Declarative vs imperative programming - use Declarative
2.3 Utility classes - don't use class with static methods
2.4 Singleton Pattern - don't use it
2.5 Functional programming - FP is good, but OOP is better if done right
2.6 Composable decorators
    // decorators pattern when used in multi-layer structures
    // Sometimes, but not necessarily they expose same interface as their encapsulated objects
3. Never accept NULL arguments
    // let NullPointerException pass through to the caller, and it will understand it's mistake. Be ignorant
4. Be loyal and immutable, or constant
    // Intuitively we expect that immutable objects act as a constant. But it is wrong assumption
    // method content() may return different values on every subsequent call, even when the object is immutable (url of the page for example, with different content)
5. Never use getters and setters
    // don't treat object as data structure
    // it is all about prefixes GET / SET. They send clear signal that object is not really an object
    // instead of cash.getDollars() use cash.dollars()
6. Don't use new outside of secondary constructors