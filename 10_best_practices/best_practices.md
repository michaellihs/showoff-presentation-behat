!SLIDE section_slide
# Best Practices



!SLIDE section_slide
# Email Testing
## How to Test Sending Emails in TYPO3



!SLIDE
# Common Test-Cases

* Double-opt-in
* Newsletter Registration
* Password forgotten



!SLIDE code_slide
# Send Your Mails to mbox File

    @@@ php
    $GLOBALS['TYPO3_CONF_VARS']['MAIL'] \
        ['transport'] \
        = 'mbox'
    $GLOBALS['TYPO3_CONF_VARS']['MAIL'] \
        ['transport_mbox_file'] \
        = '/var/apache/onebruker/log/mbox.txt'



!SLIDE code_slide
# Step Definition for Reading mbox File Content

     @@@ gherkin
     Then I should see :content \
       in the email sent to :recipient

     When I follow :link \
       in the email set to :recipient



!SLIDE code_slide
# Sample Behat Test

    @@@ gherkin
    Scenario: Registering a new customer
      When I press "Sign Up!"
      Then I should see "Thank you for signing up!"
      And I should see "You signed up to ..." \
          in the email sent to "test@test.com"
      When I am on "/"
      And I follow "/authentication.html" \
          in the email sent to "test@test.com"
      Then I should see "Thank you for registering."



!SLIDE
# SMTP Proxies

* `mailbox.txt` is great!
* An API would be nicer!

<img src="mailhog.png" height="600px">



!SLIDE section_slide
# Database Testing
## How to Manage Database State in Tests



!SLIDE
# Problems with Database Tests

* What happens if tests change database content
* How to assert database consistency
* How to handle database dumps in your tests



!SLIDE
# Basic Setup

* Add a new `TYPO3_CONTEXT` for testing
* Use a separate database for testing
* Configure test database in Behat configuration



!SLIDE code_slide
# TYPO_CONTEXT for Testing
    @@@ php
	switch ($applicationContext) {
		case 'Testing/Development':
			$GLOBALS['TYPO3_CONF_VARS']['DB'] \
			  ['username'] = 'test';
			$GLOBALS['TYPO3_CONF_VARS']['DB'] \
			  ['password'] = 'test';
			$GLOBALS['TYPO3_CONF_VARS']['DB'] \
			  ['database'] = 'test';
			break;
	}



!SLIDE code_slide
# Database Context in Behat

    @@@ yaml
    contexts:
      -
        DatabaseTestingContext:
          featureBasePath:
            Tests/Behat/Features
          databaseCredentials:
            primaryDatabase:
              database: test
              hostname: localhost
              username: test
              password: test



!SLIDE code_slide
# Database Context

    @@@ php
    class DatabaseTestingContext
          implements Context {

      /**
       * @Given /^dataset :dataset \
       *          is added to :database$/
       */
      public function importDataSetToDatabase \
        ($dataSetFilePath, $schema) { ... }

      /**
       * @Given /^the database dump :dump is \
       *          imported to :database$/
       */
      public function importDatabaseDumpToDatabase \
        ($dumpFilePath, $schema) { ... }

    }



!SLIDE code_slide
# Using DB Dumps and Fixtures

    @@@ gherkin
    Background:
        Given the database dump "Fixtures/dump.sql" \
          is imported to "primaryDatabase"
        And dataset "Fixtures/Protocol.yaml" \
          is added to "primaryDatabase"



!SLIDE
# Issue References

* Use your ISSUE IDs throughout tests, git and ticket system
* Given `PRJ-1234` is your ticket number:
  * `Scenario: See the latest events [PRJ-1234]`
  * `git commit -m "... PRJ-1234 ..."`


