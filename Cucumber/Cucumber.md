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

features in Cucumber
-------------
A feature can be defined as a unit or functionality or part of a project which is an independent functionality of the project. 
A feature contains a group of scenarios that are to be tested as a feature. There are two parts in a feature in Cucumber tool which is called feature files having scenarios in it and the feature files containing automation steps or procedure to be executed. An example of a feature can be a login functionality of a website or chat functionality of a website, a news feed of a website, etc.

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
| In TDD, writing a test fails because the specified functionality doesn't exist, then writing the most straightforward code that can make the test pass, then refactoring to remove duplication, etc.          | In BDD, creating an executable specification that fails because the feature doesn't exist, then writing the most straightforward code that can make the spec pass. You repeat this until a release candidate is ready to ship.                             |
| TDD tests are written using programming languages such as Java, .Net, Python, Ruby, etc.           | BDD tests are written in a human-readable format using Given-When-Then steps. These tests are readable and understandable by non-technical persons also.                    |
| TDD tests are difficult to read by non-programmers as they are written in specific programming languages.       | BDD tests are readable by non-programmers also as they are written in a human-readable format. |
| In TDD, the developers write the test cases. | In BDD, the automated specifications are created by users or testers then the developers wiring them to the code under test.                              |

Cucumber profiles
-------------
You can create Cucumber profiles to run a set of features and step definitions. Use the following command to execute a cucumber profile.

```log
cucumber features -p <profile_name>
#Example: cucumber features -p acceptance
```


Scenario Outline
-------------
Scenario outline is a way of parameterization of scenarios. It is used to execute scenarios multiple times using a different set of test data. 
Multiple sets of test data are provided by using ‘`Examples`’ in a tabular structure separated by pipes (`| |`)

```log
Feature: Application Login
Scenario Outline: Application Website Login
Given Open browser
When NewUser enters "<uname>" and "<password>" and "<send_text>"
Then Message displayed Login Successful

Examples: 
| uname | password | send_text |
| soude@unfpa.org | lT61m@e112 | automation laboratories |
| akoueikou@unfpa.org | oK77f@g100 | automation laboratories |
```

Scenario and Scenario Outline
-------------

- **Scenario:** Copying and pasting scenarios to use different values can quickly become tedious and repetitive:

```log
Scenario: Eat 5 out of 12
  Given there are 12 cucumbers
  When I eat 5 cucumbers
  Then I should have 7 cucumbers

Scenario: Eat 5 out of 20
  Given there are 20 cucumbers
  When I eat 5 cucumbers
  Then I should have 15 cucumbers
```


- **Scenario Outlines:**  allow us to more concisely express these examples through the use of a template with placeholders


```log
Scenario Outline: Eating
  Given there are <start> cucumbers
  When I eat <eat> cucumbers
  Then I should have <left> cucumbers

  Examples:
    | start | eat | left |
    |  12   |  5  |  7   |
    |  20   |  5  |  15  |
```

The Scenario Outline steps provide a template which is never directly run. A Scenario Outline is run once for each row in the Examples section beneath it (except for the first header row).


Step Definition
-------------

Step definition maps the test case steps in the feature files(introduced by Given/When/Then) to code which executes and checks the outcomes from the system under test. Step definitions file has the actual code implementation of the Scenario or Scenario Outline step.

**Feature file:**
```feature
Feature:
  Scenario:
    Given verify two values 'text', 'test'
```
**Step Definition:**


```java
public class Test {
    @Given("verify two values '(.*)', '(.*)'")
    public void verify_two_values(String arg1, String arg2) {
        Assert.assertEquals(arg1,arg2);
    }
```

Background in a Feature file
-------------

Steps which are written under the Background keyword are executed before every scenario.

For example: If you want to execute the same steps for every scenario like login to the website, you just write those common steps under the background keyword.


```log
Feature: Validation of Account Balance
Background:
Given I log in to the Application 
Scenario: Verify Positive Balance
Given I have $1000 in my account
When I withdraw $50
Then I should have $950 balance
Scenario: Verify Zero Balance
Given I have $1000 in my account
When I withdraw $1000
Then I should have $0 balance
```

Junit Test runner class
-------------


```java
import cucumber.api.CucumberOptions;
import cucumber.api.junit.Cucumber;
import org.junit.runner.RunWith;

@RunWith(Cucumber.class)
@CucumberOptions(
        features="src/test/resources/features",
        glue= "ca.testing.stepdefinitions",
        tags = @regression,
        dryRun = false,
        strict = true,
        monochrome = true)
public class TestRunner{}
```

`@CucumberOptions` are used to set specific properties for your cucumber test.

Properties are,

- `Feature` – path to feature file
- `Glue` – path to the step definition
- `dryRun` – boolean value – check for missing step definition
- `tags` – used to group cucumber scenarios in the feature file
- `strict` – boolean value – fail the execution if there is a missing step
- `monochrome` – boolean value – display console output in a readable way


Tags in cucumber-bdd
-------------
Cucumber tags are used to organize scenarios in your feature file. Example: `@regression`, `@sanity`, `@EndtoEnd`

Tags are used to
 - Group scenarios
 - Ignore scenarios from execution
 - Logically group (OR & AND)

```log
Feature: Validation of the Account Balance

@regression @sanity
Scenario: Verify Zero Balance
Given I have $1000 in my account
When I withdraw $1000
Then I should have $0 balance
```

Cucumber Hooks
-------------
Cucumber Hooks are blocks of code that can be used to run before and after the scenarios using @before and @after methods. It helps us eliminates the redundant code steps that we write for every scenario and also manages our code workflow.

```java
public class Hooks {

    @Before
    public void before(){
        System.out.println("This will execute before every Scenario");
    }

    @After
    public void after(){
        System.out.println("This will execute after every Scenario");
    }
}
```

Name any two testing framework that can be integrated with Cucumber?
-------------

- JUnit
- TestNG

What are the two files required to run a cucumber test?
-------------
- Feature file
- Step Definition file

Examples Table or Scenario Outline vs Data Table
-------------

| Scenario Outline       | Data Table                         | 
|-----------------|-----------------------------------|
|This uses Example keyword to define the test data for the Scenario          | No keyword is used to define the test data | 
| This works for the whole test	           | This works only for the single step, below which it is defined | 
| Cucumber automatically run the complete test   the number of times equal to the number of data in the Test Set	      | A separate code needs to understand the test data and then it can be run single or multiple times but again just for the single step, not for the complete test |


For more information:

1. [Cucumber - Overview](https://www.tutorialspoint.com/cucumber/cucumber_overview.htm)
2. [Most Asked Cucumber Interview Questions](https://www.javatpoint.com/cucumber-interview-questions)
3. [Top 20+ Cucumber Interview Questions & Answers – Automation Laboratories](https://www.automationlaboratories.com/cucumber-bdd/)