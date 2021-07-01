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
  
Two files required to execute a Cucumber test scenario:

1. Features
2. Step Definition

Example
-------------
- `Feature`: Visit XYZ page in abc.com
- `Scenario`: Visit abc.com
- `Given`: I am on abc.com
- `When`: I click on XYZ page
- `Then`: I should see ABC page

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

Cucumber supports different software platforms like −
- Ruby on Rails
- Selenium
- PicoContainer
- Spring Framework
- Watir


Feature file
-------------
Features file contain a high-level description of the Test Scenario in simple language. It is known as Gherkin which is a plain English text language. Feature File consists of the  components like:

- `Feature`: It describes the current test script which has to be executed.
- `Scenario`: It is steps and expected outcome for a specific test case.
- `Scenario outline`: Scenario can be executed for multiple sets of data using scenario outline.
- `Given`: It specifies the context of the text to be executed.
- `When`: specifies the test action which has to perform.
- `Then`: Expected outcome of the test can be represented by “Then”

Step Definition
-------------
Step definition maps the Test Case Steps in the feature files to code. It executes the steps on Application Under Test and checks the outcomes against expected results. In order to execute step definition it must match the given component in a feature.

In Cucumber, a step definition is the actual code implementation of the feature mentioned in the feature file.

Gherkin
-------------
Gherkin is a plain English text language, which helps the tool - Cucumber to interpret and execute the test scripts.

Gherkin provides the common set of keywords in English text, which can be used by people amongst the different domain and yet get the same output in the form of test scripts.

user login feature Example
-------------
- Feature − Login functionality for a social networking site. 
- Given I am a social networking site user. 
- When I enter username as username1. And I enter password as password1. 
- Then I should be redirected to the home page of the site.


Test harness in Cucumber
-------------
The test harness allows for separating responsibility between setting up the context and interacting with the browser, and cleaning up the step definition files. It collects stubs, drivers, and other supporting tools required to automate test execution in testing.



Selenium vs Cucumber
-------------

Selenium and Cucumber are both open-source testing tools, and both are used for functional testing. But there are some differences between them.

Differences between Selenium and Cucumber:

- Selenium is a web browser automation tool for web apps, while Cucumber is an automation tool for behavior-driven development that can be used with Selenium (or Appium).
- Selenium is used for automated UI testing, while Cucumber is used for acceptance testing.
- Selenium is preferred by technical teams (SDETs/programmers), while Cucumber is typically preferred by non-technical teams (business stakeholders and testers).
- Selenium can work independently of Cucumber. Cucumber depends on Selenium or Appium for step-definition implementation.
- In Selenium, the script creation is complex, while Cucumber is simpler than Selenium.

Cucumber with Selenium as Cucumber makes it easy to read and understand the application flow. The most significant benefit of using Cucumber with Selenium is that it facilitates developers to write test cases in simple feature files easily understood by managers, non-technical stakeholders, and business analysts. It provides the facility to write tests in a human-readable language called Gherkin. The Selenium-Cucumber framework supports programming languages such as Java, .NET, PHP, Python, Perl, etc.

TDD(Test-Driven Development)
-------------
DD is an acronym that stands for Test-Driven Development. This is a software development technique used to create the test cases first and then write the code underlying those test cases. Although TDD is a development technique, it can also be used for automation testing development. TDD takes more time for development because it tends to find very few defects. The result provided by the TDD development technique has improved the quality of code, and that can be more reusable and flexible. TDD also helps developers to achieve high test coverage of about 90-100%. The only disadvantage for developers following TDD is to write their test cases before writing the code.

Simple 6 step process used by TDD methodology:

1. First, write the test case: You have to write an automated test case according to your requirements.
2. Run all the test cases: Now, run these automated test cases on the currently developed code.
3. Develop the code for that test case: In this process, you must write the code to make that test case work as expected if the test case fails.
4. Run test cases again: Now, you have to rerun the test cases and check if all the test cases developed so far are implemented.
5. Refactor your code: This is an optional step. But, it is advised to refactor your code to make it more readable and reusable. That's why it is essential.
6. Repeat steps 1- 5 for new test cases: This is the last step. Here, you have to repeat the cycle for the other test cases until all the test cases are implemented.

BDD and TDD
-------------
TDD stands for Test-Driven Development, and BDD stands for Behavior Driven Development. Both are two software development techniques.

BDD and TDD are both very similar as they are both testing strategies for a software application. In both cases, the developers have to write the test before writing the code to pass the test. The second main similarity between them is in both cases; the tests can be used as part of an automated testing framework to prevent bugs.


| TDD       | BDD                         |
|-----------------|-----------------------------------|
| In TDD, writing a test fails because the specified functionality doesn't exist, then writing the most straightforward code that can make the test pass, then refactoring to remove duplication, etc.          | n BDD, creating an executable specification that fails because the feature doesn't exist, then writing the most straightforward code that can make the spec pass. You repeat this until a release candidate is ready to ship.                             |
| TDD tests are written using programming languages such as Java, .Net, Python, Ruby, etc.           | BDD tests are written in a human-readable format using Given-When-Then steps. These tests are readable and understandable by non-technical persons also.                    |
| TDD tests are difficult to read by non-programmers as they are written in specific programming languages.       | BDD tests are readable by non-programmers also as they are written in a human-readable format. |
| In TDD, the developers write the test cases. | In BDD, the automated specifications are created by users or testers then the developers wiring them to the code under test.                              |



For more information:

1. [Cucumber - Overview](https://www.tutorialspoint.com/cucumber/cucumber_overview.htm)
2. (https://www.javatpoint.com/cucumber-interview-questions)