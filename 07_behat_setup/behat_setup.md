!SLIDE section_slide
# Behat Setup

## How to Set Up Behat in TYPO3



!SLIDE code_slide
# Basic Project Layout

    @@@
    typo3conf/ext/pt_CUSTOMER_test
    ├── behat.yaml
    ├── composer.json
    ├── Fixtures
    ├── Tests
    │   └── Behat
    └── vendor
        ├── behat
        └── punktde
            └── ...
                └── Behat
                    └── Context



!SLIDE code_slide
# Using Composer

    @@@ json
    {
      "require": {
        "behat/behat": "3.0.11",
        "behat/mink-extension": "2.0.0",
        "behat/mink-selenium2-driver": "*",
      }
    }



!SLIDE
# Behat Configuration

* Behat tries to load `behat.yml` or `config/behat.yml`
* You can configure
  * paths
  * contexts
  * filters
  * profiles
  * extensions


!SLIDE code_slide small
# Sample Configuration

    @@@ Yaml
    default:
      extensions:
        Behat\MinkExtension:
          base_url: http://project_url
          default_session: selenium2
          selenium2:
            wd_host: http://localhost:4444/wd/hub
            browser: firefox



!SLIDE
# Selenium Server

* Download from [http://www.seleniumhq.org/download/](http://www.seleniumhq.org/download/)
* Start the downloaded jar with `java -jar /Applications/selenium-server-standalone-2.45.0.jar`
* Create a shell alias: <br>
`alias startselenium=java -jar /Applications/selenium-server-standalone-2.45.0.jar`



!SLIDE code_slide
# Run Your Tests

# From within the test-extension in TYPO3
$ bin/behat
