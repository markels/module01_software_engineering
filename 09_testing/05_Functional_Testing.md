# Function Test

## Behaviour Driven Development (BDD)
 
- Builds on the concepts of Test Driven Development (TDD)
- Outside looking in - What is does not how it does it
- Uses Structured natural language to capture specification   
- Tests are constructed from the specifications
- Implement one feature at a time
- Can be used to measure development progress
- The specification forms a living documentation of what the software does

TODO: Show chart

### Some Examples of Specification Languages

"It Should"
 
```gherkin
Alarm clock
 should display the time
 should wake up owner

``` 

Gherkin 

```gherkin
Given Alarm set 
When when time of Alarm reached
Then Alarm rings

```

## Gherkin in more detail
### Basic Format
```gherkin
Feature: Here is free form description of the feature that can be several lines long.

Scenario: This would be a description of one scenario
Given precondition  
When action
Then expected outcome

Scenario: A description of another scenario

```

### And and But:
```gherkin
Scenario: A more complex scenario
Given a precondition  
And another precondition
When action
And another action
Then expected outcome
And another expected outcome
But a negative expected outcome 
```

### An Example
```gherkin
Scenario: Valid login 
Given a registered user
When user supplies correct login details
Then user is logged in

Scenario: Invalid password 
Given a registered user
When user supplies incorrect password
Then user is shown "Username/Password incorrect" error message
And user not logged in

Scenario: Invalid username 
Given a registered user
When user supplies incorrect username
Then user is shown "Username/Password incorrect" error message
And user not logged in

```

### Using Example tables
```gherkin
Feature: Fruit Multi-purchase discounts.  Apples are €0.50 each for up to 4 (inclusive), then €0.45 each, for 10 or over they are €0.40.  Oranges are €0.80 each for the first 12, then €0.75.

Scenario: Shopper buys single type of fruit.
Given buying <fruit>
When shopper picks <number>
Then total price comes to €<price>

Examples:
    | fruit  | number | price |
    | apple  |   1    | 0.50  |
    | apple  |   3    | 1.50  |
    | apple  |   4    | 2.00  |
    | apple  |   5    | 2.25  |
    | apple  |   8    | 3.60  |
    | apple  |   10   | 4.00  |
    | apple  |   12   | 4.80  |
    | orange |   1    | 0.80  |
    | orange |   6    | 4.80  |
    | orange |   12   | 9.96  |
    | orange |   13   | 9.75  |

```
TODO: Add reading suggestion Specification by Example 

### Imperative and Declarative
```gherkin
Imperative
Given …
When User arrives a journal land clicks on login field
Then User is redirected to login screen
When enters text "myUserId" in field "Username"
And enters text "myPassw0rd" in field "Password"
And user clicks "Login“
Then …

Declarative
When user supplies correct login details

```

### Sensible Defaults
```gherkin
Scenario: “Default” user logs in
Given a registered user
When user supplies correct login details
Then user is logged in

Scenario: User with expired password
Given a registered user
And password has expired
When user supplies correct login details
Then user is shown change password screen
And user not logged in

```

## BDD tools
- Parse specification and executes test code
- Typically can create code place holders from specification
- Reporting of test results

Many tools are available that support many different test written in many different lanaguages.  We will look a Behave with Python.

## Behave
Behave is a BDD framework for Python (https://behave.readthedocs.io).

### Demonstration
An example of using Behave.

### Install Behave

``` 
pip install behave
```
### Using behave
Now make a directory called “features”. In that directory create a file called “tutorial.feature” containing:

```gherkin 
Feature: showing off behave

  Scenario: run a simple test
     Given we have behave installed
      When we implement a test
      Then behave will test it for us!
```

Make a new directory called “features/steps”. In that directory create a file called “tutorial.py” containing:

```python
from behave import *

@given('we have behave installed')
def step_impl(context):
    pass

@when('we implement a test')
def step_impl(context):
    assert True is not False

@then('behave will test it for us!')
def step_impl(context):
    assert context.failed is False
```

Run behave:

```
behave
```

## Exercise 
Create and execute a test against your software project using Behave


