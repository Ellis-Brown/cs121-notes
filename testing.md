# Testing
Lecture: 11/3/2021

cs121

## Opaque box testing (black box testing)
Only look at the function contracts / spec

## Glass box testing (White box testing)
- Idea: look at the code. 
- Focus on features not described by the spec
- Possibly look at performance optimizations (example: cache)
- Possibly look at error handling
---
## Coverage Criteria
"Metric of how good a test suite is."

#### Goal: Test suite covers all possible program behaviors.

The more behvaiors you cover, the more likely it is that there are no bugs, but in practice you often cant cover all behaviors.

In practice, use __structrual coverage criteria__:

- Divide a program into elements (methods, statements)
- Coverage of a test suite is 

    (# of elements executed by suite) / (total # of elements)

Types of coverage    

- **statement coverage** : hit every statement (elements are program statements.)
- **branch/condition/edge coverage** : hit every possible edge or conditional outcome (elements are edges in control flow graph: or for each branch, need to take it in all directions)
- **path coverage** - all possible cases through the program. Typically not possible (all possible paths through the control flow graph.)

> Note: there is an unbounded number of paths, since we could go through the loop any number of times 

Observation : High structural code coverage => good test suite. Almost all programming languages have ways to test structural code coverage, and often also branch/edge/condition coverage

In practice, can't achieve 100% statement coverage reliably. (85% is amazing) 

# Refactoring
Old school software development:

"Waterfall model of software development"
- Requirements ->  
    - Design ->
    - Code ->
    - Test ->
        - Deliver

*Problem: Assumed that requirements are known ahead of time*: 

*Problem: hard to design without coding*

---

"New idea"

- Come up with a reasonable design up front, and be willing to evolve the design over time.

**Key  idea:**
Wear two hats when you're coding
1. Bug fixing or feature additions
2. Refactoring - change code design but not its behavior.
    - All test cases should still pass.

Example:
```java
double area(double r) {
    return 3.14 * r * r;
}

/* refactor */

static final double pi = 3.14;
double area(double r) {
    return pi * r * r;
}
```
all test cases should still pass, just code readability increased.

Some types of refactoring:
- Replace number with a constant
- Move method from a subclass to a superclass
- Extract code into its own module

When to refactor: look for "*code smells*"
 - Everytmie I make change X, I have to make lots of other little changes to different classes
 - Theres a class but it doesnt seem useful any more.
 - A class has excess generality thats not used
 - Classes rely on too much details of each other (high coupling)
 - Subclasses doesn't use features of superclass
 
> Without refactoring, projects will gain "technical debt" which is needed refactoring and documentation for the upkeeping of the project. People push projects to completion for a deadline, then clean the code afterwards
