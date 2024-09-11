# **JForce Solutions Development Style Guide**

****
## Version 1.1

## Table Of Content

    1. Mandatory Development Rules

    2. Jforce Solutions Java & Spring Boot Style Guide 

    3. Code Review Guide

****

## 1. **Mandatory Development Rules**

****

### 1. Run all necessary apps on your local system 

### 2. If a new task/card is assigned, go through the whole requirements thoroughly.

### 3. Check the description and comments in that card.

### 4. Ask for templates, wireframes, path-links, old processes on Shortcut cards and if anything is not clear.

### 5. Create or Request for a Trello Card, to attach all docs on it. 

### 6. Trello Card should include 4 Documents only (Design Document, Reference Document(Genreated via Java Doc), Tutorial Document & Function Document)

### 7. Create Design Doc :
#### 7.1 Versioning 
#### 7.2 Flowchart
#### 7.3 Pseudocode
#### 7.4 Class Diagram, names of each classes methods or variable changes, 
#### 7.5 Entity Relationship Diagram
#### 7.6 JUnit Test Cases with Description
#### 7.7 Component Diagram 

### 8. Get Design Doc approved 

### 9. Development on the card will start once the pullrequest is approved and merged. Any additional feature, requirement, omimizations, changes in Design or Update has to approved by Team Leads, added to Design Document and only then the development will start.   

### 10. Divide every feature into minimal parts

### 11. Each part is to be pushed in a separate branch

### 12. Those branch changes should be at most 200 lines.

### 13. Create a pull request for that branch and attach on Trello card.

### 14. Every day allocate 30mins for peer review.

### 15. Peer review comments only be mentioned on pull request of a branch

### 16. Add Todo List on discord group at 9 30am

### 17. Add work report of todo list status and adhoc work at 5 30 pm

### 18. Create every module restful with rest api

### 19. Sevice Layer Method to have miniumn 80% Test Coverage

### 20. Test driven development can be implemented

### 21. Service layer methods to be developed then test case of them

### 22. Any Production Bugs occured due to deployment of developers Branch needs an RCA Document. Which is to be created by Developer of the Branch.

Location will be within microservice in the microservice_name/ReadmeFiles/RCA Report/ 

#### RCA Document Template  

Here is an example of a report  to create while solving a task:
#### Task:
The customer is unable to log in to the application.
#### Steps taken:
I verified that the customer is using the correct username and password.
I checked the application logs to see if there were any errors.
I tried to log in to the application myself using the customer's credentials.
I contacted the customer to get more information about the issue.
#### Findings:
The customer was using the correct username and password. There were no errors in the application logs. I was able to log in to the application myself using the customer's credentials. The customer is using a VPN to connect to the internet.
#### Solution:
I had the customer disable their VPN and try to log in to the application again. The customer was able to log in successfully.
Recommendations:
I recommend that the customer contact their VPN provider to see if there are any known issues with the VPN and the application.
#### Conclusion:
The customer was unable to log in to the application because they were using a VPN. I had the customer disable their VPN and they were able to log in successfully. I recommend that the customer contact their VPN provider to see if there are any known issues with the VPN and the application. 

#### Sample of our RCA Document: https://bitbucket.org/ngasceadmin/exam/src/master/ReadmeFiles/RCA%20Report/QP%20upload%20issue%20RCA%20report%20MD%20file.md

****


## **2. Jforce Solutions Java & Spring Boot Style Guide** 

### 1. Model Beans Serializable

Add implements serializable for all model beans.

To make your model beans serializable in Java, you simply need to implement the `Serializable` interface. This allows instances of your beans to be converted into a stream of bytes, which can then be stored in a file, sent over the network, or otherwise persisted.

Here's an example of how you can add the `implements Serializable` interface to a Java bean:

```java
import java.io.Serializable;

public class YourModelBean implements Serializable {
    // Your bean properties and methods here
}
```

By adding `implements Serializable` to your class declaration, you're ensuring that it adheres to the contract specified by the `Serializable` interface. This will allow instances of your model beans to be serialized and deserialized without any issues.


Source file basics
--------------------

### 2.1 File name

The source file name consists of the case-sensitive name of the top-level class it contains (of which there is [exactly one](#s3.4.1-one-top-level-class)), plus the `.java` extension.

### 2.2 File encoding: UTF-8

Source files are encoded in **UTF-8**.

### 3.3 Import statements

#### 3.3.1 No wildcard imports

**Wildcard imports**, static or otherwise, **are not used**.

#### 3.3.2 No line-wrapping

Import statements are **not line-wrapped**. The column limit (Section 4.4, [Column limit: 100](#s4.4-column-limit)) does not apply to import statements.

#### 3.3.3 Ordering and spacing

Imports are ordered as follows:

1.  All static imports in a single block.
2.  All non-static imports in a single block.

If there are both static and non-static imports, a single blank line separates the two blocks. There are no other blank lines between import statements.

Within each block the imported names appear in ASCII sort order. (**Note:** this is not the same as the import _statements_ being in ASCII sort order, since '.' sorts before ';'.)

#### 3.3.4 No static import for classes

Static import is not used for static nested classes. They are imported with normal imports.


### 4 StringBuilder to be used when using multiple concat to a string   

Add stringbuilder when using multiple concat to a string.

 In Java, when you need to concatenate multiple strings, especially within a loop or in performance-sensitive scenarios, we have to use StringBuilder over direct string concatenation using the + operator. Here's a Java example demonstrating the usage of StringBuilder:

public class StringBuilderExample {
    public static void main(String[] args) {
        // Array of strings to concatenate
        String[] words = {"Hello", " ", "world", "!"};
        
        // Using StringBuilder for concatenation
        StringBuilder sb = new StringBuilder();
        Arrays.stream(words).forEach(sb::append);
        
        // Converting StringBuilder to String
        String result = sb.toString();
        
        // Output the concatenated string
        System.out.println(result);
    }
}
Advantages of using StringBuilder over direct string concatenation:

1. Efficiency: String concatenation using StringBuilder is more efficient, especially when concatenating within loops or with a large number of strings. This is because StringBuilder internally uses a resizable array to store characters, which avoids creating multiple intermediate string objects as with direct concatenation.

2. Mutable: StringBuilder is mutable, meaning you can modify the contents of the string without creating a new object each time you make a change. This is particularly useful when you need to build a string iteratively, such as within a loop.

3. Performance: Due to its mutable nature and efficient memory management, StringBuilder generally offers better performance compared to direct string concatenation, especially in scenarios where performance is critical.

4. Convenience: StringBuilder provides convenient methods like append(), insert(), delete(), etc., which make string manipulation easier and more readable compared to manual string concatenation.

By using StringBuilder, you can optimize your code for better performance and readability, especially in scenarios where string concatenation is frequent or involves a large number of strings.

### 4 Any DAO operations taking more than 200 milli seconds to execute needs approval from Team Leads.

### 5 DAO Layer can have only have Repository Interface Call. No business logic or Data/Collection Manupulation code can be added. 

### 6 Database can be accessed strictly using Spring Data JPA. JDBC Template Librabry can't be used as we are migrating to ORM.  

### 7 Avoid mutable variables   

### 8 Avoid Sharing full Custom Model in Methods (avoid doing methodName(StudentBean s), instead pass only required props) 

### 9. avoid using "Select \* from ..." 

### 10 Sub-Queries
avoid using  

### 11. Check Each and every thing in View (use only JSTL)   

### 12. Check Each functionality if changes made in controller or afftecting other modules

### 13. Comment Reference  i.e if changes done at once place which places it must be changed (add java doc comments)

### 14. Component Layer (if needed)

### 15. DAO layer cannot have exception handling. The exception handling can be done in the Class it is called.  

### 16. Delete query will not return anything  (delete/update () must return only int value)

### 17. Do not allow null values unless later its to be updated by student (avoid null insert in db table)

### 18. Do not return null 

### 19. Exception Handling to done at Controller layer. Rest of layers can throw Exceptions in catch block.

### 19.1 Caught exceptions: not ignored

Except as noted below, it is very rarely correct to do nothing in response to a caught exception. (Typical responses are to log it, or if it is considered "impossible", rethrow it as an `AssertionError`.)

When it truly is appropriate to take no action whatsoever in a catch block, the reason this is justified is explained in a comment.

try {
  int i = Integer.parseInt(response);
  return handleNumericResponse(i);
} catch (NumberFormatException ok) {
  // it's not numeric; that's fine, just continue
}
return handleTextResponse(response);

**Exception:** In tests, a caught exception may be ignored without comment _if_ its name is or begins with `expected`. The following is a very common idiom for ensuring that the code under test _does_ throw an exception of the expected type, so a comment is unnecessary here.

try {
  emptyStack.pop();
  fail();
} catch (NoSuchElementException expected) {
}

### 20 `@Override`: always used

A method is marked with the `@Override` annotation whenever it is legal. This includes a class method overriding a superclass method, a class method implementing an interface method, and an interface method respecifying a superinterface method.

**Exception:** `@Override` may be omitted when the parent method is `@Deprecated`.



### 21 Static members: qualified using class

When a reference to a static class member must be qualified, it is qualified with that class's name, not with a reference or expression of that class's type.

Foo aFoo = ...;
Foo.aStaticMethod(); // good
aFoo.aStaticMethod(); // bad
somethingThatYieldsAFoo().aStaticMethod(); // very bad


22. Function should do one thing (divide into multiple () )

23. Impact Analysis check references  (very imp)

24. Interface for each method except controller mandatory   

25. Java Standard Bean Validation API

26. Junit test case last

27. Loop should iterate through whole list and create seperate list of exceptions and success sir send 

28. No joins for student n admin end (use java (hashmaps, etc) for processing n denormalized tables. Checking if data already in session.)

29. No repeatition 

30. One flawed line/character can destroy whole code \*\*

31. preparedstatements ()

32. Do not use traditional for/while loops. Use Stream to manupulate data/ Joins/ iteration. 

Use of streams instead of traditional for loops in Java can lead to more concise, readable, and expressive code. Streams leverage functional programming concepts to operate on collections of data in a declarative manner.

Here's how you can rewrite common loop patterns using streams:

1. Iterating over a Collection:

   ```java
   // Traditional for loop
   for (String item : collection) {
       // Process item
   }
   
   // Using streams
   collection.forEach(item -> {
       // Process item
   });
   ```

2. Filtering elements:

   ```java
   // Traditional for loop
   List<String> filteredList = new ArrayList<>();
   for (String item : collection) {
       if (condition) {
           filteredList.add(item);
       }
   }
   
   // Using streams
   List<String> filteredList = collection.stream()
                                          .filter(item -> condition)
                                          .collect(Collectors.toList());
   ```

3. Transforming elements:

   ```java
   // Traditional for loop
   List<Integer> transformedList = new ArrayList<>();
   for (String item : collection) {
       transformedList.add(transformFunction(item));
   }
   
   // Using streams
   List<Integer> transformedList = collection.stream()
                                             .map(item -> transformFunction(item))
                                             .collect(Collectors.toList());
   ```

4. Combining elements:

   ```java
   // Traditional for loop
   StringBuilder result = new StringBuilder();
   for (String item : collection) {
       result.append(item);
   }
   
   // Using streams
   String result = collection.stream()
                            .collect(Collectors.joining());
   ```

5. Reducing elements:

   ```java
   // Traditional for loop
   int sum = 0;
   for (Integer number : numbers) {
       sum += number;
   }
   
   // Using streams
   int sum = numbers.stream()
                   .reduce(0, Integer::sum);
   ```

By using streams, you can write more concise and expressive code, benefiting from built-in methods for filtering, mapping, reducing, and more.

33. Profiler time execution to be commented for each method (add a commnet of each method with  time)

34. Remove console logs

35. Remove Sys outs (use logger instead)

36. Service Layer 

37. Session checks (very imp)

38. Throw Exception instead of error codes

39. use Java8 new features in code (streams api, lamda () , etc).

40. USE of DTO & Assembler (eg shared on general) 

41. where = null is sql  work and return empty, to be handled via bean level

42. Update Query check count. Will return zero if not updated. Zero has to be handled. 

43. Query null values of parameters have to be checked before sending to DAO.

44. Do not use inline JS

45. Loggers to be add at in every catch and places at important data is been processed

46. Add spring rest docs

47. Javadoc
---------

### 47.1 Formatting

#### 47.1.1 General form

The _basic_ formatting of Javadoc blocks is as seen in this example:

/\*\*
 \* Multiple lines of Javadoc text are written here,
 \* wrapped normally...
 \*/
public int method(String p1) { ... }

... or in this single-line example:

/\*\* An especially short bit of Javadoc. \*/

The basic form is always acceptable. The single-line form may be substituted when the entirety of the Javadoc block (including comment markers) can fit on a single line. Note that this only applies when there are no block tags such as `@return`.

#### 47.1.2 Paragraphs

One blank line—that is, a line containing only the aligned leading asterisk (`*`)—appears between paragraphs, and before the group of block tags if present. Each paragraph except the first has `<p>` immediately before the first word, with no space after it. HTML tags for other block-level elements, such as `<ul>` or `<table>`, are _not_ preceded with `<p>`.

#### 47.1.3 Block tags

Any of the standard "block tags" that are used appear in the order `@param`, `@return`, `@throws`, `@deprecated`, and these four types never appear with an empty description. When a block tag doesn't fit on a single line, continuation lines are indented four (or more) spaces from the position of the `@`.

### 47.2 The summary fragment

Each Javadoc block begins with a brief **summary fragment**. This fragment is very important: it is the only part of the text that appears in certain contexts such as class and method indexes.

This is a fragment—a noun phrase or verb phrase, not a complete sentence. It does **not** begin with `A {@code Foo} is a...`, or `This method returns...`, nor does it form a complete imperative sentence like `Save the record.`. However, the fragment is capitalized and punctuated as if it were a complete sentence.

**Tip:** A common mistake is to write simple Javadoc in the form `/** @return the customer ID */`. This is incorrect, and should be changed to `/** Returns the customer ID. */`.

### 47.3 Where Javadoc is used

At the _minimum_, Javadoc is present for every `public` class, and every `public` or `protected` member of such a class, with a few exceptions noted below.

Additional Javadoc content may also be present, as explained in Section 7.3.4, [Non-required Javadoc](#s7.3.4-javadoc-non-required).

#### 47.3.1 Exception: self-explanatory members

Javadoc is optional for "simple, obvious" members like `getFoo()`, in cases where there _really and truly_ is nothing else worthwhile to say but "Returns the foo".

**Important:** it is not appropriate to cite this exception to justify omitting relevant information that a typical reader might need to know. For example, for a method named `getCanonicalName`, don't omit its documentation (with the rationale that it would say only `/** Returns the canonical name. */`) if a typical reader may have no idea what the term "canonical name" means!

#### 47.3.2 Exception: overrides

Javadoc is not always present on a method that overrides a supertype method.

#### 47.3.4 Non-required Javadoc

Other classes and members have Javadoc _as needed or desired_.

Whenever an implementation comment would be used to define the overall purpose or behavior of a class or member, that comment is written as Javadoc instead (using `/**`).

Non-required Javadoc is not strictly required to follow the formatting rules of Sections 44.1.1, 44.1.2, 44.1.3, and 44.2, though it is of course recommended.

### 47 All Student Pages/Admin Pages UI will be created on React and Will be via RESTfull API.

## Code Review Guide

### Objective
This document provides guidelines for maintaining a 200-line-of-code (LOC) rule while working on a project, using a structured, bottom-up approach. The goal is to simplify code reviews, ensure clean merges, and maintain code quality.

We will use a hypothetical CRUD application with a focus on the following components:

* JPA Entities
* DTOs (Data Transfer Objects)
* Service Layer
* Controller

* Note: If you are following TDD (test driven development) you can choose to push those test cases along with features.

Each branch will contain small, focused code changes under 200 lines, following a systematic approach, and will be reviewed before merging.

### General Rules

#### Branching:

* Always create branches for each component you are working on.
Follow a bottom-up approach to ensure code dependencies are maintained. This means starting with the files that are least dependent on others (e.g., Entities), and progressively moving upward.


#### Naming Convention:

* Branch names should follow this pattern:
{shortcutCardName}{featureInfo}{branchInfo}{suffix}

* example:
    - feature/12345-add-exam-booking-Entities-I
    - feature/12345-add-exam-booking-Entities-1
    - feature/12345-add-exam-booking-I-Entities
    - feature/12345-add-exam-booking-1-Entities

    Suffix is an incrementing number (I, II, III, etc.) or (1, 2, 3, etc.) 

#### Line of Code Limit:

* No branch should have more than 200 lines of code.
Push only files that are not dependent on others (e.g., JPA Entities first before pushing Services, then DTOs, then Controller).

#### Code Reviews

* Each branch will be reviewed once you open a Pull Request (PR). Ensure that your branch is clear, contains descriptive commit messages, and abides by the LOC limit.
After review and merge, create a new branch for the next incremental code addition.

#### Step-by-Step Example: Building a CRUD Application

* We'll build a simple CRUD application with the following features:
    - Create, Read, Update, Delete operations for a Product. We'll apply the 200 LOC rule and use branches as follows:

#####  Start with JPA Entities (Branch I)

* Branch name: feature/1234-crudproduct-entity-I

* Description:
    In this branch, we’ll push the basic JPA entity Product for the CRUD operations. Since the entity typically doesn’t depend on other files, it will be the first to be pushed.

```java

@Entity
@Table(name = "products")
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String description;
    private Double price;

    // Getters and Setters
}
```

##### Create DTOs (Branch II)
* Branch name: feature/12345-crudproduct-dto-II

* Description:
Once the entity is merged, we’ll create the DTOs (Data Transfer Objects). DTOs are typically used to transfer data between layers, and they often depend on the entities, so they come after entities.

```java
public class ProductDTO {
    private Long id;
    private String name;
    private String description;
    private Double price;

    // Getters and Setters
}
```

#### Service Layer (Branch III)
* Branch name:
feature/crudproductserviceIII

* Description:
Once the DTOs are merged, the next step is the Service Layer. This layer will contain business logic for the CRUD operations and will interact with the repository (we assume that repositories are auto-generated for brevity).

```java

@Service
public class ProductService {
    @Autowired
    private ProductRepository productRepository;

    public ProductDTO createProduct(ProductDTO productDTO) {
        Product product = new Product();
        product.setName(productDTO.getName());
        product.setDescription(productDTO.getDescription());
        product.setPrice(productDTO.getPrice());
        
        productRepository.save(product);
        productDTO.setId(product.getId());
        return productDTO;
    }

    // Other CRUD methods
}

```

##### Controller (Branch IV)

* Branch name: feature/crudproductcontrollerIV

* Description:
Finally, after all the backend components are merged, we’ll create the Controller. The controller is the entry point for the application’s API and will make use of the Service Layer.

```java

@RestController
@RequestMapping("/products")
public class ProductController {
    @Autowired
    private ProductService productService;

    @PostMapping
    public ResponseEntity<ProductDTO> createProduct(@RequestBody ProductDTO productDTO) {
        ProductDTO createdProduct = productService.createProduct(productDTO);
        return new ResponseEntity<>(createdProduct, HttpStatus.CREATED);
    }

    // Other CRUD endpoints
}

```
By following this structure, you’ll maintain a clean, scalable, and easy-to-manage codebase. The small, incremental approach ensures that each component is reviewed thoroughly without overwhelming reviewers, reducing the risk of introducing bugs and improving the overall quality of the codebase.