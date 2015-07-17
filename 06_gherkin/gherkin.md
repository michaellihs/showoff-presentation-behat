!SLIDE section_slide

# Gherkin

## Human readable tests



!SLIDE code_slide

	@@@ Gherkin
	Feature: Language menu
      In order to switch the website language
      As a example.com website user
      I need to be able to select my language

      Scenario: Switching to German
        When I follow "Language"
        And I follow "Deutsch"
        Then I should be on "/de.html"



!SLIDE

# Gherkin Syntax

* uses indentation to define structure
* line endings terminate statements
* most lines start with a special keyword
* `#` comments out a line



!SLIDE

# Gherkin Keywords

* `Background` set the stage for the test
* `Feature` starts feature and gives a title
* `Scenario` starts scenario and gives description
* Steps - one of
  * `Given` `When` `Then` `And` `But`
  * Syntactically the same
  * Semantically different




!SLIDE

# Features

* One feature per `*.feature`-file
* Features are started by
  * `Feature:` keyword
  * 3 indented lines
  * write whatever you want until
  * first scenario, starting with `Scenario:`



!SLIDE code_slide

# Directory Layout

	@@@
	Tests
	└── Behat
	    └── Features
	        ├── Login.feature
	        ├── Register.feature
	        └── ResetPassword.feature


!SLIDE code_slide

    @@@ Gherkin
    # Feature example

    Feature: Serve coffee
      In order to earn money
      Customers should be able to
      buy coffee at all times

      Scenario: Buy last coffee
        Given there is 1 coffee left \
              in the machine
        And I have deposited 1 dollar
        When I press the coffee button
        Then I should be served a coffee



!SLIDE

# Scenarios

* Every scenario starts with `Scenario:`
  * can have an optional title following `:`
* Each feature can have 1 or more scenarios
* Every scenario consists of one or more steps



!SLIDE code_slide

    @@@ Gherkin
    # Scenario examples

    Scenario: Wilson posts to his own blog
      Given I am logged in as Wilson
      When I try to post to "Expensive Therapy"
      Then I should see "Your article was published."

    Scenario: Greg posts to a client's blog
      Given I am logged in as Greg
      When I try to post to "Expensive Therapy"
      Then I should see "Your article was published."



!SLIDE

# Steps

* `Given` puts system in a known state
* `When` describes *key action* of a scenario
* `Then` describes expected outcome
* `And` and `But` adds further steps to given, when, then



!SLIDE code_slide

    @@@ Gherkin
    Scenario: Login for secure downloads
      Given I am on the login page
      And I enter valid credentials
      And I press "Login"
      When I wait for 2 seconds
      And I follow "Secure Downloads"
      Then I should see "secret-file.txt"
      And I should see "Logout"
      But I should not see "Login"



!SLIDE

# Distinction of steps

* Behat does not distinguish between steps
* You should do so!
* Syntax vs. semantics



!SLIDE

# Backgrounds

* Allow to set context before running scenarios
* Valid for all scenarios in a feature
* Run *before each* scenario
* Contain a number of steps



!SLIDE code_slide

    @@@ Gherkin
    Feature: Multiple site support

      Background:
        Given a global administrator named "Greg"
        And a blog named "Greg's anti-tax rants"
        And a customer named "Wilson"
        And a blog named "Expensive Therapy" \
            owned by "Wilson"


      Scenario: Wilson posts to his own blog
        Given I am logged in as Wilson
        When I try to post to "Expensive Therapy"
        Then I should see "Article was published."

      Scenario: Greg posts to a client's blog
        Given I am logged in as Greg
        When I try to post to "Expensive Therapy"
        Then I should see "Article was published."

