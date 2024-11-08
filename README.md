**SOLID PRINCIPLES in Angular**

In software development, SOLID principles are a set of guidelines that help developers design scalable and maintainable systems. These principles can be seamlessly applied in Angular development to create flexible, extensible, and manageable applications.

**Single Responsibility Principle (SRP)**

The Single Responsibility Principle (SRP) is a fundamental principle of software engineering which states that a class or module should have only one reason to change. In other words, it should have only one responsibility. Violating this principle can lead to code that is difficult to maintain and understand.

Violation of SRP

Consider a component that displays a list of products and allows the user to filter them by category.

![image](https://github.com/user-attachments/assets/61eb6c82-66f4-4891-be59-09171b91cc80)

This component violates the SRP because it has two responsibilities: displaying the list of products and filtering them by category. This violates the “one reason to change” principle, as changes to the filtering behavior may affect the component’s rendering logic and vice versa.

To fix this violation, we can refactor the component into two separate components, each with its own responsibility.

**Fixing the Violation**

First, we’ll create a new component that displays the list of products:

![image](https://github.com/user-attachments/assets/2d9d7542-5eaa-4e3e-ace4-d2b475096163)

This component violates the SRP because it has two responsibilities: displaying the list of products and filtering them by category. This violates the “one reason to change” principle, as changes to the filtering behavior may affect the component’s rendering logic and vice versa.

To fix this violation, we can refactor the component into two separate components, each with its own responsibility.

**Fixing the Violation**

First, we’ll create a new component that displays the list of products:

![image](https://github.com/user-attachments/assets/9b625faf-497a-491c-b1bd-aff490853f0b)

This component is now responsible only for displaying the list of products. We’ve removed the category filtering logic to a new component.

Next, we’ll create a new component that handles the category filtering:

![image](https://github.com/user-attachments/assets/f118645e-107d-4903-8d2b-4aa2b06a2308)

This component is now responsible only for handling the category filtering. It updates the selected category and calls the getProductsByCategory() method of the ProductService to update the list of products.

Finally, we’ll update the app.component.html file to include both components:

![image](https://github.com/user-attachments/assets/df819fe1-6be9-4e3d-b229-e72c8ef9e9c1)
![image](https://github.com/user-attachments/assets/6469eb17-9a8c-4f70-9662-a946d41ef127)

The app-product-filter component emits a categorySelected event when a new category is chosen, which is handled by the app-product-list component calling its filterByCategory() method with the selected category. This refactoring separates responsibilities into two components, adhering to the Single Responsibility Principle (SRP) and making the code more modular and maintainable. Additionally, it follows the Separation of Concerns principle by dividing the system into distinct modules for different concerns. By maintaining clear responsibilities for each module, we reduce coupling and ensure that changes in one module do not negatively impact others, promoting maintainable, extensible, and reusable code.

**Open/Closed Principle (OCP)**

The Open/Closed Principle (OCP) states that software entities—such as classes, modules, and functions—should be open for extension but closed for modification. This means that new functionality can be added without altering existing code, which helps reduce code coupling, enhances scalability, and improves code reusability.

OCP can be implemented using inheritance and interfaces. By creating a base component or service that encapsulates common functionality, you can then develop child components or services that inherit from this base. Additionally, interfaces can define a set of methods or properties that must be implemented by any implementing component or service, allowing for flexibility in extending functionality while maintaining a stable codebase.

**Violating the Open/Closed Principle**

Consider, we have a component that displays a list of users. The users are retrieved and displayed in a table. The table has three columns: name, email, and phone number. We have created a UserListComponent to display this list. Initially, the component looks like this:

![image](https://github.com/user-attachments/assets/a21764e1-20a1-4347-84dc-0476f03c9bfe)

In the template file user-list.component.html, we have the following code:

![image](https://github.com/user-attachments/assets/3238cc19-eec7-4152-bd98-8681a7e17818)

Everything works fine, and we can see the list of users displayed in a table with three columns.

Now, suppose we want to add a new feature to the application, which is to allow users to view additional details for each user. We want to display the user’s address, city, and state. We can simply modify the UserListComponent to add these columns to the table. Here’s how we can do it:

![image](https://github.com/user-attachments/assets/84429d99-92fd-4e2a-95f2-15d4324e5169)

![image](https://github.com/user-attachments/assets/e7aa9cef-3b1e-47a9-ab76-7f8ee2a03bfa)

This code violates the OCP because we have modified the existing component to add new functionality. If we want to add more features to the application, we will have to keep modifying the UserListComponent, which makes it difficult to maintain and scale.

**Fixing the violation**

To fix the violation of the OCP, we need to separate the concerns of displaying the list of users and displaying the details of each user. We can create a new component called UserDetailComponent to display the additional details for each user. Here’s how we can do it:

![image](https://github.com/user-attachments/assets/782114b2-32e5-42c0-a172-84731bf1f6b2)

In the UserListComponent, we can now use the UserDetailComponent to display the additional details for each user.

![image](https://github.com/user-attachments/assets/d88540e2-0e0d-4481-a869-ddc389a8f893)

![image](https://github.com/user-attachments/assets/0859110d-57b9-4fcc-98f4-5a7a6a06af59)

In this new implementation, the UserListComponent is responsible for displaying the list of users, while the UserDetailComponent is responsible for displaying the details of each user. The UserListComponent doesn’t need to be modified to add new functionality because the UserDetailComponent can be easily extended to display additional details.

**Liskov Substitution Principle (LSP)**

The Liskov Substitution Principle (LSP) is a fundamental concept in software engineering that is essential for designing and implementing maintainable and extensible systems. LSP states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. Violating the LSP can lead to unexpected behavior and bugs.

**Violating LSP**

![image](https://github.com/user-attachments/assets/88c88940-2eeb-4c48-8a0f-829b62023a0a)

In this example, Ostrich is a subclass of Animal that overrides the move() method to reflect the fact that ostriches cannot fly. However, when we pass an instance of Ostrich to the moveAnimal() function, we get unexpected behavior because the move() method of Ostrich does not behave the same way as the move() method of Animal. This violates the LSP because Ostrich is not a true substitute for Animal.

To fix the violation, we can modify the Ostrich class to behave more like Animal:

![image](https://github.com/user-attachments/assets/9c06d1eb-6632-4066-bb5d-38abf5a97fd5)

In this updated implementation, a fly() method has been added to the Ostrich class that throws an error, as ostriches cannot fly. This ensures that Ostrich adheres to the Liskov Substitution Principle (LSP), allowing it to behave like the Animal class and be substituted for it without affecting the correctness of the program.

The Liskov Substitution Principle is crucial in software engineering for designing maintainable and extensible systems. Violating the LSP can result in unexpected behavior and bugs. These issues can be addressed by ensuring that subclasses conform to the expected behavior of their superclasses.v

**Interface Segregation Principle (ISP)**

The Interface Segregation Principle (ISP) is a software development principle stating that a software component should not be forced to depend on interfaces it does not use. Essentially, clients should only be required to depend on methods that are relevant to them. This principle reduces coupling between components and leads to more modular, flexible, and maintainable code.

ISP violations occur when a component depends on a service that exposes more methods than necessary. This unnecessary coupling complicates modifications, as changes in one component may inadvertently affect others. Additionally, it can lead to performance issues, as the component may need to load and manage unused methods from the service.

Example: Consider a scenario where a component retrieves data from a service that provides multiple methods, including some that are irrelevant to the component's functionality. Instead of depending on this broader interface, the component should interact only with the methods it actually requires, promoting a cleaner and more efficient design.

By adhering to the Interface Segregation Principle, you can create smaller, focused interfaces that help maintain clear boundaries between components, enhancing overall code maintainability and flexibility.

To demonstrate this, let’s consider an example where a component needs to retrieve data from a service. The service provides several methods, including ones that are not required by the component.

![image](https://github.com/user-attachments/assets/63768870-8818-4ff6-8236-359fecd19c6c)

The component only needs to retrieve items from the service, so it should only depend on the getItems method. However, if the component is written as follows:

![image](https://github.com/user-attachments/assets/cf4bdceb-a8a6-4d48-a06b-8f8c064552a4)

The component is depending on the DataService interface, which includes methods that are not used by the component. This can lead to unnecessary coupling and performance issues.

To fix this, we can create a new interface that only includes the getItems method and have the service implement this interface. The component can then depend on this new interface instead of the original DataService interface.

![image](https://github.com/user-attachments/assets/0fd39579-69be-4ba0-a5cf-f22cf589d819)

Now, the component only depends on the ItemsService interface, which includes only the getItems method. This helps to reduce coupling and improves performance.

The Interface Segregation Principle (ISP) is an important software development principle that helps to reduce coupling between components and makes code more modular, flexible, and maintainable. Violating ISP can lead to unnecessary coupling and performance issues. To fix this, we can create new interfaces that include only the methods needed by a component and have services implement these interfaces instead of larger interfaces. This can help to improve code quality, reduce coupling, and improve performance.

**Dependency Inversion Principle (DIP)**

Dependency Inversion Principle (DIP) is an important principle of object-oriented design. It suggests that high-level modules should not depend on low-level modules, but both should depend on abstractions. The abstractions should not depend on the details, but the details should depend on the abstractions. This principle promotes loose coupling and high cohesion in software systems.

**Violation of DIP**

Let’s consider an example where we have a CustomerService that depends on a CustomerRepository to fetch customer data. The implementation of CustomerService looks like this:

![image](https://github.com/user-attachments/assets/14725dd5-ff50-4171-aa67-3ea204f2ba1e)

The implementation of CustomerRepository looks like this:

![image](https://github.com/user-attachments/assets/a87c5358-68b9-4f18-a00a-1d0b3a80db4a)

The CustomerService class depends on the CustomerRepository class, which violates the Dependency Inversion Principle. The CustomerService class is a high-level module, and the CustomerRepository class is a low-level module. The CustomerService class should not depend on the CustomerRepository class directly.

**Fixing Violation of DIP**

To fix the violation of the Dependency Inversion Principle, we need to introduce an abstraction between the CustomerService class and the CustomerRepository class. We can introduce an interface ICustomerRepository to define the contract that the CustomerRepository class should implement. The implementation of CustomerService looks like this:

![image](https://github.com/user-attachments/assets/45540805-c93b-4a9e-a3c0-cfbcc703128d)

The implementation of ICustomerRepository looks like this:

![image](https://github.com/user-attachments/assets/53d11db2-c6fd-4514-ae6b-fb42cc928745)

The implementation of CustomerRepository now implements the ICustomerRepository interface.

![image](https://github.com/user-attachments/assets/32a64a0e-9d04-4d72-a4e3-8a8842a58543)

Now, the CustomerService class depends on the ICustomerRepository interface, and the CustomerRepository class implements the ICustomerRepository interface. This way, the CustomerService class is decoupled from the CustomerRepository class, and both depend on the abstraction.

Summary

By applying these SOLID principles in Angular development (or any software development), you can create applications that are easier to maintain, extend, and manage. Each principle promotes modular design, reducing complexity and enhancing code quality.

https://sheldonrcohen.medium.com/applying-solid-principles-to-angular-with-examples-fec460ffa541


Hashnode link:
https://hashnode.com/post/cm2ijgk10000f09l31lkg7skt














