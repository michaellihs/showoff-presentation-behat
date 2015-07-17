!SLIDE section_slide

# Gherkin Revisited

## The Remaining Features



!SLIDE

# Scenario Outlines

* Avoid *copy and paste scenarios*
* Provide a *template* and *examples*
* Use placeholder to fill in values



!SLIDE code_slide

    @@@ Gherkin
    # Without scenario outlines

    Scenario: Eat 5 out of 12
      Given there are 12 cucumbers
      When I eat 5 cucumbers
      Then I should have 7 cucumbers

    Scenario: Eat 5 out of 20
      Given there are 20 cucumbers
      When I eat 5 cucumbers
      Then I should have 15 cucumbers



!SLIDE code_slide

    @@@ Gherkin
    # With scenario outlines

    Scenario Outline: Eating
      Given there are <start> cucumbers
      When I eat <eat> cucumbers
      Then I should have <left> cucumbers

      Examples:
        | start | eat | left |
        |  12   |  5  |  7   |
        |  20   |  5  |  15  |



!SLIDE

# Using Givens as Data Fixtures

* Data fixtures are normally in separate files
* Alternative: use `Given` step with table
* Makes tests easier readable



!SLIDE code_slide

    @@@ Gherkin
    Given there are users:
    | username | password | email               |
    | everzet  | 123456   | everzet@knplabs.com |
    | fabpot   | 22@222   | fabpot@symfony.com  |


