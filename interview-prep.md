# Software Developer Internship - Interview Preparation (Java)

**Format:** 30 min Technical Interview | 50% English - 50% Vietnamese
**Structure:** Technical discussion (skillset + CV projects) + 15 min Live Code (LeetCode Easy)

---

## 1. Self-Introduction (2 minutes)

> **Opening:**
> Hi, my name is Thao - Doan Thanh Thao. I'm a third-year student at UIT VNU-HCM, studying Computer Networks and Data Communication. My GPA is 8.77/10.
>
> **Why Software Development:**
> My background is in **networking and communication**, so I'm still early in my software development journey. But through personal projects, I've grown very interested in backend development with **Java and Spring Boot** - and I'm eager to learn more in a real team.
>
> **EcoWalk Project (main highlight):**
> - My main project is **EcoWalk** - a mobile app built with **Spring Boot + PostgreSQL + Android (Java)**
> - I built the **login system** using Spring Security with JWT tokens (access + refresh)
> - I created **REST APIs** for features like Clubs and Events
> - The Android app calls these APIs using **Retrofit2**
> - Data is stored in **cloud PostgreSQL (Neon)** using **Hibernate JPA**
>
> **Other experience:**
> - Set up **microservices with Docker Compose**
> - Used **OpenTelemetry + Jaeger** for tracing requests across services
> - Deployed a **private cloud** using Apache CloudStack
>
> **Closing:**
> I'm looking for an internship to grow my Java and backend skills in a real team. I think this position is a great fit. Thank you.

---

## 2. Java Core Questions

### Basics

**Q1: What are the main principles of OOP? Can you give a simple example from your EcoWalk project?**

A: The four principles are **Encapsulation, Inheritance, Polymorphism, and Abstraction**.
- In EcoWalk, I used **encapsulation** by keeping entity fields private and exposing them through getters/setters.
- **Inheritance**: my entity classes extend a base entity that has common fields like `id` and `createdAt`.
- **Polymorphism**: Spring's dependency injection lets me swap implementations (e.g., different service implementations behind the same interface).
- **Abstraction**: I defined service interfaces (e.g., `ClubService`) and implemented the logic in `ClubServiceImpl`, so the controller only depends on the interface.

**Q2: What is the difference between `==` and `.equals()` in Java?**

A: `==` compares **references** (whether two variables point to the same object in memory). `.equals()` compares **values** (the actual content). For example, two `String` objects with the same text will return `true` with `.equals()` but may return `false` with `==` if they are different objects.

**Q3: What is the difference between `ArrayList` and `LinkedList`?**

A: `ArrayList` uses a dynamic array internally - fast random access O(1) but slow insertion/deletion in the middle O(n). `LinkedList` uses a doubly-linked list - fast insertion/deletion O(1) at known positions but slow random access O(n). For most cases, `ArrayList` is preferred because of better cache performance.

**Q4: What are access modifiers in Java?**

A: Java has 4 access modifiers:
- `private`: accessible only within the same class
- `default` (no keyword): accessible within the same package
- `protected`: same package + subclasses
- `public`: accessible from anywhere

**Q5: What is the difference between `abstract class` and `interface`?**

A: An `abstract class` can have both abstract and concrete methods, can have state (fields), and a class can only extend one abstract class. An `interface` defines a contract - before Java 8 it only had abstract methods, but now it can have `default` and `static` methods. A class can implement multiple interfaces. Use interface when you want to define a capability (e.g., `Serializable`), use abstract class when you want to share code among related classes.

**Q6: What is `final` keyword used for?**

A: `final` has 3 uses:
- **final variable**: value cannot be changed after assignment (constant)
- **final method**: cannot be overridden by subclasses
- **final class**: cannot be extended (e.g., `String` class)

**Q7: What is Exception handling in Java? Difference between checked and unchecked exceptions?**

A: Java uses try-catch-finally blocks to handle exceptions.
- **Checked exceptions** (e.g., `IOException`, `SQLException`): must be handled at compile time with try-catch or declared with `throws`. These represent recoverable conditions.
- **Unchecked exceptions** (e.g., `NullPointerException`, `ArrayIndexOutOfBoundsException`): subclass of `RuntimeException`, not required to be caught. These usually indicate programming errors.

### Collections & Data Structures

**Q8: What is a `HashMap`? How does it work internally?**

A: `HashMap` stores key-value pairs. Internally, it uses an **array of buckets**. When you put a key-value pair, Java calls `hashCode()` on the key to determine which bucket, then uses `equals()` to handle collisions. In Java 8+, if a bucket has too many entries (>8), it converts from a linked list to a balanced tree for O(log n) lookup.

**Q9: What is the difference between `HashMap` and `HashTable`?**

A: `HashMap` is not synchronized (not thread-safe) and allows one `null` key. `HashTable` is synchronized (thread-safe) but slower, and does not allow `null` keys or values. In practice, we use `ConcurrentHashMap` instead of `HashTable` for thread-safe operations.

---

## 3. Spring Boot & Backend Questions (Based on EcoWalk Project)

**Q10: Can you explain the architecture of your EcoWalk project?**

A: I used a **layered architecture**:
- **Controller layer**: handles HTTP requests, validates input, returns responses
- **Service layer**: contains business logic
- **Repository layer**: interacts with the database using Spring Data JPA
- **Entity/Model layer**: maps Java objects to database tables using Hibernate annotations

The Android client communicates with the backend through REST APIs over HTTP/JSON using Retrofit2.

**Q11: How did you implement authentication in EcoWalk?**

A: I used **Spring Security** with **stateless JWT authentication**:
1. User logs in with credentials -> server validates and returns an **access token** (short-lived) and a **refresh token** (longer-lived)
2. Client sends the access token in the `Authorization` header for each request
3. A custom **JWT filter** in the Spring Security filter chain intercepts requests, extracts and validates the token, and sets the authentication in the `SecurityContext`
4. When the access token expires, the client uses the refresh token to get a new access token without re-logging in

**Q12: What is dependency injection? How does Spring implement it?**

A: Dependency Injection (DI) is a design pattern where an object's dependencies are provided from outside rather than created inside. This makes code more **testable** and **loosely coupled**. Spring implements DI through its IoC (Inversion of Control) container. We use annotations like `@Autowired`, `@Service`, `@Repository`, `@Component` to let Spring manage object creation and injection.

**Q13: What are common HTTP methods and status codes you used in your REST APIs?**

A:
- `GET` (read), `POST` (create), `PUT` (full update), `PATCH` (partial update), `DELETE` (remove)
- `200 OK`, `201 Created`, `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`, `500 Internal Server Error`

**Q14: What is JPA and Hibernate? How did you use them?**

A: **JPA** (Java Persistence API) is a specification for ORM (Object-Relational Mapping) in Java. **Hibernate** is the most popular implementation of JPA. In EcoWalk, I used Hibernate 6.x with annotations like `@Entity`, `@Table`, `@Id`, `@ManyToOne`, `@OneToMany` to map Java objects to PostgreSQL tables. Spring Data JPA provides `JpaRepository` interface which gives us CRUD operations without writing SQL.

**Q15: What is the difference between `@Component`, `@Service`, `@Repository`, and `@Controller`?**

A: They are all specializations of `@Component` (Spring-managed beans):
- `@Controller` / `@RestController`: handles web requests
- `@Service`: business logic layer (no special behavior, just semantic clarity)
- `@Repository`: data access layer - adds automatic exception translation from database exceptions to Spring's `DataAccessException`

---

## 4. Database & SQL Questions

**Q16: What is the difference between SQL and NoSQL databases? When would you use each?**

A: **SQL** (PostgreSQL, MySQL): structured data, relationships, ACID transactions, fixed schema. Good for: banking, e-commerce, EcoWalk's user/club/event data.
**NoSQL** (MongoDB): flexible schema, horizontal scaling, eventual consistency. Good for: logs, real-time analytics, social media feeds.

**Q17: What are JOINs in SQL? Name the types.**

A: JOINs combine rows from two or more tables based on a related column.
- `INNER JOIN`: returns rows that have matching values in both tables
- `LEFT JOIN`: all rows from left table + matched rows from right table
- `RIGHT JOIN`: all rows from right table + matched rows from left table
- `FULL OUTER JOIN`: all rows from both tables

**Q18: What is database indexing and why is it important?**

A: An index is a data structure (usually B-tree) that speeds up data retrieval. Without an index, the database scans every row (full table scan). With an index on a column, the database can find rows much faster. Trade-off: indexes speed up reads but slow down writes (insert/update/delete) because the index must also be updated.

---

## 5. Docker & Infrastructure Questions (Based on Your Projects)

**Q19: What is Docker? Why did you use it in your microservices project?**

A: Docker is a platform for packaging applications into **containers** - lightweight, isolated environments that include everything needed to run the app (code, runtime, libraries). I used Docker Compose to deploy 3 microservices + MongoDB + RabbitMQ + Nginx as containers. Benefits: consistent environments, easy deployment, service isolation.

**Q20: What is the difference between a Docker image and a container?**

A: An **image** is a read-only template/blueprint (like a class in Java). A **container** is a running instance of an image (like an object). You can run multiple containers from the same image.

**Q21: Can you explain briefly what OpenTelemetry and Jaeger are and why you used them?**

A: **OpenTelemetry** is a framework for collecting observability data (traces, metrics, logs) from applications. **Jaeger** is a distributed tracing backend that visualizes how requests flow across microservices. I used them to trace end-to-end request latency and identify bottleneck services. This helped analyze P95/P99 latency during load testing with Locust.

---

## 6. General / Behavioral Questions

**Q22: Why did you choose Java for your internship track?**

A: I've been building with Java through my EcoWalk project using Spring Boot and I enjoy the strongly-typed, object-oriented nature of the language. Java's ecosystem for backend development is mature and widely used in enterprise environments. I want to deepen my skills in a professional setting.

**Q23: Tell me about a challenge you faced in a project and how you solved it.**

A: In EcoWalk, implementing JWT authentication with both access and refresh tokens was challenging. I had to understand how Spring Security's filter chain works, how to create a custom filter that intercepts every request, validates the JWT, and sets the security context. I debugged issues where the filter order was incorrect, causing 403 errors. I solved it by reading Spring Security documentation carefully and testing each filter step by step using Postman.

**Q24: How do you keep up with new technologies?**

A: I take online courses (like Clean Code on Udemy, Kubernetes on KodeKloud), read documentation, and build side projects. I also explore different areas beyond just coding - like infrastructure with Docker and CloudStack, and observability with OpenTelemetry.

---

## 7. Live Coding Preparation (15 min - LeetCode Easy)

### Common Patterns to Practice

**Pattern 1: Two Pointers**
- Two Sum (LeetCode #1) - use HashMap for O(n) solution
- Valid Palindrome (#125)
- Reverse String (#344)

**Pattern 2: HashMap / HashSet**
- Contains Duplicate (#217)
- Valid Anagram (#242)
- Intersection of Two Arrays (#349)

**Pattern 3: String Manipulation**
- Reverse Integer (#7)
- Roman to Integer (#13)
- Longest Common Prefix (#14)

**Pattern 4: Array**
- Best Time to Buy and Sell Stock (#121)
- Merge Sorted Array (#88)
- Remove Duplicates from Sorted Array (#26)

**Pattern 5: Linked List**
- Reverse Linked List (#206)
- Merge Two Sorted Lists (#21)
- Linked List Cycle (#141)

### Live Coding Tips
1. **Read the problem carefully** - don't rush. Clarify edge cases with the interviewer.
2. **Think out loud** - explain your approach before coding.
3. **Start with brute force** - mention the simple O(n^2) approach, then optimize.
4. **Write clean code** - use meaningful variable names, handle edge cases.
5. **Test with examples** - trace through your code with the given examples.
6. **Talk about time and space complexity** after finishing.

### Sample: Two Sum (Java)

```java
// Given an array of integers and a target, return indices of two numbers that add up to target.
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    return new int[] {};
}
// Time: O(n), Space: O(n)
```

### Sample: Valid Palindrome (Java)

```java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
        if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}
// Time: O(n), Space: O(1)
```

### Sample: Reverse Linked List (Java)

```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
// Time: O(n), Space: O(1)
```

---

## 8. Questions to Ask the Interviewer

1. What does a typical day look like for an intern on the team?
2. What tech stack does the team currently use?
3. How does the team handle code reviews and knowledge sharing?
4. What kind of projects would I be working on as an intern?

---

**Note:** The interviewer is a Software Engineer at NAB with experience in ReactJS, NodeJS, GraphQL, and full-stack web development. They may ask about how your backend knowledge connects with frontend concepts, or about API design since they work with both sides. Be ready to discuss REST API design decisions from EcoWalk clearly.

Good luck, Thao!
