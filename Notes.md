# 🔹 SOLID Principles
- Single Responsibility: One class should do only one thing at a time.
- Open/Closed: Classes should be open for extension but closed for modification.
- Liskov Substitution: Child class should be able to implement all the methods of the parent class seamlessly.
- Interface Segregation: Don’t force classes to implement unused methods; prefer smaller, specific interfaces.
- Dependency Inversion: Depend on abstractions, not concrete classes.
SOLID Principles
* Single Responsibility Principle
- One class should do only one thing at a time
ex,
The MessageParser handles cleaning and preprocessing user input.
The ResponseGenerator calls the LLM and creates a reply.
The ConversationLogger saves chat history.
 
* Open Closed Principle
- Classes should be open for extension but closed for modification.
Ex,
The chatbot can support new features like weather info or appointment booking by adding new modules, without changing the existing LLM response generation code.
 
* Liskov Substitution Principle
- Child class should be able to implement all the methods of the parent class seamlessly.
Ex, BaseEmployeeClass{} , InternalEmployee{}, ExternalEmployee{}
A BasicChatbot can be replaced with an AdvancedHealthcareChatbot in the system.
Both follow the same chatbot interface, so the system still works correctly.
 
* Interface Segregation Principle
Any Code should not be forced to use Methods which are not needed.
ex, Separate interfaces:
ITextChat()
IVoiceChat()
IAvatarInteraction()
IAppointmentScheduler()
A text-only chatbot doesn’t need to implement voice or avatar features.
 
* Dependency Inversion Principle
Higher level module should not depend on lower level module directly but should talk through abstraction like interface.
EX,
The chatbot logic doesn’t directly depend on OpenAI API or Azure AI API.
Instead, it depends on an abstract ILLMProvider.
Different LLM providers can be swapped without changing chatbot logic.
------------------------------------------------I
 
Interface Segregation Example
Bad ❌: One IWorker with Work() and Eat().
Good ✅: Split into IWorkable, IEatable.
 
🔹 Dependency Injection (DI) in .NET Core
Definition: Injecting dependencies (services, repositories) instead of creating them inside classes.
- A programming technique that makes a class independent of its own dependencies.
- Instead of a class creating its own dependencies, they are provided from the outside.
- A methodology where in rather than caller creating the instance its injected by someone else or some other mechanism
- DI is a technique where an object’s dependencies are provided from the outside, instead of the object creating them internally.
1. Constructor Injection
2. Method Injection
3. Property Injection
 
- Transient – new instance every time (Lightweight, stateless services)
- services.AddTransient<IEngine, PetrolEngine>();
 
- Scoped – one instance per request (web request scope)
- services.AddScoped<IEngine, DieselEngine>();
 
- Singleton – one instance for the whole application (shared state/configs)
- services.AddSingleton<ILoggingService, LoggingService>();
Benefits: Loose coupling, better testability, easier maintenance.
 
Built-in DI container: Registered in Program.cs using AddScoped(), AddSingleton(), AddTransient().
 
Scoped / Transient / Singleton
Transient: New instance every time requested. (Lightweight, stateless services)
Scoped: One instance per request (web request scope).
Singleton: Single instance throughout app lifetime (shared state/configs).
 
 
🔹 Middlewares in .NET Core
Middleware is a peice of sw that can handle http request or response.
Middleware = components in pipeline handling request/response.
Examples: Authentication, Logging, Exception Handling.
Custom Middleware: Implement Invoke or InvokeAsync method.
Use case: Adding headers, logging requests, handling exceptions.
 
 
🔹 Swagger in .NET Core
Purpose: Auto-generate API documentation and UI.
Add via NuGet: Swashbuckle.AspNetCore.
Setup: services.AddSwaggerGen(), app.UseSwaggerUI().
Helps testers and frontend teams consume APIs easily.
 
 
🔹 Authentication in API
Basic: Username/password in headers (less secure).
Token-based: JWT, OAuth2, OpenID Connect.
API Keys: Simple but less secure.
Best practice: JWT/OAuth2 for stateless authentication.
 
 
🔹 JWT (JSON Web Token)
Structure: Header.Payload.Signature.
Header: Algorithm & type.
Payload: Claims (user info, roles, expiry).
Signature: Ensures integrity using secret key.
Usage: Sent in Authorization: Bearer <token> header.
Refresh Tokens: To get new access tokens without re-login.
 
 
🔹 CORS (Cross-Origin Resource Sharing)
Problem: Browser blocks requests from different origins.
Solution: Enable CORS in .NET Core → services.AddCors().
Define allowed origins, headers, and methods.
 
 
🔹 Async / Await in .NET Core
Async: Marks method as asynchronous.
Await: Suspends method execution until task completes.
Benefits: Non-blocking, better scalability for I/O operations.
Example: DB calls, API calls.
 
 
🔹 Logging in .NET Core
Built-in ILogger<T> service.
Providers: Console, Debug, Seq, Serilog.
Supports log levels: Trace → Debug → Info → Warn → Error → Critical.
Configured via appsettings.json.
 
 
🔹 Code First vs Database First (EF Core)
Code First: Define classes → generate DB via migrations.
Database First: DB exists → scaffold C# classes.
Code First = flexible for new projects.
DB First = better when legacy DB already exists.
 
 
🔹 SQL Concepts
Joins
INNER JOIN: Common rows in both.
LEFT JOIN: All from left, matching from right.
RIGHT JOIN: All from right, matching from left.
FULL OUTER JOIN: All from both.
 
CTE (Common Table Expression)
Temporary result set defined using WITH.
Useful for recursion, readability.
 
Temp Tables
#TempTable stored in tempdb.
Used for intermediate results.
 
UNION
Combines results from two queries.
UNION removes duplicates, UNION ALL keeps them.
 
Rank vs DenseRank
RANK(): Skips numbers if ties exist.
DENSE_RANK(): No gaps in ranking.
 
 
🔹 Repository Pattern
Abstracts data access logic.
Interfaces + concrete classes → better testability.
Helps follow SOLID principles.
 
 
🔹 Angular Topics
ngOnInit → initialization & API calls.
ngOnDestroy → cleanup.
ngOnChanges → react to input changes.
ngAfterViewInit → access DOM/child components.
 
1. ngOnChanges(changes: SimpleChanges)
Called when an @Input() property value changes.
Runs before ngOnInit.
Useful for reacting to parent → child data changes.
2. ngOnInit()
Called once, after the first ngOnChanges.
Best place for initialization logic, API calls, fetching data.
3. ngDoCheck()
Runs on every change detection cycle.
Use when Angular’s default change detection isn’t enough.
Example: deep object comparison.
4. ngAfterContentInit()
Called once after external content (ng-content) is projected into the component.
5. ngAfterContentChecked()
Called after every check of projected content.
6. ngAfterViewInit()
Called once after component’s view (and child views) is initialized.
Example: Access @ViewChild DOM elements safely.
7. ngAfterViewChecked()
Called after every change detection for component’s views.
8. ngOnDestroy()
Called once when component is destroyed.
Cleanup: unsubscribe from Observables, detach event handlers, release resources.
 
 
angular.json
Angular workspace config: build, serve, test, styles, assets.
 
package.json
Node dependencies, scripts, metadata of project.
 
Pipes
Transform output in templates (e.g., date, currency, custom pipes).
 
AuthGuard
Controls route access.
Implements CanActivate, checks authentication before navigation.
 
HTTP Interceptor
Intercepts HTTP requests/responses.
Use cases: Add tokens in headers, error handling, logging.
 
NGRX
State management library.
Based on Redux: Store, Actions, Reducers, Effects.
Useful for large apps with shared state.
 
Angular Deployment
ng build --prod → generates dist/ folder.
Deploy to IIS, Nginx, Azure, or any static hosting.
Tokens in Headers (Angular)
Use Interceptor to attach Authorization: Bearer <token> to requests.
 
🔹 Unit Testing
.NET: Use xUnit, NUnit, or MSTest.
Angular: Jasmine + Karma.
Tests should cover components, services, APIs.
 
 
🔹 Design Patterns
Singleton: One instance globally (like ILogger).
Factory: Creates objects without exposing instantiation logic.
Repository: Abstraction for data access.mi