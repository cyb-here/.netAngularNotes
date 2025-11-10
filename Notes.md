## 🔹 SOLID Principles
- **1. Single Responsibility:** One class should do only one thing at a time.
```
# One class should do only one thing at a time
ex,
The ResponseGenerator() calls the LLM and creates a reply.
The ConversationLogger() saves chat history.
The MessageParser() handles cleaning and preprocessing user input.
```
- **2. Open/Closed:** Classes should be open for extension but closed for modification.
```
- Classes should be open for extension but closed for modification.
Ex,
The chatbot can support new features like weather info or appointment booking by adding new modules, without changing the existing LLM response generation code.
```
- **3. Liskov Substitution:** Child class should be able to implement all the methods of the parent class seamlessly.
```
- Child class should be able to implement all the methods of the parent class seamlessly.
Ex, BaseEmployeeClass{} , InternalEmployee{}, ExternalEmployee{}
A BasicChatbot can be replaced with an AdvancedHealthcareChatbot in the system.
Both follow the same chatbot interface, so the system still works correctly.
```
- **Interface Segregation:** Don’t force classes to implement unused methods; prefer smaller, specific interfaces.
```
Any Code should not be forced to use Methods which are not needed.
ex, Separate interfaces:
ITextChat()
IVoiceChat()
IAvatarInteraction()
IAppointmentScheduler()
A text-only chatbot doesn’t need to implement voice or avatar features.
```
- **Dependency Inversion:** Depend on abstractions, not concrete classes.
 ```Higher level module should not depend on lower level module directly but should talk through abstraction like interface.
EX,
The chatbot logic doesn’t directly depend on OpenAI API or Azure AI API.
Instead, it depends on an abstract ILLMProvider.
Different LLM providers can be swapped without changing chatbot logic.

Interface Segregation Example
Bad ❌: One IWorker with Work() and Eat().
Good ✅: Split into IWorkable, IEatable.
 ```
 
 
## 🔹 Dependency Injection (DI) in .NET Core
### Injecting dependencies (services, repositories) instead of creating them inside classes.
- Instead of a class creating its own dependencies, they are provided from the outside.
- A programming technique that makes a class independent of its own dependencies.
- A methodology where in rather than caller creating the instance its injected by someone else or some other mechanism
- DI is a technique where an object’s dependencies are provided from the outside, instead of the object creating them internally.
```
WE CAN DO 
1. Constructor Injection
2. Method Injection
3. Property Injection
``` 
1.  Transient – new instance every time requested. (Lightweight, stateless services)
services.AddTransient<IEngine, PetrolEngine>();
 
1. Scoped – one instance per request (web request scope)  
services.AddScoped<IEngine, DieselEngine>();
 
1. Singleton – Single instance throughout app lifetime (shared state/configs)
services.AddSingleton<ILoggingService, LoggingService>();
 
#### Built-in DI container: Registered in Program.cs using AddScoped(), AddSingleton(), AddTransient().

## 🔹 Middlewares in .NET Core
- Middleware is a peice of sw that can handle http request and response.
- Middleware = components in pipeline handling request/response.  
Examples: Authentication, Logging, Exception Handling.  
Custom Middleware: Implement Invoke or InvokeAsync method.  
Use case: Adding headers, logging requests, handling exceptions.
 
## 🔹 Swagger in .NET Core
- Purpose: Auto-generate API documentation and UI.  
Add via NuGet: Swashbuckle.AspNetCore.  
Setup: services.AddSwaggerGen(), app.UseSwaggerUI().  
Helps testers and frontend teams consume APIs easily.  
 
 
## 🔹 Authentication in API
- Basic: Username/password in headers (less secure).  
- Token-based: JWT, OAuth2, OpenID Connect.  
- API Keys: Simple but less secure.  
Best practice: JWT/OAuth2 for stateless authentication.  
-> Use (Authorize) property in .net controllers to force auth  
-> use interceptors to pass the token to all apis.
 
## 🔹 JWT (JSON Web Token)
### Structure: Header.Payload.Signature.
**Header:** Algorithm & type.  
**Payload:** Claims (user info, roles, expiry).  
**Signature:** Ensures integrity using secret key.  
Usage: Sent in Authorization: Bearer <token> header.  
Refresh Tokens: To get new access tokens without re-login.
User logs in → Server issues:
```
User logs in → Server issues:  
* Access token (short-lived, e.g. 15 minutes)  
* Refresh token (long-lived, e.g. 7 days)  
* Access token expires → Client sends the refresh token to the server.  
* Server validates refresh token → Issues a new access token.  
 ```
 
## 🔹 CORS (Cross-Origin Resource Sharing)  
Problem: Browser blocks requests from different origins.  
Solution: Enable CORS in .NET Core → services.AddCors().  
Define allowed origins, headers, and methods.  
```
1. Register CORS in Startup.cs or Program.cs:
services.AddCors(options =>
{
    options.AddPolicy("AllowSpecificOrigin",
        builder => builder
            .WithOrigins("http://localhost:4200")
            .AllowAnyHeader()
            .AllowAnyMethod());
});
------------------
2. Globally (in Configure method):
app.UseCors("AllowSpecificOrigin");


3. Or per controller/action:
[EnableCors("AllowSpecificOrigin")]
```
 
## 🔹 Async / Await in .NET Core
Async: Marks method as asynchronous.  
Await: Suspends method execution until task completes.  
Benefits: Non-blocking, better scalability for I/O operations.  
Example: DB calls, API calls.

## 🔹 Logging in .NET Core
Built-in ILogger<T> service.  
Providers: Console, Debug, Seq, Serilog.  
Supports log levels: Trace → Debug → Info → Warn → Error → Critical.  
Configured via appsettings.json.
 
## 🔹 Code First vs Database First (EF Core)
Code First: Define classes → generate DB via migrations.
Database First: DB exists → scaffold C# classes.
Code First = flexible for new projects.
DB First = better when legacy DB already exists.
 
 Define models in C# → Generate DB via migrations

>🔧 Commands: Package Manager Console  

🗃️ Code First Approach
> ```Add-Migration MigrationName``` → Creates a migration based on model changes.    
> ```Update-Database``` → Creates a migration based on model changes.  
> ```miGet-Migrations``` → Lists all applied and pending migrations.  
> ```Remove-Migration<MigrationName>``` → Removes the last migration (if not applied)

🗃️ Database First Approach
> ```Scaffold-DbContext "Your_Connection_String" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models```
 
## 🔹 SQL Concepts
Joins  
INNER JOIN: Common rows in both.  
LEFT JOIN: All from left, matching from right.  
RIGHT JOIN: All from right, matching from left.  
FULL OUTER JOIN: All from both.
## 🔹 SQL Joins Overview  
Used to combine rows from two or more tables based on related columns.

>🔧 Syntax Reference  
INNER JOIN  
> ```sql  
> SELECT a.*, b.*  
> FROM TableA a  
> INNER JOIN TableB b ON a.Key = b.Key;  
> ```  
> Returns only matching rows from both tables.

>LEFT JOIN  
> ```sql  
> SELECT a.*, b.*  
> FROM TableA a  
> LEFT JOIN TableB b ON a.Key = b.Key;  
> ```  
> Returns all rows from left table + matched rows from right.   
> Unmatched = NULL.

> RIGHT JOIN  
> ```sql  
> SELECT a.*, b.*  
> FROM TableA a  
> RIGHT JOIN TableB b ON a.Key = b.Key;  
> ```  
> Returns all rows from right table + matched rows from left.  
> Unmatched = NULL.

> FULL JOIN  
> ```sql  
> SELECT a.*, b.*  
> FROM TableA a  
> FULL JOIN TableB b ON a.Key = b.Key;  
> ```  
> Returns all rows from both tables.  
> Unmatched rows = NULL.

> CROSS JOIN  
> ```sql  
> SELECT a.*, b.*  
> FROM TableA a  
> CROSS JOIN TableB b;  
> ```  
> Returns Cartesian product — every row from A paired with every row from B.

> SELF JOIN  
> ```sql  
> SELECT a.*, b.*  
> FROM Employees a  
> JOIN Employees b ON a.ManagerID = b.EmployeeID;  
> ```  
> Joins a table to itself — useful for hierarchy or comparisons.

## 🔹 CTE vs Temp Tables (SQL)

CTE (Common Table Expression)  
Temporary result set defined using `WITH`.  
Useful for recursion, readability, and modular query design.

>🔧 Syntax Example  
> ```sql  
> WITH CTE_Employees AS (  
>   SELECT EmployeeID, ManagerID  
>   FROM Employees  
> )  
> SELECT * FROM CTE_Employees;  
> ```

🗃️ Temp Tables  
`#TempTable` stored in `tempdb`.  
Used for intermediate results, staging, or complex transformations.

>🔧 Syntax Example  
> ```sql  
> SELECT * INTO #TempEmployees  
> FROM Employees  
> WHERE IsActive = 1;  
>  
> SELECT * FROM #TempEmployees;  
> ```
 
## 🔹 UNION vs UNION ALL (SQL)

Combines results from two queries.  
`UNION` removes duplicates, `UNION ALL` keeps them.

>🔧 UNION  
> Combines both result sets and removes duplicates.
> ```sql  
> SELECT Name FROM Employees  
> UNION  
> SELECT Name FROM Managers;  
> ```  

🗃️ UNION ALL  
> Combines both result sets and retains duplicates.
> ```sql  
> SELECT Name FROM Employees  
> UNION ALL  
> SELECT Name FROM Managers;  
> ```  
 
Rank vs DenseRank  
RANK(): Skips numbers if ties exist.  
DENSE_RANK(): No gaps in ranking.  
 
 
🔹 Repository Pattern
Abstracts data access logic.
Interfaces + concrete classes → better testability.
Helps follow SOLID principles.
 
## 🔹 Angular Topics
ngOnInit → initialization & API calls.  
ngOnDestroy → cleanup.  
ngOnChanges → react to input changes.  
ngAfterViewInit → access DOM/child components.
 
1. **ngOnChanges(changes: SimpleChanges)**
Called when an @Input() property value changes.  
Runs before ngOnInit.  
Useful for reacting to parent → child data changes.  
1. **ngOnInit()**
Called once, after the first ngOnChanges.  
Best place for initialization logic, API calls, fetching data.  
1. **ngDoCheck()**
Runs on every change detection cycle.  
Use when Angular’s default change detection isn’t enough.  
Example: deep object comparison.  
1. **ngAfterContentInit()**
Called once after external content (ng-content) is projected into the component.  
1. **ngAfterContentChecked()**
Called after every check of projected content.  
1. **ngAfterViewInit()**
Called once after component’s view (and child views) is initialized.  
Example: Access @ViewChild DOM elements safely.
1. **ngAfterViewChecked()**
Called after every change detection for component’s views.
1. **ngOnDestroy()**
Called once when component is destroyed.  
Cleanup: unsubscribe from Observables, detach event handlers, release resources.
 
> angular.json  
> Angular workspace config: build, serve, test, styles, assets.
 
> package.json  
> Node dependencies, scripts, metadata of project.

## Pipes  
Transform output in templates (e.g., date, currency, custom pipes).  
###  Pure  
- A pure pipe executes only when Angular detects a pure change   
- meaning a change in primitive values (string, number, boolean) or object references.  
- Default: All custom pipes are pure by default unless explicitly marked otherwise.
 
### Impure
 * An impure pipe runs on every change detection cycle, regardless of whether the input has changed.
 * Behavior: Useful when the pipe depends on mutable data or external state.
 * `@Pipe({ name: 'nameHere', pure: false })`


## AuthGuard
Controls route access.
Implements CanActivate, checks authentication before navigation.
## 🔹 AuthGuard (Angular)

Controls route access.  
Implements `CanActivate` to check authentication before navigation.

>🔧 Syntax Reference  

🗃️ Create AuthGuard  
> ```ts  
> ng generate guard auth  
> ```

🗃️ Sample Implementation  
 ```ts  
 @Injectable({ providedIn: 'root' })  
 export class AuthGuard implements CanActivate {  
   constructor(private authService: AuthService, private router: Router) {}  
  
   canActivate(): boolean {  
     if (this.authService.isLoggedIn()) {  
       return true;  
     } else {  
       this.router.navigate(['/login']);  
       return false;  
     }  
   }  
 }  
 ```

🗃️ Apply to Routes  
 ```ts  
 const routes: Routes = [  
   { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] }  
];  
```

## 🔹 Angular Route Guards Overview

Used to control navigation and access in Angular apps.  
Each guard implements a specific interface to intercept routing logic.

>🔧 Guard Types & Usage  

🛡️ CanActivate  
> Checks if a route can be activated.  
> Used for authentication and role-based access.  
> ```ts  
> canActivate(): boolean | UrlTree | Observable<boolean | UrlTree> | Promise<boolean | UrlTree>  
> ```

🛡️ CanActivateChild  
> Checks if child routes can be activated.  
> Useful for nested route protection.  
> ```ts  
> canActivateChild(): boolean | UrlTree | Observable<boolean | UrlTree> | Promise<boolean | UrlTree>  
> ```

🛡️ CanDeactivate  
> Checks if user can leave the current route.  
> Used to prevent loss of unsaved changes.  
> ```ts  
> canDeactivate(component: YourComponent): boolean | Observable<boolean> | Promise<boolean>  
> ```

🛡️ CanLoad  
> Prevents lazy-loaded modules from being loaded.  
> Used for role-based module access.  
> ```ts  
> canLoad(route: Route, segments: UrlSegment[]): boolean | Observable<boolean> | Promise<boolean>  
> ```

🛡️ Resolve  
> Pre-fetches data before route activation.  
> Used for loading data into components via route.  
> ```ts  
> resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<DataType>  
> ```

>🔧 Apply Guards in Routing  
> ```ts  
> const routes: Routes = [  
>   {  
>     path: 'dashboard',  
>     component: DashboardComponent,  
>     canActivate: [AuthGuard],  
>     canActivateChild: [ChildGuard],  
>     canLoad: [LoadGuard],  
>     resolve: { data: DataResolver }  
>   }  
> ];  
> ```



 
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