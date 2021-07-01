Cucumber
========

A cucumber is a tool that is based on Behavior Driven Development (BDD) methodology.

Cucumber is a testing tool that supports Behavior Driven Development (BDD) framework. It defines application behavior using simple English text, defined by a language called Gherkin.

Cucumber allows automation functional validation that is easily read and understood. Cucumber was initially implemented in Ruby and then extended to Java framework. Both the tools support native JUnit.

Advantages of Cucumber
--------------------

- Cucumber is an open-source tool.
- The primary advantage of Cucumber is its support of Behaviour Driven Development approach in testing.
- This tool helps in eliminating the gap between different technical and non-technical members of the team.
- Automation test cases developed using the Cucumber tool are easier to maintain and understand.
- Easy to integrate with other tools such as Selenium. 

- Cucumber supports different languages like Java.net and Ruby.
- It acts as a bridge between the business and technical language. We can accomplish this by creating a test case in plain English text.
- It allows the test script to be written without knowledge of any code, it allows the involvement of non-programmers as well.
- It serves the purpose of end-to-end test framework unlike other tools.
- Due to simple test script architecture, Cucumber provides code reusability.

Example
-------------
If we are developing a user authentication feature, then the following can be few key test scenarios, which needs to get passed in order to call it a success.

- The user should be able to login with correct username and correct password.
- The user should not be able to login with incorrect username and correct password.
- The user should not be able to login with correct username and incorrect password.

By the time the code is ready, test scripts are ready too. The code has to pass the test scripts defined in BDD. 
If it does not happen, code refactoring will be needed. Code gets freezed only after successful execution of defined test scripts.


Cucumber reads the code written in plain English text (Language Gherkin – to be introduced later in this tutorial) in the feature file (to be introduced later).

It finds the exact match of each step in the step definition (a code file - details provided later in the tutorial).

The piece of code to be executed can be different software frameworks like Selenium, Ruby on Rails, etc. Not every BDD framework tool supports every tool.

This has become the reason for Cucumber's popularity over other frameworks, like JBehave, JDave, Easyb, etc.

Cucumber supports over a dozen different software platforms like −
- Ruby on Rails
- Selenium
- PicoContainer
- Spring Framework
- Watir
























For more information:

1. [Cucumber - Overview](https://www.tutorialspoint.com/cucumber/cucumber_overview.htm)